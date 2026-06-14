# Employee Satisfaction Analysis - Fiktiva

A data analysis project looking at employee data from a fictional company ("Fiktiva"), with the goal of figuring out which employee characteristics are related to job satisfaction.

## Data

The dataset (`employees_satisfaction.csv`) is **synthetic data created for a university data analysis course** - 700 fictional employees with columns like department, age, education, recruitment type, job level, performance rating, salary, gender, entry date and satisfaction status. It is not real company data, and the patterns found here describe this dataset only.

To run the notebook, place `employees_satisfaction.csv` in a `datasets/` folder next to the notebook.

## How to run

Open `fiktiva_employee_satisfaction.ipynb` in Jupyter. The notebook only needs:

- pandas
- matplotlib

## What's in the notebook

1. Understanding the dataset and checking data quality
2. Cleaning and preparing the data (renaming columns, converting salary from USD to EUR, fixing data entry errors, etc.)
3. Plausibility checks (duplicate IDs, implausible values in awards/certifications/age)
4. Exploratory analysis on a few focused questions (satisfaction by department, job level, performance rating, recruitment type, salary, and entry year)
5. Summary, limitations and next steps

## Main findings

Satisfaction is clearly related to *when* and *how* someone joined the company, and to *which department* they're in: employees who joined in 2021 or later are noticeably less satisfied than earlier hires, Sales has the highest satisfaction rate and Marketing the lowest, and Walk-in hires are more satisfied than Referrals. On the other hand, job level, performance rating and salary show almost no relationship with satisfaction.

## Caveats

This is a synthetic dataset built for a data analysis exercise, so the findings shouldn't be read as facts about real companies. The analysis is also descriptive, not causal - e.g. it can say Marketing has lower satisfaction, but not why.
