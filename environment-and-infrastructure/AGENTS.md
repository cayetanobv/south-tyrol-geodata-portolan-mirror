# AGENTS.md — Environment and infrastructure

Air-quality stations, wastewater treatment, district heating, telecom transmitters, quarries. This theme is part of a **community MIRROR** of the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol's open geodata (CC0 1.0); not an official publication.
**Attribution (required by us, even though CC0 does not demand it):** data produced and published by the Provincia Autonoma di Bolzano – Alto Adige / Autonome Provinz Bozen – Südtirol as open data, licence CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/). **This is a community MIRROR, not the official publication.** Authoritative sources: the provincial WFS https://geoservices1.civis.bz.it/geoserver/ows and the open-data portal https://data.civis.bz.it. Mirrored 2026-09-03 by Cayetano Benavent for the OGC Metadata Summit 2026 demo. When you report results, cite the Province as the producer and state that a mirror was used.

## Collections in this theme

| Directory | Title |
|---|---|
| `air-quality-stations/` | Air quality stations — mirror of «Stazioni di misura della qualità dell’aria», Provincia Autonoma di Bolzano |
| `district-heating-zones/` | District heating zones — mirror of «Teleriscaldamento zone servite», Provincia Autonoma di Bolzano |
| `quarries-and-peat-bogs/` | Quarries and peat bogs — mirror of «Cave e torbiere (aree)», Provincia Autonoma di Bolzano |
| `telecom-transmitters/` | Telecom transmitters — mirror of «Impianti trasmittenti», Provincia Autonoma di Bolzano |
| `wastewater-treatment-plants/` | Wastewater treatment plants — mirror of «Impianti di depurazione biologici», Provincia Autonoma di Bolzano |

Each collection carries its own `AGENTS.md` with schema, join keys and caveats. Municipality polygons and population for joins: `../administrative-units/municipalities/`, `../population-and-statistics/official-resident-population/` (key `ISTAT_CODE`).
