# Google Fonts Index

This repository contains a structured JSON index of Google Fonts, organized by font category and script subset.

The dataset is split into top-level manifests and per-category folders so it is easy to query either the full catalog or a narrower slice of it.

## What’s included

- `fonts.json`: the full list of font family names in the dataset.
- `categories.json`: the supported font categories.
- `subsets.json`: the supported script and language subsets.
- `display/`, `handwriting/`, `monospace/`, `sans-serif/`, `serif/`: category-specific indexes.
- Nested subset folders inside each category: subset-specific font lists.

## Repository structure

```text
.
├── categories.json
├── fonts.json
├── subsets.json
├── display/
├── handwriting/
├── monospace/
├── sans-serif/
└── serif/
```

Each category folder follows the same pattern:

```text
category/
├── fonts.json
├── subsets.json
└── subset-name/
    └── fonts.json
```

## Data format

All manifest files use the same simple shape:

```json
{
  "fonts": ["ABeeZee", "ADLaM Display", "Arimo"]
}
```

Category and subset listing files use the same shape with a different key name:

```json
{
	"categories": ["display", "handwriting", "monospace", "sans-serif", "serif"]
}
```

```json
{
	"subsets": ["latin", "latin-ext", "cyrillic", "greek", "japanese"]
}
```

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
curl https://cdn.jsdelivr.net/gh/hasinhayder/google-fonts/categories/display/latin/fonts.json
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
