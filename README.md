
Step 0:

	
Step 1:
	

Step 2:

I chose to avoid using SVM models due to the following reasons:

1) the requirement of providing probabilities for our predictions meant relying on SVC's probability parameter, which was not recommended in the lecture on linear models for classification

2) they did not exhibit significantly better performance than logistic regression models while being much greater computational complexity.

However, I used LinearSVC() in conjunction with Recursive Feature Elimination to determine which features to remove.

Having performed several different feature selection methods, I decided to drop the "age" feature due to it being deemed unimportant by each method used. I also decided to remove "nr_employed" due to its high correlation with "euribor3m" and "emp_var_rate".

Results of Logistic Regression on each balanced dataset:

rus [ 0.7806246   0.80428301  0.79278257  0.78523702  0.77735366]
sm [ 0.86010997  0.86430251  0.86183789  0.86262749  0.86390429]
enn [ 0.8659233   0.86834491  0.87277584  0.87340845  0.86797257]

Results of SGDClassifier on each balanced dataset:


