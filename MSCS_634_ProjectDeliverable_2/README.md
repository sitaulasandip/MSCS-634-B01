# MSCS 634 Project - Deliverable 2: Regression Modeling and Performance Evaluation

Name: Sandip Sitaula

Course: MSCS 634 - Advanced Big Data and Data Mining

## Dataset Summary

I used the clean Online Retail dataset from Deliverable 1 (UCI Machine Learning Repository, https://archive.ics.uci.edu/dataset/352/online+retail). It has sales from a UK online gift store from December 2010 to December 2011. After cleaning, it has 522,516 sales rows. For this deliverable I only used rows with a CustomerID.

## Goal

I want to predict how much each customer will spend in the next 3 months, based on how they bought before.

- Features come from December 2010 to August 2011.
- The target is spending from September to November 2011.
- 3,313 customers bought in the first period. 43.7% of them did not buy again, so their target is 0.
- Because spending is very skewed, the target is log(1 + spend).

## Modeling Process

1. Made basic customer features: Recency, Frequency, Monetary, Products, TenureDays and IsUK.
2. Feature engineering: added recent spending and orders (last 3 months), ActiveMonths (number of months with orders), OrdersPerMonth, AvgOrderValue, TotalQuantity, CancelRate, and log versions of the skewed features.
3. Split the customers into 80% training and 20% test.
4. Picked alpha for Ridge (300) and Lasso (0.03) with 5-fold cross-validation.
5. Compared 6 models: a baseline that predicts the average, Linear Regression with raw features, Linear Regression with engineered features, Ridge, Lasso and Random Forest.
6. Evaluated each model with 5-fold cross-validation (R², RMSE) and on the test set (R², MSE, RMSE, MAE).

## Evaluation Results

Test set results (CV R² in brackets):

- Lasso: R² 0.266, RMSE 2.827 (CV R² 0.279)
- Linear (engineered): R² 0.263, RMSE 2.832 (CV R² 0.277)
- Ridge: R² 0.263, RMSE 2.833 (CV R² 0.278)
- Random Forest: R² 0.258, RMSE 2.843 (CV R² 0.266)
- Linear (raw): R² 0.206, RMSE 2.941 (CV R² 0.233)
- Baseline (mean): R² 0.000, RMSE 3.300

The best model is Lasso Regression with engineered features. It had the best R² and RMSE, and it is simple because it removed 4 features that did not add new information.

## Key Insights

- Feature engineering helped more than changing the model. R² went from 0.206 (raw features) to 0.263 (engineered features) with the same Linear Regression.
- Linear, Ridge and Lasso gave almost the same results. Random Forest did not do better, so a simple linear model is enough.
- The most important features are ActiveMonths (how many months a customer bought in) and LogMonetary (how much they spent). Customers with a long time since their last order spend less.
- The features are strongly related to each other (multicollinearity). Ridge and Lasso gave more stable coefficients than plain Linear Regression.
- Cross-validation and test results were close, and the scores did not change much between folds, so the models generalize well.
- R² is moderate (about 0.27) because 44% of customers spend 0. When I trained only on customers who came back, CV R² went up to about 0.44. This means predicting whether a customer comes back is a big part of the problem, which I will look at with classification in Deliverable 3.

## Challenges and How I Solved Them

- Data leakage: if I used all of the data to make features and also to make the target, the model would be "cheating". I split the data by time, so features only use the past and the target only uses the future.
- December 2011 only has 9 days of data, so I did not use it in the target.
- Skewed data: spending and order counts were very skewed. I used log transforms on the target and on the skewed features, which improved the results.
- Many zeros in the target: 44% of customers did not come back. I explained this with the residual plot and tested a model on returning customers only.
- Multicollinearity: many features were strongly related. I used Ridge and Lasso and scaled the features with StandardScaler.
- Choosing alpha: I tested many alpha values with cross-validation. For Lasso, alpha of 1 or more removed almost all features, so a small alpha (0.03) was best.



## Reference

Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
