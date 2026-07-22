# Data Analysis Portfolio

A collection of data analysis projects spanning exploratory analysis (EDA), machine learning, time-series forecasting, and experiment (A/B test) analysis, showcasing skills in data cleaning, data visualization, statistical analysis, and interpretation. Each project demonstrates a complete workflow from raw data to actionable insights.

## About Me

I'm Álvaro de Diego Camarena, an engineer pivoting into data analysis. I have 4 years of professional experience in Python automation, BI dashboard development (IBM Cognos, Kibana/Elasticsearch), and operational data analytics for global retail clients, and I'm currently completing an M.Sc. in Data Science alongside the Google Data Analytics Professional Certificate. These projects are part of that transition - applying the same structured, detail-oriented approach I use in my day-to-day work to open data analysis problems, with a focus on data quality, clear visualization, and honest interpretation of results.

## Projects

### 1. Employee Satisfaction Analysis (Fiktiva)

**What**: Analysis of a synthetic HR dataset to understand which employee characteristics are related to job satisfaction, with a focus on data quality checks and honest interpretation of findings.

**Skills**: Data cleaning (fixing data entry errors, currency conversion), duplicate detection, plausibility checks, EDA with focus on group comparisons, honest assessment of what the data can and cannot show.

**Key finding**: Satisfaction is strongly related to department, recruitment type, and tenure (when someone joined), but not to salary, job level, or performance rating.

**Tools**: pandas, matplotlib

**Note**: This is synthetic data from a university course, not real company data.

[View project folder](./employee-satisfaction-analysis/) | [View notebook](./employee-satisfaction-analysis/fiktiva_employee_satisfaction.ipynb) | [View README](./employee-satisfaction-analysis/README.md)
---

### 2. Titanic Survival Analysis

**What**: Analysis of the Titanic dataset to explore which passenger characteristics were related to survival, and testing how well those characteristics can predict survival using machine learning.

**Skills**: Data cleaning, handling missing values, exploratory analysis, model comparison (Naive Bayes, Logistic Regression, Random Forest), cross-validation, feature interpretation.

**Key finding**: Gender, ticket class, and age were the strongest predictors of survival (~80% accuracy with Logistic Regression).

**Tools**: pandas, matplotlib, scikit-learn

[View project folder](./titanic-survival-analysis/) | [View notebook](./titanic-survival-analysis/titanic_survivors.ipynb) | [View README](./titanic-survival-analysis/README.md)
---

### 3. Olist E-Commerce Analysis

**What**: A larger, end-to-end project using a real Brazilian e-commerce dataset — building a SQL-backed ETL pipeline from raw CSVs, answering 11 exploratory business questions, training a machine learning model to predict delivery time before an order ships, and building a three-page Power BI dashboard on the cleaned data for a business stakeholder.

**Skills**: SQL (SQLite), ETL pipeline design, outlier investigation and plausibility checks, geospatial analysis (haversine distance, choropleth maps), cross-validated model comparison, feature importance interpretation. Power BI: star-schema data modelling, Power Query (M) transformations, DAX measures, and dashboard design.

**Key finding**: Olist's own delivery estimates are systematically too conservative, arriving 7 to 20 days early depending on the state. A random forest model predicting delivery time from order, product, and location features reaches an MAE of about 5 days (R² = 0.30), giving customers a meaningfully tighter and more realistic delivery window. Delivery timing is also the clearest driver of customer satisfaction: on-time orders average over 4 stars, while very late orders fall below 2.

**Tools**: pandas, SQLAlchemy/SQLite, seaborn, plotly, scikit-learn, Power BI (Power Query, DAX)

[View project folder](./Brazilian-E-Commerce-Public-Dataset-by-Olist/) | [View notebooks](./Brazilian-E-Commerce-Public-Dataset-by-Olist/) | [View README](./Brazilian-E-Commerce-Public-Dataset-by-Olist/README.md)

---

### 4. Cookie Cats A/B Test

**What**: Analysis of a real randomized A/B test from the mobile game Cookie Cats, testing whether moving a progression gate from level 30 to level 40 changed player retention.

**Skills**: Experiment analysis, randomization balance checks, retention/conversion lift, hypothesis testing (two-proportion z-test with a chi-square cross-check), bootstrap confidence intervals, statistical power reasoning, distinguishing statistical from practical significance.

**Key finding**: Moving the gate to level 40 did not improve retention. Day-7 retention was slightly higher for gate_30 (19.0% vs 18.2%, a 0.82 pp difference), statistically significant (p = 0.0016) with a 95% CI of [0.33, 1.35] pp that stays above zero. The effect is real but small, so the recommendation is to keep the gate at level 30.

**Tools**: pandas, numpy, statsmodels, scipy

**Note**: Data is downloaded at runtime via `kagglehub`.

[View project folder](./Cookie-Cats-A-B-Test-Analysis/) | [View notebook](./Cookie-Cats-A-B-Test-Analysis/ab-test-cookie-cats.ipynb) | [View README](./Cookie-Cats-A-B-Test-Analysis/README.md)

---

### 5. Global Child Mortality & SDG 3 Progress (R)

**What**: An exploratory analysis of global under-5 mortality trends using data from Our World in Data, examining how the world is progressing toward the SDG 3 target of fewer than 25 deaths per 1,000 live births by 2030.

**Skills**: Data wrangling in R (tidyverse), data visualization (ggplot2), unit conversion, joining datasets, working with country-level panel data, interpreting global development indicators.

**Key finding**: Global child mortality dropped 83% since 1950, but progress is slowing. Only 19% of African countries meet the SDG target, and the 20 countries furthest from it are all African — most facing active conflict. GDP per capita explains 61% of the variation in child mortality, but above ~$10,000, governance and stability matter more than additional wealth.

**Tools**: R, tidyverse (dplyr, ggplot2, readr, tidyr), scales, countrycode, R Markdown

**Note**: This project uses R instead of Python to demonstrate language versatility. Data is from Our World in Data (open access, based on UN IGME and World Bank sources).

[View project folder](./Global-Child-Mortality-and-SDG-Progress/) | [View report](./Global-Child-Mortality-and-SDG-Progress/child_mortality_analysis.md) | [View README](./Global-Child-Mortality-and-SDG-Progress/README.md)

---

### 6. Rossmann Store Sales — Demand Forecasting

**What**: Time-series forecasting of daily sales across 1,115 Rossmann drugstores in Germany (2013–2015), predicting the company-wide total six weeks ahead. The forecast is built twice — once "from scratch" with engineered lag and calendar features feeding standard regressors, and once with Prophet — to compare a fully interpretable approach against a purpose-built forecasting library.

**Skills**: Time-series feature engineering (lag features, calendar encoding), leak-free chronological train/test splitting, baseline-first evaluation, metric selection for series with near-zero days (WAPE over MAPE), model comparison (Linear Regression, Random Forest, Prophet), coefficient-level diagnosis, and honest reporting of negative results.

**Key finding**: Random Forest cuts the seasonal-naive baseline's error to under a third (WAPE 30.2% → 8.9%), and Prophet reaches a similar level (8.4%) with almost no feature engineering. Linear Regression trails because it cannot represent the promo × weekday interaction the EDA uncovered. A deliberate test of one-hot encoding the weekday returned an honest negative result: because `lag_7` already carries the weekly shape, the one-hot flags added only noise.

**Tools**: pandas, scikit-learn, Prophet, matplotlib, pyarrow

**Note**: Data is downloaded at runtime via `kagglehub`.

[View project folder](./rossmann-store-sales-forecasting/) | [View notebooks](./rossmann-store-sales-forecasting/) | [View README](./rossmann-store-sales-forecasting/README.md)

---

## What You'll Find in Each Project

Every project follows the same structure:

- **README.md**: Overview of the project, data source, how to run the notebook, main findings and caveats
- **Jupyter notebook (.ipynb) or R Markdown (.Rmd)**: Full analysis with code, visualizations, and written explanations
- **Dataset folder**: Raw data file(s) — included in the repo, downloaded separately, or fetched at runtime via `kagglehub`, depending on the project. Each README explains how to get the data.

## How to Use These Projects

1. **Clone the repository**:
```bash
   git clone https://github.com/alvdecam/data-analytics-portfolio.git
   cd data-analytics-portfolio
```

2. **Install dependencies**:
```bash
   # Python projects
   pip install -r requirements.txt

   # R project
   install.packages(c("tidyverse", "scales", "countrycode"))
```

3. **Open a specific project**:
```bash
   cd titanic-survival-analysis
   jupyter notebook titanic_survivors.ipynb
```

## Key Skills Demonstrated

- **Data Quality & Cleaning**: Handling missing values, detecting duplicates, identifying and fixing data entry errors, plausibility checks
- **Exploratory Data Analysis**: Group comparisons, trend analysis, correlation checks, summarizing findings in charts
- **Time-Series Forecasting**: Lag/calendar feature engineering, chronological (leak-free) splits, baseline-first evaluation, and model comparison including Prophet
- **Experiment Analysis (A/B Testing)**: Randomization checks, hypothesis testing (z-test, chi-square), bootstrap confidence intervals, power and effect-size reasoning
- **BI & Dashboarding**: Star-schema data modelling, Power Query (M), DAX, and stakeholder-facing dashboard design in Power BI
- **Communication**: Clear written explanations of methodology and findings, honest discussion of limitations
- **Tools & Libraries**: Python (pandas, matplotlib, scikit-learn, statsmodels, scipy), R (tidyverse, ggplot2), SQL (SQLAlchemy/SQLite), Power BI
- **Critical Thinking**: Understanding when a finding is real vs. noise, recognizing what the data can and cannot show, flagging assumptions

## My Approach

I focus on **getting the data quality right first** — understanding the data before drawing conclusions. Each project includes a dedicated data quality section where I check for missing values, inconsistencies, outliers, and other issues. I also believe in **honest interpretation** — if a finding is weak or if there's limited signal, I say so rather than overselling the results.

## Contact

Feel free to reach out with questions about any of these projects, or to discuss data analysis challenges you're working on.

- Email: alvarodediegocamarena@gmail.com
- LinkedIn: [Álvaro de Diego Camarena](https://www.linkedin.com/in/alvaro-de-diego-camarena-10b02714a/)
- GitHub: [data-analytics-portfolio](https://github.com/alvdecam/data-analytics-portfolio)

---

**Note**: Most of these projects use real or course-provided datasets. Each project README clearly states whether the data is real, synthetic, or from a university exercise. Findings from synthetic/course data are for demonstration purposes and should not be generalized to real-world scenarios.
