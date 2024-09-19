# Ethical Audit of the Home Credit Default Risk Algorithm

## Overview
This project audits the Home Credit Default Risk Algorithm (ADS), which assesses credit default risk for borrowers. The goal is to evaluate the fairness, accuracy, and inclusivity of the ADS, with a focus on improving financial inclusion for unbanked populations while maintaining ethical lending practices.

## Authors
- **MinJoo Kim**
- **Azrael Ning**

## Project Goals
The audit aims to:
1. Improve the accuracy of credit risk assessments.
2. Minimize default risks.
3. Optimize lending decisions while balancing ethical concerns.

### Trade-offs in Model Design
- **Accuracy vs. Interpretability**: Complex models may be more accurate but harder to interpret.
- **Risk Minimization vs. Inclusivity**: Striving for inclusivity may increase risk, potentially affecting financial stability.
- **Cost vs. Benefit**: Sophisticated models can incur higher costs but may lead to better long-term returns.
- **Privacy vs. Data Utility**: Balancing data privacy with the need for detailed data for accurate predictions.
- **Short-Term vs. Long-Term Objectives**: Prioritizing immediate gains can have negative long-term consequences.

## Data Input and Features
The dataset includes demographic information, financial data, and credit history, with features categorized as:
- **Integer** (e.g., IDs, target variable)
- **Floating-point** (e.g., income, credit amounts)
- **Object** (e.g., contract type, gender)

Missing values were a notable challenge, particularly in features related to assets and external data sources. 

### Key Features and Correlations
- **TARGET** has weak correlations with other features, making prediction more challenging.
- **AMT_CREDIT** shows positive correlation with goods prices and annuities.
- **DAYS_EMPLOYED** and **DAYS_BIRTH** exhibit weak negative correlations with TARGET.

## Data Preprocessing
1. **Handling Missing Values**: Missing values were either dropped or filled using zero, mean, or mode imputation.
2. **Feature Engineering**: New features like `NEW_EXT_SOURCE` and `PAYMENT_RATE` were created to improve prediction accuracy.
3. **Handling Outliers**: Outliers were identified and addressed to prevent biased model performance.

## Model Implementation and Training
The LightGBM algorithm was used for training the model. Categorical variables were encoded, and model parameters were optimized through cross-validation.

### Validation
- **Accuracy**: Achieved 91.90% validation accuracy.
- **ROC-AUC**: 0.735, indicating strong predictive performance.
- **Precision**: 0.413
- **Recall**: 0.015
- **F1-Score**: 0.029, balancing precision and recall.

## Fairness Analysis
Performance was tested across different subpopulations:
- Higher precision was observed in low-income individuals, suggesting fewer misclassifications in this group.
- **F1-scores** revealed trade-offs in performance between different age groups, with lower values for younger adults.

## Sensitivity Analysis
A sensitivity analysis was conducted by systematically varying input features. Results showed the model's predictions were highly sensitive to small changes in input values, with a range of 0.386 in model predictions.

## Conclusion
The audit highlighted the trade-offs between accuracy, fairness, and inclusivity in credit risk models. The model performed well in terms of accuracy, but further work is needed to ensure fairness across subpopulations.

### Recommendations
- **Enhance Data Quality**: Increase diversity and representation in the dataset.
- **Address Bias**: Implement fairness measures to reduce bias in predictions.
- **Improve Interpretability**: Incorporate methods for understanding model decisions.
- **Ongoing Monitoring**: Ensure transparency, accountability, and continuous monitoring of the ADS after deployment.

## References
Montoya, Anna, Kirill Odintsov, and Martin Kotek. “Home Credit Default Risk.”  
https://kaggle.com/competitions/home-credit-default-risk, 2018.
