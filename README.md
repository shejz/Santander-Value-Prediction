# [Santander Value Prediction Challenge](https://www.kaggle.com/c/santander-value-prediction-challenge/)
The aim of this challenge is to predict the "value of transactions for each potential customer" based on customer data provided by the Santander Bank. More specifically, the bank wants us to predict the "value of the customer's transaction" before it occurs. provided with an anonymized dataset containing numeric feature variables, the numeric `target` column, and a string `ID` column.

The evaluation metric for this competition is **Root Mean Squared Logarithmic Error**.

## EDA:

- Removal of train set’s constant columns from train and test
- Removal of train set’s duplicate columns from train and test
- A PCA analysis of the combined training and test dataset which found that approximately 3,000 features account for 95% of the dataset’s variance.


## Dataset Observations
- We do not have meaningful names for the features. So, we have to rely on other ways to analyze and understand the data.
- Features are numeric and anonymized.
- Features Sparsity.
- There are a LOT of features Almost 5,000 and they outnumber the number of rows in the training set.
- There are less than 5,000 training rows. In fact, there are fewer rows than columns, which means we'll have to invest a lot of effort into feature selection / feature engineering.
- Pandas is treating 1,845 features as float, and 3,147 as integer. It is possible that some of those int features are one-hot-encoded or label-encoded categorical variables. 


## Model

### Lagged Time-Series
- Best score: 0.59429
- Best lag value: 36

### LightGBM Time-Series

**1. Re-format the training and test sets by:**
- (A) Adding the train and test leaks as new metadata features in the train and test sets
- (B) Loading the feature-scoring results for the desired time-series reconstruction configuration and
integrating the highest-scoring features into the training and test sets.
- (C) Loading and integrating the pre-calculated row-wise metadata into the train and test sets
- (D) Reduce the training and test sets to only include the newly-added features indicated in items (A)
through (C)
- (E) Note that item (B)’s action can easily be modified to include the entire feature set rather than
features that have been pre-scored

**2. Scale the training and test sets to zero mean and unit variance with respect to the training set features.**

**3. Tune a LightGBM regressor while monitoring the training and validation root mean squared error (RMSE).**

**4. Make predictions on the test set using the trained LightGBM regressor.**


|Model|Public score|Private score|Final rank| 
|---|---|---|---|
| Lagged Time-Series  |0.56584|0.61634| 602/4477 ([Top 14%](https://www.kaggle.com/shielaj/competitions))|
| LightGBM Time-Series  |0.51276|0.55922| |
