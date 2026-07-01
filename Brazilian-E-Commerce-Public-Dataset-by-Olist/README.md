# Olist E-Commerce Analysis

A data engineering and data science project using the [Brazilian E-Commerce public dataset from Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — real orders placed on the platform between 2016 and 2018, covering customers, sellers, products, payments, reviews, and geolocation.

## Data

Download the dataset from Kaggle and place the CSV files in a folder. Update the `path` variable in `01_etl_pipeline.ipynb` to point to that folder. The ETL notebook will create `olist_analysis.db` (a local SQLite database) which the other two notebooks read from.

## How to run

Open the notebooks in order in Jupyter:

1. `01_etl_pipeline.ipynb`
2. `02_exploratory_analysis.ipynb`
3. `03_machine_learning.ipynb`

Dependencies: pandas, numpy, matplotlib, seaborn, plotly, sqlalchemy, scikit-learn

## What's in the notebooks

**01 — ETL pipeline**: loads the raw CSVs, cleans data types and nulls, engineers two delivery columns (`delivery_days` and `delivery_early_days`), runs plausibility checks on outliers, and loads everything into a SQLite database.

**02 — Exploratory analysis**: answers 11 questions about the data — order volume over time, delivery speed by region, top products and categories, customer and seller behaviour, the relationship between delivery timing and review scores, and physical distance between sellers and customers.

**03 — Machine learning**: builds a model to predict delivery time before an order ships. Uses linear regression as a baseline and random forest as the final model (MAE ~5 days, R² = 0.30). Includes feature importances showing that geography — distance and whether the customer is in São Paulo — drives most of the prediction.

## Main findings

Olist's own delivery estimates are systematically too conservative: orders arrive 7 to 20 days earlier than the estimated date depending on the state. A model predicting actual delivery time from order, product, and location features gives customers a meaningfully tighter window — which matters for conversion, not just satisfaction. Geography is the dominant driver: distance between seller and customer and proximity to São Paulo (where most sellers are based) together account for over 40% of the model's signal.

## Caveats

The dataset covers 2016–2018 and becomes incomplete after August 2018, so the drop in orders at the end of the period is a data cutoff, not a real decline. The model explains about 30% of the variance in delivery time — the rest is driven by things not in the data, such as carrier-level features.
