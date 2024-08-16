# Data Analysis Project

This repository contains a data analysis and processing project aimed at preparing the dataset for predictive modeling and improving its quality. The process includes handling missing values, removing outliers, and selecting relevant features.

## Objective

The goal of this project is to prepare the data for predictive analysis, ensuring that the dataset is clean and ready for use in machine learning models.

## Steps Taken

### 1. Handling Missing Values

Identified columns with a significant amount of missing values and removed those with more than 17% missing data. For categorical columns, filled missing values based on the frequency of the most common values. This approach helps maintain data integrity without introducing arbitrary values.

### 2. Outlier Treatment

Applied the Tukey method to identify and handle outliers in numeric columns. This method uses the interquartile range (IQR) to detect values that are significantly different from the main distribution of the data. Removing outliers is important to prevent extreme values from distorting the results of the analysis.

### 3. Feature Selection

Used the VarianceThreshold method to reduce the dimensionality of the dataset and improve model efficiency. Set a threshold of 0.1 to remove features with variance below this value. This helps eliminate features that do not provide significant information for the model, keeping only those with substantial variation.

### 4. Modeling

Trained the model using cross-validation across various models and selected Random Forest Regressor and XGBoost for their superior RMSE performance. In the testing phase, XGBoost performed better in the submission, so I fine-tuned it and managed to reduce the RMSE from 0.15 to 0.14.
