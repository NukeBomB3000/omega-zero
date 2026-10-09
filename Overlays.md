An overlay is a `.png` the size of your screen, laid over the game and its bezel. Name it after
the screen size and put it in the folder for its platform:

- `Overlays/GBA/640x480.png` on a 640x480 device such as the RG35XX SP
- `Overlays/GB/720x480.png` on a 720x480 device such as the RG SP

It must be transparent where the game's picture is. omega-zero checks, and ignores an overlay
that would cover more than 1% of the game, so one made for another layout never hides it (the
log says so). On a 640x480 panel, the game's picture is:

| Platform | Picture |
|---|---|
| GBA | 640x427 at the top of the screen |
| Game Boy and Game Boy Color | 480x432 in the middle (3x), or the whole screen when stretched |

Overlays made for RetroArch on 640x480 handhelds, such as
[Perfect Overlays](https://github.com/ourigen/perfect_overlays), use the same Game Boy picture
and work for it. omega-zero ships no overlays of its own.
