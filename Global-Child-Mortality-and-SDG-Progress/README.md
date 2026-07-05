# Global Child Mortality & SDG 3 Progress

An exploratory analysis in R of global under-5 mortality trends using data from [Our World in Data](https://ourworldindata.org/child-mortality). The project examines how the world is tracking against SDG 3's target of reducing child mortality to below 25 per 1,000 live births by 2030.

## Datasets

Two datasets from Our World in Data (free, open-access):

- **Child mortality** — under-5 mortality rate by country and year (1950–2023), from the UN Inter-agency Group for Child Mortality Estimation (UN IGME). [Download](https://ourworldindata.org/child-mortality)
- **GDP per capita** — PPP-adjusted, constant 2017 international dollars, from the World Bank. [Download](https://ourworldindata.org/grapher/gdp-per-capita-worldbank)

Download both CSVs and place them in a `datasets/` folder.

## How to run

Open `child_mortality_analysis.Rmd` in RStudio or Posit Cloud and click **Knit** to generate the full HTML report.

Dependencies: tidyverse, scales, countrycode

```r
install.packages(c("tidyverse", "scales", "countrycode"))
```

## What's in the analysis

The R Markdown file covers data preparation (renaming, unit conversion, filtering aggregates from countries, adding continent) and four analysis questions:

**Question 1 — Global trend:** How has child mortality changed from 1950 to 2023? Line chart with the SDG target as a reference.

**Question 2 — Regional progress:** What share of countries in each continent meet the SDG target? Bar chart by continent, plus a lollipop chart of the 20 countries furthest from the target.

**Question 3 — Biggest improvers:** Which countries reduced mortality the most since the Millennium Development Goals were launched in 2000? Bar chart of top 15 absolute reductions.

**Question 4 — Wealth and child survival:** Does GDP per capita predict child mortality? Scatter plot with log-scaled GDP showing the diminishing returns of wealth.

## Main findings

Global under-5 mortality dropped from ~225 to ~37 per 1,000 between 1950 and 2023 — an 83% reduction — but the world is still 12 points above the SDG target and progress is slowing. Africa is the most critical region: only 19% of African countries meet the target, and the 20 countries with the highest mortality are all African. Many of them — Niger, Mali, South Sudan, Somalia — face active armed conflict, making aid delivery extremely difficult. On the positive side, the biggest absolute improvements since 2000 also happened in Africa (Rwanda, Angola, Sierra Leone), driven by international health programs. GDP per capita explains 61% of the variation in child mortality (log-linear model), but the effect flattens above ~$10,000 — beyond that, governance and stability matter more than additional wealth.

## Tools

tidyverse (dplyr, ggplot2, readr, tidyr), scales, countrycode, R Markdown, Posit Cloud
