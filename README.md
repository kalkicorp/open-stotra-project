<img src="images/logo.png" alt="Project Screenshot" width="350">

An open-source, highly structured YAML dataset of multi-lingual Hindu devotional texts, curated for typography-focused e-readers under a strict non-commercial license.



## 📁 Repository Layout
```
content/            <- text data, any depth/organization, contributor's choice
  Aarti/...
  Chalisa/hanuman_chalisa.yaml
  Veda/
    AtharvaVeda/
      _meta.yaml
      kaanda_01.yaml
assets.yaml          <- category/deity image index (see below)
images/
  categories/*.jpg
  deities/*.jpg
  ATTRIBUTION.md      <- required source/author/license record for every file above
  logo.png           <- repo/project logo, unrelated to app content
```
Only files under `content/` are treated as text data. Directory structure there is purely
organizational — consuming apps never infer `deity`/`category` from folder names, only from the
fields inside each file (or a bundle's `_meta.yaml`), so reorganizing folders is always safe.

## 📄 YAML Schema

### Single-item content file
A standalone work with all its verses in one file:
```yaml
id: "hanuman_chalisa_001"
deity: "Hanuman"
category: "Chalisa"
title: "श्री हनुमान चालीसा"
author: "Tulsidas"
verses:
  - vId: "hc_v1"
    label: "दोहा"      # optional, see below
    text: "श्रीगुरु चरन सरोज रज, निज मनु मुकुरु सुधारि।\nबरनऊँ रघूबर बिमल जसु, जो दायकु फल चारि॥"
```
| Field | Required | Notes |
|---|---|---|
| `id` | yes | Globally unique across the whole repo. |
| `deity` | yes | Plain string, e.g. `"Hanuman"`. Any value is valid — it just becomes its own tile in the consuming app's deity list. |
| `category` | yes | Plain string, e.g. `"Chalisa"`. Same rule as `deity`. |
| `title` | yes | Display title, typically Devanagari. |
| `author` | yes | Traditional/attributed author. |
| `verses` | yes | Ordered list; array position is the reading order. |
| `verses[].vId` | yes | **Immutable per verse.** Never regenerate or reuse it when correcting a verse's text — consuming apps key bookmarks off `vId`, not position, so changing it silently breaks a reader's saved place. |
| `verses[].label` | no | Optional caption shown above the verse (e.g. `"दोहा"`, `"चौपाई"`, or an English equivalent like `"Doha"` — script-agnostic, no separate English/Devanagari fields). Omit the key entirely when it doesn't apply to a verse. |
| `verses[].text` | yes | Verse text. Use `\n` for an internal line break within one verse. |

### Bundle directory (multi-file single work)
A directory is a bundle when it contains a `_meta.yaml`:
```yaml
# content/Veda/AtharvaVeda/_meta.yaml
id: "atharvaveda"
deity: "Vedas"
category: "Veda"
title: "अथर्ववेद"
author: "Traditional"
parts:
  - file: "kaanda_01.yaml"
    label: "Kaanda 1"
```
Each part file holds only its slice of verses (no `id`/`deity`/etc. — that metadata lives once,
in `_meta.yaml`):
```yaml
# content/Veda/AtharvaVeda/kaanda_01.yaml
verses:
  - vId: "av_k1_v1"
    text: "..."
```
`vId`s must be globally unique and immutable across the *entire* bundle, not just within one
part file (e.g. `av_k1_v1`, `av_k2_v1`, ...).

### `assets.yaml` (category/deity display metadata)
Indexes the bilingual caption and photography for each category/deity, keyed by the same
`category`/`deity` string values used in `content/**/*.yaml` — not by folder or file name:
```yaml
categories:
  - key: "Chalisa"
    nameHindi: "चालीसा"
    image: "images/categories/chalisa.jpg"
deities:
  - key: "Hanuman"
    nameHindi: "हनुमान"
    image: "images/deities/hanuman.jpg"
```
| Field | Required | Notes |
|---|---|---|
| `key` | yes | Must exactly match a `category`/`deity` value used in `content/**/*.yaml`. |
| `nameHindi` | no | Bilingual caption shown under the English name in the consuming app. Omit rather than guessing a translation. |
| `image` | no | Path under `images/categories/` or `images/deities/`. Full-color, high-resolution photography, not icon art — see `images/README.md` for sourcing/resolution guidance and `images/ATTRIBUTION.md` for the required per-file source/author/license record. |

A `key` with no entry (or no `image`/broken image) is expected to fall back to the consuming
app's own placeholder — new content doesn't need a caption or matching art before it can ship.

## ⚖️ License & Commercial Restrictions

This project is licensed under the **Creative Commons Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)** license.

### 🚫 Commercial App Clones Prohibited
You are strictly prohibited from cloning, scraping, or utilizing this dataset, database structure, or its YAML files to power, train, or distribute any commercial, ad-supported, or monetized mobile applications, websites, or software services. This dataset is explicitly reserved for the open-source community and the private ecosystem of the **Manas** application.
