---
title: "AI-Feature Engineering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/AI-Feature_Engineering"
---

<span id="4a042c3c"></span>
# Feature Overview

Feature engineering usually refers to the process of transforming the original data source into features that better express the essence of the problem, so that the application of these features to the prediction model can improve the prediction accuracy of the model on invisible data. After we have completed the data input, we can use the feature engineering operators to further process the input data, which will be described in detail below.

<span id="2dc99152"></span>
# Operator Introduction


1. **Binarization**


In data mining, the purpose of binarization is to divide quantitative features into "yes or no" to remove redundant information.


2. **Column normalization**


Normalize one or more columns of a table to scale the original data source to the required range. After the original data source is normalized, each index is in the same order of magnitude, which is suitable for comprehensive comparison and evaluation. For the time being, inplace modification is not supported. The result is a column array. If you want to split it into individual columns, you need to add a vector resolver operator after this operator. The currently supported data scaling methods are standard, min\-max, and max\-abs.


3. **Principal component analysis**


Principal Component Analysis (PCA) is one of the most widely used data dimensionality reduction algorithms. The main idea of PCA is to map n\-dimensional features to k\-dimensional features, which are brand\-new orthogonal features, also known as principal components, and reconstruct k\-dimensional features on the basis of the original n\-dimensional features. You can only operate on properties of data type with regular roles, and the output is usually an intermediate result that needs to be used as input to other operators.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Feature column: Feature column, used to train features</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter setting</strong> dimensionality reduction method: There are three options for this parameter, and the degree of dimensionality reduction in different representations is different.</div>



* <div data-tips="true" data-tips-type="tip">Selecting none means not removing any principal components, that is, if the input data contains n attributes, then the output principal component vector is n\-dimensional;</div>


* <div data-tips="true" data-tips-type="tip">Select keepV ariance, you need to set the sub\-parameter percent;</div>


* <div data-tips="true" data-tips-type="tip">Select fixedNu mber, you need to set the subparameter k.</div>


4. **Cartesian product**


The Cartesian product refers to the Cartesian product of two sets X and Y, also known as the direct product, expressed as X × Y, where the first object is a member of X and the second object is a member of all possible ordered pairs of Y.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Field Set</strong> Left and Right Operands Selected Columns</div>



5. **Discrete cosine transform**


Discrete cosine transform (DCT) transforms a time\-domain real\-valued sequence of length N into a frequency\-domain real\-valued sequence of length N.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Feature column: Feature column, used to train features</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter setting</strong> Reverse: When this parameter is true, perform a reverse cosine transform, otherwise it is a forward cosine transform</div>



6. **Row normalization**


Row normalization is a data normalization process to ensure the comparability of data metrics. After the original data source is standardized, each index is in the same order of magnitude, which is suitable for comprehensive comparison and evaluation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Feature column: Feature column, used to train features</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter setting</strong> p: p is a real number greater than 0, indicating the canonical value. After normalization, the sum of the properties of each row to the power of p is equal to 1 (in units).</div>



7. **Column normalization**


Row normalization, normalizing a column or columns of a table to scale the original data source to the required range. After the original data source is normalized, each index is in the same order of magnitude, which is suitable for comprehensive comparison and evaluation. The currently supported data scaling methods are standard, min\-max, and max\-abs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Tip</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Feature column: Feature column, used to train features</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter settings</strong> Scaling type: including standard (scaling with mean and standard deviation, data), min\-max (scaling to minimum and maximum, between values), max\-abs (scaling to \-1 and 1) three ways</div>



* <div data-tips="true" data-tips-type="tip">Use standard deviation: Whether to scale the data to a standard deviation of 1</div>


* <div data-tips="true" data-tips-type="tip">Using Average: Whether to Scale the Data to Mean 0</div>


8. **Singular value decomposition**


Singular value decomposition is a way of data dimensionality reduction, which can simplify the processing of numerical data and project the data into a low\-dimensional space by selecting a higher singular value. It can only operate on properties whose characters are regular, and the output is usually an intermediate result that needs to be used as input to other operators. As shown in the figure, an n\-dimensional matrix can be reduced to k by SVD.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> Feature column: Feature column, used to train features</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter setting</strong> dimensionality reduction method: There are three options for this parameter, and the degree of dimensionality reduction in different representations is different.</div>



* <div data-tips="true" data-tips-type="tip">Selecting none means not removing any principal components, that is, if the input data contains n attributes, then the output principal component vector is n\-dimensional;</div>


* <div data-tips="true" data-tips-type="tip">Select keepVariance, you need to set the sub\-parameter percent;</div>


* <div data-tips="true" data-tips-type="tip">Select fixedNumber, you need to set the subparameter k.</div>


9. **Feature hash**


Feature hashing is a simple dimensionality reduction method. The goal is to compress the original high\-dimensional feature vector into a lower\-dimensional feature vector without losing the expressive ability of the original feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>parameter setting</strong></div>



* <div data-tips="true" data-tips-type="tip">Filter type: Select the range of columns covered by the filter, there are 4 different ways, all means replace all, regular_ex expression means replace when the regular expression matches</div>


* <div data-tips="true" data-tips-type="tip">Reverse selection: If selected, unselected columns are preserved</div>


* <div data-tips="true" data-tips-type="tip">Number of features: Number of features</div>


10. **One\-hot encoding**


A type conversion operator that maps a column to a 0/1 vector with at most one 1 value.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Tip</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>Field settings</strong> column: select the column for conversion, multi\-select</div>



11. **Array processing, Map processing**


When there are array or map fields in the data, the data can be split and output through Array processing and Map processing operators.

Map processing and Array processing default extraction part to do onehot to accelerate, the default value is 200000, indicating that 20w rows of data are sampled by default according to the extracted data, and the 20w data is recorded and saved as a model.


12. **Feature importance**


Calculate the weight of the attribute, the weight calculation output column name Description: For a column of data type vector, the resulting weight calculation name is VectorColName__index, VectorColName is the original vector column name, and index is the position of the element in the vector, starting from zero. Calculation weight operator supports 5 weight calculation methods: 1.chi\-square, 2.correlation 3.Gini 4.information gain 5.information Gain Ratio 6.PCA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Feature columns:</strong> features used for training</div>


* <div data-tips="true" data-tips-type="tip"><strong>Label columns:</strong> basis for classification training</div>


* <div data-tips="true" data-tips-type="tip"><strong>Feature importance calculation method:</strong> currently supports chi\-square, correlation, Gini, information gain, Information Gain Ratio, PCA.</div>


13. **Feature screening**


Filtering of the weights of the calculated attributes, weight calculation output column name Description: For columns of data type vector, the resulting weight calculation name is VectorColName__index, VectorColName is the original vector column name, index is the position of the element in the vector, starting from zero. Calculation weight operator supports 5 weight calculation methods 1.chi\-square, 2.correlation 3.Gini 4.information gain 5.information Gain Ratio 6.PCA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><strong>Feature columns:</strong> features used for training</div>


* <div data-tips="true" data-tips-type="tip"><strong>Label columns:</strong> basis for classification training</div>


* <div data-tips="true" data-tips-type="tip"><strong>Feature importance calculation method:</strong> currently supports chi\-square, correlation, Gini, information gain, Information Gain Ratio, PCA.</div>


* <div data-tips="true" data-tips-type="tip"><strong>Weight relationship selection:</strong> Which weight method to filter, provide threshold, top K, top p% three filtering methods</div>


* <div data-tips="true" data-tips-type="tip"><strong>Threshold:</strong> The threshold setting for feature filtering, set here to a value of < 1, and filter columns larger than the threshold according to the result calculated by the calculation method of feature importance</div>
