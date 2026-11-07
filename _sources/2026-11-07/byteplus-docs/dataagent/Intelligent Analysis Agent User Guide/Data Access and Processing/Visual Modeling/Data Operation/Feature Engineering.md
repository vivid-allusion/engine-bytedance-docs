---
title: "Feature Engineering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Feature_Engineering"
---

<span id="_1-概述"></span>
# 1. Overview

Feature engineering generally refers to the process of transforming raw data into features that better represent the essence of the problem, so that applying these features to predictive models can improve the model's prediction accuracy on unseen data. After completing data input, we can use feature engineering operators to further process the input data. The following text will introduce these operators in detail.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b3e7e69a34b4200b8b6957d9febfa5d~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-功能介绍"></span>
# 2. Function description

<span id="_2-1-二值化"></span>
## 2.1 Binarization

Binarization converts numerical features into binary features, 0 or 1. In the field of data mining, the purpose of binarization is to divide quantitative features into "yes or no" categories, thereby removing redundant information.

<span id="_2-2-列归一化"></span>
## 2.2 Column normalization

Column normalization processes one or more columns of a table, scaling the raw data to the required range. After data normalization, all indicators are on the same order of magnitude, making them suitable for comprehensive comparison and evaluation. In\-place modification is not currently supported. The generated result is a single array column. To split it into individual columns, a vector decomposition operator must be added after this operator. The currently supported data scaling methods are standardization (standard), min\-max scaling (min\-max), and max\-abs scaling (max\-abs).

<span id="_2-3-主成分分析法"></span>
## 2.3 Principal component analysis

Principal component analysis (PCA) is one of the most widely used data dimensionality reduction algorithms. The main idea of PCA is to map n\-dimensional features to k dimensions. These k dimensions are entirely new orthogonal features, also known as principal components, which are reconstructed from the original n\-dimensional features. Computation can only be performed on attributes that are numeric and designated as regular. The output is usually an intermediate result and needs to be used as input for other operators.

**Field settings**

Feature columns: Feature columns used for training

**Parameter settings**

Dimensionality reduction method:

This parameter has three options. Different choices represent different degrees of dimensionality reduction. Selecting none means that no principal components are removed. If the input data contains n attributes, the output principal component vector will be n\-dimensional. Selecting keepVariance requires setting the sub\-parameter percent. Selecting fixedNumber requires setting the sub\-parameter k.

<span id="_2-4-笛卡尔乘积"></span>
## 2.4 Cartesian product

The Cartesian product of two sets X and Y, also known as the direct product and denoted as X × Y, is the set of all ordered pairs where the first element is a member of X and the second element is a member of Y.

**Field settings**

Selected columns of left and right operands

<span id="_2-5-离散余弦变换"></span>
## 2.5 Discrete cosine transform

The discrete cosine transform (DCT) converts a real\-valued time\-domain sequence of length N into a real\-valued frequency\-domain sequence of length N.

**Field settings**

Feature columns: columns used for training.

**Parameter settings**

Inverse: When this parameter is true, the inverse discrete cosine transform is performed; otherwise, the discrete cosine transform is performed.

<span id="_2-6-行归一化"></span>
## 2.6 Row normalization

Row normalization is a type of data standardization processing used to address comparability between data metrics. After the original data is standardized, all metrics are at the same scale, making them suitable for comprehensive comparative evaluation.

**Field settings**

Feature columns: columns used for training.

**Parameter settings**

p: p is a real number greater than 0, representing the norm value. After normalization, the sum of the p\-th powers of each attribute in each row equals 1 (unit norm).

<span id="_2-7-奇异值分解"></span>
## 2.7 Singular value decomposition

Singular value decomposition is a method of dimensionality reduction for data. It can simplify numerical data by projecting it into a lower\-dimensional space using higher singular values. It can only operate on attributes whose role is "regular", and the output is usually an intermediate result that needs to be used as input for other operators. As shown in the figure, SVD can reduce an n\-dimensional matrix to k dimensions.

**Field settings**

Feature columns: columns used for training.

**Parameter settings**

Dimensionality reduction method: This parameter has three options, each representing a different degree of dimensionality reduction. Selecting none means that no principal components are removed. If the input data contains n attributes, the output principal component vector will be n\-dimensional. Selecting keepVariance requires setting the sub\-parameter percent. Selecting fixedNumber requires setting the sub\-parameter k.

<span id="_2-8-特征哈希"></span>
## 2.8 Feature hashing

Feature hashing is a simple dimensionality reduction method. Its goal is to compress the original high\-dimensional feature vector into a lower\-dimensional feature vector while minimizing the loss of the original feature's representation capability.

**Parameter settings**

Filter type: Select the column range to be covered by the filter. There are four different methods: all means replace all, regular_expression means replace when the regular expression matches.

Reverse selection: If selected, the columns that are not selected will be retained.

Number of features.

<span id="_2-9-one-hot编码"></span>
## 2.9 One\-hot encoding

Type conversion operator that maps a column to a 0/1 vector, where the vector contains at most one 1.

**Parameter settings**

Filter type: Select the column range to be covered by the filter. There are four different methods: all means replace all, regular_expression means replace when the regular expression matches.

Reverse selection: If selected, the columns that are not selected will be retained. Select all string\-type attributes to build an index: After enabling this parameter, there is no need to manually set the columns to be indexed. The system will automatically select all string\-type attributes to build the index. If this parameter is not enabled, you need to set the inputColumns (input columns) parameter. Click to select attributes, add the attribute names to the list of selected attributes, and click Apply to select a subset of attributes.

dropLast: Discard the last category in the encoded vector.

handle invalid: Select keep or error.

Replace original columns: Whether to replace the original columns with the newly generated columns.

Output column suffix: To distinguish from the input columns, add a suffix to the input column names to create the corresponding output column names.

Index order: Index order refers to the rule by which string indices are ordered. There are four types: frequencyDesc, frequencyAsc, alphabetDesc, and alphabetAsc. frequencyDesc and frequencyAsc indicate sorting by the frequency of occurrence of a particular string in a string\-type column, in descending and ascending order, respectively. alphabet Desc and alphabet Asc indicate sorting by encoding order in a string\-type column, in descending and ascending order, respectively.

<span id="_2-10-array处理、map处理"></span>
## 2.10 Array processing, map processing

When the data contains array or map fields, data can be split and output using the Array processing and Map processing operators.

<span id="_2-11-特征重要性"></span>
## 2.11 Feature importance

Calculate the weight of attributes. Explanation of the output column name for weight calculation: For columns with the data type vector, the generated weight calculation name is VectorColName__index, where VectorColName is the original vector column name and index is the position of the element in the vector, starting from zero. The weight calculation operator supports six weight calculation methods: 1. chi\-square, 2. correlation, 3. Gini, 4. information gain, 5. Information Gain Ratio, 6. PCA.

**Feature column:**  Features used for training

**Label column:**  Basis for classification training

**Feature importance calculation method:**  Currently supports chi\-square, correlation, Gini, information gain, Information Gain Ratio, and PCA.

<span id="_2-12-特征筛选"></span>
## 2.12 Feature selection

Selection based on attribute weights. Explanation of the output column name for weight calculation: For columns with the data type vector, the generated weight calculation name is VectorColName__index, where VectorColName is the original vector column name and index is the position of the element in the vector, starting from zero. The weight calculation operator supports six weight calculation methods: 1. chi\-square, 2. correlation, 3. Gini, 4. information gain, 5. Information Gain Ratio, 6. PCA.

**Feature column:**  Features used for training

**Label column:**  Basis for classification training

**Feature importance calculation method:**  Currently supports chi\-square, correlation, Gini, information gain, Information Gain Ratio, and PCA.

**Weight calculation method selection:**  Select which weight calculation method to use for filtering. Provides three filtering methods: threshold, top K, and top p%.

**Threshold:**  Threshold setting for feature selection. Here, the threshold is set to a value less than 1. Based on the results calculated by the feature importance method, columns with values greater than the threshold are selected.
