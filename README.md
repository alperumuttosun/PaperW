# Network structure in cross-country crop-yield transferability: replication code

All analysis code is in one file, `network_pipeline.R` (Steps 1–10). The input data are the eight country-year panels `panelv7_<crop>.xlsx` (wheat, barley, oats, rye, rice, maize, soybean, sorghum), provided in the data files.

## How to run

1. Put the eight `panelv7_*.xlsx` files in one folder and set that folder in `candidate_dirs` at the top of `network_pipeline.R`.
2. Install the packages: `readxl`, `dplyr`, `igraph`, `writexl`, `glmnet`, `xgboost` (and `WDI` only for Step 10).
3. Run `network_pipeline.R`. Outputs are written to the subfolder `network_paper/` as Excel files.

Steps 1 and 5 are skipped automatically if their output file already exists. Random seeds are fixed.

## Steps

| Step | What it does | Time | Output |
|---|---|---|---|
| 1 | Negative-transfer computation (LASSO and XGBoost, 5 repeats) | about 19 h | `networkstep1_output.xlsx` |
| 2 | Community detection, null model 1, comparison with climate/GDP clusters | minutes | `networkstep2_output.xlsx` |
| 3 | Source and target roles of countries | seconds | `networkstep3_output.xlsx` |
| 4 | GDP versus climate: which explains communities better | seconds | `networkstep4_eta_output.xlsx` |
| 5 | Pool-size check (10, 15, 20) for three crops | about 4 h | `networkstep5_poolsize_summary.xlsx` |
| 6 | Stability of communities across repeated draws | minutes | `networkstep6_output.xlsx` |
| 7 | Null model 2 (random network with the same degree sequence) | minutes | `networkstep7_output.xlsx` |
| 8 | Checks and descriptive numbers (pair counts, sign agreement, yield skewness) | seconds | `networkstep8_output.xlsx` |
| 9 | Figures 1 and 2 (PDF, EPS, 1600-dpi TIFF, 300-dpi PNG) | seconds | `network_paper/figures/` |
| 10 | Optional data check: where the GDP values come from (needs internet; off by default) | minutes | `networkstep10_output.xlsx` |
| 00 | Data download and panel construction (see note below) | very long | the eight `panelv7_*.xlsx` files |

**Step 00 note.** Step 00 is listed last. It is only the code that downloads and prepares the raw data. Please do not run it: it takes very long, and the prepared panels are already provided in the data files.
