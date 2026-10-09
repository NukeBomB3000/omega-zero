omega-zero ships a probe that writes down how your handheld is wired: its buttons, panel,
battery, lid, LEDs, audio, Wi-Fi and Bluetooth. A report from a device marked "untested" is the
most useful thing you can send.

1. Create an empty file named `RUN_PROBE` at the root of the card omega-zero runs from.
2. Boot. omega-zero writes `probe-<device>-<date>.txt` next to it and deletes `RUN_PROBE`.
3. Open a [device report](https://github.com/oauramos/omega-zero/issues/new?template=device-report.yml)
   with the file attached, and say what worked.

Over SSH (BaseOS's default login is `root` / `root`), `sh /mnt/sdcard/System/probe.sh` does the
same; see [[Wi-Fi, SSH and SFTP|Networking]].
