# Olist E-Commerce Analysis

A data engineering and data science project using the [Brazilian E-Commerce public dataset from Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) — real orders placed on the platform between 2016 and 2018, covering customers, sellers, products, payments, reviews, and geolocation.

The project runs end to end: raw CSVs → ETL → exploratory analysis → a predictive model → a stakeholder-facing Power BI dashboard. The dashboard is built on the cleaned data produced by the ETL pipeline (step 01), exported to CSV and loaded into Power BI.

## Data

Download the dataset from Kaggle and place the CSV files in a folder. Update the `path` variable in `01_etl_pipeline.ipynb` to point to that folder. The ETL notebook will create `olist_analysis.db` (a local SQLite database) which notebooks 02 and 03 read from.

The Power BI dashboard is built on the *cleaned* data leaving the ETL pipeline, not the raw Kaggle files: the cleaned tables were exported from step 01 to CSV and loaded into Power BI. Inside Power BI, Power Query then handles the modelling-layer transformations needed for the star schema (see the dashboard section below).

## How to run

Open the notebooks in order in Jupyter:

1. `01_etl_pipeline.ipynb`
2. `02_exploratory_analysis.ipynb`
3. `03_machine_learning.ipynb`

The Power BI report (`04_powerbi_dashboard.pbix`) is built on the same data and is described below.

Dependencies: pandas, numpy, matplotlib, seaborn, plotly, sqlalchemy, scikit-learn. The dashboard requires Power BI Desktop (Windows).

## What's in the project

**01 — ETL pipeline**: loads the raw CSVs, cleans data types and nulls, engineers two delivery columns (`delivery_days` and `delivery_early_days`), runs plausibility checks on outliers, and loads everything into a SQLite database.

**02 — Exploratory analysis**: answers 11 questions about the data — order volume over time, delivery speed by region, top products and categories, customer and seller behaviour, the relationship between delivery timing and review scores, and physical distance between sellers and customers.

**03 — Machine learning**: builds a model to predict delivery time before an order ships. Uses linear regression as a baseline and random forest as the final model (MAE ~5 days, R² = 0.30). Includes feature importances showing that geography — distance and whether the customer is in São Paulo — drives most of the prediction.

**04 — Power BI dashboard**: a three-page report rebuilding a BI layer on top of the same data, framed for a business stakeholder. Covers a star-schema data model, Power Query transformations, and DAX measures. Described in detail below.

## Power BI dashboard

`04_powerbi_dashboard.pbix` — a three-page interactive report. Screenshots are in `/powerbi/screenshots`.

### Data model

The eight source tables were reshaped into a star schema: a central fact table (`FactOrderItems`, one row per product line per order) surrounded by dimension tables for orders, customers, products, sellers, reviews, geography, and a generated date table. All relationships are single-direction. Most dimensions filter the fact directly; customers, reviews, and the date table connect through the orders dimension (`DimOrders`) because they share its order-level grain, and their filters flow on to the fact through it.

### The three pages

1. **Business Overview** — headline KPIs, monthly revenue trend, and top categories by revenue.
2. **Delivery Performance** — a choropleth map of Brazil coloured by average delivery days, alongside a ranked bar chart by state.
3. **Delivery & Satisfaction** — average review score by delivery-timing category, showing the drop from 4+ stars for on-time orders to below 2 for very late ones.

## Main findings

Olist's own delivery estimates are systematically too conservative: orders arrive 7 to 20 days earlier than the estimated date depending on the state. A model predicting actual delivery time from order, product, and location features gives customers a meaningfully tighter window — which matters for conversion, not just satisfaction. Geography is the dominant driver: distance between seller and customer and proximity to São Paulo (where most sellers are based) together account for over 40% of the model's signal.

Delivery timing is also the clearest driver of customer satisfaction: on-time orders average over 4 stars, while very late orders fall below 2. Review scores otherwise vary little across the country.

## Caveats

The dataset covers 2016–2018 and becomes incomplete after August 2018, so the drop in orders at the end of the period is a data cutoff, not a real decline. The model explains about 30% of the variance in delivery time — the rest is driven by things not in the data, such as carrier-level features.
