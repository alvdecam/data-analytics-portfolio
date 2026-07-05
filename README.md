# Data Analysis Portfolio

A collection of data analysis and exploratory data analysis (EDA) projects, showcasing skills in data cleaning, data visualization, statistical analysis, and interpretation. Each project demonstrates a complete workflow from raw data to actionable insights.

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

**What**: A larger, end-to-end project using a real Brazilian e-commerce dataset — building a SQL-backed ETL pipeline from raw CSVs, answering 11 exploratory business questions, and training a machine learning model to predict delivery time before an order ships.

**Skills**: SQL (SQLite), ETL pipeline design, outlier investigation and plausibility checks, geospatial analysis (haversine distance, choropleth maps), cross-validated model comparison, feature importance interpretation.

**Key finding**: Olist's own delivery estimates are systematically too conservative, arriving 7 to 20 days early depending on the state. A random forest model predicting delivery time from order, product, and location features reaches an MAE of about 5 days (R² = 0.30), giving customers a meaningfully tighter and more realistic delivery window.

**Tools**: pandas, SQLAlchemy/SQLite, seaborn, plotly, scikit-learn

[View project folder](./Brazilian-E-Commerce-Public-Dataset-by-Olist/) | [View notebooks](./Brazilian-E-Commerce-Public-Dataset-by-Olist/) | [View README](./Brazilian-E-Commerce-Public-Dataset-by-Olist/README.md)

---

## What You'll Find in Each Project

Every project follows the same structure:

- **README.md**: Overview of the project, data source, how to run the notebook, main findings and caveats
- **Jupyter notebook (.ipynb)**: Full analysis with code, visualizations, and written explanations
- **metadata**: Description of all columns and their meaning
- **Dataset folder**: Raw data file(s)

## How to Use These Projects

1. **Clone the repository**:
```bash
   git clone https://github.com/alvdecam/data-analysis-portfolio.git
   cd data-analysis-portfolio
```

2. **Install dependencies**:
```bash
   pip install -r requirements.txt
```

3. **Open a specific project**:
```bash
   cd titanic
   jupyter notebook titanic_survivors.ipynb
```

## Key Skills Demonstrated

- **Data Quality & Cleaning**: Handling missing values, detecting duplicates, identifying and fixing data entry errors, plausibility checks
- **Exploratory Data Analysis**: Group comparisons, trend analysis, correlation checks, summarizing findings in charts
- **Communication**: Clear written explanations of methodology and findings, honest discussion of limitations
- **Tools & Libraries**: pandas for data manipulation, matplotlib for visualization, scikit-learn for machine learning (where applicable)
- **Critical Thinking**: Understanding when a finding is real vs. noise, recognizing what the data can and cannot show, flagging assumptions

## My Approach

I focus on **getting the data quality right first** — understanding the data before drawing conclusions. Each project includes a dedicated data quality section where I check for missing values, inconsistencies, outliers, and other issues. I also believe in **honest interpretation** — if a finding is weak or if there's limited signal, I say so rather than overselling the results.

## Dependencies

All projects use these libraries:

- pandas
- matplotlib
- numpy
- scikit-learn (used in some projects)
- SQLAlchemy / SQLite (used in the Olist project)
- plotly (used in the Olist project)

## Contact

Feel free to reach out with questions about any of these projects, or to discuss data analysis challenges you're working on.

- Email: alvarodediegocamarena@gmail.com
- LinkedIn: [Álvaro de Diego Camarena](https://www.linkedin.com/in/alvaro-de-diego-camarena-10b02714a/)
- GitHub: [data-analytics-portfolio](https://github.com/alvdecam/data-analytics-portfolio)

---

**Note**: Most of these projects use real or course-provided datasets. Each project README clearly states whether the data is real, synthetic, or from a university exercise. Findings from synthetic/course data are for demonstration purposes and should not be generalized to real-world scenarios.