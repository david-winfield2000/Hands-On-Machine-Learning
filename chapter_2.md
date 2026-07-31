# Chapter 2 - end to end machine learning project

Pretending to be a data scientist at real estate company

1. Look at big picture
2. Get the data
3. Explore and visualize the data for insights
4. Prepare data for ML algorithms
5. Select a model and train it
6. Fine-tune model
7. Present solution
8. Launch, monitor, maintain the system

## Look at the big picture

Frame the problem

Pipeline = sequence of data processing components

Select a performance measure

RMSE = root mean suqared error
MAE = mean absolute error

Check the assumptions

## Get the data

Bias can be introduced when we pick an insufficient train/test split

- Randomized sampling could skew the test set
- Stratified sampling could correct the test set

## Explore and visualize the data for insights

Useful metrics:

- Correlation coefficient with the target feature
- Various graphs for visualization
- Experimenting with attribute combinations

## Prepare the data for machine learning algorithms

Write functions to prepare the data

- Easier to reproduce transformations on any dataset
- You'll gradually build library of transformation functions that you can reuse in future projects
- Can use functions in live system to transform new data before feeding to algorithms
- Easier to try different transformations and see which combinations work the best

Clean the data

- Handle null values:
  - Remove the rows with null data
  - Remove the attribute
  - Set missing values to some value (zero, mean, median, etc.), called imputation
    - Sklearn has a classes for this: `SimpleImputer`, `KNNImputer`, `IterativeImputer`

### Scikit-learn design

Consistency: all objects share consistend and simple interface:

- Estimators: objects that can estimate some parameters based on a dataset, with `fit()` method
- Transformers: estimators that can also transform a dataset, with `fit_transform()` method
- Predictors: estimators that can make predictions, with `predict()` and `score()` methods

Inspection: all estimator's hyperparameters are accessible through public instance variables, and all learned parameters are accessible through public instance variables with underscore suffix

Nonproliferation of classes: datasets are NumPy arrays or SciPy sparse matrices. Hyperparameters are just Python strings/numbers

Composition: Existing building blocks are reused as much as possible. Can create `Pipeline` estimator from arbitrary sequence of transformers followed by final estimator

Sensible defaults: sklearn provides reasonable default values for most parameters, making it easy to quickly create baseline working system

---

Handling text and categorical features:

- Convert the categorical attributes into numbers
- Sklearn's `OrdinalEncoder` class
- One-hot encoding = one attribute == 1 (hot), others == 0 (cold)

Sparse matrix = efficient scipy representation for matrices that contain mostly zeros (stores nonzero values and positions)

Pandas `get_dummies()` = converts categorical feature into one-hot representation, one binary feature per category

- But `OneHotEncoder` is better, since it remembers categories it was trained on

### Feature scaling and transformation

To get all attributes to have the same scale, use:

- Min-max scaling/normalization = subtract min value from all values, divide by difference between min and max
  - All values shifted + rescaled so they range from 0-1, use scikit-learn `MinMaxScaler`
- Standardization = subtract mean, divide by standard deviation
  - Much less affected by outliers
  - Use scikit-learn `StandardScaler`

Heavy tail = values far from mean are not exponentially rare, scaling squashes most values into a small range

- Before scaling, transform to shrink the heavy tail
- OR bucketize the feature (chop its distribution into roughly equal-sized buckets, replace each feature value with index of the bucket it belongs to)

Multimodal = 2 or more clear peaks in the data

You can create custom transformers, and scikit-learn provides `check_estimator()` method to help you verify your custom class

### Transformation pipelines

`Pipeline` clas helps with sequences of transformations

- Contains `fit_transform()` and `predict()`

## Select and train a model

We've already:

- Explored the data
- Sampled training and test set
- Written preprocessing pipeline to clean and prepare data for ML algorithms

Select model, train on the train set, evaluate against train set

- RMSE
- MAE
- R^2 score
- Whichever error metrics are applicable

Evaluation with `train_test_split()`
Better to use k-fold cross-validation

K-fold cross-validation = split training set into k subsets, train and evaluate model k times, picking different fold for evaluation each time and training on the other folds

- Eval with `cross_val_score()`

Try out a few models that might fit the problem
The goal is to pick a short list of 2-5 promising models, then tweak the hyperparameters to increase accuracy

## Fine-tune your model

Grid search = `GridSearchCV` class that takes in hyperparameters, and values to try, and it uses cross-validation to evaluate all combinations of hyperparameter values

- After training is complete, can select the best estimator with `best_estimator_`

Randomized search = `RandomizedSearchCV` class selects a random value for each hyperparameter at every iteration

- Specify a probability distribution for each hyperparameter

Ensemble methods = combine models, which often performs better than the best individual model

Can call `best_estimator_` and `feature_importances_` to help find the most important features, and can easily drop features that aren't important

Need to evaluate model fairness too. Should work well on various points of data, not just specific categories

Evaluate on the test set to gauge the model's true performance

Compute 95% confidence interval for the generalization error with `scipy.stats.bootstrap()`

## Launch, monitor, and maintain your system

Save model with `joblib` library

Deploy to production

- Recommended to use a REST API

Deploy to the cloud

- save model with `joblib`, upload to Google Cloud Storage, Google Vertex AI to create new model version, point to GCS file

Need to set up some form of monitoring to detect if performance drops over time

Things you can automate:

- Collect fresh data regularly and label it (ex: use human raters)
- Write a script to train the model and fine-tune the hyperparameters automatically
- Write another script to evaluate the new model and previous model on the updated test set, and deploy the new model to production if performance has not decreased

Ensure input data quality doesn't degrade, try to set up alerts if quality drops

Keep backups of models, and have process + tools to roll back to previous model quickly if new model starts failing badly for some reason
