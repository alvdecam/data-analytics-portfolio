# Cookie Cats A/B Test

An analysis of a real A/B test from the mobile game Cookie Cats, looking at whether moving a progression gate from level 30 to level 40 changed how many players came back to the game.

## Data

The dataset is the [Cookie Cats A/B testing dataset from Kaggle](https://www.kaggle.com/datasets/yufengsui/mobile-games-ab-testing) - about 90,000 real players, each randomly assigned to one of two versions of the game (gate at level 30 or level 40), with flags for whether they returned 1 day and 7 days after installing.

The notebook downloads the data automatically with `kagglehub`, so there's no CSV to place manually. If the download fails, search "Cookie Cats" / "Mobile Games A/B Testing" on Kaggle and update the dataset slug in the first cell.

## How to run

Open `ab-test-cookie-cats.ipynb` in Jupyter. The notebook needs:

- pandas
- numpy
- statsmodels
- scipy
- kagglehub

## What's in the notebook

1. Understanding the dataset and checking data quality
2. Cleaning (duplicate check, handling one implausible outlier, confirming the group labels)
3. Randomization balance check
4. Retention rates per group and the size of the difference
5. Significance test (two-proportion z-test, with a chi-square cross-check)
6. Effect size via a bootstrap 95% confidence interval
7. Recommendation, with limitations

## Main findings

Moving the gate to level 40 did not improve retention. Day-7 retention was slightly higher for the level-30 group (19.0% vs 18.2%, a 0.82 percentage-point difference). The difference is statistically significant (p = 0.0016) and the 95% confidence interval [0.33, 1.35] pp stays above zero, so it's a real effect rather than noise - but a small one. The recommendation is to keep the gate at level 30.

## Notes and caveats

- This is a real randomized experiment, so the groups differ only by the gate change and not by self-selection. That's what makes the significance test meaningful.
- The analysis measures retention, not revenue. Day-7 retention is a reasonable proxy for long-term engagement, but confirming the financial impact would need a follow-up looking at in-app spend or lifetime value.
- A note on the metric: with ~45,000 players per group the test is well powered, which is why even a sub-1-pp difference comes out significant. Significance here reflects both the effect and the large sample size.
