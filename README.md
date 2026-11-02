# Water Retention/Purification Mapping (geoskill-water-purification-mapping)

> Computes water yield via a simplified InVEST Budyko water balance, derives water retention by applying an NDVI-modulated vegetation retention coefficient, and estimates nutrient retention for purification. Maps water retention and purification with a simplified InVEST water yield model. Outputs three GeoTIFFs: water yield / retention / purification.

---

## 1. Overview

Water yield is computed with a Budyko-style water balance Y = P - AET, where AET/P = 1 + φ - (1+φ^ω)^(1/ω), with φ = ET0/P the aridity index and ω a soil moisture parameter (default 1.5). Water retention = water yield × NDVI-modulated vegetation retention coefficient (saturating type, capped at 0.85); water purification estimates nitrogen retention as nutrient load × NDVI-modulated retention efficiency (default 0.65). Use cases: water retention function assessment, basin water purification service accounting, and ecological protection red line delineation.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-water-purification-mapping.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `water_yield.tif` | GeoTIFF (float32) | Water yield (mm/yr), EPSG:4326 |
| `water_retention.tif` | GeoTIFF (float32) | Water retention (mm/yr) |
| `nutrient_retention.tif` | GeoTIFF (float32) | Nitrogen retention (kg/ha/yr) |
| `water_purification_params.json` | JSON | ω parameter and per-output means/totals |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/software versions) |

## 6. Technical Principle

(see SKILL.md for details)

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
