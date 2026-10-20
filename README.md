# Credit Card Default Risk: Visual Analytics

A visual-analytics study of consumer credit-card default, using visualisation to drive feature engineering, interpret model outputs, and assess how risk classification depends on policy thresholds.

## Overview

This project investigates how credit utilisation, repayment behaviour, and client characteristics relate to the probability of default, using the Default of Credit Card Clients dataset. The approach is deliberately visual: rather than relying on numerical summaries alone, each chart is used to reason about the data, decide which behavioural features to engineer, and interpret model outputs instead of accepting them at face value. The applied context is consumer credit risk, where understanding the behavioural drivers of default supports responsible lending and risk-management decisions.

## Data

* **Source:** [Default of Credit Card Clients](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients) (UCI, 30,000 clients; also mirrored on Kaggle)
* **Content:** anonymised credit-card client records with credit limits, monthly billing and payment amounts, repayment-delay status (PAY_0 to PAY_6), demographic attributes, and the observed next-month default outcome
* **Target:** `default.payment.next.month`

The raw dataset is not included in this repository. To run the notebook, download the CSV version of the dataset (with columns such as PAY_0 and default.payment.next.month), save it as dataset.csv and place it in the project folder.

## Approach

The analysis follows a visual-analytics workflow, where each visualisation informs the next analytical step:

1. **Multivariate structure.** A correlation heatmap of financial and behavioural variables identifies which attributes relate most strongly to default, pointing towards repayment-delay and utilisation features.
2. **Credit utilisation.** A binned plot of default rate for utilisation ratios (billed amount relative to credit limit) between 0.3 and 3.0 shows rates of about 0.1 to 0.4 across most of the range, with erratic values in the highest bins and no clear upward trend. Ratios outside 0.3 to 3.0 are not plotted and bin counts are not shown; the plot does not establish an overall relationship or a utilisation threshold.
3. **Recent repayment status.** A heatmap of default rate by the most recent repayment status (PAY_0) shows default at 0.13 to 0.17 for clients who are up to date, 0.34 at one month's delay and 0.50 to 0.78 at two months or more.
4. **Demographic variation.** A heatmap of default rate by age band and education code shows variation across groups. Subgroup counts are not shown, and education codes 0, 5 and 6 do not correspond to a defined education level (code 4 means 'others'); the differences are descriptive and do not establish interaction effects. Age and education were retained as model inputs.
5. **Transformation evaluation.** Box plots compare raw billing against the engineered utilisation and aggregated repayment-stress features, showing that the aggregated repayment-stress feature separates defaulters clearly, while utilisation adds little separation over raw billing.
6. **Latent structure.** A PCA projection of the test-set features, used for visual exploration only and not as a model input, shows defaulters and non-defaulters overlapping rather than forming clean clusters. The PCA was fitted on unscaled features, and the first component is dominated by credit limit; the overlap is read as indicative only.
7. **Calibration check.** Predicted probabilities are compared with realised default rates across risk deciles, showing where the model is reliable and where it diverges.
8. **Threshold sensitivity.** The share of clients flagged as high-risk is plotted across decision thresholds, showing that classification is a policy-sensitive choice rather than a fixed boundary.
9. **Risk stratification.** Clients are grouped into low, medium, and high behavioural-risk bands, with default rates increasing monotonically across the bands.

## Key findings

* Recent repayment delays and aggregated repayment stress show much stronger associations with observed default than credit utilisation in these visual analyses: default rates rise sharply once the most recent payment is two or more months late.
* Default risk is continuous and probabilistic rather than a clean binary split, with meaningful overlap between groups in the medium-risk region.
* Risk classification depends heavily on the chosen probability threshold, so default segmentation is a policy-sensitive decision shaped by institutional risk appetite.

## Limitations

* Figures 1 to 5 were produced on the full dataset before the 70/30 split, and they informed the choice of model features. The test set is therefore not fully independent of those exploratory choices, and the model results are exploratory rather than an unbiased estimate of out-of-sample performance.
* The logistic regression is a demonstration model for the visual analysis: it uses unscaled features, treats EDUCATION (a nominal code) as a number, and no discrimination metric such as ROC-AUC is reported.

## Tech stack

Python, pandas, NumPy, scikit-learn (PCA, modelling), matplotlib, seaborn.

## Files

* `credit-risk-visual-analytics.ipynb` is the full analysis notebook, including all figures and outputs.

## Notes

This project was developed during the Visual Analytics module of the MSc Data Science programme at City St George's, University of London. It uses visualisation as an analytical tool across feature engineering, model interpretation, calibration, and threshold sensitivity, themes that connect directly to credit-risk analysis and behavioural risk segmentation.
