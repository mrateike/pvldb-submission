# Appendix A: Our Prediction Model Details

This appendix provides additional information on the models used in our evaluation that could not be included in the main paper due to space constraints.

---

## A.1 Model Overview

We report the hyperparameters for the [GradientBoostingRegressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html) models used in the main paper for end-to-end testing (target: Perf. (ExecutorRunTimeMaxbyCore)). The best hyperparameters have been selected using 5-fold-cross-validation.

| Data |    Model    | Hyperparemters | MSE | R2 |
|:-------|:--------------|:-----------|--------|------|
| TPC-DS | 0-shot | 'n_estimators': 410, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $2.8957 \pm 0.1779$              | $0.5434 \pm 0.0156$ |
| TPC-DS | n-shot | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $0.5148 \pm 0.0385$                   | $0.9186 \pm 0.0076$      |
| SQLStorm | 0-shot |'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $2.6658 \pm 0.2016$              | $0.9400 \pm 0.0176$ |
| SQLStorm | n-shot | 'n_estimators': 460, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $0.6524 \pm 0.5041$                   | $0.9878 \pm 0.0061$      |


---

## A.2 Cross-Validation 0-shot Models 

Here we report complete results for training 0-shot models, comparing LinearRegression, GradientBoostingRegressor, and RandomForestRegressor for different targets, as explained in the main paper.

### A.2.1 TPC-DS

 | target_column   | model_name   | model_params                                                                                              | mse                              | r2                  |
|:-------------------|:------------------|:---------------------------------------------------------------------------------------------------------------|:--------------------------------------|:-------------------------|
| Cost    | Linear Regression | 'fit_intercept': False                                                                                  | $12,765,895.7817 \pm 5,101,713.6907$  | $-106.5049 \pm 43.5657$  |
| Cost    | Random Forest| 'bootstrap': True, 'n_estimators': 160, 'max_depth': 7                                                  | $45,759.9685 \pm 4,042.5299$     | $0.6174 \pm 0.0187$ |
| Cost    | Gradient Boosting | 'n_estimators': 210, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $38,652.0878 \pm 3,158.7891$     | $0.6766 \pm 0.0149$ |
| Perf (DurationStage)      | Linear Regression | 'fit_intercept': False                                                                                  | $87.2132 \pm 22.3929$            | $-3.2026 \pm 1.1611$|
| Perf (DurationStage)      | Random Forest| 'bootstrap': True, 'n_estimators': 410, 'max_depth': 7                                                  | $11.7462 \pm 0.5864$             | $0.4377 \pm 0.0116$ |
| Perf (DurationStage)      | Gradient Boosting | 'n_estimators': 410, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $10.2669 \pm 0.5193$             | $0.5085 \pm 0.0103$ |
| Perf (MaxbyCore)| Linear Regression | 'fit_intercept': True                                                                                   | $27.6213 \pm 5.3687$             | $-3.3617 \pm 0.8546$|
| Perf (MaxbyCore)| Random Forest| 'bootstrap': True, 'n_estimators': 160, 'max_depth': 7                                                  | $3.0474 \pm 0.1948$              | $0.5195 \pm 0.0175$ |
| Perf (MaxbyCore)| Gradient Boosting | 'n_estimators': 410, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $2.8957 \pm 0.1779$              | $0.5434 \pm 0.0156$ |

### A.2.2 SQLStorm

| target_column   | model_name   | model_params                                                                                              | mse                              | r2                  |
|:-------------------|:------------------|:---------------------------------------------------------------------------------------------------------------|:--------------------------------------|:-------------------------|
| Cost    | Linear Regression | 'fit_intercept': True                                                                                   | $924,778.1087 \pm 244,326.3015$  | $-2.9266 \pm 0.7885$|
| Cost    | Random Forest| 'bootstrap': True, 'n_estimators': 10, 'max_depth': 7                                                   | $13,358.5137 \pm 846.0770$       | $0.9416 \pm 0.0115$ |
| Cost    | Gradient Boosting | 'n_estimators': 260, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $11,545.1384 \pm 358.1276$       | $0.9498 \pm 0.0075$ |
| Perf (DurationStage)      | Linear Regression | 'fit_intercept': True                                                                                   | $58.4296 \pm 14.6535$            | $0.0816 \pm 0.0072$ |
| Perf (DurationStage)      | Random Forest| 'bootstrap': True, 'n_estimators': 10, 'max_depth': 7                                                   | $8.5018 \pm 1.2000$              | $0.8609 \pm 0.0255$ |
| Perf (DurationStage)      | Gradient Boosting | 'n_estimators': 360, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $6.0936 \pm 0.2921$              | $0.8971 \pm 0.0284$ |
| Perf (CostMaxbyCore)| Linear Regression | 'fit_intercept': False                                                                                  | $60.9472 \pm 11.1733$            | $-0.3060 \pm 0.1907$|
| Perf (CostMaxbyCore)| Random Forest| 'bootstrap': False, 'n_estimators': 10, 'max_depth': 7                                                  | $20.0779 \pm 7.2291$             | $0.5891 \pm 0.0637$ |
| Perf (CostMaxbyCore)| Gradient Boosting | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $2.6658 \pm 0.2016$              | $0.9400 \pm 0.0176$ |


## A.3 Cross-Validation n-shot Models 

Here we report complete results for training n-shot models, comparing LinearRegression, GradientBoostingRegressor, and RandomForestRegressor for different targets, as explained in the main paper.


### A.3.1 TPC-DS
| target_column            |  model_name        | model_params                                                                                                   | mse                                   | r2                       |
|:-------------------------|:------------------|:---------------------------------------------------------------------------------------------------------------|:--------------------------------------|:-------------------------|
  | Cost         | Linear Regression | 'fit_intercept': False                                                                                       | $56,421,446.1955 \pm 31,701,008.5355$ | $-475.6542 \pm 270.6458$ |
 | Cost         | Random Forest     | 'bootstrap': True, 'n_estimators': 110, 'max_depth': 7                                                       | $21,867.7576 \pm 1,541.9805$          | $0.8164 \pm 0.0151$      |
 | Cost         | Gradient Boosting | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $4,592.4841 \pm 334.0984$             | $0.9614 \pm 0.0035$      |
 | Perf. (DurationStage)           | Linear Regression | 'fit_intercept': False                                                                                       | $136.5464 \pm 33.6868$                | $-5.5600 \pm 1.6930$     |
 | Perf. (DurationStage)           | Random Forest     | 'bootstrap': True, 'n_estimators': 110, 'max_depth': 7                                                       | $6.1407 \pm 0.3343$                   | $0.7061 \pm 0.0079$      |
 | Perf. (DurationStage)           | Gradient Boosting | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $1.9204 \pm 0.1576$                   | $0.9079 \pm 0.0080$      |
 | Perf. (MaxbyCore)| Linear Regression | 'fit_intercept': True                                                                                        | $174.3614 \pm 46.5823$                | $-26.7242 \pm 8.0328$    |
 | Perf. (MaxbyCore)| Random Forest     | 'bootstrap': True, 'n_estimators': 110, 'max_depth': 7                                                       | $1.2151 \pm 0.0902$                   | $0.8077 \pm 0.0190$      |
 | Perf. (MaxbyCore)| Gradient Boosting | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $0.5148 \pm 0.0385$                   | $0.9186 \pm 0.0076$      |

### A.3.2 SQLStorm


| target_column            |  model_name        | model_params                                                                                                   | mse                                   | r2                       |
|:-------------------------|:------------------|:---------------------------------------------------------------------------------------------------------------|:--------------------------------------|:-------------------------|
| Cost         | Linear Regression | 'fit_intercept': True                                                                                        | $1,105,307.8681 \pm 255,780.1731$     | $-3.7082 \pm 0.8108$     |
| Cost         | Random Forest     | 'bootstrap': True, 'n_estimators': 460, 'max_depth': 7                                                       | $4,958.8561 \pm 363.9871$             | $0.9783 \pm 0.0042$      |
| Cost         | Gradient Boosting | 'n_estimators': 410, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $856.2648 \pm 522.6476$               | $0.9962 \pm 0.0025$      |
| Perf. (DurationStage)           | Linear Regression | 'fit_intercept': True                                                                                        | $56.7856 \pm 13.1241$                 | $0.1033 \pm 0.0300$      |
| Perf. (DurationStage)           | Random Forest     | 'bootstrap': True, 'n_estimators': 110, 'max_depth': 7                                                       | $6.0071 \pm 0.7221$                   | $0.9017 \pm 0.0169$      |
| Perf. (DurationStage)           | Gradient Boosting | 'n_estimators': 460, 'max_depth': 7, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $2.2269 \pm 0.3552$                   | $0.9636 \pm 0.0064$      |
| Perf. (MaxbyCore)| Linear Regression | 'fit_intercept': True                                                                                        | $65.6093 \pm 10.3240$                 | $-0.4159 \pm 0.2239$     |
| Perf. (MaxbyCore)| Random Forest     | 'bootstrap': True, 'n_estimators': 10, 'max_depth': 7                                                        | $8.5395 \pm 3.5709$                   | $0.8305 \pm 0.0439$      |
| Perf. (MaxbyCore)| Gradient Boosting | 'n_estimators': 460, 'max_depth': 6, 'learning_rate': 0.1, 'subsample': 0.5, 'min_weight_fraction_leaf': 0.0 | $0.6524 \pm 0.5041$                   | $0.9878 \pm 0.0061$      |


