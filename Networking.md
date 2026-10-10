## Joining a network

1. On the shelf, press START, go down to **Network** and press A.
2. On **Wi-Fi**, press A (or Left or Right) to switch it on. The networks in reach appear under
   **AVAILABLE NETWORKS** after a few seconds.
3. Pick yours and press A. If it needs a passphrase, type it on the keyboard (see [[Controls]])
   and press START.

Each network in the list shows its signal, a padlock when it needs a passphrase, and **CONNECTED**,
**JOINING** or **SAVED**. omega-zero remembers each network you join and joins it again at the next
boot, as long as Wi-Fi was left on. Y forgets the saved network under the cursor; the bar along the
bottom says Y FORGET while it can. Settings shows the network joined beside **Network**, and the
top bar on the shelf lights the Wi-Fi icon and **ssh** while one is joined.

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

BaseOS runs an SSH server with SFTP on every boot. On **Network**, pick **SSH** to see how to log
in once a network is joined:

| Line | Says |
|---|---|
| IP | The handheld's address |
| HOST | Its name, such as `rg35xxsp.local` |
| USER | `root` |
| PASSWORD | `root`, unless you set `ssh_password=` in `baseos.conf` at the root of the card in SD1 (see [BaseOS's settings](https://github.com/pvaibhav/BaseOS#settings)) |
| PORT | 22 |

SFTP uses the same login. With no network joined, SSH says to join one first.

- The card omega-zero runs from is `/mnt/sdcard`, so games go in `/mnt/sdcard/Games/GBA` and so on.
- Use any SFTP client, such as [Cyberduck](https://cyberduck.io),
  [FileZilla](https://filezilla-project.org) or `scp`.

```sh
scp "Metroid Fusion.gba" root@rg35xxsp.local:/mnt/sdcard/Games/GBA/
```

The name is the model's own (`rg35xxsp`, `rgsp`, ...) unless you set `hostname=` in
`baseos.conf`. If `.local` names don't resolve on your network, use the address shown.

## Network time

**Network Time**, on Network, keeps the clock right whenever Wi-Fi is joined. The time zone stays
the one you chose under Settings > Date & Time. Network Time and SSH are only listed while Wi-Fi
is on.

## Cart labels

Cart labels are no longer on this screen: they are **Labels**, in [[Settings]]. See
[[Cart Labels]].
