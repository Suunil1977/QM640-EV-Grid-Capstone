# QM640 Capstone — Data Dictionary
**Workbook:** QM640_Analysis_Panel_UPDATED.xlsx  
**Sheet:** Panel_State_FY  
**Dimensions:** 252 rows × 21 columns  
**Panel structure:** 36 Indian states/UTs × 7 financial years (FY2019-20 to FY2025-26)  
**Prepared:** July 2026 | Suunil Dabral | Walsh College QM640

---

## Column Definitions

| # | Column Name | Data Type | Nulls | Null % | Description | Source | Used in |
|---|---|---|---|---|---|---|---|
| 1 | State (ICED name) | text | 0 | 0.0% | State or Union Territory name as labelled in the NITI Aayog ICED portal export. Used as the panel join key across all sources. | NITI Aayog ICED portal | All RQs |
| 2 | FY | text | 0 | 0.0% | Financial year in format YYYY-YY (e.g. 2023-24). Indian financial year runs April to March. Panel covers FY2019-20 to FY2025-26. | Derived | All RQs |
| 3 | EV registrations | integer | 0 | 0.0% | Total number of electric vehicle registrations in the state in that financial year. Source: NITI Aayog ICED portal export (manual download). | ICED portal — iced.niti.gov.in | RQ1, RQ2, RQ3, RQ4 |
| 4 | Total registrations (all fuels) | integer | 0 | 0.0% | Total vehicle registrations across all fuel types (petrol, diesel, CNG, EV, hybrid etc.) in the state in that financial year. | ICED portal — iced.niti.gov.in | RQ1, RQ2 |
| 5 | Fuel-based (non-EV) registrations | integer | 0 | 0.0% | Derived: Total registrations minus EV registrations. Retained for audit trail. | Derived (col 4 − col 3) | Verification |
| 6 | EV share % | float (0–1) | 0 | 0.0% | Proportion of EV registrations to total registrations. Derived: col 3 ÷ col 4. Stored as a proportion (0–1); multiplied by 100 in all notebooks for display as percentage points. Complete across all 252 rows. | Derived | RQ1 (outcome), RQ2 (outcome), RQ3 (predictor lag), RQ4 (predictor) |
| 7 | Public chargers (snapshot) | integer (nullable) | 46 | 18.3% | Number of operational public EV charging stations in the state as per a point-in-time government snapshot. Used as a time-invariant covariate — same value repeated across all 7 FYs per state. Nulls: Ladakh and Mizoram absent from both PIB annexures. | PIB PRID 2003003 (Feb 2024) and PIB PRID 2151390 (Aug 2025) | RQ1, RQ2 |
| 8 | Charger snapshot definition & as-on | text | 46 | 18.3% | Text description of which PIB release the charger count came from and the as-on date. Provenance field — not used in modelling. Nulls match col 7. | PIB press releases | Documentation |
| 9 | Energy Requirement (MU) | float | 42 | 16.7% | Annual electricity energy requirement in Million Units (MU) for the state. Nulls: Ladakh, Lakshadweep, A&N absent from Ministry of Power Rajya Sabha reply annexure. | Ministry of Power Rajya Sabha reply | RQ3 (contextual) |
| 10 | Energy Supplied (MU) | float | 42 | 16.7% | Annual electricity energy supplied in Million Units (MU). Nulls match col 9. | Ministry of Power Rajya Sabha reply | RQ3 (contextual) |
| 11 | Energy Deficit % | float | 42 | 16.7% | Derived: (Energy Requirement − Energy Supplied) ÷ Energy Requirement. Negative values indicate surplus. Nulls match col 9. | Derived (cols 9, 10) | Contextual |
| 12 | PC-NSDP Current Rs (RBI/NSO) | float | 86 | 34.1% | Per capita Net State Domestic Product at current prices (Rs). The largest structural gap in the panel. Nulls: D&NH+D&D and Lakshadweep (no NSO series published); Gujarat FY2023-24 (not yet published at time of compilation); Ladakh (no separate NSO series post-bifurcation). Source: RBI Handbook of Statistics on Indian States 2024-25, Table 19. | RBI Handbook 2024-25, Table 19. URL: https://rbidocs.rbi.org.in/rdocs/Publications/DOCs/19T_11122025B8CC230E4A34431999B4D6A107707BCA.XLSX | RQ1 (control), RQ4 (predictor) |
| 13 | Urban % (Census 2011) | float | 0 | 0.0% | Percentage of state population living in urban areas per Census 2011 Primary Census Abstract (PCA). Complete across all 252 rows including bifurcated states: Telangana = 38.67%, Andhra Pradesh = 29.58%, D&NH+D&D = 58.51%, Ladakh = 22.61%. | Census 2011, MHA. Catalog ID 6191. URL: https://censusindia.gov.in/census.website/data/census-tables | RQ1 (control), RQ4 (predictor) |
| 14 | Annual Peak Demand (MW) | float | 21 | 8.3% | Annual peak electricity demand in Megawatts — defined as the maximum of monthly peak demand values for that financial year. Nulls: Ladakh, Lakshadweep, A&N absent from ICED statewise peak-demand exports. | ICED portal statewise peak demand exports (34 state sheets) | RQ3, RQ4 |
| 15 | Annual Avg Demand (MW) | float | 21 | 8.3% | Annual average electricity demand in Megawatts — mean of monthly average demand values. Nulls match col 14. | ICED portal statewise peak demand exports | Contextual |
| 16 | Peak-to-Avg Ratio | float | 21 | 8.3% | Derived: Annual Peak Demand ÷ Annual Avg Demand. Load factor indicator. Nulls match col 14. | Derived (cols 14, 15) | Contextual |
| 17 | Peak-demand YoY growth | float | 54 | 21.4% | Year-on-year growth rate of annual peak demand: (Peak_t − Peak_{t-1}) ÷ Peak_{t-1}. Nulls: FY2019-20 structurally impossible (no FY2018-19 baseline in panel); Ladakh, Lakshadweep, A&N have no peak demand data. Total 54 nulls = 33 states × 1 FY (FY2019-20) + 3 UTs × 6 FYs (FY2020-21 to FY2025-26) = 33 + 21. | Derived from col 14 | RQ3 (outcome) |
| 18 | Grid-stress class | integer (0/1, nullable) | 54 | 21.4% | Binary outcome variable for RQ4. Defined as: 1 if the state's Peak-demand YoY growth (col 17) exceeds the all-state median YoY growth for that financial year; 0 otherwise. Median is computed separately for each FY cross-section, producing a near-balanced outcome by construction. Nulls: same 54 rows as col 17. Class balance: 102 zeros, 96 ones (full df_rq4 N=198). | Derived from col 17 | RQ4 (binary outcome) |
| 19 | Projected population | integer | 0 | 0.0% | State population projection used as the denominator for charger density calculation. Source: NCP/MoHFW Technical Group Report on Population Projections, November 2019, Table 8. Complete across all 252 rows. | NCP/MoHFW Technical Group Report, Nov 2019. URL: https://nhm.gov.in/New_Updates_2018/Report_Population_Projection_2019.pdf | RQ1, RQ2 (denominator) |
| 20 | Chargers per 100k population | float | 46 | 18.3% | Derived: (Public chargers snapshot ÷ Projected population) × 100,000. Primary predictor for RQ1 and RQ2. Nulls match col 7 (same two states: Ladakh, Mizoram). | Derived (cols 7, 19) | RQ1 (predictor), RQ2 (grouping variable) |
| 21 | Remarks | text | 0 | 0.0% | Per-cell source provenance notes. Documents which source each value came from, any reconciliation decisions, and gap explanations. Complete across all 252 rows. Not used in modelling — audit trail only. | Compiled during panel construction | Documentation |

---

## Declared Structural Data Gaps

All nulls in this panel are permanent structural gaps — no alternative official source exists.

| Gap | Columns affected | Root cause |
|---|---|---|
| Ladakh + Mizoram charger data | 7, 8, 20 | Absent from both PIB charger annexures (PRID 2003003 and 2151390) |
| D&NH+D&D + Lakshadweep NSDP | 12 | No NSO Net State Domestic Product series published for these UTs |
| Gujarat FY2023-24 NSDP | 12 | Not yet published by NSO/RBI at time of panel compilation |
| Ladakh NSDP | 12 | No separate NSO series post-bifurcation from J&K in 2019 |
| Ladakh + Lakshadweep + A&N peak demand | 9, 10, 11, 14, 15, 16, 17, 18 | Absent from ICED and Ministry of Power statewise data exports |
| FY2019-20 YoY growth | 17, 18 | Structurally impossible — no FY2018-19 baseline in study panel |

---

## Three Declared Cross-Source Reconciliation Gaps

These are known discrepancies between official sources — declared transparently and not corrected:

1. **ICED vs PIB EV totals (~3.3% discrepancy):** ICED portal EV registration totals exceed Parliament reply (PIB) figures by approximately 3.3%, attributable to Telangana's late migration to the Vahan 4 platform.

2. **CEA All-India energy totals vs state-row sums:** CEA-published All-India energy requirement and supply totals exceed the sum of state rows due to unattributed demand categories not broken out by state.

3. **Sum of state peaks vs national peak (coincidence factor):** The arithmetic sum of state annual peak demands exceeds the published national peak demand figure, because state peaks do not occur simultaneously — this is a standard power systems coincidence factor and is not an error.

---

## RQ Analytical Subsets

| Subset | N | FY | Variables required | Used in |
|---|---|---|---|---|
| df_cross | 31 states | FY2023-24 | EV share %, Chargers/100k, PC-NSDP, Urban % | RQ1 |
| df_rq2 | 34 states | FY2023-24 | EV share %, Chargers/100k | RQ2 |
| df_panel / df_lag | 198 / 165 rows | FY2020-21 to FY2025-26 | EV share %, Peak-demand YoY growth | RQ3 |
| df_rq4 / df_cc | 198 / 123 rows | FY2020-21 to FY2025-26 | Grid-stress class + 4 predictors | RQ4 |

---

*This data dictionary was compiled by Suunil Dabral for the Walsh College QM640 Data Analytics Capstone. All sources are official Government of India publications. Walsh College evaluators may independently verify every URL listed above.*
