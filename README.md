# Are More Goals Scored in Women's Soccer Than Men's?

A statistical hypothesis test comparing goals scored in FIFA World Cup matches, completed as part of a DataCamp project.

## Overview

As a sports journalist covering international soccer, a hunch emerged: more goals seem to be scored in women's international matches than men's. Before publishing, that hunch needs a valid statistical test.

Because the sport has changed substantially over time and performance varies by tournament, the analysis is scoped to **official FIFA World Cup matches only** (excluding qualifiers) from **2002-01-01 onwards**.

## Research Question

> Are more goals scored in women's international soccer matches than men's?

**Significance level:** 10% (α = 0.10)

- **H₀** — The mean number of goals scored in women's international soccer matches is the same as men's.
- **H₁** — The mean number of goals scored in women's international soccer matches is greater than men's.

## Dataset

Two CSV files containing the results of every official international football match since the 19th century, scraped from a reliable online source.

| File | Description |
|---|---|
| `women_results.csv` | All women's international match results |
| `men_results.csv` | All men's international match results |

Key columns: `date`, `home_team`, `away_team`, `home_score`, `away_score`, `tournament`

## Approach

1. **Inspection** — reviewed structure and `tournament` value counts for both datasets; noted `date` was stored as `object` rather than `datetime`
2. **Filtering** — subset to `FIFA World Cup` matches, converted `date` to datetime, and restricted to matches on or after 2002-01-01
3. **Feature engineering** — created `total_goals` as `home_score + away_score`
4. **Test selection** — the two groups are **independent**, narrowing the choice to an unpaired t-test (parametric) or a Wilcoxon-Mann-Whitney test (non-parametric)
5. **Normality check** — plotted histograms with KDE overlays, then confirmed visually-apparent non-normality with the **Shapiro-Wilk test** on both groups
6. **Hypothesis test** — since neither group was normally distributed, ran a **Mann-Whitney U test** with `alternative='greater'` via `pingouin`
7. **Decision** — compared the resulting p-value against α = 0.10

## Result

The p-value fell below the 10% significance threshold, so the null hypothesis is **rejected**: there is statistically significant evidence that more goals are scored in women's FIFA World Cup matches than men's.


## Tech Stack

- Python
- pandas
- seaborn / matplotlib
- SciPy
- pingouin
