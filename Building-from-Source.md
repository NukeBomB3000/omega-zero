You need Rust (the version is pinned in `rust-toolchain.toml`), [Task](https://taskfile.dev) and,
to build for the device on a machine that is not Linux on arm64, Docker.

```sh
task run                        # build the cores and run omega-zero on the desktop
OMEGA_CANVAS=640x480 task run   # see what a 640x480 device draws
task check                      # format, lint, tests on every canvas, timing tests, card scripts
task dist:device                # the aarch64 card tree, in dist-device/
task deploy:device              # push to a device over adb and restart it
task deploy:wifi                # copy a build onto a console on your Wi-Fi and reboot it
```

The device build compiles the cores in an arm64 Linux container, which keeps the pinned toolchain
and the crates it downloads in the docker volumes `omega-zero-rustup` and `omega-zero-cargo`.
gpSP's compiler needs more memory than a 2 GB Docker VM has, and more cores build faster; with
colima, `colima start --cpu 6 --memory 6`.

## The cores

omega-zero hosts five libretro cores: mGBA and gpSP for the GBA and the Game Boys, Snes9x and
Supafaust for the SNES, and PCSX ReARMed for the PlayStation. They live in `vendor/`, which git
ignores.

- `task core` gets all five for the desktop: it builds mGBA and Supafaust (the libretro buildbot
  has no Supafaust for macOS) and fetches gpSP, Snes9x and pcsx_rearmed from the buildbot. One at
  a time: `task core:mgba:host`, `core:gpsp:host`, `core:snes9x:host`, `core:supafaust:host`,
  `core:pcsx:host`. A core that is missing runs the mock instead, a test pattern and a tone.
- `task cores:device` builds the five for the device in the container, from commits pinned in
  the taskfile. gpSP, Snes9x, Supafaust and pcsx_rearmed are built from a source archive kept
  beside them in `vendor/`, which ships in `System/licenses/`. One at a time: `task core:device`
  (mGBA), `core:gpsp`, `core:snes9x`, `core:supafaust`, `core:pcsx`; those four also have an
  `:update` task that fetches the source again. pcsx_rearmed is built with its ARM64 dynarec and
  NEON GPU.
- `task deploy:wifi CORES=1` builds the five device cores too and copies them into `System/`.

## Trying a change on the console

`task deploy:wifi` builds omega-zero, copies it to the console over SSH, checks it arrived whole,
reboots the console and waits until the new build starts. Any game still running loses whatever
it has not saved. It builds with the `device-dev` profile, which skips the release build's
whole-program optimisation, so a rebuild after an edit takes seconds; `PROFILE=device` copies the
shipping build instead. `SCRIPTS=1` copies the scripts in `card/System` too, and `CORES=1` the
five cores (see [The cores](#the-cores)).

It finds the console as `rg35xxsp.local` and the card at `/mnt/sdcard`. `CONSOLE` (a name or
address, `HOST:PORT` for another port) and `SD` change those. For root's password it takes
`CONSOLE_PASSWORD`, else the first line of `.console-password` at the root of the repository
(git ignores it), else `root`, BaseOS's own. omega-zero gives root six random digits the first
time it runs on a card, so from then on the password is the one Settings > Network shows with Y
on the SSH row (see [[Wi-Fi, SSH and SFTP|Networking]]): put it in `.console-password` once. A
console that turns the password away says so, also when a deploy reboots it into the first
omega-zero to run on a card. `task log:wifi` prints `omega-zero.log` off the console the same
way. Both need `sshpass` (`brew install sshpass`).

`task build:device PROFILE=device-dev` builds the same thing without copying it.

## The boot screen and the opening

The boot screen, the still image the bootloader shows while Linux starts, is
`card/System/bootlogo-<width>x<height>.bmp`, one per panel. `task bootlogos` renders all of them
with `crates/omega-zero/examples/bootscreens.rs`: a BIOS screen after Award's, in the opening's
letters and where its terminal prints, with the OmegaZero logo in 16 colours from
`assets/logo/omega-zero-logo-bios.png`. `assets/logo/bioslogo.sh` makes that logo again
(ImageMagick). `task bootlogos:logo` renders the logo over the shelf's grid that was the boot
screen before (Chrome and ImageMagick).

The opening is `crates/omega-zero/src/opening.rs`: what it tells, its script, fades and skip. Its
letters are `crates/omega-ui/src/opening.rs` and its sounds `crates/omega-zero/src/audio/chime.rs`.

## Cart labels

Cart labels need ScreenScraper's key for the program, which is not in the source. Set
`OMEGA_SS_DEVID` and `OMEGA_SS_DEVPASSWORD` when building to put it in; releases get it from the
repository's secrets. A build without it says so on Settings > Labels.

## The menus and the UI kit

The menus are drawn from the pixel-art kit in `assets/ui/`; its
[README](https://github.com/oauramos/omega-zero/blob/main/assets/ui/README.md) has the rules.
Open `assets/ui/storybook.html` from disk to see every component. `assets/ui/flow.html` walks
every menu screen with the slides the device draws, and is the reference the Rust screens are
built to: the arrow keys, `X`, `Z`, `Enter` and `Space` stand in for the D-pad, A, B, START and
SELECT, a toggle runs the slides five times slower, and the URL's hash picks the screen, colour,
panel size and any moment of a slide:

```
flow.html#screen=network&from=settings&t=0.5&colour=amber&shot=1
```

The kit is in Rust too, in `crates/omega-ui/src/kit/`. Its tests in
`crates/omega-ui/tests/suite/kit/` hold each face to a screenshot Chrome takes of the HTML kit,
pixel for pixel; after changing a component, `make-refs.sh` there takes the screenshots again
(`CHROME` points it at another Chrome). Each menu screen's input and drawing is a file of its
own in `crates/omega-zero/src/screens/`, its faces are made in `frontend/sync_*.rs`, and
`nav.rs` slides between them.

## Screens and tests

`task screens` draws omega-zero's main screens headless to PNGs, and `task screens:compare` fails
on any pixel that differs from a baseline: the way to prove a change leaves a layout alone.
`SCREENS_SCRIPT=file` runs another script in its place, for one-off previews.

Each crate's tests live in `tests/suite/` and build as one binary, so a run spends its time on
the tests rather than on linking and starting a binary per file. A new test file goes in that
folder and gets a `mod` line in its `main.rs`; a suite test fails on a file the list leaves out.
A test that needs a process to itself, because it changes the environment or a setting a process
makes only once, stays a file of its own in `tests/`.

The emulator's worker tests run against real time, so a plain `cargo test` leaves them out and
`task test:timing` runs them; `task check` includes it. The render tests need macOS. There, add
your terminal app under System Settings > Privacy & Security > Developer Tools, or macOS scans
every test binary the first time it runs.
