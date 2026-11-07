---
title: "Commercial Bank Customer Churn Prediction"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Commercial_Bank_Customer_Churn_Prediction"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

In the business world, a 5% increase in customer retention rate translates to a 30% increase in company profits, and the probability of selling products to existing customers is three times that of selling to new customers. Therefore, within the analytical framework of customer lifecycle management, during the customer churn phase, using marketing strategies to win back high\-value customers is often also a key indicator of the core competitiveness of the enterprise and its products.

In banking and financial scenarios, banks offer a diverse range of products and customers have more options, so customer churn has always been a major concern in the financial industry. Banks adhere to a customer\-centric approach, focusing on marketing and conversion, enhancing the customer service experience, further increasing customer loyalty, strengthening customer operations and marketing management, reducing unnecessary customer churn, promptly identifying customers at risk of churn, and taking measures to retain customers and extend their lifecycle.

This case study focuses on predicting bank customer churn and highlights the application of decision trees in real\-world scenarios. This case extracts information from customer transaction data that affects churn, thereby strengthening customer operations and marketing and reducing unnecessary customer churn.

<span id="_2-建模方法论"></span>
# 2. Modeling methodology

To address customer churn through modeling, the industry already has many mature approaches. Currently, the two main methodologies are **SEMMA methodology** and **CRISP\-DM methodology**:


* **SEMMA methodology:**  That is, Sample, Explore, Modify, Model, and Assess, emphasizing the organic cycle of these five core stages.

* **CRISP\-DM methodology:**  The full name is Cross\-Industry Standard Process for Data Mining, highlighting business understanding, data understanding, data preparation, modeling, evaluation, and deployment, and emphasizing the full integration of data mining objectives with business objectives.


In practical application, CRISP\-DM emphasizes the achievement of higher\-level business objectives, while SEMMA focuses more on the implementation of specific data mining techniques. Only by closely integrating the two approaches can better results be achieved in data analysis and mining.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57375ade31b54f2a9cf37a0beaa20bbd~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-建模过程"></span>
# 3. Modeling process

<span id="_3-1-数据描述"></span>
## 3.1 Data description

With the multi\-source data integration capability of data preparation, bank customer data can be conveniently integrated into the system. Typical customer churn data includes customers' personal information, account information, deposit information, consumption information, and fund/wealth management information. The data dimensions include:


* **Bank proprietary fields:**  Account information, personal information, deposit information, consumption and transaction information, wealth management and fund information, counter service, and online banking information

* **External third\-party data:**  Outbound customer service data, asset data, and other consumption data


This case uses a classic example of credit card customer churn. The data fields are described as follows:


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|CLIENTNUM |long |User ID |User ID, unique value |
|Attrition_Flag |string |Attrition status |Existing Customer (retained user) Attrited Customer (churned user) |
|Customer_Age |int |User age |Numerical age; generally, age is also an important factor affecting attrition |
|Gender |string |Gender |M (male) F (female) |
|Dependent_count |int |Household member statistics |Number of dependents |
|Education_Level |string |Educational background |The account holder's educational qualifications (for example: high school, college graduate, and so on) |
|Marital_Status |string |Marital status |Married, single, divorced, unknown |
|Income_Category |string |Income range |Account holder's annual income category (< $$$$40K, $$$$40K \- 60K, $$$$60K \- $$$$80K, $$$$80K \- $$$$120K, \>$120K) |
|Card_Category |string |Credit card category |Card type (Blue, Silver, Gold, Platinum) |
|Months_on_book |int |Holding period |Relationship period with the bank |
|Total_Relationship_Count |int |Number of products activated by the user |Number of products held by the customer |
|Months_Inactive_12_mon |int |Number of inactive months in the past 12 months |Number of inactive months in the past 12 months |
|Contacts_Count_12_mon |int |Number of months with contact in the past 12 months |Number of months with contact in the past 12 months |
|Credit_Limit |int |Credit card limit |Credit card limit |
|Total_Revolving_Bal |int |Total credit card limit |Total revolving balance on credit card |
|Avg_Open_To_Buy |long |Open credit limit |Open credit limit in the past 12 months |
|Total_Amt_Chng_Q4_Q1 |float |Change in transaction amount |Change in transaction amount (Q4 compared to Q1), ratio |
|Total_Trans_Amt |long |Total transaction amount |Total transaction amount (past 12 months) |
|Total_Trans_Ct |int |Total transaction count |Total transaction count (past 12 months) |
|Total_Ct_Chng_Q4_Q1 |float |Change in transaction count |Change in transaction count (Q4 compared to Q1), ratio |
|Avg_Utilization_Ratio |float |Average card utilization rate |Average card utilization rate |


<span id="_3-2-数据准备"></span>
## 3.2 Data preparation

The data in this case is integrated using Hive, which, due to its excellent capability for handling large volumes of data, supports daily event tracking statistics for customer churn. The data results are as follows. Combined with data exploration during preparation, this further helps to understand the data distribution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c647d3f3c5494d1cba52e1a637175d03~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据预处理"></span>
## 3.3 Data preprocessing

<span id="_3-3-1-数据探查"></span>
### 3.3.1 Data exploration

Exploring the data source reveals that 15% of education_level is classified as unknown, 7.4% of marital_status is unknown, and 10.98% of income_category is unknown. In practice, such data does not help determine actual churn, so the first step in exploration is to handle the distribution of the data and the presence of dirty data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb0c5ccbb36a4dd2adf926becec6f0b0~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-2-脏数据过滤"></span>
### 3.3.2 Dirty data filtering

Based on the results of data exploration and understanding of business data, the fields contain a large amount of dirty data labeled as Unknown. In addition, platinum credit cards are tracked by dedicated personnel and do not require churn determination. Therefore, we can use a filter operator to filter out data where education_level, income_category, or marital_status is Unknown, and where card_category is Platinum.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c4a571218414823add8e07b96376749~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-字符串索引"></span>
### 3.3.3 String indexing

In the data preparation and modeling process, it is necessary to index character types. Traditionally, this can be done by computing columns, such as proactively replacing Existing Customer with 0 and Attrited Customer with 1. Data preparation provides a string indexing operator that can convert all character columns into indices in one step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4c36a00d82b495d9adf04824035841d~tplv-goo7wpa0wc-image.image) </span>

The results are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f4009d35fa640ec86cd64c53dc41a9f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ead8827a81e74ed0a57b8fd5463eb22d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-特征处理"></span>
## 3.4 Feature processing

Feature processing here uses PCA for dimensionality reduction, mainly because high\-dimensional feature vectors often lead to the curse of dimensionality. As the dimensionality of the dataset increases, the number of samples required for algorithm learning increases exponentially. Therefore, using PCA can synthesize high\-dimensional variables that may be correlated into linearly independent low\-dimensional variables, called principal components. The low\-dimensional dataset will retain as much of the original data's variability as possible, while also accelerating model convergence.

<span id="_3-5-问题建模"></span>
## 3.5 Problem modeling

To construct the above training/prediction task, a decision tree is used for binary classification training on historical data. Decision trees are advantageous because the model is interpretable and classification is fast, which facilitates understanding of machine learning. The final model will be constructed as a tree structure, where each leaf node, based on if\-then logic, is determined through successive judgments, ultimately resulting in a unique classification outcome. As shown in the figure below, the fastest path can determine loan eligibility after just one decision.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fe6635e8c074905898c71264485e52b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-6-模型评估"></span>
## 3.6 Model evaluation

Data preparation integrates multiple evaluation metrics to assist in AI algorithm parameter tuning, such as the binary classification evaluation report below.

<span id="_3-6-1-混淆矩阵"></span>
### 3.6.1 Confusion matrix

Recall and precision are common metrics for evaluating accuracy:

<span id="_3-6-2-召回曲线"></span>
### 3.6.2 Recall curve

The P\-R curve visually shows the recall and precision of the learner for the entire sample set. When making comparisons, if the P\-R curve of one learner is completely enclosed by that of another learner, then the latter's performance is superior.

<span id="_3-6-3-提升曲线"></span>
### 3.6.3 Lift curve

The Lift metric measures how much the predictive power of the model improves compared to not using the model. Lift = PV / k, where PV is the hit rate of positive cases, that is, the proportion of true positive cases among the samples predicted as positive; k is the proportion of positive cases estimated using prior probability when the model is not used. The larger the Lift, the better the model performance.

<span id="_3-6-4-k-s-曲线"></span>
### 3.6.4 K\-S curve

The horizontal axis of the K\-S curve is the threshold, and the vertical axes are the true positive rate (sensitivity) and the false positive rate (1 \- specificity), with two line charts plotted. The point where the two curves are farthest apart is the KS value, which is also the maximum value of the auc on the ROC curve.

<span id="_3-6-5-roc-曲线"></span>
### 3.6.5 ROC curve

The ROC curve is plotted based on a series of different binary classification methods (cut\-off values or decision thresholds), with the true positive rate (sensitivity) as the vertical axis and the false positive rate (1 \- specificity) as the horizontal axis.

<span id="_3-7-数据生产应用"></span>
## 3.7 Data production application

After obtaining an effective model, the final results can be exported to a dataset (hive/clickhouse), and subsequent visual queries or dashboard creation can be performed on the DataWind platform. It can also be combined with CDP products for label insights, marketing applications, user segmentation, and more.
