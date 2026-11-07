---
title: "Commercial Bank Customer Churn Prediction"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Commercial_Bank_Customer_Churn_Prediction"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

In the business world, a 5% increase in customer retention rate means a 30% increase in company profits, and the probability of selling products to existing customers is three times that of selling to new customers. Therefore, within the analytical framework of customer lifecycle management, the churn stage—where marketing strategies are used to win back high\-value customers—is often a key indicator of an enterprise's and product's core competitiveness.

In banking and financial scenarios, banks offer a diverse range of products and customers have more options to choose from, so customer churn has always been one of the main topics of concern in the financial industry. Banks adhere to a customer\-centric approach, focusing on marketing and conversion, enhancing the customer service experience, further increasing customer loyalty, strengthening customer operations and marketing management, reducing unnecessary customer churn, promptly identifying customers at risk of leaving, and taking measures to retain customers and extend their lifecycle.

This case uses a bank customer churn prediction case and highlights the application of decision trees in real\-world scenarios. This case mines information from customers' transaction data that affects churn, thereby strengthening customer operations and marketing and reducing unnecessary customer churn.

<span id="_2-建模方法论"></span>
# 2. Modeling methodology

Regarding how to model and solve the customer churn problem, there are already many mature methods in the industry. Currently, the two main methodologies are **SEMMA methodology** and **CRISP\-DM methodology**:


* **SEMMA methodology:**  That is, Sample, Explore, Modify, Model, and Assess, emphasizing the organic cycle of these five core steps.

* **CRISP\-DM methodology:**  The full name is Cross\-Industry Standard Process for Data Mining, highlighting business understanding, data understanding, data preparation, modeling, evaluation, and deployment, and emphasizing the thorough integration of data mining objectives with business objectives.


In practical application, CRISP\-DM emphasizes the achievement of higher\-level business objectives, while SEMMA focuses more on the implementation of specific data mining techniques. Only by closely integrating the two methodologies can better results be achieved in data analysis and mining.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa2cfe6c9d6340b9b271513e3ea9430a~tplv-goo7wpa0wc-image.image" width="684px" /></div>


<span id="_3-建模过程"></span>
# 3. Modeling process

<span id="_3-1-数据描述"></span>
## 3.1 Data description

Leveraging the multi\-source data integration capability in data preparation, banking customer data can be conveniently imported into the system. Typical customer churn datasets include personal information, account information, deposit information, consumption information, and fund/wealth management information. The data dimensions include:


* **Bank proprietary fields:**  Account information, personal information, deposit information, consumption and transaction information, wealth management and fund information, counter service, online banking information

* **External third\-party data:**  Outbound customer service data, asset data, other consumption data


This case uses the classic example of credit card customer churn. The data fields are described as follows:


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|CLIENTNUM |long |User ID |User ID, unique value |
|Attrition_Flag |string |Attrition flag |Existing Customer (retained user) Attrited Customer (churned user) |
|Customer_Age |int |User age |Numeric age; generally, age is also an important factor affecting attrition |
|Gender |string |Gender |M (male) F (female) |
|Dependent_count |int |Household member statistics |Number of dependents |
|Education_Level |string |Education background |The account holder's educational qualifications (for example, high school, college graduate, and so on) |
|Marital_Status |string |Marital status |Married, single, divorced, unknown |
|Income_Category |string |Income range |Account holder's annual income category (< $$$$40K, $$$$40K \- $$$$60K, $$$$60K \- $$$$80K, $$$$80K \- $$$$120K, \> $120K) |
|Card_Category |string |Credit card category |Card type (Blue, Silver, Gold, Platinum) |
|Months_on_book |int |Holding period |Relationship period with the bank |
|Total_Relationship_Count |int |Number of products activated by the user |Number of products held by the customer |
|Months_Inactive_12_mon |int |Number of inactive months in the past 12 months |Number of inactive months in the past 12 months |
|Contacts_Count_12_mon |int |Number of contacts in the past 12 months |Number of contacts in the past 12 months |
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

The data in this case is imported using Hive, which, due to its excellent capability for handling large volumes of data, supports daily event tracking statistics for customer churn. The data results are as follows. Combined with data exploration during preparation, this further enhances understanding of the data distribution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67ce0ad1d2a144e9bea31f26eb4577f4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-数据预处理"></span>
## 3.3 Data preprocessing

<span id="_3-3-1-数据探查"></span>
### 3.3.1 Data exploration

Exploring the data source reveals that education_level contains 15% unknown categories, marital_status contains 7.4% unknown, and income_category contains 10.98%. In actual processing, such data does not help determine actual churn, so the first step in exploration is to handle the distribution of the data and the presence of dirty data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7d99c544c5b45908180eb7bb687bbc6~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-2-脏数据过滤"></span>
### 3.3.2 Dirty data filtering

Based on the results of data exploration and understanding of business data, the fields contain a large amount of dirty data labeled as Unknown. Additionally, platinum credit cards are tracked by dedicated personnel and do not require churn determination. Therefore, we can use a filtering operator to filter out data where education_level, income_category, or marital_status is Unknown, and card_category is Platinum.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4561d2f2cca14e4d877279f6c4b73e7f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-3-字符串索引"></span>
### 3.3.3 String indexing

During the data preparation and modeling process, it is necessary to index character types. Traditionally, this can be done by calculating columns, such as manually replacing Existing Customer with 0 and Attrited Customer with 1. Data preparation provides a string indexing operator, which converts all character columns into indices in one step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e75669c4c5474e68a354119cfe1c987f~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-特征处理"></span>
## 3.4 Feature processing

Feature processing here uses PCA for dimensionality reduction, mainly because high\-dimensional feature vectors often lead to the curse of dimensionality. As the dimensionality of the dataset increases, the number of samples required for algorithm learning grows exponentially. Therefore, PCA can synthesize potentially correlated high\-dimensional variables into linearly independent low\-dimensional variables, known as principal components. The low\-dimensional dataset will retain as many variables from the original data as possible, while also accelerating model convergence.

<span id="_3-5-问题建模"></span>
## 3.5 Problem modeling

To build the above training/prediction task, a decision tree is used for binary classification training on historical data. Decision trees offer advantages such as model interpretability and fast classification speed, which facilitate understanding of machine learning. The final model will be constructed as a tree structure, where each leaf node follows if\-then logic, making layer\-by\-layer judgments to ultimately arrive at a uniquely determined classification example. As shown in the figure below, the fastest determination of loan eligibility can be made after just one layer of judgment.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52c265b42f934984b820b1df8fa5ed8f~tplv-goo7wpa0wc-image.image" width="713px" /></div>


<span id="_3-6-模型评估"></span>
## 3.6 Model evaluation

Data preparation integrates multiple evaluation metrics to assist AI algorithms in parameter tuning, such as the following binary classification evaluation report.

<span id="_3-6-1-混淆矩阵"></span>
### 3.6.1 Confusion matrix

Common metrics for calculating recall/accuracy, which indicate precision, include:

<span id="_3-6-2-召回曲线"></span>
### 3.6.2 Recall curve

The P\-R chart visually displays the recall and accuracy of the learner across the overall sample. When making comparisons, if the P\-R curve of one learner is completely enveloped by that of another, it can be concluded that the latter outperforms the former.

<span id="_3-6-3-提升曲线"></span>
### 3.6.3 Lift curve

The Lift metric measures how much the predictive power of the model improves compared to not using the model. Lift = PV / k, where PV is the hit rate for positive cases, that is, the proportion of true positives among the samples predicted as positive; k is the proportion of positive cases estimated using prior probability when the model is not used. The larger the Lift, the better the model's performance.

<span id="_3-6-4-k-s-曲线"></span>
### 3.6.4 K\-S curve

The horizontal axis of the K\-S curve is the threshold, and the vertical axes are the true positive rate (sensitivity) and the false positive rate (1 \- specificity), with two line graphs plotted. The point where the two curves are farthest apart is the KS value, which corresponds to the maximum difference between the true positive rate and the false positive rate on the ROC curve.

<span id="_3-6-5-roc-曲线"></span>
### 3.6.5 ROC curve

The ROC curve is plotted based on a series of different binary classification methods (cutoff values or decision thresholds), with the true positive rate (sensitivity) as the vertical axis and the false positive rate (1 \- specificity) as the horizontal axis.

<span id="_3-7-数据生产应用"></span>
## 3.7 Data production application

After obtaining an effective model, the final results can be output to a dataset (hive/clickhouse), and subsequent visual queries or dashboard creation can be performed on the DataWind platform. It can also be used in conjunction with CDP products for label insights, marketing applications, user segmentation, and many other applications.
