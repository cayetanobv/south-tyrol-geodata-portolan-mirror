# AGENTS.md — Hazard zones landslides — mirror of «Piano delle Zone di Pericolo: Frane», Provincia Autonoma di Bolzano

Agent-oriented guidance for this collection. Supplements `README.md` (people) and `collection.json` (software).

## Overview

Community mirror of the dataset «Piano delle Zone di Pericolo: Frane» published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data (CC0 1.0). Extracted on 2026-09-03 from WFS layer p_bz-TerritorialPlans:UrbanPlan-HazardZonePlan-Landslides and converted to GeoParquet. This copy is NOT the official publication: the authoritative source is the Province's geoportal and open-data portal (https://data.civis.bz.it/dataset/piani-delle-zone-di-pericolo-frane). Published for the OGC Metadata Summit 2026 demo.

Source: WFS layer `p_bz-TerritorialPlans:UrbanPlan-HazardZonePlan-Landslides` of the Province's geoportal, mirrored to GeoParquet with spatial (Hilbert) ordering and a `bbox` column; a PMTiles archive and a MapLibre style (`styles/default.json`, derived from the provincial WMS style) accompany it. Geometry: Point; features: 24840.

**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

Official record of the source dataset: https://data.civis.bz.it/dataset/piani-delle-zone-di-pericolo-frane

## Accessing the data

```sql
INSTALL spatial; LOAD spatial;
SELECT * EXCLUDE (geometry) FROM read_parquet('hazard-zones-landslides.parquet') LIMIT 5;
```

CRS is **OGC:CRS84 (WGS 84 lon/lat)**. Filter on the `bbox` struct column for spatial subsets (row-group pruning). Python: `geopandas.read_parquet('hazard-zones-landslides.parquet')`.

## Schema & field notes

| Field | Type | Notes |
|---|---|---|
| `OBJECTID` | int64 |  |
| `ISTAT_CODE` | int64 |  |
| `GEM_ID` | int64 |  |
| `NAME_I` | string |  |
| `NAME_D` | string |  |
| `STATUS_GZP` | int64 |  |
| `DESC_I` | string |  |
| `DESC_D` | string |  |
| `CODE` | int64 |  |
| `PERICOLO` | string |  |
| `GEFAHR` | string |  |
| `ID_PROCESS` | string |  |
| `PROCESSO` | string |  |
| `PROZESS` | string |  |
| `ID_GP` | string |  |
| `ID_GS` | string |  |
| `GRADODISTUDIO` | string |  |
| `BEARBEITUNGSTIEFE` | string |  |
| `X_LABEL` | double |  |
| `Y_LABEL` | double |  |
| `geometry` | binary |  |
| `bbox` | struct<xmin: double, ymin: double, xmax: double, ymax: double> |  |

Attribute names are bilingual as published by the Province (Italian `_IT`/`_I`, German `_DE`/`_D`, Ladin `_LD`). **Join key to municipalities/statistics: `ISTAT_CODE`, `GEM_ID` (ISTAT municipality code).**

## Data quality & usage notes

- Screening-quality mirror of an official dataset; for official use, re-query the Province's WFS.
- Attribute semantics (codes, classes) are those of the producing office; see the README and the portal record.
- Geometries that the extraction had to repair were cleaned on 2026-09-03 to valid single-type geometries (polygons, lines or points); `ST_IsValid` holds for every row.

## Related collections

Other themes of this catalog share the producer and licence. Municipality polygons and population live under `administrative-units/` and `population-and-statistics/` (join on `ISTAT_CODE`).
