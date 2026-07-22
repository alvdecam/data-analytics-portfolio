# Rossmann Store Sales — Demand Forecasting

Time-series forecasting of daily retail sales across 1,115 Rossmann drugstores in
Germany (January 2013 – July 2015), predicting total sales six weeks ahead.

The project deliberately implements the forecast **twice**: once "from scratch" by
engineering lag and calendar features so standard regressors can be used, and once
with Prophet. The comparison shows both what a forecasting library does internally
and why a fully interpretable approach is often preferable in a business setting.

## Question

Can we forecast total daily sales six weeks ahead — and does a model actually beat
a simple rule of thumb ("same weekday last week")?

## Notebooks

Run in order. Notebook 01 must run first; it produces the clean table the others read.

| Notebook | Purpose |
|---|---|
| **01_etl_pipeline.ipynb** | Download the raw data, join `train.csv` + `store.csv`, parse dates, handle nulls, save one tidy Parquet table. |
| **02_exploratory_analysis.ipynb** | Trend, weekly and yearly seasonality, promo lift. Each finding maps to a specific modelling decision in 03/04. |
| **03_forecasting_sklearn.ipynb** | Lag + calendar + promo features → Linear Regression and Random Forest vs. a seasonal-naive baseline. Fully interpretable, no extra dependencies. |
| **04_forecasting_prophet.ipynb** | Prophet with weekly/yearly seasonality and a promo regressor, plus component decomposition. |

## Approach

Time series breaks two assumptions that standard supervised ML relies on:

1. **Observations are not independent** — today's sales depend on yesterday's and on
   the same weekday last week. Solved with **lag features**: past values of the
   target become input columns, turning forecasting into ordinary regression.
2. **The train/test split cannot be random** — shuffling would let the model see the
   future. Solved with a **chronological split**: train on the earlier period, test
   on the last six weeks.

Every model is measured against a **seasonal-naive baseline** ("predict last week's
same weekday"). Without a baseline, an error figure says nothing about whether a
model earns its complexity.

Accuracy is reported as **WAPE** (weighted absolute percentage error), not the more
familiar MAPE. The series contains public holidays where nearly all stores shut and
the daily total falls to ~100,000 against a normal ~7,000,000; MAPE divides by each
day's actual value, so being off by 500,000 on one such day would read as a 500%+
error and swamp the average. WAPE divides summed error by summed actuals and is the
standard choice in retail forecasting.

## What is forecast, and why the total

The target is the **daily total across all open stores**, not the average per store.
The two agree most of the time but tell opposite stories exactly when the number of
open stores moves. The clearest case is Sunday: almost all German stores close, so
*average per store* makes Sunday look like the best day of the week, when for the
business it is one of the lowest — the average is only high because a few open stores
serve everyone. Forecasting the total answers the real question (how much money comes
in each day) and never mistakes "fewer stores open" for "more demand".

## Key findings

- **The weekly cycle dominates.** As a daily total, Monday is the clear peak (~8.4M),
  the working week steps down gently through Saturday (~6.3M), and Sunday collapses to
  almost nothing (~0.2M) because nearly every store is shut. The weekly shape is highly
  repeatable (median week-to-average correlation 0.97; 76% of weeks above 0.9), which
  is why `lag_7` — same weekday last week — is the backbone feature.
- **Promotions lift per-store sales by +38.8%**, running on 44.6% of trading days —
  large and frequent enough to be a reliable predictor. (Promo is measured per store,
  since it is a per-store decision: some stores promote while others don't on the same
  day.) Because promo enters the model as a feature, planners can simulate promo vs.
  non-promo weeks before committing.
- **The promo lift interacts strongly with weekday**: +57% on Monday falling to +22%
  by Friday, and promos never run on weekends. This is a real argument for tree-based
  models over purely additive ones.
- **December peaks at +12.6%** above the yearly average — real, but the weakest of the
  three effects; the rest of the year is fairly flat.
- **Closed days (17% of rows) are structural zeros**, not low demand — excluded from
  the analysis rather than modelled.
- **Random Forest is the strongest model, cutting the baseline's error to under a
  third** (WAPE 30.2% → 8.9%; MAE ~2.0M → ~600k). **Prophet reaches a similar level**
  (WAPE 8.4%) with almost no feature engineering. **Linear Regression trails** (WAPE
  15.1%): it cannot represent the promo × weekday interaction, which is the main reason
  the tree wins.
- **One-hot encoding the weekday did *not* help the linear model** — a deliberate test
  with an honest negative result. Because `lag_7` already encodes the weekly shape, the
  one-hot weekday flags came out at zero and the extra columns only added noise (one-hot
  WAPE 29.2% vs. the integer model's 15.1%). A useful reminder that a "correct" encoding
  adds nothing when another feature already carries the signal.
- **Prophet's promo estimate (~+2.6M) lands near the linear model's `PromoShare`
  coefficient (~3.4M)** — two very different methods pointing to a promo effect of the
  same rough size is a useful sanity check.

## Tools

pandas, scikit-learn, Prophet, matplotlib, pyarrow

## Data

Downloaded at runtime via `kagglehub` (`pratyushakar/rossmann-store-sales`), so no
CSVs are committed to this repository. If the slug fails, search "Rossmann Store
Sales" on Kaggle and swap it in notebook 01.

- `train.csv` — ~1M rows, one per store per day (sales, customers, open, promo, holidays)
- `store.csv` — 1,115 rows, one per store (type, assortment, competition)

## How to run

```bash
pip install -r requirements.txt
jupyter notebook 01_etl_pipeline.ipynb
```

Run `01_etl_pipeline.ipynb` first — it creates `data/rossmann_clean.parquet`, which
notebooks 02–04 depend on.

## Caveats

- This is an **aggregate** forecast across all stores. Store-level decisions would
  need per-store or hierarchical models.
- Accuracy is measured on a **single six-week window**. Rolling-origin
  cross-validation would give a more robust estimate.
- A subset of stores closed for refurbishment in the second half of 2014, so store
  coverage is not perfectly constant across the history. This shows up as a dip in the
  *total* series but not in per-store demand, so it is treated as a coverage effect,
  not a drop in sales.
- Tree models cannot extrapolate beyond their training range, so a sustained upward
  trend would need monitoring for drift.
