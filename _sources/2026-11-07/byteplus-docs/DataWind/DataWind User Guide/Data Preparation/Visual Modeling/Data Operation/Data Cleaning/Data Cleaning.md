---
title: "Data Cleaning"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Cleansing"
---

<span id="_1-概述"></span>
# 1. Overview

Data cleansing typically refers to identifying and correcting recognizable errors in data files, including checking data consistency, handling invalid values and missing values, among others. After the user completes data entry, further data cleansing operations can be performed on the input data. This article will introduce the functions of the data cleansing operator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccd2023fa5cd42fe8fb17f08ce8cd62c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Function overview

<span id="_2-1-字段设置"></span>
## 2.1 Field settings

Field settings support selecting fields to retain, setting field types, setting field names, and setting field order.

Advanced configuration features are also provided, supporting one\-click modification of target field name formats, such as one\-click conversion to uppercase, one\-click conversion to lowercase, one\-click repair of illegal characters, one\-click correction of non\-standard data, and quick field sorting to improve data processing efficiency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58e670e7b0464bed8d030efe2a21c052~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-连接"></span>
## 2.2 Join

Supports creating join relationships between multiple tables.


* Select join method

* Set join fields

* Select fields to retain


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22a831f6e180448b9f316bd733ee808a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-合并行"></span>
## 2.3 Merge rows

Used to merge data from multiple tables.

**Operation panel**

Click to configure the matching relationships of fields across multiple tables. Note that only fields with the same format can be matched. If the field formats are different, add field settings or calculation column operators to process the field formats before merging.

**Processing example**

Drag different tables onto the canvas, click one of the tables to be merged, and add a merge rows node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab87b64e90e0452f93240b41db673373~tplv-goo7wpa0wc-image.image) </span>

Click the + button on the right side of other tables to be merged, and drag it to the left side of the merge rows operator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd88f3fcaadb4cbc8108146a00d08238~tplv-goo7wpa0wc-image.image) </span>

Configure the matching relationships at the bottom of the page, then click Execute to save the configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56ac6320aa194cb99be1f25b636f58f1~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-聚合"></span>
## 2.4 Aggregation

Aggregate detailed data by grouping.


* Select grouping, drag fields to "Grouping"

* Select aggregation fields and methods: drag fields to "Aggregation"; you can change the aggregation method and set the name of the aggregated field.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa35a8a360784476b8334be07b66d68a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-计算列"></span>
## 2.5 Calculation column

The calculation column operator supports custom expressions, uses Spark functions to process upstream fields, and adds new fields. The configuration process for calculated columns can clearly display newly added fields in a tabular format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f2e8fc3e5924533baf75a56a6c3f5d1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beed4a466eec4a838a24f4058c0d4559~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-筛选行"></span>
## 2.6 Filter rows

Select fields and confirm filter conditions; two levels of AND/OR logical relationships are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac260f345b0f4c8196361f7c4ed0b292~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-列转行"></span>
## 2.7 Pivot columns to rows

Convert multiple fields in the table header into a single column for display, transforming a wide table into a long table.

**Result**

For example, in a student's subject score table, the scores for Chinese, English, and Mathematics are each represented as a separate field.


|Student name |Student ID |Gender |Chinese |Mathematics |English |
|---|---|---|---|---|---|
|Zhang San |2014010201 |Male |88 |88 |88 |
|Li Si |2014010202 |Female |87 |76 |99 |
|Wang Wu |2014010203 |Male |79 |75 |78 |
|Xiao Jia |2014010204 |Female |60 | |60 |
|Xiao Yi |2014010205 |Male |90 |97 |96 |
|Xiao Bing |2014010206 |Female |80 |100 |95 |
|Xiao Ding |2014010207 |Male |90 |99 |98 |
|Xiao Xiao |2014010208 |Female |78 |98 |85 |


By pivoting columns to rows, the scores of the three subjects can be merged into a single "Score" field, and a "Subject" field can be added to distinguish the scores of each subject.


|Student name |Student ID |Gender |Subject |Score |
|---|---|---|---|---|
|Zhang San |2014010201 |Male |Chinese |88 |
|Li Si |2014010202 |Female |Chinese |87 |
|Wang Wu |2014010203 |Male |Chinese |79 |
|Xiao Jia |2014010204 |Female |Chinese |60 |
|Xiao Yi |2014010205 |Male |Chinese |90 |
|Xiao Bing |2014010206 |Female |Chinese |80 |
|Xiao Ding |2014010207 |Male |Chinese |90 |
|Xiao Xiao |2014010208 |Female |Chinese |78 |
|Zhang San |2014010201 |Male |Mathematics |88 |
|Li Si |2014010202 |Female |Mathematics |76 |
|Wang Wu |2014010203 |Male |Mathematics |75 |
|Xiao Jia |2014010204 |Female |Mathematics | |
|Xiao Yi |2014010205 |Male |Mathematics |97 |
|Xiao Bing |2014010206 |Female |Mathematics |100 |
|Xiao Ding |2014010207 |Male |Mathematics |99 |
|Xiao Xiao |2014010208 |Female |Mathematics |98 |
|Zhang San |2014010201 |Male |English |88 |
|Li Si |2014010202 |Female |English |99 |
|Wang Wu |2014010203 |Male |English |78 |
|Xiao Jia |2014010204 |Female |English |60 |
|Xiao Yi |2014010205 |Male |English |96 |
|Xiao Bing |2014010206 |Female |English |95 |
|Xiao Ding |2014010207 |Male |English |98 |
|Xiao Xiao |2014010208 |Female |English |85 |


**Processing example**

Add a pivot columns to rows node after the model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65a8c1f4e58040e1ac07267d4e0e42b0~tplv-goo7wpa0wc-image.image) </span>

Select the fields to be transformed; in this case, select "Chinese", "Mathematics", and "English".

Set the transformed column names for the original field names and field values, which in this case are "Subject" and "Score", respectively.

Execute the node to preview the data.

<span id="_2-8-行转列"></span>
## 2.8 Pivot rows to columns

Convert the values of a single field into table header columns, transforming a long table into a wide table.

**Result**

For example, in a student's subject score table, there are "Subject" and "Score" fields that record the scores for each subject.


|Student name |Student ID |Gender |Subject |Score |
|---|---|---|---|---|
|Zhang San |2014010201 |Male |Chinese |88 |
|Li Si |2014010202 |Female |Chinese |87 |
|Wang Wu |2014010203 |Male |Chinese |79 |
|Xiao Jia |2014010204 |Female |Chinese |60 |
|Xiao Yi |2014010205 |Male |Chinese |90 |
|Xiao Bing |2014010206 |Female |Chinese |80 |
|Xiao Ding |2014010207 |Male |Chinese |90 |
|Xiao Xiao |2014010208 |Female |Chinese |78 |
|Zhang San |2014010201 |Male |Mathematics |88 |
|Li Si |2014010202 |Female |Mathematics |76 |
|Wang Wu |2014010203 |Male |Mathematics |75 |
|Xiao Jia |2014010204 |Female |Mathematics | |
|Xiao Yi |2014010205 |Male |Mathematics |97 |
|Xiao Bing |2014010206 |Female |Mathematics |100 |
|Xiao Ding |2014010207 |Male |Mathematics |99 |
|Xiao Xiao |2014010208 |Female |Mathematics |98 |
|Zhang San |2014010201 |Male |English |88 |
|Li Si |2014010202 |Female |English |99 |
|Wang Wu |2014010203 |Male |English |78 |
|Xiao Jia |2014010204 |Female |English |60 |
|Xiao Yi |2014010205 |Male |English |96 |
|Xiao Bing |2014010206 |Female |English |95 |
|Xiao Ding |2014010207 |Male |English |98 |
|Xiao Xiao |2014010208 |Female |English |85 |


By pivoting rows to columns, the subject scores can be split into three fields: "Chinese Score", "Mathematics Score", and "English Score", resulting in a wide table at the student level.


|Student name |Student ID |Gender |Chinese |Mathematics |English |
|---|---|---|---|---|---|
|Zhang San |2014010201 |Male |88 |88 |88 |
|Li Si |2014010202 |Female |87 |76 |99 |
|Wang Wu |2014010203 |Male |79 |75 |78 |
|Xiao Jia |2014010204 |Female |60 | |60 |
|Xiao Yi |2014010205 |Male |90 |97 |96 |
|Xiao Bing |2014010206 |Female |80 |100 |95 |
|Xiao Ding |2014010207 |Male |90 |99 |98 |
|Xiao Xiao |2014010208 |Female |78 |98 |85 |


**Processing example**

Add pivot rows to column nodes after the model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f056a7a5b38b40a48b60630749005ae8~tplv-goo7wpa0wc-image.image) </span>

Select the field to be pivoted and the corresponding value field, and place other fields to be retained in the retained fields section. Then, click to configure new columns, specify which fields the "Subject" field should be split into, and enter the corresponding values from "Subject".

This step also supports aggregating the value fields at the same time.

The content in the red box in the above figure shows the table structure after executing the pivot rows to columns operation. Execute the node to preview the data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8855204f41554061b0c3ea326ff04f36~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-9-数据拆分"></span>
## 2.9 Data splitting

The data splitting operators include: data splitting, split field operator, and more. These allow a single dataset to be split into multiple datasets according to specified conditions. For a detailed introduction to the operators, please refer to [Data Splitting Operators](https://docs.byteplus.com/docs/DataWind/110021).

<span id="_2-10-字符串索引"></span>
## 2.10 String indexing

A type conversion operator that maps the values of specified attributes to numeric indexes, enabling operators that can only process numeric data to also handle attribute values. This operator is generally used for data preprocessing. In addition, it is not suitable for columns containing continuous data, such as ID columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec978fe0dbe447528b332b4e76ae8d67~tplv-goo7wpa0wc-image.image) </span>

**Configuration explanation**

Maps the values of specified attributes to numeric indexes, enabling operators that can only process numeric data to also handle attribute values.

**Parameter settings**

Select all string\-type attributes to create indexes:

After selecting this parameter, there is no need to manually specify the columns to be indexed. The system will automatically select all string\-type attributes to create indexes. If this parameter is not selected, you need to set the inputColumns parameter. Click to select attributes, add the attribute names you want to index to the selected attributes list, and then click Apply to select a subset of attributes.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eab8b9ae815545eaabb3ead1462d4e2f~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Invalid data handling method**

You can choose to skip invalid data (skip), raise an error (error), or do not process (keep).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/865c5752a48a42e6ad1193621594c6a4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Index order**

Index order refers to the rule by which string indexes are assigned. There are four options: frequencyDesc, frequencyAsc, alphabetDesc, and alphabetAsc.


* frequencyDesc and frequencyAsc mean sorting by the frequency of occurrence of a string in a string\-type column, in descending and ascending order, respectively.

* alphabetDesc and alphabetAsc mean sorting by encoding order in a string\-type column, in descending and ascending order, respectively.


<span id="_2-11-替换缺失值"></span>
## 2.11 Replace missing values

In a data model, some fields may contain null values. The replace missing values operator supports replacing missing data with the maximum, minimum, or average value of the column, the most frequent value, or a custom value.

**Configuration explanation**

Replace missing data with the maximum, minimum, or average value of the column, the most frequent value, or a custom value.

**Field settings**


* Fields to fill: Missing values in the selected fields will be filled.

* Parameter settings—filling rules:

   Apply the corresponding execution rules to the selected columns. Numeric columns support: 0, minimum value, maximum value, median, average value, mode, and custom value. Character types support minimum value, maximum value, and custom value.


**Processing example**

As shown in the figure, there are records in the model where subject scores are empty.

Add a node to replace missing values, and in the node settings below, select the fields to fill missing values and the filling rules.

If the selected field type is numeric, the filling rules can be 0, minimum value, maximum value, median, average value, mode, or custom value. Character types support minimum value, maximum value, and custom value; other types support filling with custom values, such as "Other".

Click Execute to preview the processed data.

<span id="_2-12-自由排序"></span>
## 2.12 Free sorting

<span id="_2-12-1-算子释义"></span>
### 2.12.1 Operator definition

Select a sorting field to sort all data or data under a certain combination dimension, and optionally extract the top K values based on the sorting. K refers to the sorting sequence number to be extracted, for example, to select the top 100 scores, 100 is the K value.

The group sorting function is equivalent to the process of setting partitions and sorting using window functions.

<span id="_2-12-2-场景释义"></span>
### 2.12.2 Scenario definition

There is data containing shopping mall, Sales representative, sales date, and sales amount. First, sort the entire dataset by sales amount to view the Top 100 sales records, selecting sales amount as the sorting field and extracting the top 100 values in descending order. If you then want to sort the sales amount for each Sales representative in each shopping mall and extract the Top 100 sales records for each, add shopping mall and Sales representative as grouping fields.

<span id="_2-12-3-配置项说明"></span>
### 2.12.3 Configuration item description


* **Sorting method:**  Supports two methods: global sorting and group sorting. Global sorting sorts all data based on the sorting field, while group sorting sets different combinations based on the grouping fields and sorts data within each combination.

* **Grouping field:**  Sets the sorting type, that is, sorts the content within each category separately. If multiple fields are selected, different categories are defined based on the combination of multiple fields for sorting.

* **Sorting field:**  The criterion for sorting. For example, if sorting by score, then score is the sorting field. Supports two sorting methods: descending and ascending:

   * Descending: sorts in reverse order based on the sorting field's results.

   * Ascending: sorts in order based on the sorting field's results.

* **To enable the [Sort Only] button**, only sorting markers need to be applied to the data according to the sorting method and sorting field, marking the specific serial number value.

* **Serial number field name:**  Stores the specific serial number according to the sorting method. You can define a function for this serial number, such as a score ranking field.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">(1) Number of K values: The default is 1000. Only integers are supported, and the minimum cannot be less than 1.</div>


<div data-tips="true" data-tips-type="warning">(2) Grouping fields and sorting fields cannot be duplicated.</div>


<div data-tips="true" data-tips-type="warning">(3) Both grouping fields and sorting fields only support numeric types (such as integers and floating\-point numbers), string types, date types, time types, and timestamp types. Special types such as arrays and maps are not supported.</div>


<span id="_2-13-去重"></span>
## 2.13 Deduplication

It is used to remove duplicate rows from the dataset.

**Field settings**

Field for deduplication: Deduplication is performed based on the selected field. If there are duplicate rows for the selected field, one row is randomly retained.

If multiple fields are selected, a row will only be deleted if all selected fields are identical.

**Processing example**

Taking the following figure as an example, the upstream data contains six entries, among which three entries have the name "Zhang San", and two entries have both the name and phone number identical.

When we add the deduplication operator, add the fields for deduplication as name and phone number, and execute the current node.

We can see that the deduplicated data contains five entries. The entry with serial number 2 is deleted because its name and phone number are identical to those of entry 1.

When we add the deduplication operator, add the fields for deduplication as name and phone number, and execute the current node.

we can see that the deduplicated data contains three entries. Entries with serial numbers 2 and 3 are deleted because their names are identical to that of entry 1.
