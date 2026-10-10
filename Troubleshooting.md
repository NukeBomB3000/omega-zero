- **omega-zero.log** at the root of the card holds the last session's log, and
  `omega-zero.log.1` the one before. The first lines name the device, panel and canvas omega-zero
  picked.
- **Crashes** leave `crash/cores.log` and a core dump on the card.
- **The boot logo** is only ever replaced with one the size of your device's own. The original is
  kept on the boot partition as `bootlogo.baseos.bmp`.
- **Button presses** can be traced to `input-trace.log` by running omega-zero with
  `OMEGA_TRACE_INPUT=1`.
- **"The Wi-Fi radio did not start"**, under the networks on Settings > Network, means BaseOS
  never brought up `wlan0`. Restart once; `baseos-boot.log` on the card says what the driver did.
  The RG35XX 2024 shares its BaseOS image with the Plus but has no radio.
- **No ScreenScraper key**, said on Settings > Labels, means the build you run was made without
  the key; official releases carry it. See [[Building from Source]].

Still stuck? Open an [issue](https://github.com/oauramos/omega-zero/issues/new/choose) with
`omega-zero.log` attached.
