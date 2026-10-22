---
title: "PlasmaCast: Plasma Donor Demand Forecasting"
excerpt: "Independent project (2026). An XGBoost pipeline that forecasts daily plasma donor demand across 10 US cities, with 6.0% mean error on a held-out year, less than half the error of a naive weekly baseline."
collection: portfolio
---

**Independent project** · April – October 2026

[GitHub repository](https://github.com/PW13052003/plasmacast) · [Live dashboard](https://pw13052003.github.io/plasmacast/)

## Overview

Plasma donation centers need to plan staffing around how many donors will walk in each day. PlasmaCast is an end-to-end machine learning pipeline that forecasts daily donor counts for centers in the 10 largest US cities, from data generation through to a forecasting API and an interactive dashboard.

## About the data

Real per-center donor counts aren't publicly available, so the donor counts are simulated. The inputs around them are real:

- **Weather:** daily historical temperature and precipitation for each city from the Open-Meteo API (2020 – 2023)
- **Holidays:** the US federal holiday calendar
- **Population:** US Census Bureau Vintage 2024 estimates

Each city's baseline comes from published industry figures (Plasma Protein Therapeutics Association collections per center, scaled by population). Day-of-week, weather, and holiday effects are then applied, plus random noise. The results show that the pipeline works end to end; they aren't a claim about forecasting real donor traffic.

## Approach

- Engineered 13 features: weather, calendar (day of week, month, season, holidays), 7- and 14-day lags, and rolling averages, computed per city and shifted so no day sees its own value
- Trained an XGBoost regressor on 2020 – 2022 and tested on 2023, using a time-based split to avoid leaking future data into training
- Served the model through a FastAPI endpoint that powers a 7-day forecast dashboard using live weather forecasts

## Results

Evaluated on 2023, a year the model never saw during training:

| Metric | Value |
|---|---|
| Mean absolute error | 6.0% of the mean daily donor count |
| Naive baseline (same day last week) | 13.0% |
| Per-city error | 5.6% – 7.5% |

## Tools

Python, pandas, NumPy, XGBoost, scikit-learn, FastAPI, Matplotlib, HTML/CSS/JavaScript
