# MDF Project Map — Deployment Bundle

Public deployment bundle for the Mule Deer Foundation Conservation Project Map. This repository is auto-updated by the MDF data pipeline after each successful run and contains only the files needed to serve the map.

---

## What this repository contains

```text
index.html
icons/
data/
├── projects.geojson
├── projects_stats.geojson
├── hunt_units.geojson
└── pipeline_status.json
```

All files use relative paths. The bundle is self-contained and portable — it runs correctly wherever it is deployed.

---

## File descriptions

### index.html

The map application. Renders the interactive Mapbox GL JS project map, including project clustering, popups with photos, impact statistics, and address and hunt unit search.

### data/projects.geojson

Visible MDF projects displayed on the map.

- Uses public coordinates for private projects.
- Excludes WRI projects from the visible map.

### data/projects_stats.geojson

All valid MDF projects used for impact statistics.

- Includes WRI projects.
- Includes projects not shown on the visible map.

### data/hunt_units.geojson

Simplified hunt unit polygons used for hunt unit boundary search and project lookup.

### data/pipeline_status.json

Health-check file generated after each successful pipeline run. Includes last run timestamp, project counts, photo counts, hunt unit counts, and output file sizes.

### icons/

Map icon assets referenced by index.html using relative paths.

---

## Update cadence

This repository is updated automatically by a GitHub Actions workflow in the MDF pipeline repository each time the pipeline runs successfully. The `pipeline_status.json` file records the timestamp of the last successful update.

---

## Notes for integration

- All paths in `index.html` are relative. The directory structure must be preserved as-is when deploying.
- Project photos are not stored in this repository. Photo URLs in the GeoJSON files point to Cloudflare R2.
- The Mapbox access token in `index.html` will be restricted to MDF domains before the map goes live on the public website.
