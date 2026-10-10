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

## Trying a change on the console

`task deploy:wifi` builds omega-zero, copies it to the console over SSH, checks it arrived whole,
reboots the console and waits until the new build starts. Any game still running loses whatever
it has not saved. It builds with the `device-dev` profile, which skips the release build's
whole-program optimisation, so a rebuild after an edit takes seconds; `PROFILE=device` copies the
shipping build instead. `SCRIPTS=1` copies the scripts in `card/System` too.

It finds the console as `rg35xxsp.local` with BaseOS's `root` password and the card at
`/mnt/sdcard`. `CONSOLE` (a name or address, `HOST:PORT` for another port), `CONSOLE_PASSWORD`
and `SD` change those. `task log:wifi` prints `omega-zero.log` off the console the same way.
Both need `sshpass` (`brew install sshpass`).

`task build:device PROFILE=device-dev` builds the same thing without copying it.

## Cart labels

Cart labels need ScreenScraper's key for the program, which is not in the source. Set
`OMEGA_SS_DEVID` and `OMEGA_SS_DEVPASSWORD` when building to put it in; releases get it from the
repository's secrets. A build without it says so on the Cart Labels screen.

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
