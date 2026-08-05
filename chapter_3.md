# Chapter 3 - classification

Regression = predicting values
Classification = predicting classes

## MNIST

MNIST dataset = 70k small images of digits handwritten by high school students + employees of the US Census Bureau, each image labeled

## Performance measures

Measure accuracy with cross-validation with `cross_val_score()`

Accuracy is generally not a good performance metric for classifiers, especially with skewed datasets

Better to use a confusion matrix (CM)

Table showing True/False Positives/Negatives for predictions

Precision = TP / (TP + FP)

- When the model predicts positive, how often is it right?

Kind of a useless metric on its own, since it's based on the predictions the classifier actually makes. If it only makes 1 guess, and it gets it right, it's 100% precise. But that's not useful unless paired with recall

Recall = TP / (TP + FN)

- Of all the actual positives, how many did the model find?

F1 score = harmonic mean of precision and recall

F1 = 2 x (precision x recall) / (precision + recall)

- Favors classifiers with similar precision and recall
- Sometimes you'll prefer higher precision, sometimes you'll prefer higher recall

### Precision/recall trade-off

Increasing precision reduces recall, and vice versa

You can't have it both ways

Can change thresholds for the decision function to affect precision/recall. As one goes up, the other goes down

How to decide on a threshold?

- `cross_val_predict()` to get scores of all instances in the training set
- `precision_recall_curve()` to compute precision and recall for all possible thresholds

Easier way to adjust decision threshold:

- `FixedThresholdClassifier` = set desired threshold manually
- `TunedThresholdClassifierCV` = uses k-fold cv to find optimal threshold for a given metric, maximizing balanced accuracy (average of recall)

### The ROC curve

ROC (receiver operating characteristic) = tool for binary classifiers, plots true positive rate against false positive rate

TPR (true positive rate)

FPR (false positive rate) = 1 - TNR

TNR (true negative rate) = specificity

ROC plots sensitivity/recall vs 1 - specificity

Tradeoff:

- Higher recall (TPR), the more false positives (FPR) the classifier produces

To compare classifiers, measure area under the curve (AUC)

- Perfect clasifier will have ROC AUC == 1
- Random classifier will have ROC AUC == 0.5

When to use ROC curve vs PR (precision/recall) curve:

- Use PR when positive class is rare or we care more about false positives than false negatives
- Otherwise, use ROC curve
