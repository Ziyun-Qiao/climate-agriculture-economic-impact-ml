# Machine Learning Approaches for Predicting the Economic Impacts of Climate Change on Agriculture

This repository contains the implementation for my MSc dissertation project at the University of Leeds:

**Machine Learning Approaches for Predicting the Economic Impacts of Climate Change on Agriculture: A Comparative Study**

The project investigates whether machine learning methods can be used to predict the recorded economic impact of climate change on agriculture and whether clustering-derived information provides additional predictive value.

---

## Project Overview

The study uses the publicly available **Climate Change Impact on Agriculture 2024** dataset from Kaggle.

The dataset contains 10,000 observations and includes climatic, agricultural, environmental, contextual, and economic variables.

The prediction target is:

`Economic_Impact_Million_USD`

which is referred to as **EconomicImpact** throughout the dissertation.

The project combines exploratory data analysis, K-Means clustering, supervised regression modelling, hyperparameter optimisation, cross-validation, and model interpretation.

---

## Research Objectives

The main objectives of the project are:

- To preprocess the dataset and examine relationships among climatic, agricultural, environmental, contextual, and economic variables.
- To apply K-Means clustering to identify broad climate-agriculture profiles.
- To develop and compare six regression models for predicting EconomicImpact.
- To optimise selected models and evaluate predictive accuracy and stability.
- To assess whether the K-Means-derived cluster feature provides additional predictive value.
- To examine prediction-error patterns and interpret variables associated with EconomicImpact.

---

## Dataset

The analysis uses the **Climate Change Impact on Agriculture 2024** dataset obtained from Kaggle.

The dataset contains 15 original variables, including:

### Contextual variables
- Year
- Country
- Region
- Crop_Type

### Climate variables
- Temperature
- Rainfall
- CO2
- ExtremeEvents

### Agricultural variables
- Yield
- Irrigation
- Pesticide
- Fertilizer

### Environmental variables
- SoilHealth
- Adaptation_Strategies

### Target variable
- Economic_Impact_Million_USD

The dataset used in this repository is included as:

`climate_change_impact_on_agriculture_2024.csv`

The dataset is used for academic and comparative methodological analysis. The original data-generation process and representativeness of the observations could not be independently verified, so the results should be interpreted within the scope of the selected dataset.

---

## Machine Learning Models

Six regression models were evaluated:

1. Linear Regression
2. Decision Tree Regressor
3. Random Forest Regressor
4. Gradient Boosting Regressor
5. XGBoost Regressor
6. Support Vector Regression

The models were evaluated using a consistent training-test split and the following metrics:

- R²
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

---

## Data Preprocessing

The preprocessing workflow includes:

- Dataset inspection
- Missing-value checking
- Duplicate checking
- One-hot encoding of categorical variables
- Train-test split
- Feature scaling where required
- StandardScaler for Support Vector Regression
- Standardisation of clustering variables for K-Means

The dataset was divided into:

- 80% training data
- 20% testing data

with:

`random_state = 42`

Preprocessing transformations required for SVR and K-Means were fitted using the training data and subsequently applied to the test data to reduce the risk of information leakage.

---

## K-Means Clustering

K-Means clustering was used to explore whether broad climate-agriculture profiles existed within the dataset.

The clustering variables were:

- Temperature
- Rainfall
- CO2
- ExtremeEvents
- Irrigation
- SoilHealth

EconomicImpact was excluded from the clustering inputs.

The Elbow Method was used to examine the number of clusters, and four clusters were retained based on the observed elbow pattern and interpretability of the resulting profiles.

The resulting cluster labels were subsequently added as an additional predictor to evaluate whether clustering-derived information improved regression performance.

---

## Hyperparameter Optimisation

Hyperparameter optimisation was performed for:

- Random Forest
- XGBoost

`GridSearchCV` with five-fold cross-validation was used on the training data.

R² was used as the optimisation scoring metric.

The test set was excluded from hyperparameter selection and was reserved for final evaluation.

---

## Model Validation

Model performance was evaluated using:

- Held-out test-set evaluation
- Five-fold cross-validation
- Actual vs predicted analysis
- Residual analysis
- Comparison of models with and without the cluster feature

The final evaluation should be interpreted as internal validation within the selected dataset.

The project does not directly test geographical or temporal generalisation across unseen countries or future time periods.

---

## Main Findings

The tuned Random Forest achieved the strongest final test performance:

- **MAE:** 224.326
- **RMSE:** 285.909
- **R²:** 0.5468

However, its advantage over the strongest alternative models was small:

- Linear Regression: R² = 0.5445
- Tuned XGBoost: R² = 0.5428

Five-fold cross-validation for the tuned Random Forest produced:

- Mean R² = 0.5161
- Standard deviation = 0.0130

The K-Means-derived cluster feature produced only negligible changes in predictive performance.

The results therefore suggest that clustering was more useful for exploratory interpretation than for improving predictive accuracy.

Yield showed a strong association with EconomicImpact, while regional and crop-related variables also captured contextual differences.

---
