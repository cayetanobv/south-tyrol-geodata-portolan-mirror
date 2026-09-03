# AGENTS.md — Bathing lakes quality — mirror of «Balneabilitá dei laghi», Provincia Autonoma di Bolzano

Agent-oriented guidance for this collection. Supplements `README.md` (people) and `collection.json` (software).

## Overview

Community mirror of the dataset «Balneabilitá dei laghi» published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data (CC0 1.0). Extracted on 2026-09-03 from WFS layer p_bz-Hydrology:WaterQuality-Lakes-Balneability and converted to GeoParquet. This copy is NOT the official publication: the authoritative source is the Province's geoportal and open-data portal (https://data.civis.bz.it/dataset/balneabilita-dei-laghi). Published for the OGC Metadata Summit 2026 demo.

Source: WFS layer `p_bz-Hydrology:WaterQuality-Lakes-Balneability` of the Province's geoportal, mirrored to GeoParquet with spatial (Hilbert) ordering and a `bbox` column; a PMTiles archive and a MapLibre style (`styles/default.json`, derived from the provincial WMS style) accompany it. Geometry: Point; features: 13.

**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

Official record of the source dataset: https://data.civis.bz.it/dataset/balneabilita-dei-laghi

## Accessing the data

```sql
INSTALL spatial; LOAD spatial;
SELECT * EXCLUDE (geometry) FROM read_parquet('bathing-lakes-quality.parquet') LIMIT 5;
```

CRS is **OGC:CRS84 (WGS 84 lon/lat)**. Filter on the `bbox` struct column for spatial subsets (row-group pruning). Python: `geopandas.read_parquet('bathing-lakes-quality.parquet')`.

## Schema & field notes

| Field | Type | Notes |
|---|---|---|
| `ID` | int64 |  |
| `CODE_PP` | int64 |  |
| `CODE_152` | int64 |  |
| `LAKE_DE` | string |  |
| `LAKE_IT` | string |  |
| `SITE` | int64 |  |
| `SITE_DE` | string |  |
| `SITE_IT` | string |  |
| `PQ_C_C` | string |  |
| `PQ_C_CI` | string |  |
| `PQ_YEAR` | int64 |  |
| `PQ_DATE` | string |  |
| `PQ_SITE_IT` | string |  |
| `PQ_SITE_DE` | string |  |
| `PQ_MUN_IT` | string |  |
| `PQ_MUN_DE` | string |  |
| `PQ_TIME` | string |  |
| `PQ_T_AIR` | int64 |  |
| `PQ_T_WATER` | double |  |
| `PQ_W_DIR` | string |  |
| `PQ_W_INT` | string |  |
| `PQ_STATE` | string |  |
| `PQ_FLW_DIR` | string |  |
| `PQ_FLW_INT` | string |  |
| `PQ_ENT` | int64 |  |
| `PQ_ENT_DE` | int64 |  |
| `PQ_ENT_IT` | int64 |  |
| `PQ_E_COLI` | int64 |  |
| `PQ_E_COLI_DE` | int64 |  |
| `PQ_E_COLI_IT` | int64 |  |
| `PQ_C_MUN` | int64 |  |
| `PQ_LAKE_IT` | string |  |
| `PQ_LAKE_DE` | string |  |
| `PQ_BA_FLAG` | string |  |
| `BAL_CODE` | int64 |  |
| `BAL_IT` | string |  |
| `BAL_DE` | string |  |
| `INFO_IT` | string |  |
| `INFO_DE` | string |  |
| `LINK` | string |  |

Attribute names are bilingual as published by the Province (Italian `_IT`/`_I`, German `_DE`/`_D`, Ladin `_LD`). No municipality code column: join spatially (ST_Intersects with `administrative-units/municipalities`).

## Data quality & usage notes

- Screening-quality mirror of an official dataset; for official use, re-query the Province's WFS.
- Attribute semantics (codes, classes) are those of the producing office; see the README and the portal record.
- Geometries that the extraction had to repair were cleaned on 2026-09-03 to valid single-type geometries (polygons, lines or points); `ST_IsValid` holds for every row.

## Related collections

Other themes of this catalog share the producer and licence. Municipality polygons and population live under `administrative-units/` and `population-and-statistics/` (join on `ISTAT_CODE`).
