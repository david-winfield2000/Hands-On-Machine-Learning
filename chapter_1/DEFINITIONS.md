# Definitions

## Contents

- [Machine Learning](#machine-learning)
- [Data Sets](#data-sets)
- [Training Supervision](#training-supervision)
- [Batch vs Online Learning](#batch-vs-online-learning)
- [Generalization and Learning Approaches](#generalization-and-learning-approaches)

## Machine Learning

**Machine learning** = A field of computer science in which a program learns patterns from data instead of following rules written by hand. The learned pattern is then used to make predictions or decisions on new data.

**Hyperparameter** = A setting chosen before training that controls how the learning process works, such as the learning rate or the amount of regularization, rather than a value the model learns from the data. Good values are usually found by comparing models on a validation set.

## Data Sets

**Training set** = The data a model learns from.

**Validation set** = Data held back from training and used to compare models and tune hyperparameters.

**Test set** = Data held back until the end and used once to estimate how well the final model performs on new cases.

**Cross-validation** = Evaluating a model on several different validation sets, each time training on the rest of the data, and averaging the results for a more reliable measure of performance. It costs more training time, since the model is trained once per validation set.

## Training Supervision

**Supervised learning** = Learning from a training set where every example is labeled with the correct answer. Example: a spam filter trained on emails already marked as spam or not spam.

**Unsupervised learning** = Learning from a training set with no labels, so the program must find structure in the data on its own.

**Semi-supervised learning** = Learning from a training set where only some examples are labeled.

**Self-supervised learning** = Creating labels automatically from unlabeled data, then training as if the data were supervised. Example: predicting a masked word in a sentence, where the hidden word serves as the label.

**Reinforcement learning** = Learning by an agent that acts in an environment and receives rewards or penalties, gradually learning which actions earn the most reward over time.

## Batch vs Online Learning

**Batch learning** = Training a model from scratch on the full dataset at once. Adding new data means retraining on everything, which takes longer as the dataset grows.

**Online learning** = Training a model incrementally in small batches of data as it arrives. A learning rate controls how strongly new data changes the model compared with older data.

## Generalization and Learning Approaches

**Generalization** = How well a model makes correct predictions on new, unseen instances of data rather than only on its training data.

**Overfitting** = When a model is too complex for the amount or noisiness of its training data, so it learns random patterns and generalizes poorly.

**Underfitting** = When a model is too simple to capture the underlying structure of the data, so it performs poorly even on the training data.

**Instance-based learning** = Learning by storing the training examples and predicting new cases by comparing them to stored examples with a similarity measure. Good for small datasets, but slow and poorly suited to high-dimensional data like images.

**Model-based learning** = Learning by building a model from the training examples and using that model, rather than the examples themselves, to make predictions.

**No free lunch theorem** = Without any assumptions about the data, no model is better than any other on average, so useful models depend on reasonable assumptions about the problem.
