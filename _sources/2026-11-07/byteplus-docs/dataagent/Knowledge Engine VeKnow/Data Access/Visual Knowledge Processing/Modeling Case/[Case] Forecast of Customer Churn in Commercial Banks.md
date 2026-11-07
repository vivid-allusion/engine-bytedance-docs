---
title: "[Case] Forecast of Customer Churn in Commercial Banks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Case_Forecast_of_Customer_Churn_in_Commercial_Banks"
---

<span id="7dedffbc"></span>
## I. Overview

In the business world, a 5% increase in customer retention means a 30% increase in company profits, and the probability of selling products to old customers is three times that of selling to new customers. Therefore, under the analytical framework of customer life cycle management, in the off\-grid stage of users, the use of marketing methods to win back high\-value users is often the key to reflecting the core competitiveness of enterprises and products.

In the banking/finance scenario, the diversification of banking products, customers can choose more ways, so user churn has always been one of the most concerned topics in the financial industry. The bank adheres to the customer\-centric approach, focuses on marketing and conversion guidelines, strengthens customer group building and enhances customer\-to\-bank viscosity, strengthens customer tracking and marketing management, reduces unnecessary customer churn, promptly detects impending customer churn, prolongs customer life cycle, and takes measures to retain customers according to local conditions.

Combined with the case of bank customer churn data prediction, this case focuses on the application of decision tree in practical cases. This case mines the information on the impact of churn through customer transaction information data, thereby strengthening customer tracking and marketing and reducing unnecessary customer churn.

<span id="98ec1207"></span>
## Problem modeling

Regarding how to model and solve the problem of customer churn, there are already many mature methods in the industry. The current two main methodologies in the industry are the SEMMA methodology and the CRISP\-DM methodology. The SEMMA methodology proposed by SAS, namely Sample, Explore, Modify, Model, and Assess, emphasizes the organic cycle of these five core links. The CRISP\-DM proposed by SPSS is the English abbreviation, and its full name is Cross\-Industry Standard Process for Data Mining. It emphasizes the links of business understanding, data understanding, data preparation, modeling, evaluation, and publication, and emphasizes the full integration of data mining goals and business goals.

In practice, CRISP\-DM emphasizes the achievement of upper\-level business goals, while SEMMA focuses more on the implementation of specific data mining techniques. Only by closely linking the two methods can we achieve better results in data analytics mining.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ba68e6689ba48cebef0a2e9c8503bd0~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="947333d8"></span>
## III. Modeling process

<span id="b13a5e08"></span>
### 1. Data description

Combined with the ability of multi\-data access of data preparation, bank customer data can be easily accessed into existing data preparation services. General customer churn data includes customer personal information, account info, deposit information, consumption information, fund/financial information. Dimensions of data include:


* Bank\-owned fields: account information, personal information, deposit information, consumption, transaction information, wealth management, fund information, counter service, online banking information

* External three\-party data: outbound call customer service data, asset class data, and other consumer data


This example uses the classic credit card user churn example, the data field description is as follows:


|field name |field type |Field meaning |Field description |
|---|---|---|---|
|CLIENTNUM |long |user id |User id, unique value |
|Attrition_Flag |string |Is it lost? |Existing Customers (retained users)<br><br>Attrited Customers (lapsed users) |
|Customer_Age |int |user age |Digital age, general age can also affect important factors in attrition |
|Gender |string |Gender |M (male) F (female) |
|Dependent_count |int |Household personnel statistics |Number of dependents |
|Education_Level |string |Education situation |The account holder's educational qualifications (e.g. high school, college graduates, etc.) |
|Marital_Status |string |Marital status |Married, single, divorced, unknown |
|Income_Category |string |income range |Account holder's annual income category (< $40K, $40K \- 60K, $60K \- $80K, $80K\- $120K, \> $120K) |
|Card_Category |string |Classification of credit cards |Card Type (Blue, Silver, Gold, Platinum) |
|Months_on_book |int |hold time |Relationship period with the bank |
|Total_Relationship_Count |int |Number of products opened by users |Number of products held by customers |
|Months_Inactive_12_mon |int |The number of inactive months in the last 12 months |The number of inactive months in the last 12 months |
|Contacts_Count_12_mon |int |Number of communication months in the last 12 months |Number of communication months in the last 12 months |
|Credit_Limit |int |Credit Card Limit |Credit Card Limit |
|Total_Revolving_Bal |int |Total credit card limit |Total revolving balance on credit card |
|Avg_Open_To_Buy |long |Open credit line |Open credit lines in the past 12 months |
|Total_Amt_Chng_Q4_Q1 |float |Transaction amount change |Transaction amount change (4th quarter vs. 1st quarter), percentage |
|Total_Trans_Amt |long |total transaction value |Total transaction amount (in the past 12 months) |
|Total_Trans_Ct |int |total number of transactions |Total number of transactions (in the past 12 months) |
|Total_Ct_Chng_Q4_Q1 |float |Changes in the number of transactions |The change in the number of transactions (Q4 vs. Q1), the proportion |
|Avg_Utilization_Ratio |float |average card usage |average card usage |


<span id="b5ec3425"></span>
### 2. Data preparation

Input access, the data in this example is accessed in a hive manner. Due to its excellent processing power of large amounts of data, it can support PB\-level users churning daily event tracking data statistics. The data results are as follows. Combined with the exploration of data preparation, further understand the data distribution

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5526a285f4034ee991c27eb7339f290f~tplv-goo7wpa0wc-image.image) </span>

<span id="be0a52a8"></span>
### 3. Data preprocessing

<span id="1b10147c"></span>
#### 3.1 Data profiling

Probe the data source, found that the education_level occupies 15% of the unknown classification, marital_status unknown accounted for 7.4%, income_category accounted for 10.98%, in the actual processing, this kind of data can not help to judge the actual loss, so the first step in the exploration of the data distribution/dirty data existence first do processing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/188edfe700a74ffbb83510905595aaa1~tplv-goo7wpa0wc-image.image) </span>

<span id="5102942e"></span>
#### 3.2 Dirty data filtering

From the results of the data profiling and understanding of the business data, the field contains a lot of dirty Unknown data, and the platinum credit card is tracked by a special project, and there is no need to make a loss judgment, so we can use the filter operator to education_level, income_category, marital_status Unkown, card_category Platinum data filtering

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca7ced1e43d43c4a6e1ed79bc3a51f4~tplv-goo7wpa0wc-image.image) </span>

<span id="26fab1e0"></span>
#### 3.3 Indexing of strings

Data preparation modeling process, since most algorithms cannot support it naturally, so the character type is required for indexing processing. Traditional methods can be used to calculate columns, such as actively replacing Existing Customer with 0 and Attrited Customer with 0. Data preparation provides a string index operator, which converts all character columns into indexes in one step

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/436403ea137f47f880d32aa3dce612ab~tplv-goo7wpa0wc-image.image) </span>

The result is as follows

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2faa8c78759243f8863a0cf2e38a0bb6~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ebca83155f547939bd41af95841fc68~tplv-goo7wpa0wc-image.image) </span>

<span id="249db4d8"></span>
### 4. Feature processing

Feature processing uses PCA dimensionality reduction here, mainly because problems involving high\-dimensional feature vectors are prone to dimensional disasters. As the dimension of the dataset increases, the number of samples required for algorithm learning increases exponentially, so the use of PCA can synthesize high\-dimensional variables that may be correlated into linearly independent low\-dimensional variables, called principal components. Low\-dimensional datasets retain the variables of the original data source as much as possible, while also accelerating the convergence of the model

<span id="5ce22a8b"></span>
### 5. Problem modeling

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70e77bbda1b84eee8bb6efde728674c6~tplv-goo7wpa0wc-image.image) </span>

Construct the above training/prediction task, use decision tree for binary classification training on historical data, decision tree because the model has the advantages of readability and fast classification speed, which can facilitate the understanding of machine learning. The final model will be built into a tree\-like structure. Each leaf node is judged by layers according to the logic of if\-then, and finally to the only example of determining the classification. As shown in the figure below, the fastest one\-layer judgment can determine whether the loan can be made

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/863093c4ba0a4952a74e438702354d2f~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="e967f80b"></span>
### 6. Model evaluation

Data preparation integrates a variety of evaluation indicators to assist in the adjustment of parameters of AI algorithms, as follows

<span id="ae80f302"></span>
#### 6.1 Confusion Matrix

Calculate recall/accuracy, indicating common metrics of accuracy

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/cdf1b04c3ab743238af268ff9bdad314) </span>

<span id="624b5a52"></span>
#### 6.2 Recall curve

The P\-R plot visually shows the recall and precision of the learner on the sample population. When comparing, if the P\-R curve of one learner is completely "wrapped" by the curve of another learner, then we can assert that the performance of the latter is better than that of the former

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/90de949bf12848eebea8b6ae0aeab227) </span>

<span id="cc6ed9c9"></span>
#### 6.3 Lifting Curve

The Lift metric measures how much the model's predictive capacity enhancement is compared to not using the model. Lift = P V/k, where PV is the hit rate of positive examples, which is the proportion of true positive examples in the sample predicted to be positive; k is the proportion of positive examples estimated by prior probability without using a model. The bigger the Lift, the better the model.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/f8fa9382a49249bea7e5307aa064ae7f) </span>

<span id="b962e885"></span>
#### 6.4 K\-S Curve

The abscissa of the K\-S curve is the threshold, and the ordinate is the true positive rate (sensitivity) and false positive rate (1\-specificity), respectively. The furthest point between the two curves is the KS value, which is also the largest value of auc on the ROC curve

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/61f456578cdb4c94849e7cfa1e84c605) </span>

<span id="4edd7abb"></span>
#### 6.5 ROC Curve

The ROC curve is a curve drawn according to a series of different binary classifications (demarcation value or determination threshold), with the true positive rate (sensitivity) as the ordinate and the false positive rate (1\-specificity) as the abscissa

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/aac888aba9384212a7a3286c89add46f) </span>

<span id="3746a351"></span>
### 7. Data production applications

After obtaining an effective model, the final results can be output to a labeling system or data source (hive/clickhouse), which, combined with the CDP module, can be put into production in labeling insights/marketing applications/user clustering. It can also be applied to ABI modules to support dashboards/visualized queries for metrics.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/0bdf46376ea1470292224fd83615450f) </span>

Label results

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/7b471fb670b24b3185197a87bac70f2b) </span>
