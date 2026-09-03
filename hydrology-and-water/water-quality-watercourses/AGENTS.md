# AGENTS.md — Water quality watercourses — mirror of «Qualitá dei corsi d'acqua», Provincia Autonoma di Bolzano

Agent-oriented guidance for this collection. Supplements `README.md` (people) and `collection.json` (software).

## Overview

Community mirror of the dataset «Qualitá dei corsi d'acqua» published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data (CC0 1.0). Extracted on 2026-09-03 from WFS layer p_bz-Hydrology:WaterQuality-Watercourses and converted to GeoParquet. This copy is NOT the official publication: the authoritative source is the Province's geoportal and open-data portal (https://data.civis.bz.it/dataset/qualita-dei-corsi-dacqua). Published for the OGC Metadata Summit 2026 demo.

Source: WFS layer `p_bz-Hydrology:WaterQuality-Watercourses` of the Province's geoportal, mirrored to GeoParquet with spatial (Hilbert) ordering and a `bbox` column; a PMTiles archive and a MapLibre style (`styles/default.json`, derived from the provincial WMS style) accompany it. Geometry: Point; features: 431.

**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

Official record of the source dataset: https://data.civis.bz.it/dataset/qualita-dei-corsi-dacqua

## Accessing the data

```sql
INSTALL spatial; LOAD spatial;
SELECT * EXCLUDE (geometry) FROM read_parquet('water-quality-watercourses.parquet') LIMIT 5;
```

CRS is **OGC:CRS84 (WGS 84 lon/lat)**. Filter on the `bbox` struct column for spatial subsets (row-group pruning). Python: `geopandas.read_parquet('water-quality-watercourses.parquet')`.

## Schema & field notes

| Field | Type | Notes |
|---|---|---|
| `ID` | int64 |  |
| `NAME_DE` | string |  |
| `NAME_IT` | string |  |
| `SECTION_DE` | string |  |
| `SECTION_IT` | string |  |
| `CODE` | string |  |
| `TYPE` | string |  |
| `NATURE_ID` | int64 |  |
| `NATURE_DE` | string |  |
| `NATURE_IT` | string |  |
| `RISK_DE` | string |  |
| `RISK_IT` | string |  |
| `RETE_DE` | string |  |
| `RETE_IT` | string |  |
| `IDENT_DE` | string |  |
| `IDENT_IT` | string |  |
| `LENGTH` | double |  |
| `TAR_CH_DE` | string |  |
| `TAR_CH_IT` | string |  |
| `TAR_OK_DE` | string |  |
| `TAR_OK_IT` | string |  |
| `O_REF_PER` | string |  |
| `O_ST_CH` | int64 |  |
| `O_ST_CH_DE` | string |  |
| `O_ST_CH_IT` | string |  |
| `O_SUPSP_DE` | string |  |
| `O_SUPSP_IT` | string |  |
| `O_ST_OK` | int64 |  |
| `O_ST_OK_DE` | string |  |
| `O_ST_OK_IT` | string |  |
| `O_MPH_VAL` | int64 |  |
| `O_MPH_DE` | string |  |
| `O_MPH_IT` | string |  |
| `O_DIA_VAL` | int64 |  |
| `O_DIA_DE` | string |  |
| `O_DIA_IT` | string |  |
| `O_MZB_VAL` | int64 |  |
| `O_MZB_DE` | string |  |
| `O_MZB_IT` | string |  |
| `O_FISH_VAL` | int64 |  |

Attribute names are bilingual as published by the Province (Italian `_IT`/`_I`, German `_DE`/`_D`, Ladin `_LD`). No municipality code column: join spatially (ST_Intersects with `administrative-units/municipalities`).

## Data quality & usage notes

- Screening-quality mirror of an official dataset; for official use, re-query the Province's WFS.
- Attribute semantics (codes, classes) are those of the producing office; see the README and the portal record.
- Geometries that the extraction had to repair were cleaned on 2026-09-03 to valid single-type geometries (polygons, lines or points); `ST_IsValid` holds for every row.

## Related collections

Other themes of this catalog share the producer and licence. Municipality polygons and population live under `administrative-units/` and `population-and-statistics/` (join on `ISTAT_CODE`).
