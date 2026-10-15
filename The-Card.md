omega-zero creates these folders on first boot. Nothing loose at the top of `Games/`, `Saves/`,
`Labels/` or `States/` reaches the shelf.

| Folder | Holds |
|---|---|
| `Games/GBA`, `Games/GB`, `Games/GBC`, `Games/SNES`, `Games/PS1` | Your legally obtained ROMs and disc images; see [[Systems]] for the files each takes. PlayStation games may also sit one folder down, as `Games/PS1/<Game>/<Game>.cue` |
| `Labels/GBA`, `Labels/GB`, `Labels/GBC`, `Labels/SNES`, `Labels/PS1` | Cart labels: a `.png` named after the ROM, for example `Labels/GBA/Metroid Fusion.png` for `Games/GBA/Metroid Fusion.gba`. A PlayStation game's label, under the game's name or its first disc's, goes on its first disc; each other disc has one under its own name, such as `Labels/PS1/Final Fantasy VII (USA) (Disc 2).png` |
| `Saves/...`, `States/...` | Battery saves and save states, per platform. A PlayStation game's memory card is its save, and `Saves/PS1/<game>.disc` says which disc is in the drive |
| `BIOS` | `gba_bios.bin`, `gbc_bios.bin`, `gb_bios.bin` for the boot animations, and a PlayStation BIOS such as `scph5501.bin` (all optional; see [[Systems]]) |
| `Wallpapers` | `.png` wallpapers for the shelf, see [[Shelf Background]] |
| `Overlays/GBA`, `Overlays/GB`, `Overlays/GBC`, `Overlays/SNES`, `Overlays/PS1` | Your [[Overlays]] |
| `Config` | Settings, `wifi.conf` with the Wi-Fi networks you have joined, your ScreenScraper account, and an optional `theme.txt`, see [[Shelf Background]]. `playlists/PS1` holds the playlists omega-zero writes for PlayStation games on several discs |
| `System` | omega-zero itself, its cores and its licences. Replaced on every update |

omega-zero can fetch labels itself over Wi-Fi; see [[Cart Labels]]. Per-cart shell colours go in
`Config/cart_shell.ini`, which also picks a SNES cart's shape; see [[Systems]].

At the root of the card, `omega-zero.log` holds the last session's log; see [[Troubleshooting]].
