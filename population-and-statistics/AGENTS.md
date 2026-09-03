# AGENTS.md — Population and statistics (ASTAT)

Official statistics by municipality from ASTAT, the provincial statistics institute: resident population, families, language groups, tourism, vehicles, census sections. This theme is part of a **community MIRROR** of the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol's open geodata (CC0 1.0); not an official publication.
**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

## Collections in this theme

| Directory | Title |
|---|---|
| `census-sections-2021/` | Census sections 2021 — mirror of «Sezioni di censimento 2021», Provincia Autonoma di Bolzano |
| `language-groups-2024/` | Language groups 2024 — mirror of «Appartenenza linguistica Censimento 2024», Provincia Autonoma di Bolzano |
| `official-resident-population/` | Official resident population — mirror of «Popolazione ufficiale [numero]», Provincia Autonoma di Bolzano |
| `registered-vehicles/` | Registered vehicles — mirror of «Veicoli iscritti nel registro automobilistico (PRA)  [numero]», Provincia Autonoma di Bolzano |
| `resident-families-civil-registry/` | Resident families civil registry — mirror of «Famiglie residenti Anagrafe [numero]», Provincia Autonoma di Bolzano |
| `resident-population-civil-registry/` | Resident population civil registry — mirror of «Popolazione residente Anagrafe [numero]», Provincia Autonoma di Bolzano |
| `tourist-overnight-stays/` | Tourist overnight stays — mirror of «Turismo Pernottamenti [numero]», Provincia Autonoma di Bolzano |

Each collection carries its own `AGENTS.md` with schema, join keys and caveats. Municipality polygons and population for joins: `../administrative-units/municipalities/`, `../population-and-statistics/official-resident-population/` (key `ISTAT_CODE`).
