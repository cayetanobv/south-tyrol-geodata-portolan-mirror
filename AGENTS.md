# AGENTS.md — South Tyrol open geodata, community mirror

This catalog is a **community MIRROR** of 69 open datasets of the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol, grouped in 11 thematic subcatalogs. It is **not** the Province's official publication. **Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

## Themes (subcatalogs)

| Subcatalog | Content |
|---|---|
| `administrative-units/` | Municipalities, districts, provincial boundary and built-up centres of South Tyrol. |
| `population-and-statistics/` | Official statistics by municipality from ASTAT, the provincial statistics institute: resident population, families, language groups, tourism, vehicles, census sections. |
| `health/` | Health-care facilities and administrative health geography: hospitals, pharmacies, rest homes, health districts and regions, territorial services. |
| `hazard-zones-and-civil-protection/` | Approved municipal hazard-zone plans (hydraulic, avalanche, landslide, geological) and civil-protection plan data. |
| `nature-and-landscape/` | Protected areas, parks, Natura 2000 sites, biotopes, natural monuments, wetlands and landscape units. |
| `hydrology-and-water/` | Watercourses, lakes, drainage basins, glaciers, drinking-water protection, gauging stations and water quality. |
| `transport-and-mobility/` | Public transport stops, school buses, cycle and hiking routes, road infrastructure and counters. |
| `cultural-heritage/` | Listed historical monuments and archaeological sites. |
| `environment-and-infrastructure/` | Air-quality stations, wastewater treatment, district heating, telecom transmitters, quarries. |
| `geology/` | Geological overview units, main faults, rock glaciers, landslide events, boreholes. |
| `land-use/` | CORINE land cover. |

Every subcatalog and collection has its own `AGENTS.md` and `README.md`. All geometries are OGC:CRS84. Municipality code `ISTAT_CODE` (sometimes `ISTAT`) joins statistics, hazard zones and facilities to `administrative-units/municipalities/`.

## What the data is NOT for

- Point layers (hospitals, pharmacies, stops, stations) are **locations, not catchments or service areas**.
- Hazard classes are **approved planning zones, not event forecasts**; not every municipality has an approved plan.
- Results are **screenings**. For decisions, go to the Province's authoritative services.

## A worked question

```sql
INSTALL spatial; LOAD spatial;
-- Health facilities inside high / very-high hydraulic hazard zones (H3/H4)
WITH hz AS (
  SELECT ISTAT_CODE, geometry
  FROM read_parquet('hazard-zones-and-civil-protection/hazard-zones-hydraulic/*.parquet')
  WHERE PERICOLO LIKE '%(H3)%' OR PERICOLO LIKE '%(H4)%')
SELECT h.NAME_IT AS hospital, h.MUNICIP_IT AS municipality, p.BW_WOHNBEV AS residents
FROM read_parquet('health/hospitals/*.parquet') h
JOIN hz ON ST_Intersects(h.geometry, hz.geometry)
LEFT JOIN read_parquet('population-and-statistics/official-resident-population/*.parquet') p ON p.ISTAT_CODE = h.ISTAT
GROUP BY ALL ORDER BY municipality;
-- verified 2026-09-03: 4 of 17 hospitals, 31 of 158 pharmacies
```

## Reporting

Cite the producer (the Province), the licence (CC0 1.0), the source records on data.civis.bz.it, the mirror date (2026-09-03) and that a mirror was used. Attach the query.
