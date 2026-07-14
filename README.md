# QM640 Capstone — EV Charging Infrastructure, Adoption, and Grid Stress in India

## Problem Statement
India's EV adoption, public charging deployment, and electricity-grid planning are progressing without an empirical model that connects them at the state level. This project builds a State × Financial-Year panel (FY2019-20 to FY2025-26) from official Government of India sources to test four hypotheses linking charger density, EV adoption, and grid stress.

## Research Questions
1. **RQ1** — Does public charging-infrastructure density significantly predict EV adoption across Indian states? (Multiple regression)
2. **RQ2** — Is there a significant difference in mean EV adoption between high- and low-charger-density states? (t-test / ANOVA)
3. **RQ3** — Does EV adoption significantly predict growth in state electricity demand? (Lagged panel regression)
4. **RQ4** — Do charging-infrastructure, EV-adoption, and economic variables significantly predict the probability of a state being in high grid stress? (Logistic regression)

## Data Sources (all official, direct URLs)
| Dataset | Publisher | URL |
|---|---|---|
| EV / total vehicle registrations | MoRTH (Vahan) via NITI Aayog ICED | https://iced.niti.gov.in |
| Public charging stations (operational, installed) | Ministry of Power / MHI, PIB | PRID 2003003, PRID 2151390 |
| Energy Requirement vs. Supplied | Ministry of Power, Rajya Sabha Q.150 | powermin.gov.in |
| Statewise peak demand | NITI Aayog ICED dashboard | https://iced.niti.gov.in |
| Per-capita NSDP | MoSPI, PIB PRID 1942055 | pib.gov.in |
| Urban population share | Census of India 2011 | censusindia.gov.in |
| Projected population | National Commission on Population, MoHFW | nhm.gov.in |

Full source registry with as-on dates and extraction dates: see `docs/source_registry.md`.

## Repository Structure
See `docs/folder_tree.txt` for the full layout.

## Reproducibility
No dataset here is interpolated or synthesized. Charging-station figures are used only at their as-on snapshot dates. All derived columns (EV share %, Energy Deficit %, grid-stress class) are computed with documented formulas in `docs/data_dictionary.md`.

## License / Use
Code (src/, notebooks/) is MIT licensed — see `LICENSE`. Underlying datasets (data/) are Government of India public data, each with its own source and terms documented in `docs/source_registry.md`. The synopsis report (reports/) is academic coursework for Walsh College QM640, shared here for reviewer transparency, not for reuse.
