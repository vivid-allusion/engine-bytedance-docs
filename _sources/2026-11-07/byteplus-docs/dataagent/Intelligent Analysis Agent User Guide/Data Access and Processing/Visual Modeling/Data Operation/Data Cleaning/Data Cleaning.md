---
title: "Data Cleaning"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Cleansing"
---

Data cleansing is the core stage of data preprocessing, designed to address quality issues that arise after data input. It corrects data errors and optimizes data structure through a series of standardized operations. Data cleansing operators are a collection of tools that implement this process, meeting diverse needs from basic data correction to complex structural transformations. This article introduces the specific functions of data cleansing operators.

<span id="_1-概述"></span>
# Function overview

Data cleansing typically refers to identifying and correcting recognizable errors in data files, including checking data consistency, handling invalid values, missing values, and more. After completing data input, users can further perform data cleansing operations on the input data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e26f75b0d7084fbaa6fe1fac2f7c597e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# Function introduction

<span id="_2-1-字段设置"></span>
## Field settings

The field settings function supports modifying the target field's name, field type, and other attributes. If no changes are made, the default is to match the upstream field name and type.

Advanced configuration is also provided, supporting one\-click formatting of target field names, such as converting to uppercase, converting to lowercase, removing illegal characters, correcting non\-standard data, and quick field sorting to improve data processing efficiency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33b72de5745b4f05a0b2a3ffcb9355fe~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-连接"></span>
## Join

Supports creating a join relationship between two tables. Users must complete the join by selecting the join method, setting the join fields, and choosing the fields to retain, in sequence.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf7421e826dc4423b30610e64452b33b~tplv-goo7wpa0wc-image.image) </span>

<span id="d48b9146"></span>
## Multi\-table join

Supports creating join relationships among multiple tables, similar to the functionality of the "Join" operator.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b15514beb23481285d91632feea5961~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-合并行"></span>
## Merge rows

Used to merge data from multiple tables. Click to configure the matching relationships of fields across multiple tables. Caution: Only fields with the same format can be matched. If the field formats differ, add a field settings operator or a calculated column operator to process the field format before merging.


1. Drag different tables onto the canvas, then click one of the tables to be merged and add a merge rows node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c76b54472420490c81095ec10601e6cf~tplv-goo7wpa0wc-image.image) </span>

2. Click the + button on the right side of other tables to be merged, and drag it to the left side of the merge row operator;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d55ac28f9db45f29fd949fa974fa37d~tplv-goo7wpa0wc-image.image) </span>

3. Configure the matching relationship at the bottom of the page, then click Execute to save the configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95fe859c36a4479e85fb88ca46730fa7~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-4-聚合"></span>
## Aggregation

Aggregate detailed data by grouping.


1. Select a group and drag fields to "Group".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/253f788e00fe4e759e9cda9f3ea62900~tplv-goo7wpa0wc-image.image) </span>

2. Select aggregation fields and methods. Drag fields to "Aggregation" to change the aggregation method or set the name of the aggregated field.


<span id="_2-5-计算列"></span>
## Computed column

The computed column operator supports custom expressions, uses Spark functions to process upstream fields, and adds new fields. The configuration process for computed columns can clearly display newly added fields in a tabular format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/881962eb8a7e4184a71224893b32aca3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd07c67a27dd49c98eaf68448b6bc138~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-筛选行"></span>
## Row filtering

Select fields and confirm filter conditions. Supports two levels of and/or logical relationships.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/866e34f5fa424070ac10174b6fe06555~tplv-goo7wpa0wc-image.image) </span>

<span id="95b2d52e"></span>
## Data splitting category

The data splitting category operator includes: data splitting, split field operator, and more. It enables splitting a single dataset according to certain conditions to obtain multiple datasets. For detailed operator descriptions, see [Data Splitting Operators](https://docs.byteplus.com/docs/dataagent/Data_Splitting_Operators).

<span id="5be7611c"></span>
## Custom sorting

<span id="300904ec"></span>
### Operator definition

Select a sorting field to sort all data or data under a specific combination of dimensions. You can also choose to extract the top K values based on the sorting order, where K is the sorting rank to be extracted. For example, to select the top 100 by score, 100 is the K value.

The group sorting function is equivalent to the process of setting partitions and sorting using window functions.

<span id="10f79cca"></span>
### Scenario definition

Suppose you have data that includes shopping mall, sales representative, sales date, and sales amount. First, sort all records by sales amount to view the top 100 sales records; select sales amount as the sorting field and extract the top 100 values in descending order. To sort the sales amount for each sales representative in each shopping mall and extract the top 100 sales records for each, add shopping mall and sales representative as grouping fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c5bd3f52e014b899cafb93f34792b96~tplv-goo7wpa0wc-image.image) </span>

<span id="15353aab"></span>
### Configuration item description


* **Sorting method:**  It supports two methods: global sorting and group sorting. Global sorting sorts all data based on the sorting field, while grouped sorting sorts data within each combination defined by the grouping field.

* **Grouping field:**  Determines how sorting is performed, that is, sorts the content within each category. If multiple fields are selected, sorting is based on the combination of these fields, defining different groups for sorting.

* **Sorting field:**  The criterion for sorting. For example, if sorting by score, then score is the sorting field. Two sorting orders are supported: descending and ascending:

   * Descending order means arranging the results in reverse order based on the sorting field.

   * Ascending order means arranging the results in order based on the sorting field.

* **If the [Sort Only] button is enabled**, you only need to mark the data according to the sorting order and sorting field, assigning a specific sequence number.

* **Sequence number field name**: Stores the sequence number according to the sorting order. You can define the function of this sequence number, such as a score ranking field.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">(1) Number of K values: Default is 1000, only integers are supported, and the minimum cannot be less than 1.</div>


<div data-tips="true" data-tips-type="warning">(2) Grouping fields and sorting fields must not overlap.</div>


<div data-tips="true" data-tips-type="warning">(3) Both grouping fields and sorting fields only support numeric types (such as integer and floating point), string types, date types, time types, and timestamp types. Special types such as arrays and maps are not supported.</div>


<span id="a83b367e"></span>
## Deduplication

Used to remove duplicate rows from the dataset.

**Field settings**

Fields to deduplicate: Deduplication is performed based on the selected fields. If there are duplicate rows for the selected fields, one row is retained at random.

If multiple fields are selected, the data will only be deleted if all selected fields are identical.

**Processing example**

For example, upstream data contains many records, among which dozen records have the same gender or member level, then the two records have different genders, and the four records have different member levels.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bbeaefd9fe440c7b69ef149511d3215~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88f8515ced194e1bb464cc0ef02cb06a~tplv-goo7wpa0wc-image.image) </span>

When the deduplication operator is added and the fields to be deduplicated are set to MemberLevel and AgeGroup, and the current node is executed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c94ce53ded74c76bb443e7110f7b1ee~tplv-goo7wpa0wc-image.image) </span>

When the deduplication operator is added and the field to be deduplicated is set to user identification, and the current node is executed.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/1c8a647998f74b73a3e6f0739495a65e~tplv-em5hxbkur4-noop.image?width=1919&height=945) </span>

We can see that after deduplication, the data contains a total of 3 records. The records with serial numbers 2 and 3 were deleted because their names were identical to that of record 1. Details are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16e4f66c36524c1683fa7c3bc5176b2c~tplv-goo7wpa0wc-image.image) </span>

<span id="64778e35"></span>
## Sampling

Select a subset of data from the entire dataset for analysis to discover useful information applicable to larger datasets.

There are three common types of sampling: random sampling, stratified sampling, and downsampling.

**Usage example**:

During customer research, a large volume of behavioral data was collected. However, not all of this data is needed for actual analysis, so sampling analysis is desired. To ensure the uniformity of the sampling results, extract a certain proportion of data by age group. This operator can be used for stratified sampling. For example, based on sample data, 50% of the data for each age group can be extracted for sampling analysis according to the "age" field. The output will retain only 50% of the data, which can then be used in subsequent operators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19cb672b4bb5487f8d7b713ca6f5e5dc~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-列转行"></span>
## Column\-to\-row transformation

Convert multiple columns of indicators in the table header into a single column for display, transforming a wide table into a tall table.

**Effect achieved**

For example, in a student subject score table, the scores for Chinese, English, and Mathematics are each represented as a separate field.


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


By performing a column\-to\-row transformation, the scores for the three subjects can be merged into a single "score" field, and a "subject" field can be added to distinguish the scores for each subject.


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

Add a column\-to\-row node after the model.

Select the fields to be transformed; in this case, select "Chinese", "Mathematics", and "English".

Set the transformed column names for the original field names and field values; in this case, use "subject" and "score" respectively.

Execute the node to preview the data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19cb672b4bb5487f8d7b713ca6f5e5dc~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-8-行转列"></span>
## Row\-to\-column transformation

Convert the values of a single column into table header columns, transforming a tall table into a wide table.

**Effect achieved**

For example, in a student subject score table, there are "subject" and "score" fields that record the scores for each subject.


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


By performing a row\-to\-column transformation, the subject scores can be split into three fields: "Chinese score", "Mathematics score", and "English score", resulting in a wide table at the student level.


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


**Example of processing**

Add a pivot node after the model.

Select the fields to be pivoted and their corresponding value fields, and place any other fields that need to be retained in the reserved fields section. Then, click to configure new columns, specifying into which fields the "subject" should be split, and enter the corresponding values from "subject".

This step also supports aggregating the value fields simultaneously:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27a5ee8ae37248369a3e341182603393~tplv-goo7wpa0wc-image.image) </span>

The content in the red box in the above figure shows the table structure after the pivot operation is performed. Execute the node to preview the data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/089f9caea64e40259b0775344c1a5d45~tplv-goo7wpa0wc-image.image) </span>

<span id="71c61201"></span>
## Encryption and decryption

Refers to the data security management feature that encrypts or decrypts specified fields in the data source using specific encryption or decryption algorithms.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The system does not manage keys at the system level. If keys are generated automatically or entered manually, please manage them properly.</div>


**Usage example**:

Obtain a set of core user credit score rating data, which contains sensitive information such as the user's "age", "gender", "salary income", and "marital status". However, this data must be integrated into the platform for actual use, and whether the data is in plaintext or ciphertext does not affect statistical usage. Therefore, to ensure data security, it is desirable to encrypt sensitive fields after integration into the platform, with the encryption key known only to the user. In this case, this operator can be used to encrypt data, such as encrypting the "salary income" field, with the key generated and managed by the platform's key generator.

Conversely, if the data warehouse stores encrypted result data and user profiling needs to be performed based on plaintext, decrypting all data at the data warehouse level is clearly impractical. In this case, this operator can be used to decrypt data, and ciphertext can be entered for decryption either using the system's built\-in method or manually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41036d3d41604783b5d4e71c95a190d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-11-替换缺失值"></span>
## Replace missing values

Some fields in the data model may contain null values. The missing value replacement operator supports replacing missing data with the maximum, minimum, or average value of the column, the most frequent value, or a custom value.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c474644d161146d5916f0ba8c0e2e8e2~tplv-goo7wpa0wc-image.image) </span>

**Configuration description**

Replace missing data in the column with the maximum, minimum, average, mode, or a custom value.

**Field settings**


* Fields for missing value imputation: Missing value imputation will fill missing values for the selected fields.

* Parameter settings—imputation rule:

   Apply the corresponding imputation rule to the selected columns. For numeric columns, the following are supported: 0, minimum, maximum, median, average, mode, and custom value. For string type, minimum, maximum, and custom value are supported.


**Processing example**

As shown in the figure, there are subject scores with missing values in the model.

Add a missing value replacement node, and in the node settings below, select the fields for missing value imputation and the imputation rule.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a13d8265637741f2a843464279bc910d~tplv-goo7wpa0wc-image.image) </span>

If the selected field type is numeric, the available imputation rules are 0, minimum, maximum, median, average, mode, and custom value. For string type, minimum, maximum, and custom value are supported; for other types, filling with a custom value is supported, such as "Other".

Click Execute to preview the processed data.

<span id="dba2636f"></span>
## String indices

A type conversion operator that maps the values of specified attributes to numeric indices, allowing operators that can only process numeric data to also process these attributes. This operator is generally used for data preprocessing. In addition, it is not suitable for columns containing continuous data, such as ID columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3306306f3e38441584b2a5637cbf0fcb~tplv-goo7wpa0wc-image.image) </span>

**Configuration explanation**

Map the values of specified attributes to numeric indices, allowing operators that can only process numeric data to also process these attributes.

**Parameter settings**

Select all string\-type attributes to create indices:

After selecting this parameter, you do not need to manually specify the attributes to be indexed. The system will automatically select all string\-type attributes to create indexes. If you do not select this parameter, you need to configure the inputColumns parameter. Click to select attributes, add the attribute names to be indexed to the selected attributes, and click Apply to choose a subset of attributes.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71fca3de4b6f4ada85312e560c03e84a~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Invalid data processing method**

You can choose to skip invalid data (skip), report an error (error), or leave it unprocessed (keep).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39c31260e80e4116868c14cc98cf1f05~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Index order**

Index order refers to the rule by which string indexes are sorted. There are four types: frequencyDesc, frequencyAsc, alphabetDesc, and alphabetAsc.


* frequencyDesc and frequencyAsc indicate sorting by the frequency of occurrence of a string in a string\-type column, in descending and ascending order, respectively.

* alphabetDesc and alphabetAsc indicate sorting by encoding order in a string\-type column, in descending and ascending order, respectively.
