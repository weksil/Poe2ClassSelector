# PoE2 Ascendancy Roulette

One-page site: a roulette wheel that picks a Path of Exile 2 ascendancy class and generates a character nickname.

- Open `index.html` in a browser (or serve the folder statically, e.g. `python -m http.server`).
- Wheel sectors show *ascendancy + character class*; after the spin the page background switches to the class art.
- Language selector with the 9 languages of the official language switcher on pathofexile2.com; class names are the official translations from that site.
- Randomness comes from the random.org HTTP API (true random numbers). If random.org is unreachable, the page falls back to `crypto.getRandomValues` and says so in the status line.
- Nickname generator builds Path-of-Exile-compatible names (3–23 characters, letters and underscores), flavoured by the rolled character class.

## Assets

- `assets/bg/*.webp` — wide class artworks used as the page background (from poe2db.tw).
- `assets/art/*.webp` — round ascendancy illustrations used in the result card (from poe2db.tw). Abyssal Lich has no wide art, so its illustration is used as the background.

Class names © Grinding Gear Games (pathofexile2.com). Art hosted by poe2db.tw.
