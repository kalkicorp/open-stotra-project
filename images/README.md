# images/

`logo.png` is the repo/project logo (unrelated to app content).

`categories/` and `deities/` hold the photography indexed by `assets.yaml` at the repo root,
shown on Manas's Dashboard for each category/deity tile.

## Style guidance for new images
- Full-color photography, high resolution (aim for at least ~1200px on the shorter side —
  tiles are shown on high-DPI phone screens) so images stay crisp when cropped to a tile.
  Coil crops to fill (`ContentScale.Crop`), so compose the subject roughly centered.
- Only use images you have the right to redistribute under this repo's terms — see
  `ATTRIBUTION.md`, which every file added here must have an entry in. Wikimedia Commons
  (CC0/CC BY/CC BY-SA) is the default source; keep the attribution requirement in mind for
  anything CC BY/BY-SA (the app should credit the photographer somewhere, e.g. an in-app
  "credits" screen — not yet built, see .claude/specs/missing-and-deferred-items.md in the
  Manas repo).
- Add the new file under `categories/` or `deities/`, add its `key`/`image` pair to
  `assets.yaml`, and add its source/author/license to `ATTRIBUTION.md`. The `key` must exactly
  match the `category`/`deity` string used in the corresponding `content/**/*.yaml` files — it
  is not derived from folder names.
- A category/deity with no entry (or a broken URL) falls back to Manas's bundled default
  icon — it's fine to leave newer or minor content unillustrated.
