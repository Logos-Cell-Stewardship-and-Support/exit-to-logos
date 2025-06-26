## **📂 Cell Map Automation Scaffold**

This section outlines a GitHub-to-Figma visualization pipeline for displaying the global network of Logos Cells using structured metadata, GeoJSON, and Figma overlays.

### 🧭 Overview

The goal is to create a semi-automated, human-readable and designer-friendly method to:

* Track Cell status across the world
* Generate a discoverable, social-proofing map
* Keep it version-controlled and transparent
* Allow export to SVG or overlay in Figma for visual storytelling

---

## 🗂 Repository Structure

```
logos-cell-map/
├── README.md
├── data/
│   └── cells.json           # master list of all Cells
├── scripts/
│   └── convert-to-geojson.py  # script to convert cells.json to GeoJSON
├── geo/
│   └── cells.geojson        # output for visualization
├── assets/
│   └── map-template.fig     # optional Figma or SVG template
├── .github/
│   └── workflows/
│       └── build.yml        # automate GeoJSON generation on commit
```

---

## 📄 Example: `data/cells.json`

```json
[
  {
    "city": "Bangkok",
    "country": "Thailand",
    "lat": 13.7563,
    "lon": 100.5018,
    "status": "active",
    "lead": "Kit",
    "open_slots": 0
  },
  {
    "city": "Lagos",
    "country": "Nigeria",
    "lat": 6.5244,
    "lon": 3.3792,
    "status": "forming",
    "lead": null,
    "open_slots": 3
  }
]
```

---

## 🔁 Conversion Script: `scripts/convert-to-geojson.py`

This script reads the `cells.json` file and outputs a clean `cells.geojson` file suitable for:

* Import into Figma via plugins (Figmapp)
* Mapbox or Leaflet display
* Embedding in campaign microsites or blogs

---

## 🚀 Automation via GitHub Actions

* On each push to `main` or any edits to `cells.json`, trigger the script
* Commit the updated `cells.geojson` back to `geo/`

### `.github/workflows/build.yml`

```yaml
name: Generate GeoJSON
on:
  push:
    paths:
      - 'data/cells.json'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Run conversion script
        run: |
          python scripts/convert-to-geojson.py
      - name: Commit results
        run: |
          git config user.name 'github-actions'
          git config user.email 'github-actions@github.com'
          git add geo/cells.geojson
          git commit -m 'Auto-generate GeoJSON'
          git push
```

---

## 🧪 Next Steps

* Add more Cells manually or via Discord bot form
* Set up a visual interface (MapLibre, Leaflet, or Figma overlay)
* Invite community to maintain the file with PRs

> *This becomes both a social proof layer and a tool for finding nearby Logos activity.*

---

## ⬇ Appendices

* GeoJSON template
* Initial Figma overlay mock
* Reference map assets and style guide

---

*See the main Exit to Logos strategy for how this scaffolding integrates into our broader communications plan.*
