omega-zero runs on BaseOS, a minimal Linux for H700 handhelds. You need the BaseOS image for your
exact model.

## On one card

1. Download the BaseOS image for your device from the
   [BaseOS releases](https://github.com/pvaibhav/BaseOS/releases/latest) (for example
   `baseos-rg35xxsp-*.img.zip`) and write it to a microSD card with a tool such as
   [Raspberry Pi Imager](https://www.raspberrypi.com/software/).
2. Put the card in the slot marked **SD1** (TF1) and power on. BaseOS expands its storage, then
   says no frontend was found. Power off.
3. Download the latest [omega-zero release](https://github.com/oauramos/omega-zero/releases/latest),
   unzip it, and copy the contents of the `omega-zero-vX.Y.Z/` folder to the root of the card.
4. Put your games in `Games/GBA`, `Games/GB` and `Games/GBC`. Labels are optional; see
   [[The Card]] and [[Cart Labels]].
5. Put the card back in SD1 and boot.

## What you see as it starts

While Linux starts, the handheld shows a still boot screen: an old PC's BIOS screen, after
Award's, told about omega-zero. Its first boot only puts that screen on the boot partition, so
the first one shows BaseOS's own logo and every boot after it shows omega-zero's.

Then omega-zero plays its opening. The boot screen fades to black, and a terminal after Mega Man
X5's boot screen types its way through ten seconds about the handheld: its model, its memory, the
H700, the battery and its charge. Then the shelf fades in. Any button skips it; see [[Controls]].
A boot that goes straight back into a game, or to the clock, plays no opening.

## On two cards

1. Write BaseOS to the card in **SD1** as above.
2. Format a second card as FAT32 or exFAT with an MBR partition table, and copy the contents of
   the release's `omega-zero-vX.Y.Z/` folder to it.
3. Add your games to the second card and put it in **SD2**. BaseOS runs omega-zero from SD2
   whenever one is there.

## Updating

Replace the `System/` folder on the card omega-zero runs from with the one from the new release.
Your games, saves, save states, labels, wallpapers, overlays and settings all live outside
`System/`.

Once Wi-Fi is set up, you can also copy the new `System/` over SFTP; see
[[Wi-Fi, SSH and SFTP|Networking]].
