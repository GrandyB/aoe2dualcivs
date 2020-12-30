# https://grandyb.github.io/aoe2dualcivs/
Very simple site to stack two players' civs on a single webpage, utilising aoe2techtree.net.
Created with casters in mind; especially when combined with a spreadsheet to generate the URL, could be used to quickly compare civs outside of the game, and be easily referencable.

## How-to
Add parameters to the page URL to setup the comparison:

- **p1Civ** and **p2Civ** - correspond to the civ name that the https://aoe2techtree.net/#CivNameHere URL uses; if not provided, uses aoe2techtree.net's default of 'Aztecs'
- **p1Name**, **p1Color**, **p2Name**, **p2Color** - all optional but will display in a fixed position on top of each tree
- **strict** - forces `p1Civ` and `p2Civ` to be non-optional
- **arrangement** - optional parameter for layout that defaults to `top-bottom`, but can also be `left-right`, depending on what layout you want

e.g.
- https://grandyb.github.io/aoe2dualcivs/?p1Name=Sally&p2Name=Jim&p1Color=Blue&p2Color=Pink&p1Civ=Britons&p2Civ=Ethiopians
- https://grandyb.github.io/aoe2dualcivs/?p1Civ=Aztecs&p2Civ=Mayans
- https://grandyb.github.io/aoe2dualcivs/ (defaults to Aztecs for both, as per aoe2techtree.net's default)
- https://grandyb.github.io/aoe2dualcivs/?p1Name=Sally&p2Name=Jim&p1Color=Blue&p2Color=Pink&p1Civ=Britons&strict (shows error in p2's slot as it's missing `p2Civ`)

## Combining with Google Sheets [optional]
Makes it easier to generate/manipulate URLs, especially if already using Sheets to power the broadcast data too.
This setup assumes 3 cells per player - player one's name/color/civ being A1/B1/C1 and player two's name/color/civ being A2/B2/C2

For each name (A1, A2):
- Can either just have a regular old cell, or a list of names of known participants as per examples below

For each color (B1, B2):
- Data -> Validation
- "Items from a list" -> `Blue,Red,Green,Yellow,Cyan,Pink,Orange`
- Tick "Show drop-down list in cell" and "Reject input" on invalid data

For each civ (C1, C2), much the same:
- Same as color, except use: `Aztecs,Berbers,Britons,Bulgarians,Burmese,Byzantines,Celts,Chinese,Cumans,Ethiopians,Franks,Goths,Huns,Incas,Indians,Italians,Japanese,Khmer,Koreans,Lithuanians,Magyars,Malay,Malians,Mayans,Mongols,Persians,Portuguese,Saracens,Slavs,Spanish,Tatars,Teutons,Turks,Unknown,Vietnamese,Vikings`

Then you want a separate cell that combines the output of these cells, into a clickable URL.

`=CONCATENATE("https://grandyb.github.io/aoe2dualcivs/?p1Civ=", B1, "&p2Civ=", B2, "&p1Name=", SUBSTITUTE(A1, " ", "%20"), "&p2Name=", SUBSTITUTE(A2, " ", "%20"), "&p1Color=", B1, "&p2Color=", B2)`

This cell should then have a link to the two civs and their names/colours displayed; a nice quick version should you want the player names/colours easily, and/or are using spreadsheets as part of your broadcast already. Grandy uses [SheetsIO](https://github.com/GrandyB/SheetsIO) to populate OBS text/image elements with values from Google Sheets for example.
