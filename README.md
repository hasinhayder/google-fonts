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

- build font pickers or filters
- generate subset-aware font previews
- power search or autocomplete over Google Fonts families
- keep a local snapshot of available font metadata

## Notes

- The repository is data-only.
- Folder and file names are lowercase and hyphenated where needed.
- Category and subset indexes are intended to stay consistent with the top-level manifests.
