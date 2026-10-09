## Joining a network

1. On the shelf, press MENU, go down to **Wi-Fi** and press A.
2. Press A again to switch Wi-Fi on. The networks in reach appear under it after a few seconds.
3. Pick yours and press A. If it needs a passphrase, type it on the keyboard (see [[Controls]])
   and press START.

omega-zero remembers each network you join and joins it again at the next boot, as long as Wi-Fi
was left on. On the list, Y forgets a saved network. The top bar on the shelf lights the Wi-Fi
icon and **ssh** while a network is joined.

The networks are kept on the card in `Config/wifi.conf`, in
[wpa_supplicant](https://w1.fi/wpa_supplicant/)'s format. You can add one from a computer:

```
network={
	ssid="My Network"
	psk="my passphrase"
}
```

The passphrase is stored as plain text, like BaseOS's SSH password, so keep that in mind before
lending the card out. Networks that need a username (enterprise Wi-Fi such as eduroam) are not
supported.

## Copying games over SSH and SFTP

Once joined, the Wi-Fi screen shows the handheld's name, such as `root@rg35xxsp.local`, and its
address. BaseOS runs an SSH server with SFTP on every boot.

- **User:** `root`. **Password:** `root`, unless you set `ssh_password=` in `baseos.conf` at the
  root of the card in SD1 (see [BaseOS's settings](https://github.com/pvaibhav/BaseOS#settings)).
- The card omega-zero runs from is `/mnt/sdcard`, so games go in `/mnt/sdcard/Games/GBA` and so on.
- Use any SFTP client, such as [Cyberduck](https://cyberduck.io),
  [FileZilla](https://filezilla-project.org) or `scp`.

```sh
scp "Metroid Fusion.gba" root@rg35xxsp.local:/mnt/sdcard/Games/GBA/
```

The name is the model's own (`rg35xxsp`, `rgsp`, ...) unless you set `hostname=` in
`baseos.conf`. If `.local` names don't resolve on your network, use the address shown.

## Network time

**Network Time**, on the Wi-Fi screen, keeps the clock right whenever Wi-Fi is joined. The time
zone stays the one you chose under Date & Time.

## Cart labels

**Cart Labels**, on the Wi-Fi screen, fetches real label scans; see [[Cart Labels]].
