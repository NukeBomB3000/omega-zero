omega-zero creates these folders on first boot. Nothing loose at the top of `Games/`, `Saves/`,
`Labels/` or `States/` reaches the shelf.

| Folder | Holds |
|---|---|
| `Games/GBA`, `Games/GB`, `Games/GBC` | Your legally obtained ROMs |
| `Labels/GBA`, `Labels/GB`, `Labels/GBC` | Cart labels: a `.png` named after the ROM, for example `Labels/GBA/Metroid Fusion.png` for `Games/GBA/Metroid Fusion.gba` |
| `Saves/...`, `States/...` | Battery saves and save states, per platform |
| `BIOS` | `gba_bios.bin`, `gbc_bios.bin`, `gb_bios.bin` for the boot animations (optional) |
| `Wallpapers` | `.png` wallpapers for the shelf, see [[Shelf Background]] |
| `Overlays/GBA`, `Overlays/GB`, `Overlays/GBC` | Your [[Overlays]] |
| `Config` | Settings, `wifi.conf` with the Wi-Fi networks you have joined, your ScreenScraper account, and an optional `theme.txt`, see [[Shelf Background]] |
| `System` | omega-zero itself, its cores and its licences. Replaced on every update |

omega-zero can fetch labels itself over Wi-Fi; see [[Cart Labels]]. Per-cart shell colours go in
`Config/cart_shell.ini`.

At the root of the card, `omega-zero.log` holds the last session's log; see [[Troubleshooting]].
