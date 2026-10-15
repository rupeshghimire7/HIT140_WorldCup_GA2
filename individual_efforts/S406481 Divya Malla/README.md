# FIFA World Cup 2026: Linear Regression (Assessment 3, Objective 2)

Divya Malla (S406481) · Sydney Group 25

## How to run
1. Install the packages: `pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn lxml`
2. Open `WC2026_Linear_Regression.ipynb` and choose **Run All**. It takes about 2–3 minutes.
3. Figures and the two final datasets are saved to `outputs/`.

## Data (raw, unchanged)
| File | Content |
|---|---|
| `data_raw/fbref_wc2026_scores_fixtures.html` | FBref *2026 World Cup Scores & Fixtures* page (saved): all 104 matches with round, date, teams, score, venue and notes |
| `data_raw/results.csv` | about 49,900 men's international matches, 1872–2026, used for each team's pre-match history and to cross-check the FBref scores |

## Final datasets
* `outputs/lr21_dataset.csv`: 104 rows, 8 explanatory variables, target `goal_diff`
* `outputs/lr22_dataset.csv`: 208 rows, 8 explanatory variables, target `goals`

## Decision log
| Decision | Why |
|---|---|
| Use FBref match scores as targets | official source named in the brief |
| Build our own Elo, form and attack/defence variables from match history | all are known before kick-off |
| LR 2.1 uses match differences; LR 2.2 uses team and opponent levels | keeps the two models distinct (0 shared variables) |
| Select 8 variables by \|Pearson r\| ranking with a VIF < 5 rule | brief requires exactly 8; avoids multicollinearity |
| Tune every competing algorithm with a grid search before comparing | fair, systematic comparison |
| Apply the five optimisation steps and keep a step only if it helps across 50 CV splits | rigorous, not judged on one lucky split |
| LR 2.1 final = baseline OLS; LR 2.2 final = OLS + outlier removal + Yeo-Johnson + z-standardisation | steps did not help 2.1; they helped 2.2 slightly |
| Recommend linear regression for both tasks | equal accuracy to all competitors, interpretable |
