# PoE2 Ascendancy Roulette

One-page site: a roulette wheel that picks a Path of Exile 2 ascendancy class and generates a character nickname.

- Open `index.html` in a browser (or serve the folder statically, e.g. `python -m http.server`).
- Wheel sectors show *ascendancy + character class*; after the spin the page background switches to the class art.
- Language selector with the 9 languages of the official language switcher on pathofexile2.com; class names are the official translations from that site.
- Randomness comes from the random.org HTTP API (true random numbers). If random.org is unreachable, the page falls back to `crypto.getRandomValues` and says so in the status line.
- Nickname generator builds Path-of-Exile-compatible names (3–23 characters, letters and underscores), flavoured by the rolled character class.
- The result card draws the ascendancy passive tree the way poe2db does: the round class art with the nodes and their connections on top. Hovering or tapping a node opens a Path-of-Exile-style tooltip with its name and effect in the selected language.

## Assets

- `assets/bg/*.webp` — wide class artworks used as the page background (from poe2db.tw).
- `assets/art/*.webp` — round ascendancy illustrations used in the result card (from poe2db.tw). Abyssal Lich has no wide art, so its illustration is used as the background.
- `assets/nodes/*.webp` — 250 passive node icons, and `assets/ui/frame-*.webp` — the node frames (from poe2db.tw).
- `data/trees.js` — the 23 ascendancy trees: viewBox, node coordinates, connections, and the name plus description of all 427 nodes in 9 languages, scraped from the ascendancy SVG and passive list on the localized poe2db.tw class pages. Where poe2db has no translation (Thai throughout, and Devotion to the King in five languages) the page falls back to English.

Class names © Grinding Gear Games (pathofexile2.com). Art hosted by poe2db.tw.
