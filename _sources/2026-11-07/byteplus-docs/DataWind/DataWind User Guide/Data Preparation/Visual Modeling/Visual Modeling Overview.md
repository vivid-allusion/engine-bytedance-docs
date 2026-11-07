---
title: "Visual Modeling Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visual_Modeling_Overview"
---

<span id="_1-产品概述"></span>
# 1. Product overview

Visual modeling is an interface\-based, drag\-and\-drop data processing and modeling feature provided by this product. This capability is commonly referred to as ETL (Extract\-Transform\-Load), and can also be called data modeling. As an intermediate step between data sources and visualization display, visual modeling enables users to efficiently process initial datasets in a drag\-and\-drop, low\-barrier, and intelligent manner before visual queries and dashboard creation. After data is cleaned, transformed, and loaded, the resulting datasets are more suitable for business analysis. Additionally, this module supports model training and algorithm prediction scenarios.

\****Visual modeling is not available in the personal and standard editions***

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9d38546464047b28521232320c01503~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-使用流程"></span>
# 2. Workflow

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d179dbd2e7845b187a023a589aba0d2~tplv-goo7wpa0wc-image.image) </span>

Create a visual modeling task \-\-\> Select a data connection \-\-\> Add data operators \-\-\> Configure operator relationships \-\-\> Configure operators \-\-\> Execute operators \-\-\> Output operators \-\-\> Set the storage method for output operators. For a complete learning course, please refer to the documentation[Volcano Engine Digital Intelligence Platform Learning Center](https://docs.byteplus.com/docs/DataWind/Volcano_Engine_Digital_Intelligence_Platform_Learning_Center).

<span id="_3-核心功能"></span>
# 3. Core functions

Visual modeling transforms the data development process into a productized, tool\-based, and visual workflow. Users only need basic data knowledge and do not require assistance with data development. Complex data processing can be accomplished in just a few drag\-and\-drop steps, making it low\-barrier and highly efficient. These capabilities are made possible by the product's core functions. The core functional modules of visual modeling include the following:

(1) **Input and output datasets**

Supports extracting data from data sources, adding data processing nodes via drag\-and\-drop, and outputting processed data to the target source. Supports output to built\-in data sources: datasets stored in Hive, ClickHouse, and ByteHouse. The overall workflow is to extract data from data sources, add data processing nodes via drag\-and\-drop, and output processed data to the target source, forming output datasets.

(2)**Data processing and cleaning**

Data cleaning typically refers to identifying and correcting recognizable errors in data files, including checking data consistency, handling invalid values, missing values, and so on. Our visual modeling supports field configuration, row filtering, adding calculated columns, aggregation, joining, merging, row and column transposition, and other operations.

(3)**AI model building**

Visual modeling encapsulates the capabilities of more than 30 common AI operators. You only need to understand the purpose of the algorithm and configure the input and training target of the algorithm operator through a configuration\-based approach to complete model training, and quickly obtain prediction results based on other configured data content.

This includes three categories: feature engineering, machine learning, and natural language processing.

Taking feature engineering as an example, here is a brief introduction: Feature engineering generally refers to the process of transforming raw data into features that better express the essence of the problem, so that applying these features to predictive models can improve the model's prediction accuracy for unseen data. After completing data input, we can use feature engineering operators to further process and refine the input data.

(4)**Task configuration and management**

Operations such as viewing, operating, running management, status statistics, and management configuration of visual modeling tasks. In the overview section of visual modeling tasks, users can view an overview of all visual modeling tasks within the project, including task status statistics and the task list. In the details section of a visual modeling task, you can view detailed configuration information for the visual modeling task, including basic information, processing flow, input and output table data preview, and run records.

<span id="_4-应用场景"></span>
# 4. Application scenarios

<span id="_4-1-所想即所得，可视化完成数据处理过程"></span>
## 4.1 What you see is what you get: visually complete the data processing workflow

To obtain the number of orders and order amounts at the granularity of date and city, and to obtain the city data for the daily top 10 consumption amounts.


|**Standard data processing workflow** |**Visual modeling workflow** |
|---|---|
|1. Obtain detailed order data from the data warehouse or BP (Business Partner), including order ID, order amount, user ID, order date, city, and more<br><br>2. Use pivot table operations to set the row fields as order date and city, and set the metrics as the sum of order amount and the count of order IDs<br><br>3. Sort the pivot results by amount, then assign serial numbers<br><br>4. Use a filter to select the Top 10 data |1. Select the data source, choose a database table, upload a CSV file, or connect to Feishu Sheet<br><br>2. Filter the required field information and configure custom field names and formats<br><br>3. Select the aggregation operator to aggregate and calculate order quantity and order amount by date and city<br><br>4. Select the Top value operator to obtain the Top 10 amounts<br><br>5. Output the dataset, which can be used in DataWind to create charts |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e8b947c60e3496eb70ec337810509c6~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-2-多表快速结合，轻松解决多数据关联计算"></span>
## 4.2 Rapid multi\-table integration for easy multi\-source data association and computation

During data processing, multiple data sources need to be combined. For example, there are two large\-volume order data tables and one customer attribute information table. The profit amount needs to be calculated based on the billing amount and cost amount, and then the Top 100 user order records are selected according to the profit contribution ranking.


|**Standard data processing workflow** |**Visual modeling workflow** |
|---|---|
|1. After opening the two order data files, copy and merge the data into one file<br><br>2. Use VLOOKUP to find user data in the orders and customers, then combine the two sets of data to generate new data<br><br>3. Use a pivot table to calculate the user's billing amount and cost amount, then calculate the profit amount<br><br>4. Sort by profit amount to obtain Top N customer information |1. You can upload CSV files or use LarkSheet to construct data input<br><br>2. Then, you can merge the March and April order data into a single dataset<br><br>3. Connect the customer attribute table and bind customer attribute information<br><br>4. Select aggregation and calculate the billing amount and cost amount for each customer<br><br>5. Select the calculation column and calculate the profit amount based on the billing amount and cost amount<br><br>6. Sort by profit amount to obtain information for the Top N customers |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/211487d418cb43e5b0c27d6a3b8fcd4e~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-ai-数据挖掘能力无代码即可配置"></span>
## 4.3 No\-code configuration of AI data mining capabilities

Visual modeling encapsulates more than 30 types of common AI operator capabilities. It is only necessary to understand the function of the algorithm and configure the input and training targets of the algorithm operator through configuration to complete model training, and quickly obtain prediction results based on other configured data content.


* **Feature engineering operators (13)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e71f200d8a4443386ee7180485412f3~tplv-goo7wpa0wc-image.image) </span>


* **Machine learning operators (22)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9302c73e45a4579962d9ec90a1c6f30~tplv-goo7wpa0wc-image.image) </span>


* **Natural language processing operators (3)** 


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f540cf8e25d4f6083937ce5da48db29~tplv-goo7wpa0wc-image.image) </span>


* **AI operator parameter configuration**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fe6ea75dd9244a088a231ec7d971050~tplv-goo7wpa0wc-image.image) </span>


* **AI model training results**


<span id="_4-4-客户意向度挖掘预测"></span>
## 4.4 Customer intent mining and prediction

For example, to mine customer intent based on existing high\-intent customer samples:

(1) Drag in sample data and all data as data inputs

(2) Drag in a classification algorithm, such as the XGB algorithm, for model training

(3) Drag in a prediction operator to establish the relationship between the model and all data for prediction

(4) Combine actual data and prediction results to output a dataset, thereby analyzing the intent distribution of all user data

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19a598706dc54c09bd6fc0084fc35fd6~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-5-回购预测模型搭建"></span>
## 4.5 Building a repurchase prediction model

In e\-commerce scenarios, it is necessary to build a user repurchase model based on existing data. During model construction, after data cleaning and format conversion, a gradient boosting tree is used to build the prediction model. At this point, the repurchase model workflow can be built using visual modeling as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d996100b589946e39fae73298e4a8f01~tplv-goo7wpa0wc-image.image) </span>

(1) Merge rows: Merge the output data tables of n operators (rectangles in the diagram) into a single consolidated data table according to consistent headers. If there are no added, deleted, or new attributes in the user sales data, no changes are needed here.

(2) Missing value replacement: When there are null values in attribute columns, it will affect subsequent model calculations. Use the missing value replacement operator to replace null values with a specified default value. If there are no additions, deletions, or new attributes in the user's sales data, no changes are needed here.

(3) One\-hot encoding: Attribute columns of text type cannot be directly used for model training and need to be one\-hot encoded into numeric vectors, for example:

This content cannot be displayed outside Feishu for now

(4) Gradient boosting tree: Responsible for fitting the training data and outputting a model that can be used for prediction (parameters not labeled in the diagram do not need to be modified by maintenance personnel):

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d2fc030cd604aea8ea6bf8db736097d~tplv-goo7wpa0wc-image.image) </span>

(5) Aggregate_1: Remove duplicates from the prediction data and select the maximum probability.

(6) Extract fields: Extract the necessary label and probability values for output.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1eb56d580d7545d781f11a0e69915065~tplv-goo7wpa0wc-image.image) </span>
