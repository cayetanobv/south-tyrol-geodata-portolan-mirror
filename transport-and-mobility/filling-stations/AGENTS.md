# AGENTS.md — Filling stations — mirror of «Distributori di carburante», Provincia Autonoma di Bolzano

Agent-oriented guidance for this collection. Supplements `README.md` (people) and `collection.json` (software).

## Overview

Community mirror of the dataset «Distributori di carburante» published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data (CC0 1.0). Extracted on 2026-09-03 from WFS layer p_bz-TransportNetwork:Infrastructures-FillingStations and converted to GeoParquet. This copy is NOT the official publication: the authoritative source is the Province's geoportal and open-data portal (https://data.civis.bz.it/dataset/distributori-di-carburante). Published for the OGC Metadata Summit 2026 demo.

Source: WFS layer `p_bz-TransportNetwork:Infrastructures-FillingStations` of the Province's geoportal, mirrored to GeoParquet with spatial (Hilbert) ordering and a `bbox` column; a PMTiles archive and a MapLibre style (`styles/default.json`, derived from the provincial WMS style) accompany it. Geometry: Point; features: 160.

**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

Official record of the source dataset: https://data.civis.bz.it/dataset/distributori-di-carburante

## Accessing the data

```sql
INSTALL spatial; LOAD spatial;
SELECT * EXCLUDE (geometry) FROM read_parquet('filling-stations.parquet') LIMIT 5;
```

CRS is **OGC:CRS84 (WGS 84 lon/lat)**. Filter on the `bbox` struct column for spatial subsets (row-group pruning). Python: `geopandas.read_parquet('filling-stations.parquet')`.

## Schema & field notes

| Field | Type | Notes |
|---|---|---|
| `ID` | int64 |  |
| `IDENTNR` | int64 |  |
| `OWNER` | string |  |
| `BRAND` | string |  |
| `TYPE_IT` | string |  |
| `TYPE_DE` | string |  |
| `MUNICIPALITY_IT` | string |  |
| `MUNICIPALITY_DE` | string |  |
| `FRACTION_IT` | string |  |
| `FRACTION_DE` | string |  |
| `STREET_IT` | string |  |
| `STREET_DE` | string |  |
| `STREET_NUMBER` | string |  |
| `UTF_IDNR` | double |  |
| `HAS_PREPAY_SERVICE` | int64 |  |
| `HAS_POSTPAY_SERVICE` | int64 |  |
| `HAS_NIGHT_SERVICE` | int64 |  |
| `HAS_OTHER_SERVICE` | int64 |  |
| `HAS_SUPER_FUEL` | int64 |  |
| `HAS_UNLEADED_FUEL` | int64 |  |
| `HAS_DIESEL_FUEL` | int64 |  |
| `HAS_GPL_FUEL` | int64 |  |
| `HAS_METHANE_FUEL` | int64 |  |
| `HAS_AVIO` | int64 |  |
| `HAS_BIOD` | int64 |  |
| `CLOSURE_DATE` | string |  |
| `LABEL` | string |  |
| `SUSPENSION_FROM` | string |  |
| `SUSPENSION_TO` | string |  |
| `SUSPENDED` | int64 |  |
| `MISE_ID` | int64 |  |
| `SOS_STATION` | int64 |  |
| `SOS_POWER` | int64 |  |
| `geometry` | binary |  |
| `bbox` | struct<xmin: double, ymin: double, xmax: double, ymax: double> |  |

Attribute names are bilingual as published by the Province (Italian `_IT`/`_I`, German `_DE`/`_D`, Ladin `_LD`). No municipality code column: join spatially (ST_Intersects with `administrative-units/municipalities`).

## Data quality & usage notes

- Screening-quality mirror of an official dataset; for official use, re-query the Province's WFS.
- Attribute semantics (codes, classes) are those of the producing office; see the README and the portal record.
- Geometries that the extraction had to repair were cleaned on 2026-09-03 to valid single-type geometries (polygons, lines or points); `ST_IsValid` holds for every row.

## Related collections

Other themes of this catalog share the producer and licence. Municipality polygons and population live under `administrative-units/` and `population-and-statistics/` (join on `ISTAT_CODE`).
