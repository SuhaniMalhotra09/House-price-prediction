# House Price Prediction

A supervised machine-learning regression project that predicts residential sale prices using the Ames Housing dataset from Kaggle's **House Prices: Advanced Regression Techniques** competition.

The project covers exploratory data analysis, data cleaning, feature engineering, preprocessing pipelines, model comparison, cross-validation, hyperparameter tuning, validation, and Kaggle-format prediction generation.

## Dataset

Source: [Kaggle – House Prices: Advanced Regression Techniques](https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data)

- Training set: 1,460 houses and 81 columns (including `SalePrice`).
- Test set: 1,459 houses and 80 columns.
- Target: `SalePrice`.

Download `train.csv` and `test.csv` from Kaggle and place both files in the repository's root directory, alongside the notebook. The datasets are not included in this repository.

## Project Structure

```text
House-price-prediction/
├── figures_detailed/                 # EDA, model-comparison and diagnostic plots
├── outputs/                          # Saved analysis and preprocessing outputs
├── processed_data/                   # Processed datasets and reports
├── model_training_and_evaluation.ipynb
├── submission.csv                    # Generated Kaggle-format predictions
├── requirements.txt
├── .gitignore
└── README.md
```

## Workflow

1. **Data understanding and EDA:** inspect dimensions, data types, summary statistics, target distribution, feature relationships and correlations.
2. **Data quality and cleaning:** check duplicates and invalid values; distinguish structural missing values from genuinely unknown values.
3. **Outlier analysis:** use the IQR rule to flag unusual observations, then remove only the two identified abnormal partial-sale records from the training data.
4. **Feature engineering:** create `TotalSF`, `TotalBathrooms` and `HouseAge`.
5. **Feature preparation:** ordinal-encode quality ratings, one-hot encode nominal categories, transform skewed features and remove unreliable `GarageYrBlt`.
6. **Preprocessing pipeline:** impute remaining missing values, scale numeric features and one-hot encode categorical features. Learned preprocessing steps are fitted within the training pipeline.
7. **Model comparison and tuning:** compare a mean baseline and nine regression models using 5-fold cross-validation; tune Ridge, Lasso and Gradient Boosting with `GridSearchCV`.
8. **Evaluation and prediction:** select the tuned model using cross-validation, evaluate it on a held-out validation set, inspect residuals and feature coefficients, then train on the labelled data for test-set predictions.

## Results

**Best model: Ridge Regression (`alpha=30`)**, selected using the lowest 5-fold cross-validation RMSE among the tuned candidates.

| Metric | Ridge (selected model) | Mean baseline |
|---|---:|---:|
| 5-fold CV RMSE (log price) | **0.1102** | — |
| Validation R² (log target) | **0.9123** | -0.0058 |
| Validation RMSE (price) | **$23,905** | $88,272 |
| Validation MAE (price) | **$15,041** | $59,930 |
| Validation median percentage error | **6.18%** | 27.08% |

The validation results are from the notebook's saved run using an 80/20 train-validation split (random state 42). Dollar-based errors are calculated after converting predictions back from the logarithmic scale. The validation set contains 292 houses and is separate from the data used to fit and tune the models.

**Important:** these are local validation results, not a Kaggle leaderboard score. The competition test labels are hidden, so a test-set RMSE or R² cannot be calculated from the supplied test data.

## Visualizations

The `figures_detailed/` folder contains the notebook's plots, including:

- Sale-price and feature distributions.
- Correlation and missing-value analysis.
- Cross-validation model comparison.
- Actual-versus-predicted prices and residual diagnostics.
- Feature coefficients for the selected Ridge model.

## Run the Project

1. Clone the repository:

   ```bash
   git clone https://github.com/SuhaniMalhotra09/House-price-prediction.git
   cd House-price-prediction
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Download `train.csv` and `test.csv` from the Kaggle competition and place them in the repository root.

4. Start Jupyter and run `model_training_and_evaluation.ipynb` from top to bottom:

   ```bash
   jupyter notebook
   ```

The notebook saves the final test predictions to `submission.csv` with the required `Id` and `SalePrice` columns.

## Technologies

Python, Pandas, NumPy, Matplotlib, scikit-learn and Jupyter Notebook.

## Author

Suhani Malhotra · [GitHub](https://github.com/SuhaniMalhotra09)
