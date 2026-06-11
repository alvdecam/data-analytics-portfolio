# Employee Satisfaction Analysis — Fiktiva

A simple end-to-end data analysis project on a fictional company's employee dataset. The goal of this repository is to demonstrate a clean, reproducible analytical workflow that I can also reuse as a template for future projects.

## Business question

Which employee characteristics seem to be related to employee satisfaction, and what data quality issues should be considered before interpreting the results?

## Dataset

- 700 employees of the fictional company *Fiktiva*
- 14 columns covering demographics, role, performance and a binary `satisfied` flag
- See `datasets/metadata.txt` for the column descriptions

## Approach

1. Understand the dataset (shape, types, missing values)
2. Clean and prepare the data (renaming, type conversion, category unification)
3. Run plausibility checks (ID consistency, entry age, outliers)
4. Exploratory data analysis on seven focused questions
5. Summarise findings, limitations and next steps

## Main findings

- 68% of employees are satisfied overall.
- **Marketing** has the lowest satisfaction (61%), 16 points below **Sales** (77%).
- Satisfaction among **recent hires is declining**: 2021 cohort at 40%, 2025 cohort at 47%, versus 70%+ for older cohorts.
- Salary and performance rating do **not** appear to be the main drivers of satisfaction in this dataset.

Full numbers and charts are in the notebook.

## How to run

```bash
pip install -r requirements.txt
jupyter notebook fiktiva_employee_satisfaction.ipynb
```

## Repository structure

```
.
├── fiktiva_employee_satisfaction.ipynb   # main analysis notebook
├── datasets/
│   ├── employees_satisfaction.csv        # raw dataset
│   └── metadata.txt                      # column descriptions
├── requirements.txt
└── README.md
```

## Tools

Python 3, pandas, matplotlib, Jupyter.
