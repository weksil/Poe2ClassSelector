# Ascendancy Roulette

One-page site: a roulette wheel that picks an ascendancy class and generates a character nickname. It covers both games, switched with the toggle in the header — **Path of Exile 2** (23 ascendancies) and **Path of Exile** (21 ascendancies).

- Open `index.html` in a browser, or serve the folder statically, e.g. `python -m http.server`.
- Wheel sectors show *ascendancy + character class*; after the spin the page background switches to the class art.
- The sectors are laid out in a fresh random order on every page load, with a plain random comparator, since this is only the visual arrangement.
- The page opens already showing whichever ascendancy the pointer happens to be aiming at, art and tree included.
- Language selector with the 9 languages of the official language switcher on pathofexile2.com. The chosen game and language are remembered between visits.
- Randomness comes from the random.org HTTP API (true random numbers). If random.org is unreachable, the page falls back to `crypto.getRandomValues` and says so in the status line.
- The wheel starts turning on the click itself: it spins freely while random.org is being asked, then brakes onto the drawn sector with no jump in speed, so the button never feels like it is waiting for the network.
- Nickname generator builds Path-of-Exile-compatible names (3–23 characters, letters and underscores), flavoured by the rolled character class.
- The result card draws the ascendancy passive tree the way poe2db and poedb do: the round class art with the nodes and their connections on top. Hovering or tapping a node opens a Path-of-Exile-style tooltip with its name and effect in the selected language.

## Data

Each game has one data file, fetched only when that game is selected.

- `data/poe2.js` — 23 ascendancies, 427 tree nodes. Class names are the official translations from the pathofexile2.com locale dictionaries; trees come from the ascendancy SVG and passive list on the localized class pages of [poe2db.tw](https://poe2db.tw/us/Ascendancy_class).
- `data/poe1.js` — 21 ascendancies, 390 tree nodes, all of it from the localized class pages of [poedb.tw](https://poedb.tw/us/Ascendancy_class).

Each file holds the class list, the ascendancy and character names in 9 languages, and per tree the viewBox, node coordinates, connections and the name plus description of every node in 9 languages.

Where the source has no translation the page falls back to English. That is Thai throughout the Path of Exile 2 node text, and the Devotion to the King node in five languages.

## Assets

- `assets/poe2/bg/*.webp` — wide class artworks used as the page background. `assets/poe2/art/*.webp` — round ascendancy illustrations used in the result card and as the tree background. Abyssal Lich has no wide art, so its illustration serves as the background too.
- `assets/poe1/bg/*.webp` — the round ascendancy-screen medallion of each class, used for the tree, the result card and, dimmed, as the page background.
- `assets/<game>/nodes/*.webp` — passive node icons, 250 for Path of Exile 2 and 271 for Path of Exile.
- `assets/<game>/ui/` — the node frames, plus the centre ornament of the Path of Exile ascendancy panel.

Class names and art © Grinding Gear Games. Art hosted by poe2db.tw and poedb.tw.
