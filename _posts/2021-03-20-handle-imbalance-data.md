---
layout: post
title: How to handle imbalanced dataset
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Machine Learning, Python, Tools and Libraries]
---

Many times we face problem of imbalanced classes in the dataset where some classes have majority of observations and rest have only a few observations. Class imbalance can be found in disease diagnosis like Cancer detection, fraud detection or spam filtering. In this article, we'll see few techniques which can be used to deal with imbalanced datasets. 

1. Change the evaluation matrix

If we apply wrong evaluation matrix on the imbalance dataset, it can lead to misleading results. Let us take the example of credit card fraud detection. There will be very less data points for "fraud" class(suppose 1%). So if we take "accuracy" to measure the performance of the model and our model predicts all the observations as "not fraud" then it will give 99% accuracy score. In this way, we can understand that accuracy is not the best metric in this situation. What else we can use:

	* Confusion Matrix: It tells us about the false positive, false negative, true positive and true negative. It can be used understand the number of correct and incorrect predictions. 

	* Precision: Number of true positive divided by total positives. It is also known as Specificity. It tells us how many chosen instances by the model are relevant(fraud in our example).

	* Recall: It can be calculated by dividing total number of true positives with the sum of number of true positives and the number of false negatives. It is also known as Sensitivity. It tells us how many relevant instances are chosen by the model.

	* F1-Score: Harmonic mean of precision and recall.

	* AUC-ROC: It gives us the relation between true-positive rate and false positive rate. 

2. Resample the dataset

Resample means to change the distribution of the imbalance classes in the dataset. We can either do undersampling by reducing the number of observation from the majority classes or we can do Over-sampling in which we can increase the data for minority classes. Let's see each of these types in action:

	* Undersampling: In this we'll reduce the number of observation from the majority class. Python has a library for this - `imblearn` We can understand it from this example:

	```
	from collections import Counter
    from sklearn.datasets import make_classification
    from imblearn.under_sampling import RandomUnderSampler
    X, y = make_classification(n_classes=2, random_state=42, n_features=20, n_informative=3,
    weights=[0.1, 0.9], n_redundant=1, flip_y=0, n_clusters_per_class=1, n_samples=1000, class_sep=2)
    print('Original data shape %s' % Counter(y))
    random_sampler = RandomUnderSampler(random_state=42)
    X_res, y_res = random_sampler.fit_resample(X, y)
    print('Resampled data shape %s' % Counter(y_res))
	```

	* Oversampling: In this we'll increase the number of observation for the minority class. We can understand it from this example:

	```
	from collections import Counter
    from sklearn.datasets import make_classification
    from imblearn.under_sampling import RandomOverSampler
    X, y = make_classification(n_classes=2, random_state=42, n_features=20, n_informative=3, 
    weights=[0.1, 0.9], n_redundant=1, flip_y=0, n_clusters_per_class=1, n_samples=1000, class_sep=2)
    print('Original data shape %s' % Counter(y))
    random_sampler = RandomOverSampler(random_state=42)
    X_res, y_res = random_sampler.fit_resample(X, y)
    print('Resampled data shape %s' % Counter(y_res))
	```

	NOTE: Before doing oversampling, we should split the dataset into train and test otherwise same data point can come in both train and test data and it will lead to overfitting. Our model won't be able to give proper generalized results.

	* SMOTE: There is one more technique which can be used for oversampling that is SMOTE. It stands for Synthetic Minority Over-Sampling Technique. In this technique we generate synthetic data for minority classes using nearest neighbors algorithm.

	```
	from imblearn.over_sampling import SMOTE
	target = df.Class
	train = df.drop('Class', axis=1)
	X_train_data, X_test_data, y_train, y_test = train_test_split(train, target, test_size=0.25, random_state=27)
	sm = SMOTE(random_state=27, ratio=1.0)
	X_train, y_train = sm.fit_sample(X_train_data, y_train) 
	```

3. Change the algorithm and approach to take the problem

One way is to try different algorithms and see how they perform. Generally algorithms like logistic regression or random forest tend to discard the rare classes while training. Decision tree can be used in this case as it takes care of all the classes while building if-else rules. Another way to deal with imbalance dataset is to use ensemble technique. In that we can split the majority class data into n samples and club them with rare classes to train n different models. This way we can generalize our final model.

I hope you guys must have found this article helpful. This is a good starting point to learn how to handle a imbalanced dataset. You can try these techniques to check which one works best in your case. Till then keep learning :) 
