# Patient-Improvement-MLM

## Overview
This project evaluates whether an **experimental treatment** leads to faster patient improvement over time using **multilevel (mixed-effects) modeling** on a longitudinal dataset where repeated measurements are nested within patients and hospitals. The outcome variable is **Improvement**, and the analysis tests time-varying treatment effects via a **Treatment × Time** interaction.

## Data
- Longitudinal patient improvement records with repeated measures over time (Time).
- Key variables: Patient_ID, Hospital_ID, Age, Severity, Treatment, Time, Improvement.

## Why multilevel modeling?
Observations are not independent because measurements are repeated within the same patient and clustered by hospital. A three-level longitudinal framework is used to partition variability across:
1) within-patient (time), 2) between-patient, 3) between-hospital levels, supported by ICC/VPC decomposition.

## Approach & What I did
1) **EDA & structure checks**
   - Visualized relationships (Age/Severity vs Improvement), trajectories by Treatment over Time, and hospital-level outcome differences.

2) **Model building (incremental)**
   - Model 1: Baseline treatment effect (no clustering).
   - Model 2: Random intercept for Hospital_ID; tested random slopes for Treatment by hospital.
   - Model 3: Random intercepts for Hospital_ID and Patient_ID; compared additive vs interaction model (Treatment × Time).
   - Model 4: Added covariates (Age, Severity) to test incremental explanatory power.

3) **Model selection & diagnostics**
   - Compared models using AIC and likelihood ratio tests (LRT).
   - Checked residual normality (Q–Q) and predictive adequacy via predicted vs actual patterns and treatment trajectories.

## Key findings (from the final model)
- The **Treatment × Time** interaction is statistically significant, indicating treatment effects evolve over time and the experimental group improves more rapidly as time progresses.
- A model with random intercepts at **both hospital and patient levels** is strongly justified by variance partitioning (ICC/VPC).
- Adding **Age** and **Severity** did not significantly improve fit beyond the interaction model.

## Deliverables
- Full report: `MLM Summative Assignment.pdf` (in this repo)

## Tech stack
R: lme4, lmerTest, ggplot2, sjPlot, effectsize, performance, ggeffects, broom.mixed, dplyr, etc.

---
Author: Shu-Yu Lin
