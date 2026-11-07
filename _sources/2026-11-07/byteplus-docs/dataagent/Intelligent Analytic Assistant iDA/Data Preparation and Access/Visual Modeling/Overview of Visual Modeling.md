---
title: "Overview of Visual Modeling"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Visual_Modeling_"
---

<span id="_1-产品概述"></span>
# 1. Product overview

Visual modeling is an interface\-based, drag\-and\-drop data processing and modeling feature provided by this product. This capability is commonly referred to as ETL (Extract\-Transform\-Load), and can also be called data modeling. As an intermediate step between data sources and visual presentation, visual modeling enables users to efficiently process initial datasets through drag\-and\-drop, low\-barrier, and intelligent methods. After data is cleaned, transformed, and loaded, it outputs datasets that are more conducive to business analysis. In addition, this module also supports model training and algorithm prediction scenarios.

\****Visual modeling is not available in the personal and standard editions***

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/802d68be577f4247b2a02a31355beaec~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-使用流程"></span>
# 2. Workflow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/882aed13ca214e848692c411591702ef~tplv-goo7wpa0wc-image.image) </span>

Create a visual modeling task \-\-\> Select a data connection \-\-\> Add data operators \-\-\> Configure operator connection relationships \-\-\> Configure operators \-\-\> Execute operators \-\-\> Output operators \-\-\> Set the storage method for output operators.

<span id="_3-核心功能"></span>
# 3. Core functions

Visual modeling transforms the data development process into a product, a tool, and a visual workflow. Users only need to have basic data knowledge and do not require assistance with data development. Complex data processing can be accomplished in just a few drag\-and\-drop steps, with low barriers and high efficiency. These results are achieved based on the product's core functions. The core functional modules of visual modeling include the following:

(1) **Input & output datasets**

Supports extracting data from data sources, adding data processing nodes via drag\-and\-drop, and outputting the processed data to the target source. Supports outputting to built\-in data sources: datasets stored in Hive, ClickHouse, and ByteHouse. The overall process is to extract data from data sources, add data processing nodes via drag\-and\-drop, and output the processed data to the target source, forming an output dataset.

(2)**Data processing and cleaning**

Data cleaning typically refers to identifying and correcting recognizable errors in data files, including checking data consistency and handling invalid and missing values, among others. Our visual modeling supports field configuration, row filtering, adding calculated columns, aggregation, joining, merging, row and column transposition, and more.

(3)**AI model building**

Visual modeling encapsulates more than 30 types of common AI operator capabilities. To train a model, users only need to understand the purpose of the algorithm and configure the input and training targets for the algorithm operators. Prediction results can be quickly obtained based on other configured data.

This includes three categories: feature engineering, machine learning, and natural language processing.

Taking feature engineering as an example, here is a brief introduction: Feature engineering usually refers to the process of transforming raw data into features that better express the essence of the problem, so that applying these features to prediction models can improve the model's prediction accuracy for unseen data. After completing data input, users can use feature engineering operators to further process and refine the input data.

(4)**Task configuration and management**

Users can view, operate, manage execution, track status statistics, and configure management settings for visual modeling tasks. In the visual modeling task overview section, users can view an overview of all visual modeling tasks within the project, including task status statistics and the task list. In the details section of visual modeling tasks, users can view detailed configuration information for visual modeling tasks, including basic information, processing flow, input and output table data preview, and run records.

<span id="_4-应用场景"></span>
# 4. Application scenarios

<span id="_4-1-所想即所得，可视化完成数据处理过程"></span>
## 4.1 What you see is what you get: visually complete the data processing workflow

To obtain the number of orders and order amounts by date and city granularity, and to retrieve the city data for the daily top 10 consumption amounts.


|**Standard data processing workflow** |**Visual modeling workflow** |
|---|---|
|1. Retrieve detailed order data from the data warehouse or BP, including order ID, order amount, user ID, order date, city, and more<br><br>2. Use pivot table operations to set the rows as order date and city, and set the metrics to the sum of order amount and the sum of order ID<br><br>3. Sort the pivot results by amount, then assign serial numbers<br><br>4. Use a filter to select the Top 10 data |1. Select the data source, choose a database table, upload a CSV file, or connect to LarkSheet<br><br>2. Filter the required field information, configure custom field names and formats<br><br>3. Select the aggregation operator, aggregate order quantity and order amount by date and city<br><br>4. Select the Top value operator to obtain the Top 10 amounts by value<br><br>5. Output the dataset, which can be used in DataWind to create charts |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f62b4de9592d43dab7a77aa977d27478~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-多表快速结合，轻松解决多数据关联计算"></span>
## 4.2 Rapid multi\-table integration: easily solve multi\-data association calculations

During data processing, multiple data sources need to be combined. For example, there are two large order datasets and a customer attribute information table. The profit amount is calculated based on the bill amount and cost amount, and then the order information of the Top 100 users by profit contribution is selected.


|**Standard data processing workflow** |**Visual modeling workflow** |
|---|---|
|1. After opening both order datasets, copy and merge the data into a single file<br><br>2. Use VLOOKUP to search for user data in orders and customers, then combine both datasets to generate new data<br><br>3. Use a pivot table to calculate the user's bill amount and cost amount, then calculate the profit amount<br><br>4. Sort by profit amount to obtain Top N customer information |1. Upload CSV files or use LarkSheet to build data input<br><br>2. Then merge the order data for March and April into a single dataset<br><br>3. Connect the customer information attribute table and bind customer attribute information<br><br>4. Select aggregation to calculate the billing amount and cost amount for each customer<br><br>5. Select a calculated column to compute the profit amount based on the billing amount and cost amount<br><br>6. Sort by profit amount to obtain the Top N customer information |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecd29d3a162845f0895bce2b38d05c13~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-ai-数据挖掘能力无代码即可配置"></span>
## No\-code configuration of AI data mining capabilities

Visual modeling encapsulates more than 30 types of common AI operator capabilities. You only need to understand the function of the algorithm and complete model training by configuring the input and training target of the algorithm operator. Prediction results can be quickly obtained based on other configured data content.


* **Feature engineering operators (13)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ff9b2eecf034a56bc987ca874cc49a0~tplv-goo7wpa0wc-image.image) </span>


* **Machine learning operators (22)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e495aab700a04d6ebed4221786b98786~tplv-goo7wpa0wc-image.image) </span>


* **Natural language processing operators (3)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fc50b8626e7478b8efe10c79d17bc2f~tplv-goo7wpa0wc-image.image) </span>


* **AI operator parameter configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e244825c0cf46339aa4ec55ab3d1cdc~tplv-goo7wpa0wc-image.image) </span>


* **AI model training results**


<span id="_4-4-客户意向度挖掘预测"></span>
## Customer intent mining and prediction

For example, customer intent mining can be performed based on samples of existing high\-intent customers:

(1) Drag sample data and all data as input

(2) Drag a classification algorithm, such as the XGB algorithm, for model training

(3) Drag a prediction operator to build the relationship between the model and all data for prediction

(4) Combine actual data and prediction results to output a dataset, thereby analyzing the intent distribution of all user data

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b95276fa0064b36939f1591bec4f6c3~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-5-回购预测模型搭建"></span>
## Building a repurchase prediction model

In e\-commerce scenarios, a user repurchase model needs to be built based on existing data. During model construction, after data cleaning and format conversion, a gradient boosting tree is used to build the prediction model. At this point, the repurchase model workflow can be constructed using visual modeling as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a63598c827498a8981049d912ab0e1~tplv-goo7wpa0wc-image.image) </span>

(1) Merge rows: Merge the output data tables of n operators (rectangles in the diagram) into a single consolidated data table according to consistent headers. If the user's sales data does not add, delete, or modify attributes, no changes are needed here.

(2) Missing value replacement: When there are empty values (null) in attribute columns, it will affect subsequent model calculations. Use the missing value replacement operator to substitute empty values with a specified default value. If the user's sales data does not add or remove attributes, no changes are needed here.

(3) One\-hot encoding: Attribute columns of text type cannot be used directly for model training and need to be one\-hot encoded as numerical vectors, for example:

Content cannot be displayed outside Feishu Docs at this time

(4) Gradient boosting tree: Responsible for fitting the training data and outputting a model that can be used for prediction (parameters not labeled in the diagram do not require maintenance personnel to modify):

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1344489a69084d95bfedd906652bd675~tplv-goo7wpa0wc-image.image) </span>

(5) Aggregate_1: Remove duplicates from the prediction data and select the maximum probability.

(6) Field extraction: Extract the necessary label and probability values for output.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1344489a69084d95bfedd906652bd675~tplv-goo7wpa0wc-image.image) </span>
