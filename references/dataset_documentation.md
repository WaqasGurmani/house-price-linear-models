\# Dataset Documentation



\## Dataset Information



\- \*\*Name:\*\* Melbourne Housing Snapshot

\- \*\*Source:\*\* \[Kaggle – Melbourne Housing Snapshot](https://www.kaggle.com/datasets/dansbecker/melbourne-housing-snapshot)

\- \*\*File used:\*\* `melb\_data.csv`

\- \*\*Target column:\*\* `Price`

\- \*\*Problem type:\*\* Supervised regression

\- \*\*Domain:\*\* Residential property sales in Melbourne, Australia



\## Dataset Origin



The dataset is a static snapshot of Melbourne property-sale records collected from publicly available results on Domain.com.au. The Kaggle dataset was published by DanB and credits Tony Pino as the original dataset creator.



\## Project Usage



Only `melb\_data.csv` is used in this project. An independent training and test split will be created from this file. The final test subset will remain untouched during preprocessing decisions and hyperparameter selection.



The original CSV is stored locally at:



`data/raw/melb\_data.csv`



The raw dataset is not modified or committed to GitHub. Users can download it from the source link above.



\## Data Validation Plan



Before modelling, the project will check:



\- Dataset dimensions and column types

\- Missing values

\- Duplicate rows

\- Target validity

\- Numerical and categorical features

\- Unusual values and possible outliers

\- High-cardinality columns

\- Target distribution and skewness



All reported findings will be based on the actual notebook outputs.



\## Preprocessing Rules



Preprocessing parameters will be learned from training data only. Imputation, encoding, scaling, transformations, and feature-engineering decisions will not use information from the final test subset.



\## Limitations



\- The data represents a historical snapshot of the Melbourne housing market.

\- Results may not generalize to other cities, countries, or current market conditions.

\- Property prices can be affected by economic and location factors not included in the dataset.

\- Missing values, unusual observations, and scraped-data quality issues must be inspected before modelling.

\- Model performance represents predictive association and does not establish causation.



\## License and Attribution



The Kaggle dataset is listed under the \*\*CC BY-NC-SA 4.0\*\* license. This project provides attribution and links to the original source instead of redistributing the raw CSV.

