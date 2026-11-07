---
title: "Machine Learning"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Machine_Learning"
---

<span id="_1-概述"></span>
# 1. Overview

Machine learning refers to the use of machine learning operators supported by visual modeling to process and transform data, enabling users to perform model training, in\-depth analysis, predictive analysis, and more based on the data. This article introduces the functions of machine learning operators.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07d186ba63654d95a9f83ef33d1cf739~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-功能介绍"></span>
# 2. Function overview

<span id="_2-1-预测"></span>
## 2.1 Prediction

Apply the model trained by the machine learning operator to the data to be predicted. This is typically connected after the machine learning operator.

**Field settings**

Feature column mapping: Set the mapping relationship between the feature columns in the model and the feature columns in the data.

Label column: The label column, which serves as the basis for classification training.

**Parameter settings**

Prediction column name: The name of the column to be predicted.

<span id="_2-2-one-hot-模型应用"></span>
## 2.2 One\-hot model application

The one\-hot model application operator is connected after the one\-hot encoding operator. The one\-hot operator not only supports representing string\-type columns as arrays, but also supports saving the transformation process as a model. Combined with the one\-hot model application operator, similar columns can be encoded and transformed again.

**Feature column mapping:**  Set the mapping relationship between the feature columns in the model and the feature columns in the data.

<span id="_2-3-分类"></span>
## 2.3 Classification

The following models are supported. For details, refer to the function page.


|Model name |Model overview |
|---|---|
|Logistic regression |Logistic regression is a classic statistical learning classification model. It adds a nonlinear function mapping to the linear regression mapping by first computing the linear sum of the features of the sample, then using the logistic function to map the value to between 0 and 1, representing the probability that the sample belongs to each class. The class with the highest probability is selected as the final predicted class for the sample. This operator supports binary and multi\-class classification problems, and supports both continuous and categorical features. However, after string indexing of categorical features, one\-hot encoding must be applied. |
|Xgboost |Number of boosting rounds: The number of boosting iterations during training.<br><br>Use the best model: Selects the best model based on the evaluation metric chosen for optimal model selection.<br><br>Label index sorting method: 'frequency' means sorting by frequency, and 'alphabet' means sorting by string comparison. |
|Catboost |A GBDT framework based on the oblivious trees algorithm, featuring a small number of parameters, support for categorical variables, and high accuracy. It primarily addresses the challenge of efficiently and effectively handling categorical features. CatBoost is named from the combination of 'categorical' and 'boost'. It also addresses issues such as gradient bias and prediction shift, thereby improving the accuracy and generalization ability of the algorithm. CatBoost has the following five main features: 1. High model quality can be achieved without parameter tuning. Excellent results can be obtained using default parameters, reducing the time spent on tuning. 2. Supports categorical variables, with no need to preprocess non\-numeric features. 3. Fast and scalable GPU version, allowing you to train your model using a GPU\-based gradient boosting algorithm, with support for multi\-GPU parallelism. 4. Improves accuracy by introducing a new gradient boosting mechanism to build models and reduce overfitting. 5. Fast prediction, enabling rapid and efficient model deployment even for tasks with very strict latency requirements. |
|Naive Bayes |Naive Bayes is a classification method based on Bayes' theorem and the assumption of conditional independence among features. Naive Bayes classifiers are easy to construct and suitable for large datasets, but their drawback is the need to assume a prior distribution. This operator supports both binary and multiclass classification problems, and supports categorical and non\-negative continuous features. However, categorical features need to be preprocessed with string indexing. |
|Support vector machine |is a statistical learning classification model. Its basic idea is to find a separating hyperplane that can correctly classify the training dataset and maximize the geometric margin. |
|Multilayer perceptron |It simulates biological neural networks and is a type of pattern matching algorithm. Each layer consists of a linear transformation followed by a sigmoid activation function, and the output layer applies a softmax transformation. This operator supports both binary and multiclass classification problems, and supports categorical and continuous features. However, categorical features need to be preprocessed with string indexing. |
|Decision tree |is one of the commonly used classification algorithms and often performs well in exploratory knowledge discovery. The principle of decision trees is very simple. They can handle high\-dimensional data and do not require prior knowledge of the model's features. These characteristics make decision trees widely used. Decision trees use a greedy algorithm, and their construction process also requires training data. The core issues of decision trees are determining the branching criteria and the split points. |
|Random forest |In machine learning, a random forest is a classifier that contains multiple decision trees, and its output class is determined by the mode of the classes output by the individual trees. For each tree in a random forest, the training data is a subset drawn with replacement from the original training dataset. In addition, a random subset of all features is selected, and the optimal feature for splitting is chosen from this subset, rather than always selecting the globally optimal split point. This helps prevent individual decision trees from overfitting. |
|Gradient boosting tree |The gradient boosting tree is an ensemble learning model, where the internal models use decision trees. Unlike random forests, it trains only one tree at a time, and each new decision tree gradually corrects the errors made by the previous decision trees. As more trees are added, the model's expressive power becomes stronger. |


<span id="_2-4-聚类"></span>
## 2.4 Clustering

The following models are supported. For details, refer to the function page.


|Model name |Model overview |
|---|---|
|K\-means clustering |The K\-means algorithm is a typical distance\-based clustering algorithm that uses distance as the similarity evaluation metric. After specifying K initial cluster centers (initial cluster mean centers), the distance between each sample and the K cluster mean centers is calculated. Each sample is then assigned to the cluster whose mean center is closest to it. After each assignment, the cluster mean centers are updated, and the distances between all samples and the cluster mean centers are recalculated. This process repeats until all given samples are clustered into K clusters and the cluster mean centers no longer change. |
|Gaussian mixture |The Gaussian mixture clustering algorithm uses the Gaussian probability density function (normal distribution curve) to precisely quantify objects, allowing sample points to be clustered into several sets formed based on the Gaussian probability density function (normal distribution curve). In theory, it can fit any continuous function, but its drawback is a high computational cost. |
|Bisecting K\-means |The bisecting K\-means clustering algorithm is a variant of the K\-means clustering algorithm, primarily designed to address the issue of uncertainty in clustering results caused by the randomness of selecting initial centroids in the K\-means algorithm. In contrast, the bisecting K\-means algorithm is less affected by the random selection of initial centroids. |


<span id="_2-5-回归"></span>
## 2.5 Regression

The following models are supported. For details, refer to the function page.


|Model name |Model overview |
|---|---|
|Linear regression |Linear regression is a type of regression analysis that models the relationship between one or more independent variables and a dependent variable using the least squares function of the linear regression equation. As shown in the figure below, the upper part displays the basic formula, which is the linear combination of features. |
|Decision tree regression |Decision trees can be used for predicting continuous values and often perform well in exploratory knowledge discovery. The principle of decision trees is very simple; they can handle high\-dimensional data and do not require prior knowledge of the model's features. These characteristics make decision trees widely used. Decision trees use a greedy algorithm, and their construction process also requires training data. The core issues of decision trees are determining the branching criteria and the split points. |
|Random forest regression |Random forest is an ensemble model, where the internal models use decision trees and random feature selection is introduced during training. Specifically, traditional decision trees select the optimal feature for splitting from the set of features at the current node (assuming there are d features); in contrast, in random forest, for each node of the base decision tree, a subset containing k features is randomly selected from the feature set at that node, and then the optimal feature is chosen from this subset for splitting. This operator supports continuous labels, as well as continuous and categorical features. |
|Gradient Boosted Decision Tree Regression |An ensemble model in which the internal models use decision trees. Unlike random forest, it trains only one tree at a time, and each new decision tree gradually corrects the errors made by the previous decision trees. As more trees are added, the model's capacity increases. |
|Isotonic regression |Isotonic regression is a type of regression algorithm. Isotonic regression is defined as follows: Given a finite set of real numbers Y = {y_1, y_2, ..., y_n}, where Y represents known observed data, and X = {x_1, x_2, ..., x_n} represents unknown values, the goal is to find the minimum value of the function f(x) = sum_{i=1}^n w_i(y_i \- x_i)^2, while ensuring that x_1 through x_n are in increasing order. |


<span id="_2-6-时间序列"></span>
## 2.6 Time series

**ARIMA model**

Treat the data sequence formed by the prediction target over time as a random sequence, and use a mathematical model to approximate this sequence. Once this model is identified, it can predict future values based on past and present values of the time series. This can help enterprises make predictions about the future, thereby guiding their next decisions. Application scenarios: stock market trend prediction and analysis, supermarket revenue prediction and analysis, housing price trend prediction and analysis, employee turnover prediction and analysis, product sales volume prediction and analysis, weather condition prediction and analysis, and more.

<span id="_2-7-评估"></span>
## 2.7 Evaluation

The following evaluation models are supported. For details, refer to the functionality page.


|Model name |Model overview |
|---|---|
|Binary classification evaluation |This performance evaluation operator should be used for classification tasks, that is, when the label attribute has a binary value type. The input of this operator is a test sample set, which contains an attribute with the label role and an attribute with the prediction role. The operator calculates and outputs a performance vector containing performance metric values based on these two attributes. |
|Multiclass evaluation |This performance evaluation operator should be used for classification tasks, that is, when the label attribute has a categorical value type. The input of this operator is a test sample set, which contains an attribute with the label role and an attribute with the prediction role. The operator calculates and outputs a performance vector containing performance metric values based on these two attributes. |
|Clustering evaluation |This performance evaluation operator is used to evaluate the performance of clustering models. This operator expects the input to be a test sample set, which contains a column with the prediction role and a column with all features. |
|Regression evaluation |This performance evaluation operator should be used for classification tasks, that is, when the label attribute has a numeric value type. The input of this operator is a test sample set, which contains an attribute with the label role and an attribute with the prediction role. The operator calculates and outputs a performance vector containing performance metric values based on these two attributes. |
