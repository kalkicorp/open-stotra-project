# images/

`logo.png` is the repo/project logo (unrelated to app content).

`categories/` and `deities/` hold the photography indexed by `assets.yaml` at the repo root,
shown on Manas's Dashboard for each category/deity tile.

## Style guidance for new images
- Full-color photography, high resolution so images stay crisp when cropped to a tile on
  high-DPI phone screens. Coil crops to fill (`ContentScale.Crop`), so compose the subject
  roughly centered. Minimum pixel dimensions per tile type:
  - `categories/` (Dashboard's horizontal category slider, ~2:3 portrait tile): **at least
    600×900px**.
  - `deities/` (Dashboard's gods list, 1:1 square tile): **at least 300×300px**.
- Only use images you have the right to redistribute under this repo's terms. Free-to-use
  stock sources (Unsplash, Wikimedia Commons, Pinterest, etc.) are fine.
- Add the new file under `categories/` or `deities/`, and add its `image` path to that key's
  entry in `assets.yaml` (creating the entry, with a `nameHindi`, if it doesn't exist yet — see
  the root README's `assets.yaml` section). The `key` must exactly match the `category`/`deity`
  string used in the corresponding `content/**/*.yaml` files — it is not derived from folder
  names.
- A category/deity with no `image` entry (or a broken URL) falls back to Manas's own themed
  placeholder — it's fine to leave newer or minor content unillustrated.
