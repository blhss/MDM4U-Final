# Data dictionary and audit rules

Unit: one country or territory; period: published 2023 observations/estimates. No population weights.

| Field | Definition / transformation |
|---|---|
| source_row | Row in original workbook Data sheet |
| country / iso3 | Original name and three-character WDI country/territory or aggregate code |
| afr | Original E column: annual births per 1,000 women ages 15–19 |
| tfr | Original M column: period total fertility, births per woman |
| region / income_group | Original Metadata - Countries sheet; used for aggregate filtering and region sensitivity |
| is_aggregate | Region absent; INX explicitly identified as Not classified |
| gdp_ppp | WDI NY.GDP.PCAP.PP.KD, 2023, constant 2021 international dollars per person |
| ln_gdp | Natural logarithm of positive gdp_ppp |
| female_schooling | UNDP HDR2025 mys_f_2023: mean schooling years of women ages 25+, published 2023 series including modeled/earlier-survey inputs |
| adult_contribution | tfr − 0.005 × afr, approximate arithmetic residual; not a separately measured adult or cohort fertility rate |
| complete | Not aggregate, all four main variables observed, GDP positive |
| inclusion_reason | Included or explicit missing-data/aggregate exclusion reason |

Original numeric strings such as '..' are converted to missing. No imputation or year substitution. Codes are unique before and after each one-to-one merge. The current WDI API leaves ISO3 empty for five income/Not-classified aggregates; its XD/XM/XN/XY/XT IDs are mapped to the original HIC/LIC/LMC/INX/UMC codes for the revision audit. These aggregates never enter the main models.

Raw source URLs and hashes: source_manifest.json. The copy original_data.xlsx is byte-identical to the source workbook. Model outputs use original fertility values; current WDI AFR/TFR are reserved for the revision audit and sensitivity. Source estimate uncertainty is not propagated into regression confidence intervals.
