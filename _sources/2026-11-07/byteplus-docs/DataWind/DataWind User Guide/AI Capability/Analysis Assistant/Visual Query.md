---
title: "Visual Query"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visual_Query_"
---

<span id="dcff49df"></span>
# 1. Overview

The intelligent data insight analysis assistant (hereinafter referred to as the DataWind analysis assistant, analysis assistant, or AI assistant) is a self\-service analysis intelligent assistant. During the process of self\-service data retrieval and chart creation, users may need to create a large number of charts for business scenarios. The analysis assistant can not only help users quickly generate and modify field expressions required for chart creation, but also assist users in analyzing the query results of the current chart through secondary analysis. By simply describing requirements in natural language, the analysis assistant can help users quickly complete data retrieval and chart building tasks.

<span id="_2-功能入口"></span>
# 2. Feature entry point

Secondary analysis: Click the analysis configuration area, then select secondary analysis. If a dialog box appears as shown below, it indicates that secondary analysis has been successfully enabled.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b031c43d4a7b4262aa5aca409668510b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能详解"></span>
# 3. Analysis assistant

<span id="_3-1-可视化查询字段表达式生成"></span>
## 3.1 Field expression generation

<span id="a130515c"></span>
### 3.1.1 Generate expressions

When adding a new field in visual query, for the step of defining the field expression, the analysis assistant can provide expression suggestions based on your natural language description and help you correct erroneous expressions.

**Step 1**: In the visual query editing interface, at the upper left of the field list area, click the operator to the right of the dataset name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e1115733338466c8bbe9d3d662fa3d4~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: In the field expression box, describe your requirements for generating the expression.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please describe your requirements to the AI Assistant as thoroughly as possible, so that it can provide more accurate answers.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1efafa0f5acf420d98c28371380e3bad~tplv-goo7wpa0wc-image.image) </span>

<span id="1ac707d9"></span>
### 3.1.2 Expression explanation

You can move the mouse over the generated expression, and the AI assistant will provide the logic for generating the expression. You can learn how to write the corresponding type of expression by reviewing the logic.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1371c7affd484b1696030851a0cc202e~tplv-goo7wpa0wc-image.image) </span>

<span id="dac4b6fb"></span>
### 3.1.3 Example scenarios

<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcaf4592928d40d59791b77d8771e665~tplv-goo7wpa0wc-image.image" controls></video>


<span id="_3-2-chart-generation"></span>
## 3.2 Chart generation

This feature supports generating charts based on your natural language descriptions. When generating charts, it supports using analysis features and creating expressions.

<span id="9ea0f99f"></span>
# 4. Secondary analysis

Secondary analysis allows analyzing the query results of the current chart using natural language, and supports saving the results to the dashboard.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please use the fields displayed in the chart.</div>


* <div data-tips="true" data-tips-type="warning">If a field's display name has been modified, use the field name as shown in the chart.</div>


* <div data-tips="true" data-tips-type="warning">Chart types are table, pivot table, and detail table.</div>



Click Analyze and select Secondary analysis to ask questions in the dialog box.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fe36f97f0d34aa5a3e41abb843a89d0~tplv-goo7wpa0wc-image.image) </span>

<span id="eac6ee34"></span>
## 4.1 View historical analysis

Secondary analysis supports multi\-turn dialogue. You can use the "Historical analysis steps" button on the right side of Secondary analysis to view all steps of the current round of secondary analysis. You can also click the "Apply" button after each step to revert the chart to the state at that step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d915dff57c5b4770abbcd48f14222375~tplv-goo7wpa0wc-image.image) </span>

<span id="c613e4c2"></span>
## **4.2 Secondary calculation and analysis of derived fields from analysis features**

After applying the analysis features of visual queries, additional metric fields, that is, derived fields, will be added, such as quarter\-over\-quarter growth rate, quarter\-over\-quarter original value, percentage of metrics, and more. Secondary analysis enables secondary calculations on derived fields.

<span id="b472c194"></span>
### **4.2.1 Calculations between derived fields**

(1) Add a new column for the quarter\-over\-quarter growth value of income plus cost by adding the quarter\-over\-quarter growth values of income and cost.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/311a50bfa786409e88d38a3165c8b7b3~tplv-goo7wpa0wc-image.image) </span>

(2) Add a new column for the percentage ratio by dividing the percentage of sales amount by the percentage of profit, with the data rounded to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/759802d12dd0421c83c94b2272d224c2~tplv-goo7wpa0wc-image.image) </span>

<span id="e844cc80"></span>
### **4.2.2 Calculations between derived fields and dataset fields**

Add a new column for the growth coefficient, which calculates the ratio of the month\-over\-month profit growth value to the profit.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0683736d9f824a6f8269bd6c2f86324b~tplv-goo7wpa0wc-image.image) </span>

<span id="bf21a648"></span>
### **4.2.3 Derived field filtering**

Filter data where the month\-over\-month profit growth rate is greater than 5%.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e273205366984ac88cfa33309bd15ecd~tplv-goo7wpa0wc-image.image) </span>

<span id="1aaa1f5f"></span>
## **4.3 Multi\-round aggregation operations**

Secondary analysis can achieve multi\-round aggregation based on different dimensions, such as the need for stratification by a certain metric.

(1) Add a new column: provinces with revenue greater than 900,000 are classified as high\-revenue provinces, and those with less are classified as low\-revenue provinces:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edc5818c79cd4c3bb0bfc1c850f1cea8~tplv-goo7wpa0wc-image.image) </span>

(2) Calculate the number of provinces in each revenue category and their total revenue, then remove the province column:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/005e9d2066b34ba48f7ed3d7c09b3cd1~tplv-goo7wpa0wc-image.image) </span>

<span id="38c416ae"></span>
## **4.4 Enhanced filtering capabilities**

After applying table calculation functionality, secondary analysis can filter the final results for further analysis of specific dimensions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Since secondary analysis filters based on chart results, the filtered fields must be present in the chart.</div>


<span id="7b7c1518"></span>
### **4.4.1 Dimension filtering based on final chart results**

View only the data for the Northeast region:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef0f45fea84c475997038572af833b96~tplv-goo7wpa0wc-image.image) </span>

<span id="dfd7e2ea"></span>
### 4.4.2 Filter data that meets multiple field conditions simultaneously

Filter out provinces that rank in the top three for both revenue and order quantity:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/388c1e7660fa4b93aec741b14255b179~tplv-goo7wpa0wc-image.image) </span>

<span id="e6942c70"></span>
### 4.4.3 Simultaneously filter two types of fields

Filter provinces that are both Zhejiang and sell "Road 15" type of products:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4aa7881d121b4feaaacaf10e87a7fc16~tplv-goo7wpa0wc-image.image) </span>

<span id="01443802"></span>
## **4.5 Add virtual columns to the pivot table**

Secondary analysis enables calculations between different enumerated values under the same column dimension in the pivot table.

For example: add a new column named 'Cost', which equals multiply sale_price by 0.65.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31e5da525caa429582da3e058b997cc4~tplv-goo7wpa0wc-image.image) </span>

<span id="c82905e8"></span>
## **4.6 Enhanced table calculation capabilities**

Secondary analysis supports more calculation methods for table calculations and also supports multi\-metric calculations.

<span id="4e68767b"></span>
### **4.6.1 Calculate the ratio between column fields**

Add a new column for the ratio to the most recent day's profit, calculating the ratio of profit to the most recent day's profit, rounded to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fc21084c282420daaa4b1f2395335d4~tplv-goo7wpa0wc-image.image) </span>

<span id="355a9dfa"></span>
### **4.6.2 Cross\-row calculations based on multiple metrics**

Add a new column named 'Difference between current day's revenue and previous day's cost', which uses the current date's revenue minus the previous day's cost, rounded to two decimal places.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2920c9682a104c5b9cf8d05daa64487a~tplv-goo7wpa0wc-image.image) </span>

<span id="d39bc942"></span>
### **4.6.3 Aggregate long\-tail metrics into a single row for display**

Combine provinces with revenue less than 1,000,000 into a single row named 'Other', sum the revenue column, and for the revenue summary column in this row, use the sum of the revenue column for all rows in the current result.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e13bbd8e44dd4946a6cdcf441d7b1a7e~tplv-goo7wpa0wc-image.image) </span>

<span id="55b19cc3"></span>
## **4.7 Perform row merging operations based on identical dimension enumeration values**

There is an event dataset that includes event A and event B. Event A contains id and timestamp a, and event B contains id and timestamp b.

Metric to calculate: timestamp b minus timestamp a for the same id in events A and B. To achieve this requirement, use id to match the two events and subtract the reported timestamps of the two events.

For example, merge rows with the same customer_id, keep one row in the associated result.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41e30d8a7d5b455297fedf16da57767b~tplv-goo7wpa0wc-image.image) </span>

<span id="ff234857"></span>
## 4.8 Custom rule **sorting**

When there are many dimension enumeration values in the chart, secondary analysis allows for quickly sorting the chart according to the specified order of enumeration values.

For example, place Liaoning at the top among provinces, and sort the rest in descending order by sales amount.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ec1e54fdcaf4854a7a43eb1456c3c8b~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-特别声明"></span>
# 5. Special statement

(1) All content output by this service is generated by artificial intelligence models.

(2) Applicable users for this feature: limited to customers for internal, proprietary business, and personal use only. Customers are not allowed to provide generative artificial intelligence services to the public through the Analysis Assistant.

(3) This feature is a value\-added module that supports both SaaS and on\-premises deployment versions. For purchase or trial, please contact business personnel for consultation.

(4) Currently, the AI capabilities of Intelligent Data Insight DataWind support the following types of datasets:


* Supports extracted datasets and datasets uploaded as Excel/CSV files.

* Supports direct connection datasets, currently including only: ClickHouse / ByteHouse, Doris / selectdb.
