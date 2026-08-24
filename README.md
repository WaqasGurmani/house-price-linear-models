# \# House Price Linear Models

# 

# This project studies and compares four linear regression algorithms on the Melbourne Housing Snapshot dataset:

# 

# 1\. Linear Regression

# 2\. Ridge Regression

# 3\. Lasso Regression

# 4\. Elastic Net Regression

# 

# The project follows a reproducible workflow covering data validation, exploratory analysis, preprocessing, model training, cross-validation, diagnostics, and final comparison.

# 

# \## Project Objectives

# 

# \- Understand how linear regression estimates house prices.

# \- Study the effect of L1 and L2 regularization.

# \- Compare prediction performance using the same dataset and test set.

# \- Examine coefficients, residuals, multicollinearity, and prediction errors.

# \- Prevent data leakage through pipelines and train-only preprocessing.

# 

# \## Dataset

# 

# \- \*\*Name:\*\* Melbourne Housing Snapshot

# \- \*\*Source:\*\* \[Kaggle](https://www.kaggle.com/datasets/dansbecker/melbourne-housing-snapshot)

# \- \*\*Local file:\*\* `data/raw/melb\_data.csv`

# \- \*\*Target:\*\* `Price`

# \- \*\*Problem:\*\* Supervised regression

# 

# The original CSV is kept unchanged and is not committed to this repository. Download instructions, attribution, limitations, and data-handling rules are available in \[`references/dataset\_documentation.md`](references/dataset\_documentation.md).

# 

# An independent train/test split will be created from `melb\_data.csv`. The final test subset will not be used for preprocessing decisions or hyperparameter selection.

# 

# \## Project Structure

# 

# ```text

# house-price-linear-models/

# ├── data/

# │   ├── raw/

# │   └── processed/

# ├── notebooks/

# ├── results/

# │   ├── figures/

# │   └── tables/

# ├── models/

# ├── src/

# ├── references/

# ├── tests/

# ├── .gitignore

# └── README.md

# ```

# 

# \## Notebook Sequence

# 

# 1\. `01\_data\_understanding.ipynb`

# 2\. `02\_eda\_and\_data\_quality.ipynb`

# 3\. `03\_preprocessing\_pipeline.ipynb`

# 4\. `04\_linear\_regression.ipynb`

# 5\. `05\_ridge\_regression.ipynb`

# 6\. `06\_lasso\_regression.ipynb`

# 7\. `07\_elastic\_net\_regression.ipynb`

# 8\. `08\_final\_model\_comparison.ipynb`

# 

# \## Modelling Workflow

# 

# \- Validate the dataset and target.

# \- Inspect missing values, duplicates, distributions, and unusual observations.

# \- Separate features and target.

# \- Create a fixed train/test split.

# \- Fit preprocessing steps using training data only.

# \- Use `Pipeline` and `ColumnTransformer`.

# \- Establish a `DummyRegressor` baseline.

# \- Select regularization parameters with cross-validation on training data.

# \- Evaluate final models on the untouched test set.

# \- Save important figures and result tables.

# 

# \## Evaluation Metrics

# 

# Each model will be evaluated using:

# 

# \- Mean Absolute Error (`MAE`)

# \- Root Mean Squared Error (`RMSE`)

# \- Coefficient of Determination (`R²`)

# 

# If the model is trained on `log1p(Price)`, predictions will be converted back with `expm1()` before final MAE and RMSE are reported.

# 

# \## Reproducibility Rules

# 

# \- A fixed `random\_state` will be used.

# \- Learned preprocessing parameters will come from training data only.

# \- Unknown categorical values will be handled safely.

# \- Cross-validation will use training data only.

# \- The final test set will remain untouched until model evaluation.

# \- Observations will be based only on actual outputs.

# 

# \## Current Status

# 

# Project setup and dataset documentation are in progress. Results will be added notebook by notebook.

