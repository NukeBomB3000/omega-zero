- **omega-zero.log** at the root of the card holds the last session's log, and
  `omega-zero.log.1` the one before. The first lines name the device, panel and canvas omega-zero
  picked.
- **Crashes** leave a line each in `crash/cores.log` on the card. When omega-zero itself goes down,
  `crash/` also keeps what it last said, `omega-zero.log`, and its memory as it went down,
  `omega-zero.core.gz`, for a debugger. omega-zero starts again once the core is written, a few
  seconds later. A crash within ten minutes of the last keeps the first core, and none is written
  when it would leave the card less than 512 MB.
- **"LAST START FAILED"**, after the opening, means a game took omega-zero down as it started. The
  next boot leaves it on the shelf rather than resume it, so one game cannot keep the handheld from
  starting. Try it on its other core with X (GBA and SNES), or hold A to start it clean, without
  its resume. If it still goes down, open an issue with `crash/omega-zero.log`.
- **The boot screen** is put on the boot partition as omega-zero starts, from
  `System/bootlogo-<width>x<height>.bmp`, so it shows from the boot after that. It is only ever
  replaced with one the size of your device's own, and the original is kept on the boot
  partition as `bootlogo.baseos.bmp`.
- **Button presses** can be traced to `input-trace.log` by running omega-zero with
  `OMEGA_TRACE_INPUT=1`.
- **"The Wi-Fi radio did not start"**, under the networks on Settings > Network, means BaseOS
  never brought up `wlan0`. Restart once; `baseos-boot.log` on the card says what the driver did.
  The RG35XX 2024 shares its BaseOS image with the Plus but has no radio.
- **No ScreenScraper key**, said on Settings > Labels, means the build you run was made without
  the key; official releases carry it. See [[Building from Source]].

Still stuck? Open an [issue](https://github.com/oauramos/omega-zero/issues/new/choose) with
`omega-zero.log` attached.
