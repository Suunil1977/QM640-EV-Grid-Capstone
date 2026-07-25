# QM640 Capstone — Verified Official Data Source Registry
**Topic:** EV Charging Infrastructure vs. Adoption vs. Grid Stress (India, 2023–2026)
**Prepared:** 04 July 2026 | All sources are Government of India portals or official Parliament replies. No Kaggle. No synthesized data.

---

## DATASET 1 — Statewise Vehicle Registrations (All Types) and EV Registrations

### 1.1 Vahan Dashboard (PRIMARY SOURCE) — Ministry of Road Transport & Highways
- **Direct link:** https://analytics.parivahan.gov.in/analytics/publicdashboard/vahan?lang=en
- **Parent portal:** https://analytics.parivahan.gov.in/analytics/
- **What it gives:** State × Year × Month × Fuel type (incl. Pure EV, Strong Hybrid, Plug-in Hybrid) × Vehicle category registrations. Coverage from 2014 to current date. Exportable as Excel from the dashboard interface.
- **How to extract:** Public Dashboard → select "Fuel" tab → filter Fuel = ELECTRIC(BOV) → group by State → select calendar years 2023, 2024, 2025, 2026 → export. Repeat with no fuel filter for total (all-type) registrations.
- **Timestamp method:** The dashboard shows "data as on" at the top of each view. Record this date + your extraction date in your data log. Screenshot each export for the university's verification trail.
- **Known caveat (declare in your Limitations section):** Vahan 4 covers RTOs migrated to the platform; Telangana joined late and Lakshadweep is not fully covered for early years. Figures for the current year update continuously, so fix an extraction cut-off date and state it.

### 1.2 data.gov.in static snapshots (fixed-timestamp verification anchors) — MoRTH
These are frozen point-in-time tables the university can independently open and verify:
- State/UT-wise registered EVs **as on 06-03-2023**: https://www.data.gov.in/resource/stateut-wise-details-registered-electric-vehicles-india-e-vahan-portal-ministry-road
- State/UT-wise EVs **and total vehicles** on road **as on 14-07-2023**: https://www.data.gov.in/resource/stateut-wise-detailed-list-electric-vehicles-and-total-vehicles-roads-e-vahan-portal
- Year-wise registered EVs, **FY 2019-20 to FY 2023-24**: https://www.data.gov.in/resource/year-wise-number-registered-electric-vehicles-e-vahan-portal-2019-20-2023-24
- Full keyword index for newer snapshots: https://www.data.gov.in/keywords/Electric

### 1.3 NITI Aayog India Electric Mobility Index (secondary/cross-check)
- **Direct link:** https://iemi.niti.gov.in/dashboard/market-insights
- Government-owned dashboard sourced from Vahan; use to cross-validate your Vahan extracts, not as the primary citation.

---

## DATASET 2 — Statewise Public EV Charging Stations (Installed & Operational)

There is **no single downloadable statewise time series** from the government; the official record is a sequence of Parliament replies (via PIB) at fixed "as on" dates. This is actually favourable for your rubric — every figure is a ministerial statement with a legal timestamp. Two annexures have already been extracted into the accompanying CSV.

### 2.1 PIB / Ministry of Heavy Industries Parliament replies (PRIMARY SOURCE)
| As-on date | Metric | National total | Direct link |
|---|---|---|---|
| 02-02-2024 | **Operational** PCS, statewise (Annexure-II) | 12,146 | https://www.pib.gov.in/PressReleaseIframePage.aspx?PRID=2003003 |
| 01-08-2025 | **Installed** EVCS, statewise (Annexure) | 29,277 | https://www.pib.gov.in/PressReleasePage.aspx?PRID=2151390 |
| 01-08-2025 | Year-wise installs since 2022 + UP district-wise | 29,277 | https://www.pib.gov.in/PressReleasePage.aspx?PRID=2154127 |
| ~Mar 2025 (5-yr statewise) | Installed, statewise, fast (8,805) vs slow (20,346) split | 29,151 | https://www.pib.gov.in/PressReleasePage.aspx?PRID=2204635 |

### 2.2 data.gov.in — year-wise PCS deployment (trend series)
- **Direct link:** https://www.data.gov.in/resource/year-wise-details-public-electric-vehicle-ev-charging-stations-pcs-deployed-country-31st
- Year-wise PCS deployed, **31-12-2022 to 01-04-2025**. Source stated on the page: Rajya Sabha Session 267, Unstarred Question No. 3929, answered 04-04-2025.

### 2.3 Sansad (Parliament) question database — for the newest 2026 figures
- **Lok Sabha Q&A search:** https://sansad.in/ls/questions | **Rajya Sabha:** https://sansad.in/rs/questions
- Search "EV charging stations" filtered to Ministry of Heavy Industries / Ministry of Power, Budget Session 2026. Parliament data tabled in early 2026 reports the installed-vs-operational gap (installed ≈ 27,7xx vs operational ≈ 22,7xx as of March 2026 per secondary reporting) — **verify the exact figures from the tabled annexure PDF itself before citing**, since I could only confirm this via secondary sources.
- **Analytical note for your research questions:** the installed ≠ operational gap (~18% non-functional per that reply) is itself a strong finding for your grid-stress/utilization angle.

### 2.4 BEE EV Yatra portal (operational status, live)
- **Direct link:** https://evyatra.beeindia.gov.in
- Bureau of Energy Efficiency is the Central Nodal Agency for public charging infrastructure. Live operational counts differ slightly from PIB totals due to reporting lag — cite PIB for benchmarks, EV Yatra for operational-status context.

---

## DATASET 3 — Statewise Electricity Demand

### 3.1 CEA Power Supply Position reports (PRIMARY SOURCE) — Central Electricity Authority, Ministry of Power
- **Monthly Power Supply reports:** https://cea.nic.in/power-supply/?lang=en
- **Monthly reports archive (2023 → current):** https://cea.nic.in/monthly-reports-archive/?lang=en
- **What it gives:** For every State/UT, monthly **Energy Requirement vs Energy Availability (MU)** and **Peak Demand vs Peak Met (MW)** — exactly the demand variables you need, at the State × Month grain that joins with Vahan and the PIB charging data.
- **Timestamp method:** Each monthly PDF/XLS is dated in its header; the archive lists publication months. Download the monthly files for Apr-2023 through the latest available 2026 month.

### 3.2 CEA interactive dashboard (statewise, month-wise selectable)
- **Direct link:** https://cea.nic.in/dashboard/?lang=en
- Select Parameter = Power Supply Position → Month-wise → select each state. Good for quick validation; use the monthly PDFs as the citable source.

### 3.3 Ministry of Power Parliament reply — statewise energy requirement/supplied, FY 2023-24 onward
- **Direct link (PDF):** https://www.powermin.gov.in/static/uploads/2025/08/5804f7f17e764f9ba1951183379b8e31.pdf
- Rajya Sabha Q&A (03-02-2025) containing State/UT-wise power supply position for the last five years and FY 2024-25 up to December 2024 — a single citable document covering most of your window.

### 3.4 Supplementary
- **National Power Portal (daily statewise):** https://npp.gov.in
- **Grid-India (POSOCO) monthly operation reports:** https://grid-india.in — regional/state drawal and frequency data if your grid-stress model needs finer resolution.

---

## JOIN KEY & HARMONIZATION (critical before Synopsis lock)
- Common key: **State/UT × Month (or FY)**. All three datasets support it: Vahan (state × month), CEA (state × month), charging stations (state × as-on date snapshots — interpolate or treat as panel checkpoints).
- Harmonize names before joining: *U.P ↔ Uttar Pradesh; Pondicherry ↔ Puducherry; D&D and DNH ↔ UT of D&NH and D&D; Orissa ↔ Odisha*. The Feb-2024 annexure omits Ladakh and Mizoram (not yet reported), so treat those as missing, not zero.
- **The 2026 boundary:** calendar 2026 data exists only up to the current month, and FY 2025-26 CEA data completes after March 2026 publications. Define your study window explicitly (recommended: Jan 2023 – Mar 2026, i.e., FY 2022-23 Q4 through FY 2025-26) and state the extraction cut-off date in your methodology.

## VERIFICATION PROTOCOL FOR THE UNIVERSITY
For every extract, log four fields: (1) direct URL, (2) publisher (MoRTH/MHI/MoP/CEA), (3) the source's own "as on" date, (4) your download date + screenshot. The PIB releases carry Parliament reply identifiers (PRID + Question numbers), which are the strongest form of verifiable government citation available.
