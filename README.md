# HIT140 Assessment 3, Objective 2: FIFA World Cup 2026

Predicting the **goal difference** of a match (LR 2.1) and the **goals scored by one team** (LR 2.2) with multiple linear regression, using only information known before kick-off. Linear regression is then compared with eight other regression models.

**Group:** Sydney 25

| Member | Student ID |
|---|---|
| Rupesh Ghimire | s403354 |
| Quoc An Vuong | s406838 |
| Gaurav Aryal | s403279 |
| Divya Malla | s406481 |

This README describes the final submission folder, `FINAL_SUBMISSION_CODE_DOCS/`. The other top-level folders in the repository hold individual members' working files and are not part of the submission.

## The two tasks

| | LR 2.1 | LR 2.2 |
|---|---|---|
| Target | goal difference (home minus away) | goals scored by one team |
| Rows | 104 (one per match) | 208 (one per team per match) |
| Explanatory variables | exactly 8 | exactly 8 |
| Shared with the other model | 4 | 4 |
| Unique to this model | 4 | 4 |

Together the two models use **12 distinct variables** (4 shared + 4 unique + 4 unique). Every variable is known before kick-off.

## Folder structure (final submission folder)

```
FINAL_SUBMISSION_CODE_DOCS/
├── data/                                 input files (see below)
├── report/                               HIT140_A3_Group_Report.docx (group report, max 4 pages)
├── notebook/
│   └── HIT140_Objective2_Analysis.ipynb  the full analysis, run top to bottom
└── output/                               created when the notebook runs
    ├── figures/                          fig1 to fig9 (PNG)
    ├── lr21_final_dataset.csv            104 rows: id columns, target, the 8 variables
    ├── lr22_final_dataset.csv            208 rows: id columns, target, the 8 variables
    ├── lr21_all_candidates.csv, lr22_all_candidates.csv   every candidate variable
    ├── variable_selection_table.csv      expected sign, correlation, VIF, decision
    ├── optimisation_stages.csv           result of each optimisation step
    ├── model_comparison_21.csv, model_comparison_22.csv
    ├── bootstrap_table.csv, summary_table.csv
```

## Data (put these files in `data/`)

| File | Used for |
|---|---|
| `fbref_matches.csv` | The 104 matches: date, kick-off time, venue, round, score. Source of both targets and the match order. |
| `worldcup2026_elo.csv` | Elo rating of both teams **before** each match (the "after" columns are used only for an integrity check). |
| `worldcup2026_market_value_transfermarkt_million.csv` | Squad market value in € million (log scale in the model). |
| `team_appearances.csv` | World Cup history since 1930: earlier tournaments played and historical goal difference (men's tournaments only). |
| `international-fifa-world-cup-2018-russia-matches-2018-to-2018-stats.csv` | 2018 match statistics (possession, shots, corners, cards, fouls, clean sheets). |
| `international-fifa-world-cup-2022-qatar-matches-2022-to-2022-stats.csv` | 2022 match statistics, same columns. |

`world_cup_match_data.csv` and `.xlsx` are **not read by the notebook**. If they are in your repository, they do no harm.

Source URLs (add before submitting): FBref, World Football Elo ratings, Transfermarkt, the World Cup history database, FootyStats (2018 and 2022 files).

## How to run

1. Python 3.10 or newer. From the repository root, install the packages with `pip install -r requirements.txt`. The notebook imports pandas, numpy, scipy, matplotlib, seaborn, statsmodels and scikit-learn, and runs in Jupyter.
2. Check that `FINAL_SUBMISSION_CODE_DOCS/data/` contains the six files above.
3. Open `FINAL_SUBMISSION_CODE_DOCS/notebook/HIT140_Objective2_Analysis.ipynb` in Jupyter and choose **Run All**. The notebook reads `../data/` and writes `../output/`. It does not use Google Drive and needs no internet access. A full run takes a few minutes.

If any integrity check fails, the notebook stops with an assertion error that names the check.

## What the notebook does

1. **Data source justification**: why external sources were used beyond the three recommended sites.
2. **Load and clean**: strip country codes from FBref team names, read penalty-shoot-out scores, one team spelling for all files, 8 integrity checks, an Elo join check (a team's Elo after one match equals its Elo before the next, 100% of matches).
3. **EDA**: target distributions, goals by stage, Elo against squad value.
4. **Leak-safe variables**: form from earlier matches only, using a shrunk average so a team's first match is not filled with zeros. Two leak checks, including shuffling the results of matches 85+ and confirming no earlier feature changes.
5. **Variable selection**: availability audit, expected signs written first, then Pearson correlation and VIF on the first 83 matches only. Shared variables are the four strongest on average across both tasks; unique ones come from separate pools.
6. **Modelling**: chronological split (matches 1-83 train, 84-104 test), grouped 5-fold cross-validation, five optimisation steps (outlier removal, non-linearity check, multicollinearity check, Yeo-Johnson, z-standardisation), each kept only if cross-validation improves. OLS inference with cluster-robust standard errors for LR 2.2.
7. **Feature analysis**: drop-one-variable and shared-only versus unique-only experiments.
8. **Competing models**: Ridge, Lasso, Elastic Net, kNN, SVR, Random Forest, Gradient Boosting, and Poisson (LR 2.2). Settings tuned inside the training matches, then judged on the 21 held-out matches and a rolling backtest (matches 49-104), with a bootstrap over matches.

## The 12 variables

| Type | LR 2.1 (home minus away) | LR 2.2 (team minus opponent, or team/opponent) |
|---|---|---|
| Shared (4) | squad value (log), Elo, earlier World Cups played, historical World Cup goal difference | same four |
| Unique (4) | possession, corners, fouls (2018/22), confederation strength | own shots (2018/22), opponent's shots on target conceded (2018/22), opponent's goals conceded and clean-sheet rate in 2026 so far |

## Main results

| | LR 2.1 | LR 2.2 |
|---|---|---|
| R² / adjusted R² (training) | 0.554 / 0.506 | 0.329 / 0.292 |
| Test RMSE, 21 matches (mean baseline) | 1.469 (1.747) | 1.273 (1.322) |
| Backtest RMSE, 56 matches (mean baseline) | 1.335 (1.956) | 1.248 (1.293) |
| Best model on the backtest | SVR (1.29), not clearly better than linear regression | Random Forest (1.13) |

Squad market value is the clearest predictor in both models. The four unique variables add very little. The 21-match test set is small, and the backtest overlaps the training period for matches 49-83, so differences between the top models should not be over-read.

## Limitations

- Only 104 matches; the hold-out test has 21.
- Elo, squad value and World Cup experience are strongly correlated, so single coefficients are unstable.
- 18 of 48 teams played neither the 2018 nor the 2022 World Cup and receive the all-team average for the style variables.
- No 2026 bookmaker odds or in-match statistics are used.

## Reproducibility

All random steps use seed 42. Results should be identical on the same package versions; small differences in the last digit can appear across scikit-learn versions.

## AI usage

Generative AI (Claude) was used for brainstorming, for the notebook code and its notes, and for report drafts. See the signed AI Usage Declaration Form for the full account and the conversation link.