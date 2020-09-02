update: 08/29/2020

# LendingClub Data Challenge
Name: Tao He

## Five Questions to be Answered:
### 1. Why did you choose the specific modeling algorithm you did
Three types of models were applied to compare their performance. They are logistic regression model, random forest model, and XGBOOST model.

Logistic regression (LR) model, who uses sigmoid function to transform the linear regression into the probablity, uses the features linear relataion with target to fit. The benifits of LR model includes its diretcly indicate the feature's weights, thus the impact of the features on the prediction.To reduce the overfitting, the L1 and L2 regularization were used. 

Random forest(RF) model, as the ensemble method of decision trees, combines the latter's advantage of less bias with its own improvement on the reduction of variance, which is the key issue of decision tree. Compared with LR model, the RF model could capture the interaction relationship between features and can skip the scaling and normalization process, which is the eseential step for LR. 

XGBOOSt model, as one type of boosting tree model, is currently popular model, which can automatically deal with missing values.

To compare those model's performance with this dataset, the cross-validation method implemented with the metrics of f1 and ROC curve of different threasholds.

The resuls of different models as shown below: (Table)

### 2. How did you handle missing data in your analysis? What are the strengths and weaknesses of your approach? What are alternate ways to handle missing data?
There are serveral ways to deal with missing data:
- imputation with constant, median, mean, mode and other descriptive statistical parameters. (simple, may not accurate)
- imputatation with inferred by other data (kmeans method as an example, may not accurate)
- remove the entries that has missing data (data bias, possible useful information lost) 

In this case, the features have missing values are dropped 

- Data sets includes those in years of 2011 and 2013. Feature dropped if the data in one feature missed all in either one of two years
- When more than 50% of missing in the feature of whole data sets

For the LR model, the missing data were imputed by 

For the RF model, missing data was handled by imputation with certain constants. For example, for the numerical data, -999.9 was used for imputation and "Missing" was applied for string type before label encoding to numerical. Because of the function of decision tree, these constants will be assigned to the same node of trees. The benifits includes: convinience and simple, and surpuringly effective for tree-like model. And probally those data missed indicates those events did not occur yet.

The missing data in XGBOOST is automatically proceed with filled with constant value.

### 3. Discuss any limitations to the data.

Better if someone in the Lending Club could explain what means for missing value in features. Some missing values may left without purpose or data logging issue, but some are not. It may indicate the event in that feature not occur yet.

Lack of time series data to monitor the change of features including FICO score, Grade by LC, Subgrade by LC, Interet Rate, Loan Payment.

Economic indicators: such as GDP growth, empolyement data and other major ecnomical indicators. Those factors could impact on borrowers' ability to pay back the money as they has higher risk being income loss, not to say even being laid off when the economy worsen.  

### 4. Discuss additional variables that weren’t present in the data but could have greatly improved your model.
- Timestemp of features: FICO score, Grade, Subgrade, Interest Rate, Loan Payment.
- Economic indicators: such as GDP growth, empolyement data and other major ecnomical indicators. T

### 5. What are the best opportunities to limit Lending Club charge-offs


### 6. How would you mesure the stability of your insights over time, if you were in charge of implementing the identified opportunities?


### 7, Which account does your model predict as most likely to charge off that did not? Why do you think this false positive occurred?