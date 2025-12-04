# Machine Learning Project - Machine Predictive Maintenance

```
contributors: MOESLE Marina, MHIBIK Nour, NAJJI-DELMAS Axelle (group 5, MMN4)
```

## Introduction
In modern industrial environments, unplanned machine downtime can lead to significant financial losses, production delays, safety risks, and diminished customer satisfaction. Predictive maintenance aims to strike a better balance. By analyzing machine data, we can forecast when a failure is likely to occur, so that maintenance can be scheduled just in time.

We will base this work on the Machine Predictive Maintenance Classification dataset from Kaggle. This dataset includes sensor readings (temperature, machine failure, etc.).


## Project objective
To build a predictive model that can forecast, as early as possible, the occurrence of a machine failure (or faults), enabling maintenance teams to intervene proactively before the failure manifests.


## Dataset

1. **Initial dataset: *predictive_maintenance.csv***

Initial source of the dataset: [AI4I 2020 Predictive Maintenance Dataset](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset)
Which has been slitghly modified in Kaggle competition (the one we took): [Machine Predictive Maintenance Classification](https://www.kaggle.com/datasets/shivamb/machine-predictive-maintenance-classification/data)

The data set contains 10,000 rows and 10 columns.
Eight of them are predictive values:
- *UID (integer):* unique identifier ranging from 1 to 10000 ;
- *Product ID (categorical):* consisting of a letter L for low (50% of all products),
M for medium (30%), and H for high (20%) as product quality variants and a variant-
specific serial number;
- *Type (categorical):* indicates the letter of Product ID;
- *Air temperature [K] (integer):* generated using a random walk process later
normalized to a standard deviation of 2 K around 300 K ;
- *Process temperature [K] (integer):* generated using a random walk process nor-
malized to a standard deviation of 1 K, added to the air temperature plus 10 K, 300+-10K ;
- *Rotational speed [rpm] (integer):* calculated from powepower of 2860 W, over-
laid with a normally distributed noise
- *Torque [Nm] (integer):* torque values are normally distributed around 40 Nm
with an Ïƒ = 10 Nm and no negative values.
- *Tool wear [min] (integer):* The quality variants H/M/L add 5/3/2 minutes of
tool wear to the used tool in the process.

There are 2 target variables:
- *Target (integer):* indicates whether there is a fail or not (1 or 0);
- *Failure Type (categorical):* indicates the type of fail : Heat Dissipation Failure,
No Failure, Overstrain Failure, Power Failure, Random Failure, Tool Wear Failure.

2. **After pre-processing: *preprocessed_predictive_maintenance.csv***

The dataset *preprocessed_predictive_maintenance.csv* stands for the version of the initial dataset after we pre-processed it. We split it into: 
- X_test.csv: 1995 rows, columns: Type, Air temperature [K], Process temperature [K], Rotational speed [rpm], Torque [Nm], Tool wear [min]
- X_train.csv: 7978 rows
- y_test.csv: 1995 rows, columns: Target, Failure Type
- y_train.csv: 7978 rows

3. **To use if a rebalancing of the dataset is necessary**

If we want to predict Target (with sensible models such as Logistic Regression, linear SVM, KNN...)
- X_train_resampled_target.csv: 15414 rows, columns: Type, Air temperature [K], Process temperature [K], Rotational speed [rpm], Torque [Nm], Tool wear [min]
- y_train_resampled_target.csv: 1544 rows, only to use "Target" column

If we want to predict Failure Type (with sensible models such as Logistic Regression multinomial, SVM One-vs-Rest or One-vs-One,...)
- X_train_resampled_failure_type.csv: 200 rows, columns: Type, Air temperature [K], Process temperature [K], Rotational speed [rpm], Torque [Nm], Tool wear [min]
- y_train_resampled_failure_type.csv: 200 rows, only to use "Failure Type" column


## Step-by-step Plan:

1. **Data analysis**

   * Exploration
   * Visualization
  
2. **Pre-processing**

   * Removing inconsistencies
   * Encoding categorical variables
   * Spliting into train and test 

3. **Overcoming obstacles before prediction**

   * Data imbalanced: Preparing different dataset and knowing in wich case / with which model they must be used
   * Preparing parameters for specific models

4. **Model training and comparison**

   * For each prediction (Target and Failure Type), same procedures:
       * Applying simple models to determine which are the best with highest Recall
       * Optimizing parameters for each with GridSearch
       * Trying multiple comparison (Bagging, Voting and Stacking classifiers) to find best prediction
  
5. **Final pipeline**
   
   * Creating final version of a model prediction that predicts Target, then if a failure is detected will predicts Failure Type, according to best outcome by using the best combination found in step 4
