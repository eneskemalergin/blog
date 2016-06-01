---
layout: post
title: Machine Learning - Lesson 2
modified:
categories: blog
excerpt:
tags: ["Machine Learning", "Python"]
image:
  feature:
date: 2015-04-28
---

## Content of Naive Bayes
---

1. Basic intro to Concept
2. Gaussian Naive Bayes
	a. Example Usage
	b. Methods

### Basic Introduction to Concept
Naive methods are a set of supervised learning algoritms based on applying Bayes' theorem with the "naive" assumption of independence between every pair of features. Naive bayes has a lot of usage in real world situations, famously document classification and spam filtering. It requires small amount of training data to estimate the necessary parameters.

Naive Bayses learners and classifiers can be extremely fast compared to more sophisticated methods. On the other hand, although naive bayes is know as a decent classifier, it is known to be a bad estimator, so the probability outputs from predict_proba are not to be taken too seriously.

### Gaussian Naive Bayes

#### Example Usage

```Python
# Calling numpy as np
import numpy as np
# Creating a point data X, Y
X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
Y = np.array([1, 1, 1, 2, 2, 2])
# Calling sklearn.naive_bayes.GaussianNB
from sklearn.naive_bayes import GaussianNB
# Creates a classifier
clf = GaussianNB() #! This is very important
# Trains the classifier, learns the patterns, Two arguments X,Y
clf.fit(X, Y)

# Gives the prediction of given array.
print(clf.predict([[-0.8, -1]]))
```

#### Methods

- fit(X,y): fits the GaussianNB according to X and y
- get_params([deep]): Gets the parameters for this estimator
- partial_fit(X,y[, classes]):  Incremental fit on a batch of samples.
- predict(X): Performs classification on an array of test vectors X.
- predict_log_proba(X): Return log-probability estimates for the test vector X.
- predict_proba(X):  Return probabilitiy estimates for the test vector X.
- score(X,y[,sample_weight]): Returns the mean accuracy on the given test data and labels.
- set_params(**params): Set the parameters of this estimator.
