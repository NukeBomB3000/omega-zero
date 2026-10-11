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

**Wi-Fi**, **Network Time** and **SSH** are each ON or OFF: A, Left or Right switches them. Y on
any of the three opens its own panel (the bar says Y INFO there), and B comes back to the row.
Wi-Fi's panel shows:

| Line | Says |
|---|---|
| NETWORK | The network joined; a long name is cut short |
| SIGNAL | Its strength in dBm: the nearer 0, the stronger |
| IP | The handheld's address |
| HOST | Its name, such as `rg35xxsp.local` |
| MAC | The Wi-Fi radio's hardware address, for a router that only lets in devices it knows |

Until a network is joined and has given the handheld an address, the panel says what comes first.

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

BaseOS runs an SSH server with SFTP. On **Network**, the **SSH** row switches it **ON** or **OFF**
with A, Left or Right: ON starts the server, OFF stops it (logins already made stay), and
omega-zero keeps your choice across restarts. Y on the row opens how to log in:

| Line | Says |
|---|---|
| IP | The handheld's address |
| HOST | Its name, such as `rg35xxsp.local` |
| USER | `root` |
| PASSWORD | Six random digits, which omega-zero gives root the first time it runs on a card. It keeps them as `ssh_password=` in `baseos.conf` at the root of the card in SD1, so BaseOS keeps them too. A password you set there yourself is kept (see [BaseOS's settings](https://github.com/pvaibhav/BaseOS#settings)) |
| PORT | 22 |

SFTP uses the same login. With no network joined, the panel says to join one first, and with SSH off, to turn it on.

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
is on. Y on the row opens its panel:

| Line | Says |
|---|---|
| STATUS | SYNCED once a time server has set the clock, WAITING until then |
| DATE | The date on the clock |
| TIME | The time on the clock |
| ZONE | The time zone, such as `UTC-03:00`, set under Settings > Date & Time |

With Network Time off, the panel says to turn it on first.

## Cart labels

Cart labels are no longer on this screen: they are **Labels**, in [[Settings]]. See
[[Cart Labels]].
