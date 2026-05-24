# Predicting Treatment Dropout in Substance Use Programs: A Competing Risks Survival Analysis

## Overview

Voluntary dropout from substance use treatment reduces program effectiveness and wastes clinical resources. This project applies a competing risks survival analysis framework to 22,028 discharge records from the 2023 TEDS-D dataset to examine which participant characteristics and treatment factors predict the timing of voluntary dropout. Rather than treating all non-dropout exits as censored, death, incarceration, and facility termination are modeled as competing events, producing unbiased cumulative incidence estimates.

## Background

This project extends prior work predicting dropout in longitudinal research studies using logistic regression and simulated data. The present analysis moves to real administrative health data, a competing risks time-to-event outcome, and a larger, more representative sample — demonstrating progression from binary prediction to survival modeling.

## Dataset

Treatment Episode Data Set — Discharges (TEDS-D) 2023, obtained from SAMHSA. Public use file downloaded at no cost.

- Starting sample: 51,971 discharge records
- Analytic sample: 22,028 participants (42.4% retained after cleaning)
- Overall dropout rate: 20.6%
- Competing events: death (0.2%), incarceration (1.7%), facility termination (9.5%)

**Key features included:** age, sex, race/ethnicity, employment status, health insurance, primary substance, co-occurring mental health disorder, referral source, treatment setting, frequency of use at intake.

## Methods

* Competing risks analysis using the Aalen-Johansen estimator
* Log-rank tests for unadjusted group comparisons
* Stratified Cox proportional hazards model (stratified on treatment setting due to severe proportional hazards violations)
* Proportional hazards assumption tested using Schoenfeld residuals

## Key Findings

* Benzodiazepine users dropped out 57.8% faster than alcohol users (HR=1.578, p=0.0004) — the strongest substance effect
* Black or African American participants dropped out 18.2% faster than White participants after controlling for all other covariates (HR=1.182, p<0.0005)
* Court-mandated participants dropped out 23.4% slower than self-referred participants (HR=0.766, p<0.0005)
* Participants reporting no substance use at intake retained significantly better than daily users (HR=0.771, p<0.0005)
* Co-occurring mental health disorder lost significance after adjustment (HR=1.007, p=0.799), indicating confounding in unadjusted analyses
* Model concordance: 0.626 | Partial AIC: 70,797.908

## Tools

Python, pandas, numpy, lifelines, scikit-learn, matplotlib, seaborn

## Files

- TEDS_Survival_Analysis.ipynb — full analysis notebook
- competing_risks_curve.png — overall cumulative incidence curve
- group_comparison_demographics.png — survival curves by demographics
- group_comparison_curves.png — survival curves by participant characteristics
- group_comparison_treatment.png — survival curves by treatment context
- cox_stratified_hazard_ratios.png — adjusted hazard ratio forest plot
- descriptive_dropout_rates.png — dropout rates by participant characteristics
- event_type_distribution.png — discharge outcome distribution

## References

- Gustavson, K., Røysamb, E., von Soest, T., Mathiesen, K. S., & Karevold, E. (2012). Attrition and generalizability in longitudinal studies. BMC Research Notes. https://doi.org/10.1186/1756-0500-5-1
- McGovern, M., Halvorsen, J. Ø., Ørstavik, M. S., Dyrdal, B., & Bjørkly, S. (2024). Who will stay and who will go? Identifying risk factors for psychotherapy dropout. Counselling and Psychotherapy Research. https://doi.org/10.1002/capr.12783
- Park, S. H., Han, K., & Park, S. Y. (2021). Mistakes to avoid for accurate and transparent reporting of survival analysis in imaging research. Korean Journal of Radiology, 22(10), 1587–1593. https://doi.org/10.3348/kjr.2021.0579
- Substance Abuse and Mental Health Services Administration. (2023). Treatment Episode Data Set — Discharges (TEDS-D): 2023. SAMHSA. https://www.samhsa.gov/data
- Swift, J. K., & Greenberg, R. P. (2012). Premature discontinuation in adult psychotherapy: A meta-analysis. Journal of Consulting and Clinical Psychology, 80(4), 547–559. https://doi.org/10.1037/a0028226
