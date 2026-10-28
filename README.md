# House Price Linear Models

A regression study comparing Linear Regression, Ridge, and Lasso on the Melbourne Housing Snapshot dataset. The project covers data quality assessment, exploratory analysis, leakage-aware preprocessing, cross-validation, model diagnostics, and final held-out evaluation.

## Results

All three models used the same training data, preprocessing strategy, and five cross-validation folds.

| Model | Mean CV MAE (AUD) | Mean CV RMSE (AUD) | Mean CV R² |
|---|---:|---:|---:|
| Linear Regression | 242,395.38 | 395,384.44 | 0.618 |
| Ridge | 237,848.21 | 388,385.43 | 0.631 |
| Lasso | 238,895.73 | 390,142.86 | 0.627 |

Ridge with **alpha = 10** was selected using the lowest mean validation RMSE.

### Final Held-Out Test Results

Only the selected Ridge model was evaluated on the reserved test set.

| Model | Test Properties | MAE (AUD) | RMSE (AUD) | R² |
|---|---:|---:|---:|---:|
| Ridge | 2,716 | 233,860.35 | 349,213.56 | 0.693 |

R² is not percentage accuracy. Test results were not used to retune the model.

## Dataset

- **Name:** Melbourne Housing Snapshot
- **Source:** [Kaggle — Melbourne Housing Snapshot](https://www.kaggle.com/datasets/dansbecker/melbourne-housing-snapshot)
- **Original file:** `data/raw/melb_data.csv`
- **Target:** `Price`
- **Training records:** 10,864
- **Test records:** 2,716
- **Prepared predictors:** 16

The original CSV, split indices, and prepared training and test CSVs are included in this repository. The original dataset is retained unchanged. Prepared predictor files can still contain missing values because imputation is performed inside the model pipelines.

See [dataset documentation](references/dataset_documentation.md) for additional source information and data context. Dataset ownership remains with its respective owners.

## Notebook Sequence

Run notebooks from the `notebooks` directory in the following order:

1. `01_data_understanding.ipynb`
2. `02_eda_and_data_quality.ipynb`
3. `03_preprocessing_and_feature_engineering.ipynb`
4. `04_linear_regression_baseline.ipynb`
5. `05_ridge_regression.ipynb`
6. `06_lasso_regression.ipynb`
7. `07_final_model_evaluation.ipynb`

The notebooks use `Path.cwd().parent` to locate the project root.

## Methodology

1. Validate the dataset and establish a fixed training/test split.
2. Explore training-data distributions, missingness, unusual values, and feature relationships.
3. Apply documented cleaning rules consistently to training and test data.
4. Prepare numerical and categorical predictors.
5. Fit numerical median imputation and standard scaling within each training fold.
6. Fill missing categorical values with `Unknown` and apply one-hot encoding with unseen-category handling.
7. Establish a mean-prediction DummyRegressor baseline.
8. Compare Linear Regression, Ridge, and Lasso using the same shuffled five-fold cross-validation splits with `random_state=42`.
9. Select regularization strength using mean validation RMSE.
10. Evaluate the selected Ridge pipeline on the held-out test set.

Models predict price directly; no logarithmic target transformation was applied.

Ridge and Lasso scores are development estimates from the folds used for hyperparameter selection, rather than independent estimates of the entire tuning procedure.

## Main Findings

- Ridge modestly improved cross-validation performance over Linear Regression and Lasso.
- Lasso selected **alpha = 100** and set **481 of 802 transformed-feature coefficients to zero**, leaving 321 non-zero coefficients.
- Regularization did not eliminate large prediction errors.
- Training out-of-fold diagnostics showed underprediction for several expensive properties and a large overprediction associated with an extreme recorded building area.
- Large errors alone were not used as a reason to remove observations.

## Saved Artifacts

- `results/tables/`: cross-validation scores, coefficient summaries, diagnostic tables, and final test results.
- `results/figures/`: EDA and model diagnostic plots.
- `models/preprocessor_unfitted.joblib`: preprocessing specification.
- `models/ridge_pipeline_fitted.joblib`: selected fitted Ridge pipeline.
- `models/lasso_pipeline_fitted.joblib`: fitted Lasso candidate pipeline.

The fitted pipelines include learned imputation, scaling, encoding, and model parameters. They expect the same **16 prepared predictor columns** used during training. Raw-data cleaning and feature preparation must be applied separately.

## Running the Project

The notebooks use Python, Jupyter, pandas, NumPy, Matplotlib, Seaborn, scikit-learn, and joblib.

From the project root, open Jupyter inside the notebook directory:

```bash
cd notebooks
jupyter notebook
```

Run notebooks in the documented order. Hyperparameter searches can take time on a CPU.

For inference with the selected model, load the fitted Ridge pipeline and call `.predict()` on prepared inputs. Do not refit preprocessing on test or inference data.

Serialized model compatibility depends on the Python and package versions used to create the artifact. Load only trusted joblib files.

## Limitations

- Missing values and unresolved extreme measurements can affect predictions.
- Small or rare categories may have limited training support.
- Coefficients describe fitted conditional associations, not causal effects.
- Correlated predictors and overlapping categorical encodings complicate coefficient interpretation.
- A random split does not establish performance on future sales or unseen geographic markets.
- The held-out test set has now been evaluated. Further development should use training cross-validation and a new independent evaluation set.

## Project Status

The three-model study and final Ridge evaluation are complete.

Elastic Net was part of the initial plan but was not implemented in this version. It is not included in the reported comparison.