# Modelling the Relationship Between Electric Vehicle Adoption, Public Charging Infrastructure, and Electricity-Grid Stress Across Indian States

**Student:** Suunil Dabral | sdabral@mail.walshcollege.edu
**Institution:** Walsh College
**Course:** QM640: Data Analytics Capstone
**Mentor:** Vikas S
**Term:** Summer 2026
**Study Period:** FY2019–20 to FY2025–26

---

## Project Overview

This capstone project investigates the empirical relationship between public EV charging infrastructure density, electric vehicle (EV) adoption rates, and electricity grid stress across 36 Indian states and Union Territories over seven financial years (FY2019–20 to FY2025–26). All data are sourced exclusively from official Government of India publications. The project addresses four research questions through panel regression, group comparison, and classification methods.

---

## Research Questions and Results

| RQ | Question | Method | Primary Result |
|---|---|---|---|
| RQ1 | Does charging infrastructure density significantly predict EV adoption? | OLS multiple regression + Ridge | F(3,27)=4.18, p=.015 — model significant; charger density positive but not individually significant |
| RQ2 | Do high-density states have significantly higher EV adoption? | Welch t-test (two-tailed) + ANOVA | t(31.97)=1.499, p=.144 — fail H0; ANOVA significant (p=.015, η²=.237) |
| RQ3 | Does prior-year EV adoption predict electricity demand growth? | Lagged panel regression + year FE | β_lag=0.0199, p=.902 — fail H0 |
| RQ4 | Do infrastructure, adoption, and economic variables predict grid stress? | Logistic regression (5 predictors) + ML benchmark | χ²(5)=3.35, p=.646 — fail H0; AUC=0.576 |

---

## Repository Structure

```
QM640-EV-Grid-Capstone/
├── README.md
├── LICENSE
├── .gitignore
├── data/
│   ├── raw/                                        # Verbatim government exports
│   │   ├── ICED_EV_Vehicle_Registered.xlsx         # NITI Aayog ICED portal
│   │   ├── CEA_PeakDemand_Statewise_34sheets.xlsx  # CEA statewise peak demand
│   │   ├── PIB_Chargers_Operational_02Feb2024.pdf  # PIB PRID 2003003
│   │   └── PIB_Chargers_Installed_01Aug2025.pdf    # PIB PRID 2151390
│   └── panel/
│       └── QM640_Analysis_Panel_UPDATED.xlsx       # Master panel — 252 rows × 21 cols
├── notebooks/
│   ├── 01_data_cleaning_join.ipynb                 # Data cleaning and verification
│   ├── 02_eda.ipynb                                # Exploratory data analysis
│   ├── 03_RQ1_regression.ipynb                     # RQ1: OLS regression + Ridge
│   ├── 04_RQ2_ttest_anova.ipynb                    # RQ2: Welch t-test (two-tailed) + ANOVA
│   ├── 05_RQ3_lagged_panel.ipynb                   # RQ3: Lagged panel regression + two-way FE
│   └── 06_RQ4_logistic_classification.ipynb        # RQ4: Logistic regression + ML benchmark
├── reports/
│   ├── QM640_Synopsis_Suunil_Dabral.docx           # Submitted synopsis
│   └── QM640_Interim_Report_Suunil_Dabral.docx     # Interim report
├── images/
│   └── screenshots/                                # Executed Colab notebook outputs
│       ├── nb01_shape_check.png
│       ├── nb01_null_audit.png
│       ├── nb01_dtype_correction.png
│       ├── nb01_subset_sizes.png
│       ├── nb02_descriptive_stats_png_1.png
│       ├── nb02_descriptive_stats_png_2.png
│       ├── nb02_distributions.png
│       ├── nb02_correlation_heatmap.png
│       ├── nb02_null_heatmap.png
│       ├── nb03_ols_coefficients.png
│       ├── nb03_ols_assumption_diagnostics.png
│       ├── nb03_residual_plots.png
│       ├── nb03_ridge_path.png
│       ├── nb04_ttest_results.png
│       ├── nb04_anova_results.png
│       ├── nb05_lag_regression.png
│       ├── nb05_twoway_fe.png
│       ├── nb06_logistic_results_1.png
│       ├── nb06_logistic_results_2.png
│       ├── nb06_ml_benchmark_1.png
│       └── nb06_ml_benchmark_2.png
└── docs/
    ├── QM640_EV_Data_Source_Registry.md            # All source URLs and provenance
    ├── data_dictionary.md                          # All 21 column definitions
    └── folder_tree.txt                             # This repository structure
```

---

## Master Panel

**File:** `data/panel/QM640_Analysis_Panel_UPDATED.xlsx` | Sheet: `Panel_State_FY`
**Dimensions:** 252 rows × 21 columns
**Coverage:** 36 Indian states and Union Territories × 7 financial years (FY2019–20 to FY2025–26)
**Unit of analysis:** State × Financial Year

### Analytical Subsets

| Subset | N | FY Coverage | Used For |
|---|---|---|---|
| df_cross | 31 states | FY2023–24 | RQ1 — OLS regression |
| df_rq2 | 34 states (17 per group) | FY2023–24 | RQ2 — Welch t-test |
| df_lag | 165 rows | FY2021–22 to FY2025–26 | RQ3 — Lagged panel |
| df_cc | 123 rows | FY2020–21 to FY2025–26 | RQ4 — Logistic regression |

---

## Data Sources

All data are from official Government of India publications. No private or commercial datasets are used.

| Source | Variable(s) | URL |
|---|---|---|
| NITI Aayog ICED portal | EV registrations; peak demand | https://iced.niti.gov.in |
| Ministry of Heavy Industries (PIB PRID 2003003) | Public chargers operational 02.02.2024 | https://pib.gov.in/PressReleaseIframePage.aspx?PRID=2003003 |
| Ministry of Heavy Industries (PIB PRID 2151390) | Public chargers installed 01.08.2025 | https://pib.gov.in/PressReleasePage.aspx?PRID=2151390 |
| Reserve Bank of India Handbook 2024–25, Table 19 | Per capita NSDP | https://rbi.org.in |
| Census 2011 Primary Census Abstract | Urban % | https://censusindia.gov.in/nada/index.php/catalog/6191 |
| MoHFW NCP Technical Group Report 2019 | Projected population | https://nhm.gov.in/New_Updates_2018/Report_Population_Projection_2019.pdf |
| Ministry of Power Rajya Sabha reply | Energy requirement/supply | https://powermin.gov.in |
| CEA Power Supply Reports | Peak demand cross-check | https://cea.nic.in/power-supply/?lang=en |

---

## Declared Data Gaps

All null values are permanent structural gaps traceable to official sources — no imputation was applied.

| Variable | Nulls | Root Cause |
|---|---|---|
| Chargers per 100k | 46 (18.3%) | Ladakh and Mizoram absent from both PIB annexures |
| PC-NSDP | 86 (34.1%) | D&NH+D&D, Lakshadweep, Gujarat FY2023–24, Ladakh: no NSO series |
| Annual Peak Demand | 21 (8.3%) | Ladakh, Lakshadweep, A&N absent from ICED exports |
| YoY growth / Grid-stress class | 54 (21.4%) | FY2019–20 structurally impossible (no FY2018–19 baseline) |

### Three Declared Cross-Source Reconciliation Gaps

1. ICED portal EV totals exceed PIB Parliamentary reply figures by ~3.3% (Telangana late Vahan 4 migration)
2. CEA All-India energy totals exceed sum of state rows (unattributed demand categories)
3. Sum of state annual peak demands exceeds national peak (coincidence factor — standard in power systems)

---

## Running the Notebooks

All notebooks are designed for **Google Colab**.

1. Upload `data/panel/QM640_Analysis_Panel_UPDATED.xlsx` to your Colab session
2. Run notebooks in order: 01 → 02 → 03 → 04 → 05 → 06
3. Each notebook reads directly from `QM640_Analysis_Panel_UPDATED.xlsx` — no intermediate cleaned file is created

**Requirements:** pandas, numpy, scipy, sklearn, matplotlib (all pre-installed on Colab)

---

## Key Methodological Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Charger density denominator | Per 100,000 population | MoHFW NCP Technical Group Report, Nov 2019, Table 8 |
| Grid stress definition | Binary: 1 if YoY peak demand growth > all-state FY median | Avoids absolute threshold; near-balanced outcome (102 vs 96) |
| RQ2 test direction | Two-tailed (H1: μHigh ≠ μLow) | Per synopsis specification |
| RQ4 predictor count | 5 predictors (EV share %, Chargers/100k, PC-NSDP, Urban %, EVgrowth) | Per synopsis specification; EPV=12.0 ≥ 10 |
| RQ3 outcome variable | Peak-demand YoY growth (MW) | Better state-level coverage than energy requirement (MU) |
| Charger snapshot | Time-invariant covariate | Same official snapshot value repeated across all FYs per state |
| No imputation | All nulls retained | Structural gaps — no alternative official source exists |

---

## Deliverables Status

| Deliverable | Status |
|---|---|
| Synopsis (25pp, APA7, 21 refs) | ✅ Submitted |
| Master panel (252×21) | ✅ Complete and locked |
| Notebooks 01–06 | ✅ Built and executed in Colab |
| GitHub repository | ✅ Complete |
| Interim Report (200 marks) | ✅ Complete |
| Final Report | 🔲 Pending |
| Final Presentation | 🔲 Pending |

---

## Citation

Dabral, S. (2026). *Modelling the relationship between electric vehicle adoption, public charging infrastructure, and electricity-grid stress across Indian states.*

---

*All data sourced from official Government of India publications. Walsh College evaluators may independently verify every source URL listed above.*
