# Definitions

## Contents

- [Performance measures](#performance-measures)
- [Sampling](#sampling)
- [Data preparation](#data-preparation)
- [Scikit-learn design](#scikit-learn-design)
- [Model selection and fine-tuning](#model-selection-and-fine-tuning)

## Performance measures

**RMSE (root mean squared error)** = The square root of the average squared difference between predictions and true values. It is in the same units as the target and penalizes large errors more heavily.

**MAE (mean absolute error)** = The average absolute difference between predictions and true values. It is in the same units as the target and treats all errors equally.

**R^2 score** = The proportion of the target's variance that the model explains. It is at most 1, where 1 is perfect and 0 means no better than predicting the mean. It can be negative.

## Sampling

**Stratified sampling** = Splitting data so each subgroup (stratum) appears in the test set in the same proportion as in the full dataset. Example: making sure every income category is represented proportionally in the test set.

## Data preparation

**Imputation** = Filling in missing values with an estimated value, such as the mean, median, or zero.

**Ordinal encoding** = Converting each category to an integer. It implies an order between categories, so it suits ordered categories.

**One-hot encoding** = Converting a categorical feature into one binary attribute per category. The attribute for the instance's category is 1 (hot) and all others are 0 (cold).

**Sparse matrix** = A matrix representation that stores only the nonzero values and their positions. It is efficient when most entries are zero, as with one-hot encoding.

**Min-max scaling** = Rescaling values to range from 0 to 1 by subtracting the minimum and dividing by the maximum minus the minimum.

**Standardization** = Subtracting the mean and dividing by the standard deviation, so the values have mean 0 and standard deviation 1. Unlike min-max scaling, the values are not bounded to a fixed range, and it is much less affected by outliers.

**Heavy tail** = A distribution where values far from the mean are much more common than in a normal distribution. Scaling alone squashes most values into a small range, so transform the feature first (e.g., with a logarithm) or bucketize it.

**Bucketizing** = Dividing a feature's distribution into roughly equal-sized buckets and replacing each value with the index of its bucket.

**Multimodal** = A distribution with two or more clear peaks.

## Scikit-learn scaling methods

**fit()** = Learns parameters from a dataset, such as means or category lists. Call it on the training set only, so no information from other sets leaks into preprocessing.

**transform()** = Applies the parameters learned by `fit()` to a dataset. Use it on the validation, test, and production data.

**fit_transform()** = Runs `fit()` and then `transform()` on the same data in one call. Use it on the training set.

## Scikit-learn design

**Estimator** = Any object that can estimate parameters from a dataset, using a `fit()` method.

**Transformer** = An estimator that can also transform a dataset, using a `fit_transform()` method.

**Predictor** = An estimator that can make predictions, using `predict()` and `score()` methods.

**Pipeline** = A sequence of processing steps where each step's output feeds the next.

## Model selection and fine-tuning

**K-fold cross-validation** = Splitting the training set into k subsets, then training on k - 1 of them and evaluating on the remaining one. This repeats so each subset is the evaluation fold once.

**Grid search** = Trying every combination of a set of hyperparameter values, evaluating each with cross-validation.

**Randomized search** = Trying random hyperparameter values drawn from a probability distribution specified for each hyperparameter.

**Ensemble method** = Combining several models so their joint prediction often beats the best individual model.
