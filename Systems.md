omega-zero plays five systems, each on a shelf of its own. L1 and R1 move between the shelves; a
system with no games has no shelf. The pill in the bottom bar names the one you are on.

| System | Games go in | Files | Cores | On the shelf |
|---|---|---|---|---|
| Game Boy Advance | `Games/GBA` | `.gba` | mGBA, gpSP | Its cart |
| Game Boy | `Games/GB` | `.gb`, `.gbc` | mGBA | Its pak |
| Game Boy Color | `Games/GBC` | `.gb`, `.gbc` | mGBA | Its pak |
| SNES | `Games/SNES` | `.sfc`, `.smc` | Snes9x, Supafaust | The American SNES cart or the Super Famicom's |
| PlayStation | `Games/PS1` | `.cue` with its `.bin`, `.chd`, `.pbp`, `.m3u` | PCSX ReARMed | Its disc |

Where a system has two cores, X on the shelf opens the cart and picks the core it runs on; the
choice is kept per cart. The first one listed is the one a cart starts on. See [[Controls]] for
the buttons, and [[The Card]] for every folder.

## SNES

A game from the USA (or Canada, which had the same carts) stands as the American SNES cart, in
its dark grey. A game from Japan, Europe or anywhere else stands as the Super Famicom cart, in
its light grey, as Europe's carts were the Super Famicom's shape. The region comes from the
ROM's header; a tag in the file name, such as `(USA)`, `(Japan)` or `(Europe)`, wins over it. A
ROM with a copier's 512-byte header in front is read too.

To choose the shape yourself, give the cart a line in `Config/cart_shell.ini`, the shape then the
plastic's colour and finish:

```
Super Mario World (Europe) = ntsc 8b8a91 solid
Chrono Trigger (USA) = sfc b7b6bb solid
```

`ntsc` is the American cart and `sfc` the Super Famicom's. `auto` leaves the shape to the ROM.

The SNES pad is the handheld's own: A, B, X, Y, L1 and R1 are the game's. L2 rewinds and R2
fast-forwards, as on the GBA. The picture is drawn at twice its size, 512x448 in the middle of
the screen (512x478 for a game that shows its overscan); a game's hi-res and interlaced screens
fill the same space. A game made for 50 Hz runs at 50 Hz.

Snes9x is the default core. Supafaust, Mednafen's SNES core, is the other. Snes9x is free for
non-commercial use only; its licence is in `System/licenses/` with the others.

## PlayStation

omega-zero looks in `Games/PS1` and in each folder directly inside it, so a game kept as
`Games/PS1/<Game>/<Game>.cue` with its `.bin` beside it is found. A `.bin` is never a game on its
own: it is the data its `.cue` points at.

A game on several discs is one game on the shelf, its discs stacked one behind another with a
gap between them; the whole stack goes down into the handheld when you play it.

- An `.m3u` playlist that lists the discs is one game, named after the playlist. The discs it
  lists don't stand on their own as well.
- Discs in one folder whose names differ only by a `(Disc 1)`, `(Disc 2)` tag (or `(Disc 1 of
  2)`) are one game, named without the tag. omega-zero writes a playlist for them in
  `Config/playlists/PS1/` and keeps it up to date.

In a game, SELECT + MENU opens **DISC** to put another disc in the drive; see [[Controls]]. The
disc in the drive is kept in `Saves/PS1/<game>.disc`, so a game you come back to is on the disc
you left it on.

PCSX ReARMed carries a BIOS of its own, and needs nothing more. A BIOS from a real console is used
when it is in `BIOS/`, named `scph5501.bin` (or `scph5500.bin`, `scph5502.bin`, `scph1001.bin`,
`scph7001.bin`, `scph101.bin`, `psxonpsp660.bin`). Each game has a memory card of its own, kept
with its saves in `Saves/PS1`.

The pad: ✕, ○, □ and △ are B, A, Y and X, where they sit on the handheld; L1, R1, L2 and R2 are
the game's. So fast-forward is SELECT + R2 held (twice to lock it on), and a PlayStation game has
no rewind. The picture is 4:3: the whole screen on a 640x480 handheld, 640x480 in the middle of a
720x480 one, and 720x540 on the square 720x720. A game made for 50 Hz runs at 50 Hz.

A disc's region comes from its file name's tags, or else from the serial printed on it, such as
`SLUS-00594`.
