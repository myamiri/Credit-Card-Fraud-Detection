# Fraud-Detection

# Summary

The Credit Card Fraud Detection Problem includes modeling past credit card transactions with the knowledge of the ones that turned out to be a fraud. 
This model is then used to identify whether a new transaction is fraudulent or not. 
Our aim here is to detect 100% of the fraudulent transactions while minimizing the incorrect fraud classifications.


# Problem

Very few transactions are actually fraudulent (less than 1%). The data set is highly skewed, consisting of 492 frauds in a total of 284,807 observations. This resulted in only 0.172% fraud cases. This skewed set is justified by the low number of fraudulent transactions.

Why does class imbalanced affect model performance?
1) In general, we want to maximize the recall while capping FPR (False Positive Rate), but you can classify a lot of charges wrong and still maintain a low FPR because you have a large number of true negatives.
2) This is conducive to picking a relatively low threshold, which results in the high recall but extremely low precision.


# Solution

Training a model on a balanced dataset optimizes performance on validation data.
However, the goal is to optimize performance on the imbalanced production dataset. You ultimately need to find a balance that works best in production.

One solution to this problem is: 
Use all fraudulent transactions, but subsample non-fraudulent transactions as needed to hit our target rate.


# Data

The datasets contains transactions made by credit cards in September 2013 by European cardholders. This dataset presents transactions that occurred in two days, where we have 492 frauds out of 284,807 transactions. The dataset is highly unbalanced, the positive class (frauds) account for 0.172% of all transactions.

It contains only numerical input variables which are the result of a PCA transformation. Features V1, V2, ... V28 are the principal components obtained with PCA, the only features which have not been transformed with PCA are 'Time' and 'Amount'.


# Modeling

I will implement "Random Under Sampling" which basically consists of removing data in order to have a more balanced dataset and thus avoiding our models to overfitting.

Steps:

The first thing we have to do is determine how imbalanced is our class (use "value_counts()" on the class column to determine the amount for each label)

![ana12](https://user-images.githubusercontent.com/33470542/81507828-e966c980-92cd-11ea-8574-b43549833c92.png)

Once we determine how many instances are considered fraud transactions (Fraud = "1") , we should bring the non-fraud transactions to the same amount as fraud transactions (assuming we want a 50/50 ratio), this will be equivalent to 492 cases of fraud and 492 cases of non-fraud transactions.

After implementing this technique, we have a sub-sample of our dataframe with a 50/50 ratio with regards to our classes. Then the next step we will implement is to shuffle the data to see if our models can maintain a certain accuracy everytime we run this script.


![ana 13](https://user-images.githubusercontent.com/33470542/81507837-026f7a80-92ce-11ea-9101-05a4d35b7ce5.png)


# Result

1) Never test on the oversampled or undersampled dataset.
2) If we want to implement cross validation, remember to oversample or undersample your training data during cross-validation, not before!

 Result of undersampling before cross-validation :

![ana10](https://user-images.githubusercontent.com/33470542/81507545-39dd2780-92cc-11ea-9c6f-bbdb9c1985f0.png)


 Result of undersampling during cross-validation :

![ana11](https://user-images.githubusercontent.com/33470542/81507947-b4a74200-92ce-11ea-9124-ebba94fff0a3.png)



3) Don't use accuracy score as a metric with imbalanced datasets (will be usually high and misleading), instead use f1-score, precision/recall score or confusion matrix





