# Chapter 1 - the machine learning landscape

Machine learning = science (and art) of programming computers to learn from data

## Best uses for ML models

Data mining = digging into data to discover hidden patterns

- Problems where existing solutions require lots of work
- Complex problems where traditional approaches don't provide any good solutions
- Fluctuating environments
- Gaining insights on complex problems and large datasets

## Types of machine learning systems

### Training supervision

- Supervised = training set is labeled
- Unsupervised = training set is unlabeled
- Semi-supervised = training set is partially labeled
- Self-supervised = generating a fully labeled training set from a fully unlabeled one
- Reinforcement = an agent observes and interacts with environment, and using rewards/penalties, learns which policies earn the highest reward over time

### Batch vs online learning

Batch learning = can only be trained from scratch on the full dataset

- More susceptible to data drift/model decay
- Takes longer to train as the dataset expands

Online learning = can be trained in multiple batches

- Can set learning rate to determine how reactive the model is to new data points vs forgetting older ones
- Susceptible to performance drops if fed bad data over a period of time, difficult to resolve

### Instance-based vs model-based learning

Generalization = making predictions on unseen instances of data

Instance-based

- Learns examples, generalizes to new cases using a similarity measure
- Pros: good for small datasets
- Cons: requires deploying whole copy of training set to production, slow search, doesn't work with high dimensional data like images

Model-based

- Build a model of examples, use that model to make predictions

Utility function = measure how good model is
Cost function = measure how bad model is

## Main challenges of machine learning

Bad data:

- Insufficient quantity of training data
- Nonrepresentative training data
- Poor-quality data
- Irrelevant features

Feature engineering = defining a good set of features to train on

- Feature selection = selecting most useful features
- Feature extraction = combining existing features to create a more useful one, like with dimensionality reduction
- Creating new features by gathering new data

Bad algorithms:

- Overfitting the training data

Overfitting happens when model is too complex relative to the amount + noisiness of the training data, so it learns random patterns. Possible solutions:

- Simplify model by picking one with fewer parameters, reducing number of attributes in training data, or constraining the model
- Gather more training data
- Reduce the noise in the training data (fix data errors, remove outliers)

Regularization = constraining model to make it simpler + reduce overfitting risk

Hyperparameter = parameter of learning algorithm

- Controls amount of regularization to apply during learning

Underfitting = model is too simple to learn the underlying structure of the data. Possible solutions:

- Pick more powerful model with more parameters
- Feed better features to the learning algorithm (feature engineering)
- Reduce constraints on the model (ex: reducing regularization hyperparameter)

## Testing and validating

Training set = data you train model with
Test set = data you test model with
Generalization error = error rate on new cases

Hyperparameter tuning and model selection

Holdout validation = multiple sets of data with retraining

1. Train on training set
2. Evaluate against dev set, retrain
3. Evaluate final model against test set

Cross-validation = using many validation sets

- Each model evaluated once per validation set, after being trained on the rest of the data
- By averaging out all evaluations of a model, you get a more accurate measure of its performance
- Cons: training timme multiplied by number of validation sets

Data mismatch

No free lunch theorem = if you make no assumption about the data, then there's no reason to prefer one model over any other

- The only way to know for sure which model is best is to evaluate them all
- Not possible to evaluate all, so you have to make some reasonable assumptions about the data + evaluate only a few reasonable models
