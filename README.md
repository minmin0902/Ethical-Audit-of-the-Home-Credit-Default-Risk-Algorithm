# Ethical Audit of the Home Credit Default Risk Algorithm

> A fairness and accuracy audit of an algorithmic decision system (ADS) used for credit default risk assessment, with a focus on financial inclusion for unbanked populations.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Language](https://img.shields.io/badge/language-Jupyter-orange.svg)
![Status](https://img.shields.io/badge/status-complete-green.svg)

## Authors

- **MinJoo Kim**
- **Azrael Ning**

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
- [Results](#results)
- [Fairness Analysis](#fairness-analysis)
- [Findings & Recommendations](#findings--recommendations)
- [References](#references)
- [License](#license)

## Overview

This project audits the **Home Credit Default Risk** algorithm — an ADS that assesses credit default risk for borrowers. The audit evaluates:

- **Accuracy** of credit risk predictions
- **Fairness** across demographic subpopulations
- **Inclusivity** for unbanked populations
- **Trade-offs** in model design

### Design Trade-offs Considered

| Trade-off | Tension |
|---|---|
| Accuracy vs. Interpretability | Complex models predict better but explain worse |
| Risk Minimization vs. Inclusivity | Stricter filters exclude marginal borrowers |
| Cost vs. Benefit | Sophisticated models cost more upfront |
| Privacy vs. Data Utility | Detailed data improves predictions but risks privacy |
| Short-Term vs. Long-Term | Quick gains can hurt long-term outcomes |

## Project Structure

```
.
├── Home_Credit_Default_Risk_Predictor.ipynb   # Main analysis notebook
├── Ethical Audit ... _Report.pdf              # Full written report
├── LICENSE
└── README.md
```

## Methodology

### Data Input

The dataset combines demographic information, financial data, and credit history. Features fall into three types:

| Type | Examples |
|---|---|
| Integer | IDs, target variable |
| Float | Income, credit amounts |
| Object | Contract type, gender |

### Preprocessing

1. **Missing values** — dropped or imputed (zero, mean, mode)
2. **Feature engineering** — added `NEW_EXT_SOURCE`, `PAYMENT_RATE`
3. **Outlier handling** — identified and addressed

### Model

**LightGBM** with cross-validated hyperparameters and encoded categorical features.

## Results

| Metric | Score |
|---|---|
| Accuracy | **91.90%** |
| ROC-AUC | 0.735 |
| Precision | 0.413 |
| Recall | 0.015 |
| F1-Score | 0.029 |

### Key Feature Correlations

- `TARGET` shows weak correlations with most features → harder to predict
- `AMT_CREDIT` correlates positively with goods prices and annuities
- `DAYS_EMPLOYED`, `DAYS_BIRTH` weakly negative with `TARGET`

## Fairness Analysis

Performance was tested across subpopulations defined by **income** (low / middle / high) and **age** (young adults / middle-aged / elderly):

- **Best accuracy** — elderly and low-income subgroups
- **Precision** — highest in low-income groups (fewer misclassifications)
- **F1-score** — reveals trade-offs across age brackets; younger adults underperform middle-aged

### Sensitivity

Predictions are highly sensitive to small input changes (range of 0.386 across perturbations).

## Findings & Recommendations

The audit surfaces clear trade-offs between accuracy, fairness, and inclusivity. Key recommendations:

- **Data quality** — increase diversity and representation in the dataset
- **Bias mitigation** — implement fairness measures to reduce prediction bias
- **Interpretability** — add methods to explain model decisions
- **Monitoring** — ensure transparency and continuous monitoring post-deployment

## References

> Montoya, A., Odintsov, K., & Kotek, M. (2018). *Home Credit Default Risk.*
> https://kaggle.com/competitions/home-credit-default-risk

## License

MIT — see [LICENSE](LICENSE) for details.
