OUTPUT FOLDER GUIDE (Phase 1: preprocessing)

model_ready/  -> MODEL-READY (used directly for modeling in Phase 2)
  X_train_preprocessed.csv, X_valid_preprocessed.csv, X_test_preprocessed.csv
  y_train.csv, y_valid.csv  (columns: Id, SalePrice, log1p_SalePrice)
  test_ids.csv              (Ids for the Kaggle submission file)
  preprocessor.joblib       (fitted pipeline; expects data after structural fills + feature engineering)

analysis/     -> FOR ANALYSIS (cleaned, human-readable, not encoded or scaled)
  train_cleaned_with_features.csv, test_cleaned_with_features.csv

reports/      -> DOCUMENTATION of findings and decisions
  missing values, data quality checks, outlier reports, transformation_log.csv

plots/        -> FIGURES for the presentation

The original train.csv and test.csv were never modified.
