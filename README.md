



I chose to avoid using SVM models due to the following reasons:

1) the requirement of providing probabilities for our predictions meant relying on SVC's probability parameter, which was not recommended in the lecture on linear models for classification

2) they did not exhibit significantly better performance than logistic regression models while being much greater computational complexity.

However, I used LinearSVC() in conjunction with Recursive Feature Elimination to determine which features to remove.

Having performed several different feature selection methods, I decided to drop the "age" feature due to it being deemed unimportant by each method used.