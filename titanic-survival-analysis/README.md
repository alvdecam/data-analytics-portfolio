# Titanic Survival Analysis

A data analysis project looking at the classic Titanic passenger dataset, with the goal of figuring out which passenger characteristics were related to survival - and then testing how well those characteristics can actually predict survival.

## Data

The dataset is the well-known [Titanic dataset from Kaggle](https://www.kaggle.com/c/titanic/data) - real passenger records (name, age, sex, ticket class, fare, etc.) from the 1912 disaster, including whether each passenger survived.

To run the notebook, download `Titanic-Dataset.csv` and place it in a `datasets/` folder next to the notebook.

## How to run

Open `titanic_survivors.ipynb` in Jupyter. The notebook only needs:

- pandas
- numpy
- matplotlib
- scikit-learn

## What's in the notebook

1. Understanding the dataset and checking data quality
2. Cleaning and preparing the data (handling missing ages, dropping the Cabin column, etc.)
3. Plausibility checks (looking for outliers and inconsistent values)
4. Exploratory analysis on a few focused questions (survival by class, gender, age, family size)
5. Comparing a few machine learning models (Naive Bayes, Logistic Regression, Random Forest) to predict survival
6. Summary, limitations and next steps

## Main findings

Gender, ticket class, and age turned out to be the strongest predictors of survival - women, 1st class passengers, and younger passengers had noticeably higher survival rates. Logistic Regression and Random Forest both reached around 80% accuracy, with Logistic Regression being the more consistent of the two across cross-validation folds.

## Caveats

This is descriptive/predictive, not causal - the analysis can say *which* groups were more likely to survive, but not establish *why* beyond the historical context (e.g. "women and children first").
