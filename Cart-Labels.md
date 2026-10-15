A cart with no label of its own carries its name. omega-zero can fetch the real thing: the scan of
the label on a real cart, from [ScreenScraper](https://www.screenscraper.fr), a free database run
by its community. You need a ScreenScraper account (free) and Wi-Fi joined.

1. On the shelf, press START and pick **Labels**.
2. On **ScreenScraper**, press A and type your user name, then your password, on the keyboard.
3. Press START, or A on **Fetch Labels**. Press it again to stop.

omega-zero looks up each cart that has no label by its ROM's checksum, so a renamed file is still
found. It takes the label from the region the ROM is from, (USA), (Europe) or (Japan), and from
another region when that one was never scanned. Each label goes on the shelf as it arrives, into
`Labels/GBA`, `Labels/GB`, `Labels/GBC`, `Labels/SNES` or `Labels/PS1` under the ROM's name. A
label you put there yourself is never replaced, and a cart ScreenScraper has no scan for, such as
a ROM hack, keeps its name.

A SNES cart's label is taken to suit its shell: the American labels for the American cart, the
Japanese and European ones for the Super Famicom's (see [[Systems]]).

A PlayStation game is looked up disc by disc, and no disc image is ever read whole: by its cue
sheet's checksum, then by the serial printed on the disc (read from a `.cue`'s data track or a
`.pbp`, not from a `.chd`), then by its file's name and size. Each disc gets the scan of its own
printed face. The first disc's goes under the game's name and is its label on the shelf; the
others go under their own names, such as `Labels/PS1/Final Fantasy VII (USA) (Disc 2).png`, and
show on the stack and on the DISC screen.

Your account is kept in `Config/screenscraper.conf`, as plain text: anyone with the card can read
it. Y on **ScreenScraper** signs out and deletes it; the bar along the bottom says Y SIGN OUT
while it can. A free account can look up thousands of carts a day, and the screen shows how many
are left.

You can also make labels yourself: a `.png` named after the ROM in `Labels/<platform>/`; see
[[The Card]].

Each label is cut once to the size the shelf shows it at, and the cut is kept in a `.cut` folder
beside it (`Labels/GBA/.cut`, and so on), so the shelf comes up at once however many labels the
card holds. A fetched label is cut as it arrives. A label you put on the card yourself is cut in
the background the first time omega-zero starts with it, and its cart carries its name until
then. A label you replace is cut again. Deleting a `.cut` folder loses nothing: its cuts are
made again.

Once it is cut, the label itself is shrunk to the smallest size that still covers every cart of
its system, since the shelf never draws one bigger: labels take about a quarter of the room they
did, and Fetch Labels asks for them about that size to begin with. Labels you put on the card
yourself are shrunk too, so keep a copy elsewhere if you want the full-size picture. At boot every
cart comes up carrying its name, and its label is drawn on while the opening plays, the carts on
screen first.
