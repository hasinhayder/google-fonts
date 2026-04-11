# Google Fonts Index

This repository contains a structured JSON index of Google Fonts, organized by font category and script subset.

The dataset is split into top-level manifests and nested folders so it is easy to query either the full catalog or a narrower slice of it.

## What's included

- `fonts.json`: the full list of font family names in the dataset.
- `categories.json`: the supported font categories.
- `subsets.json`: the supported script and language subsets.
- `updated.json`: timestamp of the last time the manifests were generated.
- `categories/`: category-specific indexes (`display`, `handwriting`, `monospace`, `sans-serif`, `serif`).
- `subsets/`: subset-specific indexes (`latin`, `arabic`, `cyrillic`, `devanagari`, etc.).
- `fonts/`: per-font metadata files — one JSON file per font family.

## Repository structure

```text
.
├── fonts.json                          → all font families
├── categories.json                     → all categories
├── subsets.json                        → all subsets
├── fonts/
│   └── inter.json                      → per-font metadata
│   └── ...                             → 1,900+ more
├── categories/
│   ├── display/
│   │   ├── fonts.json                  → all display fonts
│   │   ├── subsets.json                → all subsets in display
│   │   ├── latin/
│   │   │   └── fonts.json              → display + latin
│   │   └── ...                         → 40+ more subsets
│   ├── handwriting/
│   ├── monospace/
│   ├── sans-serif/
│   └── serif/
└── subsets/
    ├── latin/
    │   ├── fonts.json                  → all fonts with Latin script
    │   └── categories.json             → which categories include Latin
    └── ...                             → 180+ more subsets
```

## Data format

### Top-level manifests

```json
// fonts.json
{
  "fonts": ["ABeeZee", "ADLaM Display", "Arimo"]
}
```

```json
// categories.json
{
  "categories": ["display", "handwriting", "monospace", "sans-serif", "serif"]
}
```

```json
// subsets.json
{
  "subsets": ["latin", "latin-ext", "cyrillic", "greek", "japanese"]
}
```

```json
// updated.json
{
  "last_updated": "2026-04-10T17:20:04Z"
}
```

### Category index

```text
categories/<category>/
├── fonts.json        # all fonts in this category
├── subsets.json      # all subsets used in this category
└── <subset>/
    └── fonts.json    # fonts in this category + subset
```

### Subset index

```text
subsets/<subset>/
├── fonts.json        # all fonts in this subset
├── categories.json   # categories that appear in this subset
└── <category>/
    └── fonts.json    # fonts in this subset + category
```

### Per-font metadata

```json
// fonts/abeezee.json
{
  "family": "ABeeZee",
  "slug": "abeezee",
  "categories": ["sans-serif"],
  "subsets": ["latin", "latin-ext"],
  "variants": ["regular", "italic"],
  "version": "v23",
  "lastModified": "2025-09-08"
}
```

## Generating the manifests

```bash
./generate-font-manifests.sh              # uses webfonts.json
./generate-font-manifests.sh custom.json  # uses your own file
```

The script cleans previous output, generates all index files, and writes a fresh `updated.json` timestamp.

## Common use cases

You can use these files to:

- **Build font pickers & filters** — populate dropdowns, checkboxes, or searchable UIs with category and subset filters
- **Generate subset-aware font previews** — show only the fonts that support a given script (e.g. Arabic, Bengali, Devanagari, Cyrillic)
- **Power search or autocomplete** — load a lightweight JSON index instead of hitting an API or scraping
- **Generate dynamic `@import` or `<link>` tags** — fetch the font family name from JSON and construct Google Fonts embed URLs on the fly
- **Keep a local or CDN-cached snapshot** — avoid rate limits by using the structured JSON via jsDelivr instead of querying Google Fonts directly
- **Feed into design systems & component libraries** — validate typography tokens against the real Google Fonts catalog
- **Drive static site generation** — pre-render font preview cards, style guides, or comparison tables at build time

## CDN Usage

All JSON files are available via [jsDelivr](https://www.jsdelivr.com/) CDN:

```
https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts/
```

### Examples

```bash
# Full font list
curl https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts/fonts.json

# Full font list (latest tag)
curl https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts@latest/fonts.json

# Fonts in a specific subset and category
curl https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts/subsets/latin/display/fonts.json

# Fonts in a specific category and subset
curl https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts/categories/sans-serif/latin/fonts.json
```

### Versioned URLs

You can pin to a specific tag or commit for caching:

```
https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts@v1.2.0/fonts.json
```

## Notes

- The repository is data-only.
- Folder and file names are lowercase and hyphenated where needed.
- Category and subset indexes are intended to stay consistent with the top-level manifests.
