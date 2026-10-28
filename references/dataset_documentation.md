# Dataset Documentation

## Dataset Information

- **Name:** Melbourne Housing Snapshot
- **Source:** [Kaggle - Melbourne Housing Snapshot](https://www.kaggle.com/datasets/dansbecker/melbourne-housing-snapshot)
- **File:** `data/raw/melb_data.csv`
- **Target:** `Price`
- **Problem:** Supervised regression
- **Domain:** Residential property sales in Melbourne, Australia

## Attribution

The Kaggle dataset was published by DanB and credits Tony Pino as the original dataset creator. The source describes property-sale records collected from Domain.com.au.

This repository uses the dataset for an educational regression study. Dataset ownership is not claimed by the project author.

## Files Included in This Repository

The original `melb_data.csv` is included and retained unchanged.

The repository also contains derived files under `data/processed/`, including saved split indices, cleaned datasets, prepared predictors, and targets.

Prepared predictor files retain missing values where appropriate. Learned imputation is performed within model pipelines rather than applied to the entire dataset before cross-validation.

## Training and Test Split

The dataset contains 13,580 records:

- Training set: 10,864 records
- Held-out test set: 2,716 records

Saved row indices identify the fixed split. Exploratory analysis and model-development decisions used the training data.

Linear Regression, Ridge, and Lasso were compared using the same five cross-validation folds. Ridge was selected using mean validation RMSE before final test evaluation.

The held-out test set has now been evaluated. Its results were not used to retune the selected model.

## Data Quality Review

The notebooks document checks covering:

- Missing values and zero-value meanings
- Duplicate records and target validity
- Numerical distributions and extreme observations
- Construction years relative to sale dates
- Agreement between related predictors
- Category frequencies and rare categories
- Feature relationships and target associations

Unresolved extreme measurements were not corrected by guessing or removed solely because they produced large prediction errors.

## Preprocessing

Documented cleaning rules were applied consistently to training and test data.

Numerical median imputation, standard scaling, categorical imputation, and one-hot encoding were fitted within each cross-validation training fold. The selected pipeline was then fitted on the full training set.

Test inputs were transformed using those fitted parameters. No preprocessing parameters were fitted on the test set.

The saved pipelines expect 16 prepared predictor columns. Earlier raw-data cleaning and feature preparation are separate from the fitted pipelines.

## Limitations

- The dataset represents a historical snapshot of the Melbourne housing market.
- Missing values and unresolved unusual measurements can affect results.
- Some categories have limited representation.
- A random split does not establish performance on future sales or unseen geographic markets.
- Predictive associations do not establish causation.
- Further development requires a new independent evaluation set if the existing test results influence modelling decisions.

## License and Attribution

The project's recorded dataset license is CC BY-NC-SA 4.0. Consult the original Kaggle source for the applicable license and attribution details.

The raw dataset and derived CSVs are redistributed with attribution for this non-commercial educational project. Dataset reuse must comply with its applicable license, including attribution, non-commercial use, and share-alike requirements. Any separate license for project code does not replace the dataset license.