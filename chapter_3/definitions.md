# Definitions

## Contents

- [Datasets](#datasets)
- [Classifiers](#classifiers)
- [Performance measures](#performance-measures)
- [Multiclass classification](#multiclass-classification)
- [Multilabel and multioutput classification](#multilabel-and-multioutput-classification)

## Datasets

**MNIST** = A dataset of 70,000 small images of handwritten digits, each labeled with its digit. The digits were written by high school students and US Census Bureau employees.

## Performance measures

**Confusion matrix** = A table that counts how predictions fall into true positives (TP), false positives (FP), true negatives (TN), and false negatives (FN). The other metrics in this section are computed from these four counts.

**ROC curve** = A plot of the true positive rate against the false positive rate at every threshold. Use it for binary classifiers, and prefer the precision/recall curve when the positive class is rare.

**ROC AUC** = The area under the ROC curve. It is between 0 and 1: 1 is a perfect classifier and 0.5 is a random one.

## Multiclass classification

**Multiclass classification** = Classification with more than two classes.

**One-versus-the-rest (OvR)** = A strategy that trains one binary classifier per class, each separating its class from all the others. The predicted class is the one whose classifier gives the highest score.

**One-versus-one (OvO)** = A strategy that trains one binary classifier for every pair of classes, so N classes need N x (N - 1) / 2 classifiers. Each is trained only on the instances of its two classes.

## Multilabel and multioutput classification

**Multilabel classification** = Classification where each instance can have several labels at once. Example: a photo tagged both "beach" and "sunset".

**Classifier chain** = A sequence of binary classifiers where each one also receives the predictions of the classifiers before it. In scikit-learn it is implemented as `ClassifierChain`.

**Multioutput classification** = A generalization of multilabel classification where each label can take more than two values.
