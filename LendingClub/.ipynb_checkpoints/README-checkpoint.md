update: 08/29/2020

# LendingClub Data Challenge
Name: Tao He

## Five Questions to be Answered:
1. Why did you choose the specific modeling algorithm you did
Three types of models were applied to compare their performance. They are logistic regression model, random forest model, and XGBOOST model.

Logistic regression (LR) model, who uses sigmoid function to transform the linear regression into the probablity, uses the features linear relataion with target to fit. The benifits of LR model includes its diretcly indicate the feature's weights, thus the impact of the features on the prediction.To reduce the overfitting, the L1 and L2 regularization were used. 

Random forest(RF) model, as the ensemble method of decision trees, combines the latter's advantage of less bias with its own improvement on the reduction of variance, which is the key issue of decision tree. Compared with LR model, the RF model could capture the interaction relationship between features and can skip the scaling and normalization process, which is the eseential step for LR. 

XGBOOSt model, as one type of boosting tree model, is currently popular model, which can automatically deal with missing values.

To compare those model's performance with this dataset, the cross-validation method implemented with the metrics of 
