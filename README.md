# 🧃 Packet Picker

A little mobile web app for rating drink packets (the powders and squeezes you dump in water), filtering them, and letting it randomly pick one for you.

Single self-contained `index.html` — no build step, no dependencies. Drop it on GitHub Pages and it just runs.

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

1. Create a repo and upload `index.html` (and this `README.md`).
2. **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `root`**.
3. Give it a minute; your app will be live at `https://<username>.github.io/<repo>/`.

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
