[![Build Status](https://travis-ci.com/AppliedMachineLearning/homework-iii-wl2522.svg?token=iNBzZsJXgnHySWzKHvjP&branch=master)](https://travis-ci.com/AppliedMachineLearning/homework-iii-wl2522)


Step 0
------


I experimented with treating the "month", "day_of_week", and "prev_days" features as both continuous and categorical.
I decided to treat all three as continuous variables for the Logistic Regression model that I chose since it provided slightly better performance than when treaing them as categorical features.
In this step, the data is loaded and the categorical features are encoded as integers in preparation for one hot encoding.
Lastly, I create three balanced datasets using the following resampling methods:


1) Random Undersampling (rus)
2) SMOTE (sm)
3) SMOTE Edited Nearest Neighbors (enn)

	
Step 1
------
	

From the histograms of categorical features, I noticed that the "prev_days" feature was highly left-skewed, with a huge majority of the samples having a value of 999, meaning they were not previously contacted.
Also, I found that the "nr_employed", "euribor3m", and "emp_var_rate" features were highly correlated with each other, mostly likely due to the fact that all three are economic indicators.


Step 2
------


I used the following feature selection methods to help decide which features are candidates for removal:


1) Recursive Feature Selection with linear SVM
2) Recursive Feature Selection with Logistic Regression
3) SelectKBest with F-Scores
4) SelectKBest with Mutual Information
5) Stability Selection with Logistic Regression


Having performed these different feature selection methods, I decided to try dropping some features in varying combinations. In the end, I left out the "age", "job", and "housing" features due to them being deemed unimportant by almost every feature selection method. I decided to remove "nr_employed" due to its high correlation with "euribor3m" and "emp_var_rate", though I assume that removing one of the other two features instead would have a similar effect. Lastly, I dropped "cons_price_idx" and saw a less than 1% decrease in the roc_auc scores. Therefore, I decided to leave it out for the sake of having a simpler model. Removing "prev_days" seemed to cause a more significant decrease in roc_auc scores so I left it in my model. My final feature set includes the following features: 

"marital_status", "education", "credit_default", "loan", "contact", "month", "day_of_week", "campaign", "prev_days", "prev_contacts", "prev_outcomes", "emp_var_rate", "cons_conf_idx", "euribor3m"


I chose to avoid using SVM models due to the following reasons:


1) the requirement of providing probabilities for our predictions meant relying on SVC's probability parameter, which was not recommended in the lecture on linear models for classification
2) they did not exhibit significantly better performance than logistic regression models while requiring much longer to compute.


For each Logistic Regression model, I performed one hot encoding on the categorical variables, providing the number of categories that should be in each feature to account for rare categories that may be present in the training set but not in the test set. I used MaxAbsScaler() rather than StandardScaler() due to the sparsity of the encoded arrays.

Afterward, I tried using the same reduced feature set on an SGDClassifier and found that the results were slightly worse overall compared to the Logistic Regression model.


Mean roc_auc scores achieved with Logistic Regression using the reduced feature set on each balanced training set:


rus: 0.773443799587

sm : 0.847589670258

enn: 0.850619097685


roc_auc scores achieved with Logistic Regression using the reduced feature set on each balanced test set:


rus: 0.719288793103

sm : 0.771667008687

enn: 0.771292064811


Mean roc_auc scores achieved with the SGDClassifier using the reduced feature set on each balanced training set:


rus best score: 0.775891872894

sm  best score: 0.830834331782

enn best score: 0.835541548231


roc_auc scores achieved with the SGDClassifier using the reduced feature set on each balanced test set:


rus: 0.721444222657

sm : 0.756969852776

enn: 0.761043865103


Step 3
------


In this section, I tried using a single decision tree model, a random forest model, and an ExtraTreesClassifier model. I tried each model with both the full feature set and the reduced one that I used in step 2. I found that the results were either very close or the reduced feature set performed much worse. Therefore, I decided to use the full feature set for use with three models.


Mean roc_auc scores achieved with one Decision Tree on each balanced training set:


rus: 0.655539439416

sm : 0.895182311169

enn: 0.896686871576


roc_auc scores achieved with one Decision Tree on each balanced test_set:


rus: 0.916124713879

sm: 0.964969314802

enn: 0.899284923307


Mean roc_auc scores achieved with a Random Forest on each balanced training set:


rus: 0.979832158723

sm : 0.996729402728

enn: 0.999999991477


roc_auc scores achieved with a Random Forest on each balanced test_set:


rus: 0.92825020223

sm: 0.981237022125

enn: 0.945911511396


Mean roc_auc scores achieved with the ExtraTreesClassifier on each balanced training set:


rus: 0.979832158723

sm : 0.996729402728

enn: 0.999999991477


roc_auc scores achieved with the ExtraTreesClassifier on each balanced training set:


rus: 0.944855948244

sm: 0.983914240581

enn: 0.955509035091


Step 4
------


