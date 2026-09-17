# Ascendancy Roulette

One-page site: a roulette wheel that picks an ascendancy class and generates a character nickname. It covers both games, switched with the toggle in the header — **Path of Exile 2** (23 ascendancies) and **Path of Exile** (21 ascendancies).

- Open `index.html` in a browser, or serve the folder statically, e.g. `python -m http.server`.
- Wheel sectors show *ascendancy + character class*; after the spin the page background switches to the class art, the drawn name flies up out of the hub and the result card flares, the same celebration the last one standing gets in a knockout run.
- The sectors are laid out in a fresh random order on every page load, with a plain random comparator, since this is only the visual arrangement.
- The page opens already showing whichever ascendancy the pointer happens to be aiming at, art and tree included.
- Two modes, side by side above the button. **Single roll** draws one ascendancy. **Elimination** knocks the sector under the pointer off the wheel on every spin — the remaining sectors widen, the panel keeps the ladder of who went out and in which place, and the last one standing is crowned. Every round waits for a click: the button and the wheel itself read *Spin again*, and *Start over* once there is a winner.
- **Minimum spin** sets the least number of seconds a spin may last (2–60). The wheel cruises at full speed until only the braking is left to do, so the drawn sector still arrives under the pointer with no jump in speed; a short minimum shortens the braking too, so asking for a quick spin really gets one.
- A knockout throws an ember burst in the colours of the character class off the pointer, shakes the wheel and strikes the name through; the winner gets a golden shockwave off the hub, confetti down the page and a glow on the wheel. All of it sits on one full-screen canvas that only animates while something is alive on it, and it steps aside for `prefers-reduced-motion`.
- A badge beside the title links to [twitch.tv/blindermine](https://www.twitch.tv/blindermine), the channel this is made for. It loads the channel picture: decapi.me answers with the current Twitch CDN url, unavatar.io serves the picture itself if it does not, and the Twitch glyph stays in place if neither answers — nothing on the page waits on either service.
- The wheel clacks once for every sector edge that passes the pointer, the way a peg wheel does. The knock is synthesised in the Web Audio API — a short noise burst through a bandpass, louder and brighter the faster the wheel goes — so there is no audio file to load. The speaker button mutes it, and the choice is remembered.
- The sparkle button turns the effects off: no bursts, no confetti, no labels, no shake, and whatever is in the air at that moment is cleared. It is remembered too, and the browser's reduced-motion setting still turns the particles off on its own.
- The pointer is hinged at its base and rides the sectors like the flapper of a peg wheel: an edge drags it along the way the wheel turns, a spring pulls it back once the edge clears, and on the way back it slaps against the rim instead of swinging freely, in step with the clack. It rides held over while the wheel is fast and flicks once per sector as it slows. The knock is the same event as the sound, so the pointer keeps swinging with the sound muted; only reduced-motion turns it off.
- The wheel line-up is editable: the panel lists every class of the active game, clicking one takes it off the wheel or puts it back. Two always stay on, and the choice is kept per game between visits.
- Language selector with the 9 languages of the official language switcher on pathofexile2.com. The chosen game, language, mode and minimum spin are remembered between visits.
- Randomness comes from the random.org HTTP API (true random numbers). If random.org is unreachable, the page falls back to `crypto.getRandomValues` and says so in the status line.
- The wheel starts turning on the click itself: it spins freely while random.org is being asked, then brakes onto the drawn sector, so the button never feels like it is waiting for the network. The sector is drawn on the wheel as it currently stands, so a knocked-out one can never come up again.
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
- `assets/poe1/bg/*.webp` — the round ascendancy-screen medallion of each class, used for the tree, the result card, and as the page background where it is blown up to fill the screen, capped at three times the size it would need to fit.
- `assets/<game>/nodes/*.webp` — passive node icons, 250 for Path of Exile 2 and 271 for Path of Exile.
- `assets/<game>/ui/` — the node frames, plus the centre ornament of the Path of Exile ascendancy panel.

Class names and art © Grinding Gear Games. Art hosted by poe2db.tw and poedb.tw.
