# Restaurant_Recommendation_Challenge
Predict which restaurants (in Oman) customers will most likely order from

Collaboration: Swati Kohli, Divya Raghunathan, Poonam Patil

## Overview

The objective of this project is to build a recommendation engine to predict what restaurants customers are most likely to order from given the customer location, restaurant information, and the customer order history.

This solution will allow Akeed, an app-based food delivery service in Oman, to customise restaurant recommendations for each of their customers and ensure a more positive overall user experience.

Received an F1 score of 0.0536257482092042 using KNN and SMOTE (resampling) technique 

## Data

There are ~10,000 customers in the test set. These are the customers you will need to recommend a vendor to. Each customer can order from multiple locations (LOC_NUM).

There are ~35,000 customers in the train set. Some of these customers have made orders at at least one of 100 vendors.

The objective of this competition is to build a recommendation engine to predict what restaurants customers are most likely to order from, given the customer location, the restaurant, and the customer order history.

* test_customers.csv - customer id’s in the test set.
* test_locations.csv - latitude and longitude for the different locations of each customer.
* train_locations.csv - customer id’s in the test set.
* train_customers.csv - latitude and longitude for the different locations of each customer.
* orders.csv - orders that the customers train_customers.csv from made.
* vendors.csv - vendors that customers can order from.
* VariableDefinitions.txt - Variable definitions for the datasets
* SampleSubmission.csv - is an example of what your submission file should look like. The order of the rows does not matter, but the names of CID X LOC_NUM X VENDOR must be correct. The column "target" is your prediction. The submission file is large so please allow up to 30 minutes for your score to reflect.

## Data Cleaning and Pre-processing
### Pre-processing
Since the recommendation engine requires likelihood of order from given the customer ID, customer location and Vendor ID, in the format CID X LOC_NUM X VENDOR, some data pre-processing steps are required for both testing and training data. 
For preparing test data, duplicates are dropped for test customers which are not verified. Then, test customer and location are merged and thereafter, for each row of test all rows of vendors are added. Finally id column is created using the three columns mentioned in the name of sample submission id. As a check, the number of rows in the test match the sample submission.
Same steps for training dataset are followed.
Orders table is used to make target. If ID of train is present in orders then target is 1,if not then 0.
### Cleaning

## Model Building
Multiple approaches were used at dataset level (resampling strategies and feature selection techniques) and at algorithm level ( Logistic, KNN, Random Forest, Clustering, gradient Boosting). Following two approaches gave best/similar results.

### Approach 1 KNN with SMOTE(resampling) Strategy
KNN approach is used for implementing recommendation system. However, the dataset has highly imbalanced data distribution. Supervised ML techniques such as KNN, Decision Tree, Logistic Regression have a bias towards the majority class, and tend to ignore the minority class due to which they only predict majority class. There are two approaches followed to resolve this challenge, first on data level and second on algorithm level.

1. On data level, resampling techniques were applied to get balanced distribution, like undersampling, Smote and Near-miss. Smote (synthetic minority oversampling technique) yielded better results with KNN out of all which is presented in the notebook wherein synthetic training records are generated.
2. On algorithm level, hyperparameter selection and tuning was done along with threshold adjustments.
Python Notebook presents the code for the model used.

## Model Performance
### Approach 1 KNN with SMOTE(resampling) Strategy
After running several iterations of model and resampling strategies we obtained best results with KNN using Smote resampling and cosine metric.
The best F1 score we achieved is 0.0536257482092042 (with 0.8 threshold). 

## Evaluation

The error metric for this competition is the F1 score, which ranges from 0 (total failure) to 1 (perfect score). Hence, the closer your score is to 1, the better your model.

F1 Score: A performance score that combines both precision and recall. It is a harmonic mean of these two variables. The formula is given as: 2*Precision*Recall/(Precision + Recall)

Precision: This is an indicator of the number of items correctly identified as positive out of total items identified as positive. The formula is given as: TP/(TP+FP)

Recall / Sensitivity / True Positive Rate (TPR): This is an indicator of the number of items correctly identified as positive out of total actual positives. The formula is given as: TP/(TP+FN)

Where:

* TP=True Positive
* FP=False Positive
* TN=True Negative
* FN=False Negative

Your submission file should look like:

Where 1 indicates that a customer will order from that restaurant and 0 that they will not order from that restaurant.

|CID X LOC_NUM X VENDOR |    target                    |
|-----------------------|:-----------------------------|
|A7B8IGM X 0 X 105      |      0
|NS70FA9 X 0 X 105      |      1
|WTWOE69 X 0 X 105      |      0









