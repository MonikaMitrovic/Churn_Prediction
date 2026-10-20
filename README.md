# Churn Prediction Project

## Project Overview

The goal of this project is to predict customer churn and identify users who are at high risk of leaving the service. Customer churn represents a significant business cost, as losing existing customers is usually more expensive than retaining them. For this reason, the main focus of the project is to correctly identify churn customers while keeping a reasonable balance between false negatives and false positives.

The dataset used in this project (Telco Customer Churn) is imbalanced (about 27% churn), which makes it particularly suitable for practicing real-world binary classification problems and evaluating models using appropriate metrics beyond simple accuracy.

---

## Exploratory Data Analysis

The EDA answers a business question: *which customers leave, when do they leave, and where should a retention team act first?*

The data is split into an EDA set (80%) and a test set (20%) **before** the analysis, so the test set never influences any decision (no data leakage).

Key findings:
- **Contract type** is the strongest signal: month-to-month customers churn at ~43% versus ~3% on two-year contracts.
- **The first year is critical:** churn is ~52% in the first six months of tenure and ~10% after four years.
- **Fiber optic customers** account for a disproportionate share of departures (roughly two-thirds), especially when new and on month-to-month contracts.
- **Protective services** (Online Security, Tech Support) go with retention: churn is ~42% without them and ~14–15% with them. Streaming services show little relationship with churn.
- **Electronic check** is a specific risk indicator (~46% churn versus ~15–19% for other payment methods).
- **Gender and phone service** carry no useful signal.

These are associations, not proven causes, so any retention action should be tested experimentally before scaling.

---

## Model Choice and Motivation

Support Vector Classification (SVC) was selected as the main model for this project. Although other models such as Logistic Regression, XGBoost, or other tree-based methods may be more commonly used or better suited for this type of problem, the choice of SVC was intentional.

The goal was to practice and demonstrate a structured approach to working with this model, including preprocessing, feature engineering, hyperparameter tuning, probability calibration, and threshold optimization. The project focuses on extracting the maximum possible performance from SVC through careful analysis rather than relying on more complex models.

---

## Modeling Strategy

The modeling workflow includes:
- Feature engineering and preprocessing using pipelines and transformers
- Hyperparameter tuning with cross-validation
- Probability calibration to improve reliability of predicted probabilities
- Threshold optimization with a focus on recall and F2-score

Special attention is given to reducing false negatives, as missing a churn customer has a higher business cost than incorrectly flagging a non-churn customer.

---

## Business Perspective

From a business point of view, the priority is customer retention. The model is designed to identify as many churn customers as possible, even if this leads to some false positives. Offering a retention incentive to a customer who would not churn is generally less costly than losing a customer who would.

Instead of using only a binary prediction, a more practical approach is to use churn probabilities as the final output. Customers can then be grouped based on their predicted risk, for example:
- **Low risk (0.1 – 0.3):** unlikely to churn, no action needed
- **Medium risk (0.3 – 0.6):** customer contact and satisfaction assessment
- **High risk (> 0.6):** proactive retention actions such as better offers or service upgrades

This probability-based strategy allows for more flexible and cost-effective decision-making.

---

## Project Structure

- `churn_eda.ipynb` – Exploratory data analysis (statistical tests, tenure and service analysis, variable interactions, key findings and recommendations)
- `churn_prediction_svc.ipynb` – Model training, calibration, evaluation, and final results
