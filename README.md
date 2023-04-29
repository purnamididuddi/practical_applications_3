# Practical Application III: Comparing Classifiers

**Overview**: In this practical application, your goal is to compare the performance of the classifiers we encountered in this section, namely K Nearest Neighbor, Logistic Regression, Decision Trees, and Support Vector Machines.  We will utilize a dataset related to marketing bank products over the telephone.  


## Business Objective:
The dataset contains information from direct marketing campaigns of a Portuguese bank. It contains 3 types of information related to the clients:
(a) Client personal information like Age, Job, Marital status, etc
(b) Information pertaining to this client in the Current campaign
(c) Information pertaining to this client in the previous campaings

The business objective of the bank is very clear: Whether a given customer will subscribe or not, to the Term Deposit product that the bank is trying to sell.


### Excerpts of the analysis from the Jupyter notebook:
##### Many models were built in an effort to give best results to our customer (i.e., Portuguese Bank). Below is a summary of each of their performance


| <span style='background:orange'>Model | <span style='background:orange'>Train Time | <span style='background:orange'>Train Accuracy | <span style='background:orange'>Test Accuracy |
| <span style='background:orange'> Basic Logistic Regression | <span style='background:orange'>0.29 sec | <span style='background:orange'>88.73 | <span style='background:orange'>88.73 |
| <span style='background:orange'>Basic kNN | <span style='background:orange'>0.05 sec | <span style='background:orange'>89.08 | <span style='background:orange'>87.71 |
| <span style='background:orange'>Basic Decision-tree | <span style='background:orange'>0.38 sec | <span style='background:orange'>91.82 | <span style='background:orange'>86.31 |
| <span style='background:orange'> Basic SVM | <span style='background:orange'>24.9 sec | <span style='background:orange'>88.87 | <span style='background:orange'>88.69 |


I did hyper-parameter fine-tuning of the models and also have adjusted the performance metric from Accuracy to Weighted F1-score.

#### Performance Evaluation metric
For this dataset, just looking at the train/test Accuracy scores is a little mis-leading. 

For example, look at Model 1 above (Logistic regression): From it's confusion matrix, we can wee that it predicted everything as class 0 (the True-positives and False-positives are 0), yet it shows a 88.73% accuracy.

More importantly, the target classes are unevenly distributed. 

For these reasons, the correct performance metric is using F1-score. If we want to penalize hard on not predicting the positive-class correctly, one can use the macro average of the F1-score.

I'm going to use the Weighted Average of the F1-score, that gives weights proportionate to target class distribution.


##### Below is a summary of the models after hyper-parameter tuning along with the chosen best parameters
    
| <span style='background:orange'>Model | <span style='background:orange'> Parameters | <span style='background:orange'> Train Time | <span style='background:orange'> Train F1 score | <span style='background:orange'> Test F1 score |
| <span style='background:orange'> Tuned Logistic Regr | <span style='background:orange'> {'lgr__C': 1e-05, 'lgr__max_iter': 200} | <span style='background:orange'> 0.95 sec | <span style='background:orange'>83.44 | <span style='background:orange'>83.44|
| <span style='background:orange'> | Tuned kNN | <span style='background:orange'> {'knn__n_neighbors': 20} | <span style='background:orange'>69.97 sec | <span style='background:orange'>84.27 | <span style='background:orange'>83.74 |
| <span style='background:orange'>Tuned Decision tree | <span style='background:orange'>{'dt__max_depth': 10, 'dt__min_samples_split':... | 0.51 sec | <span style='background:orange'>83.44 | <span style='background:orange'>83.44 |


### Conclusion
All the tuned models are performing almost equally, while kNN has a tiny bit better F1 score. 


While all the models are doing good with target-class 'no' (a.k.a target-class = 0), only the kNN model has a non-zero F1-score for target class 'yes' (a.k.a. target-class = 1). The logistic regression and decision tree based have F1-score = 0 for target class 'yes'.

##### I would recommend using kNN based model as it is able to do some amount of justice to target-class 1.


### Next steps and recommendations
1. Fine-tune the models further especially for target-class 'yes'. 


2. The exercise asked to use only the customer's personal information as the feature-set. There are other features related to campaigns. Build more models using these other features.


3. Only 10% of the data has target-class 'yes' and the rest 90% is 'no'. Maybe, we should use the entire data for training and use the cross-validation scheme for testing, as opposed to keeping separate set for testing


4. As we will learn in later modules, build ensemble techniques based models.

### Note

#### I haven't performed Exploratory Data Analysis as the exercise already hand-picked a subset of features and asked to jump into modeling straight