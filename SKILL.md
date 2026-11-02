---
name: geoskill-water-purification-mapping
description: '简化 InVEST Budyko 水量平衡计算产水量，叠加 NDVI 调制的植被截留系数得水源涵养量，并估算养分截留净化量。Maps water retention and purification with a simplified InVEST water yield model. 输出产水/涵养/净化三张 GeoTIFF。'
---

# 水源涵养/净化功能制图 | Water Purification Mapping

Water yield is computed with a Budyko-style water balance Y = P - AET, where AET/P = 1 + φ - (1+φ^ω)^(1/ω), φ = ET0/P is the dryness index, and ω is the soil-water parameter (default 1.5). Water retention = water yield × NDVI-modulated vegetation interception coefficient (saturating type, capped at 0.85); water purification estimates nitrogen retention as nutrient load × NDVI-modulated interception efficiency (default 0.65).

Use cases: water-retention function assessment, watershed water-purification service accounting, and ecological conservation red line delineation.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy
```

## Usage / 使用方法

### Example 1: Synthetic Climate/Soil/Vegetation Scenario

```bash
python geoskill-water-purification-mapping.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./output
```

### 示例 2：真实 5 波段输入（precip,et0,awc,ndvi,n_load）

```bash
python geoskill-water-purification-mapping.py --input water_inputs.tif --output-dir ./real
```

### 示例 3：调整 Budyko ω 参数

```bash
python geoskill-water-purification-mapping.py --bbox 116 39 117 40 --synthetic --omega 2.0 --output-dir ./tuned
```

### Example 4: Different Regions

```bash
python geoskill-water-purification-mapping.py --bbox 121 31 122 32 --synthetic --output-dir ./shanghai
```

### Example 5: Silent Batch Mode

```bash
python geoskill-water-purification-mapping.py --bbox 113 23 114 24 --synthetic --quiet --output-dir ./batch
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `water_yield.tif` | GeoTIFF (float32) | Water yield (mm/yr), EPSG:4326 |
| `water_retention.tif` | GeoTIFF (float32) | Water retention (mm/yr) |
| `nutrient_retention.tif` | GeoTIFF (float32) | Nitrogen retention (kg/ha/yr) |
| `water_purification_params.json` | JSON | ω parameter and per-product means/totals |
| `output-manifest.json` | JSON | Run manifest (inputs/outputs/QA/software versions) |

## Data Source / 数据源 / Source

Local GeoTIFF (optional 5-band factor input); the Budyko water balance is a public hydrological model; synthetic mode is generated locally with no external data source.

## Privacy / 隐私声明 / Privacy

- Fully offline by default; no network requests are made
- `--synthetic` mode reads no external data
- All computation is done locally; no user data is uploaded

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
