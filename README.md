# Home-Credit-Default-Risk
# Introduction
The task of this competition is about determining the clients' repayment abilities; Will they repay the loan they took out 
or will they have trouble repaying it? Due to the power of gradient boosting methods, I have used these methods, 
especially LightGBM.
The label is called TARGET, where zero indicates that there will be no problem in repaying and 1 means customer will not
be able to repay. Customer attributes are given in several tables in several files as input.
# EDA
First, I obtained different patterns of different files with Exploratory Data Analysis. First, we obtained the missing values 
of different features percentage, and then, with visualization I were able to see the distribution of several features. 
Finally, I obtained the correlation between the different variables with the TARGET.
Feature Importance
At this step, after learning the XGBoost model, I got the feature importance.
Feature Engineering
Feature engineering is required to achieve higher performance. New features are created using existing ones, as well as
in some features’ values. I need to get rid of the observations that have missing data. By dividing some of the features 
into some others, I came up with new ratios that could play an important role in classification. Some of the columns in 
the previous_application file had values of 365243, which meant missing value, so they were replaced by -1.
In other files, there is historical data about the customer, such as customer credit, customer transaction information, and 
so on. Since in these files, the primary key is not customer ID, I must reach useful information by GroupBy on the 
customers and the appropriate aggregation functions, and then join them with the data.
# Modeling
I used the LightGBM algorithm with the following parameters to create a model.
nthread=4, n_estimators=12000, learning_rate=0.02, num_leaves=31,colsample_bytree=0.85, subsample=0.9, 
max_depth=8, reg_alpha=0.0415, reg_lambda=0.073, min_split_gain=0.022, min_child_weight=39.32, silent=-1, 
verbose=-1
To have a better evaluation, I used K-Fold Cross Validation with 10 folds. Due to the imbalance data, to have training 
and validation data from both classes, the evaluation was performed by stratified cross validation method.
For the final submission, instead of predicting test data after evaluation with a single model, I used the cross-validation 
loop and I predicted test data in each iteration, and then all of them were blended. This improved the AUC.
# Experimental Result
I reached to the Public score 0.79052 and Private score 0.78741 as it shown below.
![Result in Kaggle](https://user-images.githubusercontent.com/45369296/112872613-dcf38700-90c0-11eb-8265-a011886f4e81.JPG)
