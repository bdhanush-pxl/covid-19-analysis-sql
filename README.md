# COVID-19 Data Explorer (SQL)

A SQL-based exploratory data analysis of global COVID-19 statistics — infection trends, mortality rates, and vaccination progress — using joins, CTEs, temporary tables, window functions, and aggregate functions across multiple tables.

---

## 📊 Overview

This project analyzes worldwide COVID-19 data (cases, deaths, and vaccinations) to answer key questions about the pandemic's global and regional impact, such as:

- What is the mortality rate in each country over time?
- What percentage of a country's population was infected?
- Which countries/continents had the highest infection and death rates relative to population?
- What were the global daily case and death counts?
- What is the rolling (cumulative) count of people vaccinated over time, by location?

---

## 🗂️ Data

- **`coviddeaths`** — Case counts, death counts, population, and location/date data.
- **`covidvaccinations`** — Vaccination data joined against `coviddeaths` on `location` and `date`.
- Raw data is provided as `CovidDeaths.zip` in this repo (extract before loading into your database).

> Source data is based on the publicly available [Our World in Data COVID-19 dataset](https://ourworldindata.org/covid-deaths).

---

## 🛠️ Techniques Used

- **Joins** — combining `coviddeaths` and `covidvaccinations` on location and date.
- **CTEs (Common Table Expressions)** — e.g. `PopVsVac` for computing rolling vaccination counts.
- **Temporary Tables** — an alternative approach to the CTE for the same rolling-vaccination calculation.
- **Window Functions** — `SUM() OVER (PARTITION BY ... ORDER BY ...)` for running/cumulative totals.
- **Aggregate Functions** — `MAX()`, `SUM()` with `GROUP BY` for country- and continent-level summaries.
- **Type Casting** — `CAST(... AS BIGINT)` to safely aggregate large vaccination counts.
- **Views** — 8 SQL views created to persist query results for downstream analysis/visualization (e.g. in Tableau or Power BI).

---

## 🔍 Key Queries (in `Analysis.sql`)

| # | Query | What it answers |
|---|---|---|
| 1 | Mortality rate | `total_deaths / total_cases` by location and date |
| 2 | Percent population infected | `total_cases / population` by location and date |
| 3 | Highest infection rate by country | Country with highest infection % relative to population |
| 4 | Highest death rate by country | Country with highest death % relative to population |
| 5 | Highest death count by country | Country with the highest total death count |
| 6 | Highest death count by continent | Continent with the highest total death count |
| 7 | Global daily cases/deaths | Daily new cases, new deaths, and death rate worldwide |
| 8 | Rolling vaccinated count (CTE) | Cumulative vaccinated population over time, per location |
| 9 | Rolling vaccinated count (Temp Table) | Same as above, implemented with a temp table |
| 10 | Views | Persists each of the above analyses as a reusable SQL view |

---

## 🚀 Getting Started

### Prerequisites
- A SQL Server (or compatible) instance — the script uses SQL Server syntax (`NVARCHAR`, `#TempTable`, `CAST ... AS BIGINT`).

### Steps

1. Extract `CovidDeaths.zip` and load the data into a `coviddeaths` table (and a `covidvaccinations` table, if using a separate vaccinations dataset).
2. Run `Analysis.sql` against your database.
3. Query the created views (`mortalityrate`, `PercentagePopulationInfected`, `HighestInfectedCountry`, `HighestDeathperPopulation`, `hightestDeathCountLocation`, `HighestDeathCountContinent`, `GlobalCasesPerDay`, `RollingCountofPeopleVaccinated`) directly for downstream analysis or to connect to a BI/visualization tool.

---

## 👤 Author

**Dhanush Bandi**
- GitHub: [@bdhanush-pxl](https://github.com/bdhanush-pxl)
- LinkedIn: [dhanushbandi](https://www.linkedin.com/in/dhanushbandi-0b06412b5)
