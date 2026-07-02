# 🧃 Packet Picker

A little mobile web app for rating drink packets (the powders and squeezes you dump in water), filtering them, and letting it randomly pick one for you.

Plain `index.html` plus an icon set — no build step, no framework. Drop it on GitHub Pages and it just runs. Live at `https://meghanareed.github.io/flavor-selector/`.

## Files

| File | What it's for |
|------|---------------|
| `index.html` | The whole app (UI, logic, and seed data) |
| `manifest.json` | Name, colors, and icons for "Add to Home Screen" |
| `icon-180.png` | Home-screen icon for iOS |
| `icon-192.png` / `icon-512.png` | Home-screen icon + PWA install for Android |

All five live together in the repo root.

## What it does

- **Rate & add packets** — brand, flavor, purpose, 0–5 rating (quarter-steps), notes, sugar-free, dye-free.
- **Filter** — by purpose, brand, minimum rating, sugar-free / dye-free, plus text search and sort.
- **🥤 Pour me one** — picks a random packet *from whatever is currently filtered* and spotlights it. Set your filters first ("sugar-free energy, 4+"), then pour.
- **Edit / delete** — tap ✎ on any card.

Purposes: Flavor · Hydration · Calming · Energy · Protein · Other.

## Using it

Just open the page. Add packets with the ＋ button; edit or delete with ✎ on a card. Your list is saved automatically in the browser.

## How data is stored

Packets are saved to your browser's **localStorage**, which means:

- It saves automatically — no accounts, no server.
- It's **per device and per browser**. Add a packet on your phone and it stays on your phone; it won't show up on your laptop.

To move data between devices, or to make changes permanent:

- **Export** (bottom bar) downloads a `packets.json` backup.
- **Import** loads a `packets.json` back in.

### Making your list the default

If you want your current packets baked into the app itself (so any device or a cleared browser starts with them):

1. Tap **Export** to get `packets.json`.
2. Open `index.html` and find the `const SEED = [ ... ]` array near the top of the `<script>`.
3. Replace it with the contents of `packets.json` (the objects have the same fields — `id`/`added` are fine to leave in).
4. Commit the change.

The app uses `SEED` only when the browser has no saved data yet, so this sets the fresh-start list.

## Publishing to GitHub Pages

1. Create a public repo and **Add file → Upload files**; drag in all five files (`index.html`, `manifest.json`, and the three `icon-*.png`).
2. Commit, then go to **Settings → Pages → Deploy from a branch → `main` / `root`**.
3. Give it ~60 seconds; the app goes live at `https://<username>.github.io/<repo>/`.

## Updating

Same drag-and-drop flow as the book app: **Add file → Upload files**, drop the changed file(s) in, and GitHub replaces the old ones on commit. Pages redeploys in ~30–60s. On your phone, close and reopen the app (or pull to refresh) to pick up the new version.

## Add to Home Screen

- **iOS (Safari):** Share → *Add to Home Screen*. Uses `icon-180.png`.
- **Android (Chrome):** ⋮ menu → *Add to Home screen* / *Install app*. Uses the manifest + 192/512 icons.

The icons are wired up in `index.html` (`apple-touch-icon` + `manifest`), so the custom soda-glass icon shows instead of a screenshot. If you swap the artwork, replace the three `icon-*.png` files (same names) — no HTML change needed. iOS caches icons hard, so after updating: delete the old shortcut, reopen the URL fresh, and re-add.

## Data shape

Each packet is a JSON object:

```json
{
  "id": "auto",
  "brand": "Starburst",
  "flavor": "cherry",
  "purpose": "flavor",
  "rating": 5,
  "notes": "extra water",
  "sugarFree": false,
  "dyeFree": false
}
```

`purpose` must be one of: `flavor`, `hydration`, `calming`, `energy`, `protein`, `other`.
