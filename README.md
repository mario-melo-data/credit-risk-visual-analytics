# Credit Card Default Risk: Visual Analytics

A visual-analytics study of consumer credit-card default, using visualisation to drive feature engineering, interpret model outputs, and assess how risk classification depends on policy thresholds.

## Overview

This project investigates how credit utilisation, repayment behaviour, and client characteristics relate to the probability of default, using the Default of Credit Card Clients dataset. The approach is deliberately visual: rather than relying on numerical summaries alone, each chart is used to reason about the data, decide which behavioural features to engineer, and interpret model outputs instead of accepting them at face value. The applied context is consumer credit risk, where understanding the behavioural drivers of default supports responsible lending and risk-management decisions.

## Data

* **Source:** Default of Credit Card Clients (UCI / Kaggle)
* **Content:** anonymised credit-card client records with credit limits, monthly billing and payment amounts, repayment-delay status (PAY_0 to PAY_6), demographic attributes, and the observed next-month default outcome
* **Target:** `default.payment.next.month`

The raw dataset is not included in this repository. To run the notebook, download the data from the source and place it in the project folder.

## Approach

The analysis follows a visual-analytics workflow, where each visualisation informs the next analytical step:

1. **Multivariate structure.** A correlation heatmap of financial and behavioural variables identifies which attributes relate most strongly to default, pointing towards repayment-delay and utilisation features.
2. **Behavioural stress.** A utilisation curve (billed amount relative to credit limit) reveals non-linear escalation in default risk at higher stress levels.
3. **Sequential repayment behaviour.** A heatmap of default rate across repayment-delay status shows that sustained delays carry more risk than isolated missed payments.
4. **Demographic heterogeneity.** A heatmap of default rate by age band and education level reveals interaction effects, motivating ordered demographic features.
5. **Transformation evaluation.** Box plots compare raw billing against the engineered utilisation and aggregated repayment-stress features, confirming the transformed features separate defaulters more clearly.
6. **Latent structure.** A PCA embedding shows that defaulters and non-defaulters overlap rather than forming clean clusters, indicating that default risk is continuous and probabilistic.
7. **Calibration.** Predicted probabilities are compared with realised default rates across risk deciles, showing where the model is reliable and where it diverges.
8. **Threshold sensitivity.** The share of clients flagged as high-risk is plotted across decision thresholds, showing that classification is a policy-sensitive choice rather than a fixed boundary.
9. **Risk stratification.** Clients are grouped into low, medium, and high behavioural-risk bands, with default rates increasing monotonically across the bands.

## Key findings

* Behavioural credit stress, particularly credit utilisation and persistent repayment delays, is a dominant driver of default, with non-linear escalation that simple summaries do not reveal.
* Default risk is continuous and probabilistic rather than a clean binary split, with meaningful overlap between groups in the medium-risk region.
* Risk classification depends heavily on the chosen probability threshold, so default segmentation is a policy-sensitive decision shaped by institutional risk appetite.

## Tech stack

Python, pandas, NumPy, scikit-learn (PCA, modelling), matplotlib, seaborn.

## Files

* `credit-risk-visual-analytics.ipynb` is the full analysis notebook, including all figures and outputs.

## Notes

This project was developed during the Visual Analytics module of the MSc Data Science programme at City St George's, University of London. It uses visualisation as an analytical tool across feature engineering, model interpretation, calibration, and threshold sensitivity, themes that connect directly to credit-risk analysis and behavioural risk segmentation.
