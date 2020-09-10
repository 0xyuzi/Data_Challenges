update: 09/03/2020

# LendingClub Data Challenge
Name: Tao He

This challenge is to predict Lending Club's "charge-off" label by using this company's data in 2011 and 2013. To limit the "charge-off" cases, as an equivalent of "default", is to reduce the risk of losing money in this business. 

There three main steps in the analysis:
1. Data exploration and visualization
2. Feature Engineering 
3. Prediction models including Logistic Regression, Random Forest, and LightGBM


Jupyter notebooks for prediction model section:
- [LR_predict_model for Logistic Regression Classifier](LR_predict_model.ipynb)
- [RF_predict_model for Random Forest Classifier](RF_predict_model.ipynb)
- [predict_model-LightGBM for LightGBM Classifier](predict_model-LightGBM.ipynb)

Jupyter notebooks for feature engineering
- [feature_selection_eng_LR for Logistic Regression features](feature_selection_eng_LR.ipynb)
- [feature_selection_eng_RF_GBM_model for Random Forest and LightGBM features](feature_selection_eng_RF_GBM_model.ipynb)

Jupyter notebooks for data exploration and visualization
- [data_exploration_1](data_exploration_1.ipynb)
- [data_exploration_2](data_exploration_2.ipynb)
- [data_exploration_3](data_exploration_3.ipynb)


## Five Questions to be Answered:
### 1. Why did you choose the specific modeling algorithm you did
Three types of models were applied to compare their performance. They are the logistic regression model, the random forest model, and the LightGBM model. The deep neural network model is not chosen because this data is small that this model could be easily overfitted.  

The logistic regression (LR) model is selected because it could generate prediction probability, but not just "1" or "0".  The probability of "charge-off" could represent the rate of default. This rate is essential for the loan company’s risk management.  If the default rate is so high, the company may have a higher chance to lose money because more percentage of borrowers will not pay back the loan. On the other hand, if the company is very conservative to set a very low default rate. Fewer borrowers will be approved and less potential income will be generated for the company. In addition, the LR model provides each feature's coefficient which could indicate one feature's importance compared with other features. This capability could be used to explain why some borrowers being declined and others being approved without discrimination based on sex and race. Moreover, this model also could test each feature's statistics significant to filter out some features which have false high levels of the coefficient. The issue of the LR model is that feature engineering takes much more effort as the features should be scaled and normalized, or one-hot-encoded.  

Random forest (RF) model as the ensemble decision tree model to reduce the model bias. Compared with the LR model, the RF model could capture the interaction relationship between features and can skip the scaling and normalization process. It also produces the prediction probability.   

LightGBM model, as one type of gradient boosting tree model, is currently one of the most popular models. As the counterpart of the xgboost model, it has a similar power performance. LightGBM, however, applies the histogram approximation method to run faster than the histogram exact value method in xgboost. This model also generates prediction probability.

As a result, the LightGBM model has the highest score among the three models. The LR model gets the 2nd highest score, and the RF model ranks the last. 


To compare those model's performance, the ROC-AUC score is applied. Another two scores: the Gini coefficient and max diff of the Kolmogorov-Smirnov (K-S) curve are selected. They are commonly used in the credit risk industry to evaluate the model’s discriminatory power. The larger the Gini coefficient and max Kolmogorov-Smirnov, the better the models are.

The details of results of different models as shown below:


| Model         |    Roc_auc  | Gini Coef     | K-S max |
| :---          |    :----:   |         :---: |   ---:  |
| Logistic Reg  |     0.664   |    0.329      |  0.280  |
| Random Forest |     0.653   |    0.305      |  0.247  |
| LightGBM      |     0.683   |    0.365      |  0.287  |


As the results showed, LightGBM performs the best with ROC-AUC 0.683, Gini coefficient 0.365, and K-S max as 0.287. The logistic regression model ranks 2nd and Random Forest is ranked last.

Below are the performance plots

__ROC AUC__

LightGBM ROC-AUC 
![LightGBM ROC-AUC ](./figs/gbm_roc_auc.PNG)

Logistic Regression ROC-AUC
![Logistic Regression ROC-AUC ](./figs/logit_reg_roc_auc.PNG)

Random Forest ROC-AUC
![Random Forest ROC-AUC ](./figs/rf_roc_auc.PNG)

__Gini Curve__

LightGBM Gini curve
![LightGBM Gini curve ](./figs/gbm_gini.PNG)

Logistic Regression Gini curve
![Logistic Regression Gini curve ](./figs/logit_reg_gini.PNG)

Random Forest Gini curve 
![Random Forest Gini curve ](./figs/rf_gini.PNG)

__K-S Curve__

LightGBM K-S curve
![LightGBM K-S curve ](./figs/gbm_ks.PNG)

Logistic Regression Gini curve
![Logistic Regression Gini curve ](./figs/logit_reg_ks.PNG)

Random Forest Gini curve
![Random Forest Gini curve ](./figs/rf_ks.PNG)


### 2. How did you handle missing data in your analysis? What are the strengths and weaknesses of your approach? What are the alternative ways to handle missing data?
There are several ways to deal with missing data:
- imputation with constant, median, mean, mode, and other descriptive statistical parameters. (simple, may not accurate)
- imputation with inferred by other data (k-means method as an example, may not accurate)
- remove the entries that have missing data (data bias, possible useful information lost) 

The features have missing values are dropped when in conditions below, 

- Data sets include those in 2011 and 2013. Feature dropped if the data in one feature missed all in either one of two years
- When more than 50% of missing in the feature of whole data sets


For the RF model and LightGBM, missing data were handled by imputation with certain constants. For example, for the numerical data, -999.9 was used for imputation and "Missing" was applied for string type before label encoding to numerical. Because of the function of the decision tree, these constants will be assigned to the same node of trees. The benefits include convenience and simplicity, and surprisingly effective for tree-like models. And probably those data missed indicates those events did not occur yet.


For the LR model, because the features are all in the format of one-hot-encoding. So, the imputation method is to fill with constant, which is followed by that used in the RF model and LightGBM.


### 3. Discuss any limitations to the data.

Better if someone in the Lending Club could explain what means for the missing value in features. Some missing values may be left without purpose or data logging issues, but some are not. It may indicate the event in that feature has not occurred yet.

Lack of time series data to monitor the change of features including FICO score, Grade by LC, Subgrade by LC, Interest Rate, Loan Payment.

Economic indicators: such as GDP growth, employment data, and other major economic indicators. Those factors could impact borrowers' ability to pay back the money as they have a higher risk of income loss, not to say even being laid off when the economy worsens.  

### 4. Discuss additional variables that weren’t present in the data but could have greatly improved your model.
Economic indicators: such as GDP growth, employment data, and other major economic indicators. Those data and indicators would largely impact the borrower's ability to pay back the loan as they are not controllable by individuals.

### 5. What are the best opportunities to limit Lending Club charge-offs
(To be continue)

### 6. How would you measure the stability of your insights over time, if you were in charge of implementing the identified opportunities?
The model prediction over time will be challenged by the change of the underlying distribution of the data samples. For example, a series of new types of employment emerges as Youtubers, Instagram influencers. They seldom exist in the training data at an earlier time when the working prediction model was built. Another example is more and more young people apply for loans so the age distribution will be different than before. The model performance may reduce as the distribution of population changes.

The "population Stability Index (PSI)", which is a score to evaluate the difference between two data populations, could be implemented for a stability test. In a short term, if the index is <0.1, the two populations are not much change and it's relatively safe to use the working model; if the index is in the range of 0.1 and 0.25, it is better to be cautious and to monitor the model's performance carefully, even be prepared to train a new model if working model performance gets worse; if index >0.25, the working model should be immediately be discarded and the new model has to be trained as quickly as possible.


### 7, Which account does your model predict as most likely to charge off that did not? Why do you think this false positive occurred?
(To be continue)
Tentative answers:
- Order predicted results from the highest default probablity to lowest default prebablity. 
- Check the false positive results, select top 10% - 20% of them. 
- What factors lead to those false positive results? Are they on near the predicton threashold?
- Explored those samples with grouping method? KNN, Kmeans?

After selected the 50 false positive accounts with the highest predicted probility, it was found:
- Those accounts has higer average loan amount distribution compared with overall non-default accounts
- The fico scores distribution of those accounts are lower
- They has less income than the overall-defult accounts 
- They has higher loan-income ratio, which is the loan amount divided by income.

From factors resulted from logistic regression model


