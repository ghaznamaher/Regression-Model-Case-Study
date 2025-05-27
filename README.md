# Regression-Model-Case-Study
Report: Analysis and Modeling of University Admissions Data

1. Introduction

This report is highlihting the process of analyzing and modeling different regression models  to predict the "Chance of Admit" based on various applicant attributes/criteria. 

2. Data Loading and Exploration

The dataset was loaded from a CSV file. Initial exploration included checking the shape, data types, and value counts of each column. The dataset consists of both continuous and categorical features.

Data Shape: The dataset contains 400 rows and 9 columns.
Data Types: All columns have correct data types.
Value Counts: To access if any irrelevant value is not present.

3. Data Preprocessing


Statistical Summary: Descriptive statistics were generated to understand the central tendency, dispersion, and shape of the data. Minimum and maximum values were checked and found to be within expected ranges.
Duplicate and Missing Value Check:  No duplicates or missing values were found.
Column Dropping: The "Serial No." column was dropped as it is not relevant for prediction.
Outlier Checking: Box plots were used to visualize potential outliers in numerical columns. Outliers were observed in "LOR" and "CGPA", but these values are valid data points reflecting real applicant profiles ,hence kept.
Scaling: The features (excluding "Chance of Admit") were scaled using MinMaxScaler. This was chosen because many features are not perfectly Gaussian and the target variable is between 0 and 1, making the scaled feature range compatible.

4. Data Visualization

Visualizations were used to gain insights into the data distribution and relationships:

Histograms: Histograms were plotted for all features and the target variable to visualize their distributions.
Pair Plot: A pair plot was generated to visualize the relationships between all pairs of variables. This revealed apparent linear relationships between "Chance of Admit" and several features (GRE Score, TOEFL Score, University Rating, SOP, LOR, CGPA, and Research).
Scatter Plots: Individual scatter plots of each feature against "Chance of Admit" were created to confirm the observed linear relationships.
Heatmap: A heatmap of the correlation matrix was generated to understand the linear correlations between variables. High correlations were observed between "TOEFL," "CGPA," and "GRE," indicating potential multicollinearity.

5. Model Building and Evaluation

Three different regression models were implemented and evaluated: Multiple Linear Regression, Decision Tree Regression, and Random Forest Regression. The data was split into an 80:20 train-test set for model training and evaluation.

Multicollinearity Check (VIF): Variance Inflation Factor (VIF) was calculated for the scaled features to quantify multicollinearity. GRE Score, TOEFL Score, and University Rating showed high VIF values, confirming the multicollinearity observed in the heatmap.

Multiple Linear Regression:

A Linear Regression model was trained on the scaled training data.
Model performance was evaluated using Mean Squared Error (MSE), Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), and R² Score on the test set.
The model's performance on the training set was compared to the test set to check for overfitting or underfitting. The R² scores were similar, suggesting the model generalizes well.
An independent prediction with an arbitrary input resulted in an invalid negative prediction, highlighting a limitation of the linear model for this problem where the output must be between 0 and 1.
Ridge Regression (Regularized Linear Regression):

A Ridge Regression model was trained to address potential issues arising from multicollinearity.
The model was evaluated on the test set. The R² score did not significantly improve compared to standard Linear Regression, suggesting that while multicollinearity exists, its impact was not severe enough for Ridge to offer a substantial improvement in this case.
Decision Tree Regression:

A Decision Tree Regressor was trained on the training data.
Initial evaluation showed a high R² score on the training set (1.0) and a significantly lower R² score on the test set (0.63), indicating severe overfitting.
Hyperparameter Tuning: GridSearchCV was used to find the best hyperparameters for the Decision Tree model to mitigate overfitting. The optimized model was evaluated on the test set, showing an improved R² score.
The optimized Decision Tree was visualized.
Random Forest Regression:

A Random Forest Regressor was trained.
Initial evaluation showed a training R² score close to 1.0 and a test R² score around 0.85, suggesting mild overfitting compared to the Decision Tree, but still better generalization than the un-tuned Decision Tree.
Hyperparameter Tuning: RandomizedSearchCV was used to tune the hyperparameters of the Random Forest model. The optimized model's performance was evaluated on the test set.
One of the trees from the optimized Random Forest was visualized.

6. Feature Selection-Based Modeling

Feature importances were extracted from the best Random Forest model to identify the most influential features. The models were then retrained using only the top 5 features.

Feature Importances: The importance of each feature in predicting the "Chance of Admit" was determined. CGPA, GRE Score, TOEFL Score, University Rating, and SOP were identified as the top 5 most important features.
Model Retraining with Top 5 Features:
Random Forest, Decision Tree, and Multiple Linear Regression models were retrained using only the top 5 features.
The R² scores of these models were evaluated on the test set. Retraining with a reduced set of features generally resulted in slightly lower R² scores compared to models trained on all features, but this can help in building simpler and potentially more interpretable models while still retaining a good level of predictive power.

7. Final Evaluation

The final evaluation results for all models are summarized below:

Model	R² Score (Test)
Multiple Linear Regression	0.80
Ridge Regression	0.80
Decision Tree Regression (Untuned)	0.63
Decision Tree Regression (Tuned)	0.72
Random Forest Regression (Untuned)	0.85
Random Forest Regression (Tuned)	0.87
Random Forest (Top 5 Features)	0.85
Decision Tree (Top 5 Features)	0.67
Multiple Linear Regression (Top 5 Features)	0.78

8. Conclusion

Based on the evaluation, the tuned Random Forest Regression model performed best in predicting the "Chance of Admit," achieving the highest R² score on the test set. Decision Tree Regression significantly improved after hyperparameter tuning, reducing overfitting. Multiple Linear Regression provided a reasonable baseline but struggled with generating valid predictions for all inputs due to the bounded nature of the target variable. Retraining models with the top 5 features showed that a good level of predictive performance can be maintained with a reduced set of features, which can be beneficial for model interpretability and efficiency.

Further work could involve exploring other regression algorithms, advanced feature engineering techniques, or incorporating external factors that might influence university admissions.
