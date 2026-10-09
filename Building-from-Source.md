You need Rust (the version is pinned in `rust-toolchain.toml`), [Task](https://taskfile.dev) and,
to build for the device on a machine that is not Linux on arm64, Docker.

```sh
task run                        # build the cores and run omega-zero on the desktop
OMEGA_CANVAS=640x480 task run   # see what a 640x480 device draws
task check                      # format, lint, tests on every canvas, timing tests, card scripts
task dist:device                # the aarch64 card tree, in dist-device/
task deploy:device              # push to a device over adb and restart it
```

The device build compiles the cores in an arm64 Linux container. gpSP's compiler needs more
memory than a 2 GB Docker VM has; with colima, `colima start --memory 4`.

## Cart labels

Cart labels need ScreenScraper's key for the program, which is not in the source. Set
`OMEGA_SS_DEVID` and `OMEGA_SS_DEVPASSWORD` when building to put it in; releases get it from the
repository's secrets. A build without it says so on the Cart Labels screen.

## Screens and tests

`task screens` draws omega-zero's main screens headless to PNGs, and `task screens:compare` fails
on any pixel that differs from a baseline: the way to prove a change leaves a layout alone.
`SCREENS_SCRIPT=file` runs another script in its place, for one-off previews.

The emulator's worker tests run against real time, so a plain `cargo test` leaves them out and
`task test:timing` runs them; `task check` includes it. The render tests need macOS.
