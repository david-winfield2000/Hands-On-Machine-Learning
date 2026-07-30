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
