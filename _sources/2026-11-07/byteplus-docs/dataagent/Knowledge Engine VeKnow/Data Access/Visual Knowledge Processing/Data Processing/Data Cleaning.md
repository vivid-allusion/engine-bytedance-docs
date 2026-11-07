---
title: "Data Cleaning"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Cleaning_"
---

<span id="ed1cff68"></span>
# Feature Overview

After the data input is completed, the input data can be further processed. This chapter describes the functions of the data cleaning operator.

<span id="a20082c1"></span>
# Operator introduction

The current data cleaning operators supported by the visual knowledge processing module are as follows:


|**operator type** |**describe** |**scene interpretation** |**task type** |
|---|---|---|---|
|connect |Based on the connection field and the given connection method, the new data is obtained by combining the two data fields. |There is only "product id" in the "order table", and there is no specific information of the product. You need to connect the "product information table" and match the "product name", "product category" and other information according to the "product id". |offline task |
|multi\-table join |Combine multiple tables into a new table based on certain fields |Combine [student table], [grade table], and [class schedule] into a table to see the students' grades for each course. |offline task |
|merge row |merge row |The fields of the two data of "January Order Table" and "February Order Table" are the same and merged into one data. |offline task |
|polymerization |Aggregate calculation of detailed data by grouping |Calculate the number of times and total amount of orders placed by each user from the "Order Table", group by "User ID", and aggregate calculate the sum of the count of "Order ID" and "Order Amount". |offline task |
|filter row |Select fields, confirm filter criteria, support two layers and/or logical relationships |The "Behavior Table" contains all the user's behavior records. When you only focus on registration and login behavior, you can filter "Event Name" to belong to registration and login. |Offline tasks, real\-time tasks |
|split field |Split into multiple fields (columns) according to field format or content, support splitting according to separators, Map JSON nested field parsing splitting, array JSON nested field parsing splitting, and also support parsing the content in pure array fields into multiple rows. Note that array JSON nested fields will be tiled into multiple rows according to the content of the array after parsing, which may cause the amount of data to increase. Please confirm the data content in advance. |1. Separator splitting: There is a city field that stores the content as "City\-Code", which needs to be split into two fields of city name + city Code according to the separator '\-'. At this time, you can choose the splitting method of the separator to split and generate two fields<br><br>2. Split in JSON format: There is a city field storage structure as a JSON structure, such as city {"city name": "Shanghai", "city code": "123"}, which needs to be extracted separately. At this time, you can choose to extract the nested fields by splitting in JSON format |Offline tasks, real\-time tasks |
|deduplicate |Split one piece of data into two pieces according to a set ratio |There may be repeated users in the "user table to be visited", and the "user id" is deduplicated, and only one row of data is kept for each user. |offline task |
|column to row |One\-click to directly transpose multiple columns into multiple rows, the column names will be stored as enumeration values, and the number of data rows will increase according to the enumeration values |In the "Student Result Sheet", there are 100 rows for 100 students, and the results of 6 subjects are displayed in 6 columns. Convert "Name\-Subject\-Grade" to 600 rows of data in 3 columns. |offline task |
|row to column |One\-click to convert a column of data into multi\-column data according to the enumeration value, each enumeration value corresponds to a column, and the number of data rows will be reduced according to the enumeration value |Inverse operation of column to row. Convert the data of 600 rows in 3 columns of "Name", "Subject", "Grade" into 100 rows of data of "Name \- Subject 1 Grade \- Subject 2 Grade \- Subject 3 Grade \- Subject 4 Grade \- Subject 5 Grade \- Subject 6 Grade". |offline task |
|Replace missing values |Replace missing data with the column's maximum/minimum/average, highest frequency, or custom value |The "discount amount" of some orders in the "Order Table" is empty, that is, there is no discount and the original price is purchased. Replace null with 0. |offline task |
|field settings |Support for selecting reserved fields, setting field types, setting field names, and setting field sorting. ||Offline tasks, real\-time tasks |
|calculated column |Support for custom expressions, use Spark functions to process upstream fields and add new fields ||Offline tasks, real\-time tasks |
|Sampling |There may be repeated users in the "user table to be visited", and the "user id" is deduplicated, and only one row of data is kept for each user. ||offline task |
|data splitting |Split one piece of data into two pieces according to a set ratio ||offline task |
|String index |Maps the value of the specified attribute to a numeric index so that operators that can only process numeric data can also process the attribute. ||offline task |
|IDMapping operator |Depending on the ID\-Mapping type selected, the query is transformed through the ID\-Mapping service to an existing OneID, which cannot be used if the CDP product has not been purchased.<br><br><br>1. According to the entered ID type, query the OneID corresponding to the ID. If the ID contains pure new IDs, it may be filtered.<br><br>2. Convert to another ID according to the input ID type. At this time, the amount of data may increase due to the data mapping relationship. Please choose according to your needs. For example, check the device number through the mobile phone number. The mobile phone number: device number is 1: N. At this time, the original 1 line of data may become multiple lines of data ||Offline tasks, real\-time tasks |


<span id="d04f26f4"></span>
### **1. Field settings**

Support selecting target field, setting target field type, setting target field name, setting field sorting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ac2f3a105814786b1d4c26a8d410695~tplv-goo7wpa0wc-image.image) </span>

<span id="d04b397a"></span>
### **2. Connect**

Support for creating joins between multiple tables.


* Select a connection method

* Set connection field

* Select the corresponding field


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20262982488e443f80c3d0971e7e46b1~tplv-goo7wpa0wc-image.image) </span>

<span id="076f7ca9"></span>
### **3. Merge lines**

For merging multi\-table data

**Operation panel** click Configure multi\-table field matching relationship, note that only the same format of the field support matching, such as field format is not the same, please add field settings or calculation column and other operators to process the field format after merging

**Processing example**


1. Drag the different tables into the canvas and click on one of the tables that needs to be merged to add a Merge Row node.

2. Click the + button on the right side of other tables that need to be merged, and drag it to the left of the merge row operator.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00e3d8616e8f44668db4422b3fcf17cd~tplv-goo7wpa0wc-image.image) </span>


3. Configure the match at the bottom of the page and click Execute Save Configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b983eeed545047fe91ffc3ecbb4b4441~tplv-goo7wpa0wc-image.image) </span>

<span id="3573b63c"></span>
### **4. Aggregation**

The aggregate calculation of detailed data is realized by grouping.


* Select Group, drag and drop fields to "Group"

* Select the aggregation field and method: drag and drop the field to "aggregation" to change the aggregation method and set the aggregated field name.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/555059e3c83b4446860e2e4f206b3a75~tplv-goo7wpa0wc-image.image) </span>


<span id="2091a9af"></span>
### **5. Calculation column**

Calculate column operators, support custom expressions, use Spark functions to process upstream fields and add new fields. The configuration flow for computed columns clearly displays new fields in tabular form.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c398ec18d15d409e912e56d7a65486bd~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c853387b7c6430f90a6c05952907572~tplv-goo7wpa0wc-image.image) </span>

<span id="988076a7"></span>
### **6. Filter rows**

Select a field, confirm the filter criteria, support two layers and/or logical relationships.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/71e74db63324409c8a70cae63eea7b88~tplv-goo7wpa0wc-image.image) </span>

<span id="7741b6dc"></span>
### 7. C**olumn to row**

One\-click to directly transpose multiple columns into multiple rows, column names will be stored as enumeration values, and the number of data rows will increase according to enumeration values. **Realize the effect** , such as the student's subject score sheet, Chinese, English, mathematics three subject scores for each field


|student name |Student ID |Gender |Chinese |mathematics |English |
|---|---|---|---|---|---|
|Zhang San |2014010201 |male |88 |88 |88 |
|Li Si |2014010202 |female |87 |76 |99 |
|Wang Wu |2014010203 |male |79 |75 |78 |
|Jia |2014010204 |female |60 | |60 |
|Primary One |2014010205 |male |90 |97 |96 |
|Xiaoice |2014010206 |female |80 |100 |95 |
|Xiaoding |2014010207 |male |90 |99 |98 |
|little |2014010208 |female |78 |98 |85 |


By switching columns, you can combine the grades of three courses into one "grade" field, and add a "subject" field to distinguish the grades of each subject


|student name |Student ID |Gender |subject |score |
|---|---|---|---|---|
|Zhang San |2014010201 |male |Chinese |88 |
|Li Si |2014010202 |female |Chinese |87 |
|Wang Wu |2014010203 |male |Chinese |79 |
|Jia |2014010204 |female |Chinese |60 |
|Primary One |2014010205 |male |Chinese |90 |
|Xiaoice |2014010206 |female |Chinese |80 |
|Xiaoding |2014010207 |male |Chinese |90 |
|little |2014010208 |female |Chinese |78 |
|Zhang San |2014010201 |male |mathematics |88 |
|Li Si |2014010202 |female |mathematics |76 |
|Wang Wu |2014010203 |male |mathematics |75 |
|Jia |2014010204 |female |mathematics | |
|Primary One |2014010205 |male |mathematics |97 |
|Xiaoice |2014010206 |female |mathematics |100 |
|Xiaoding |2014010207 |male |mathematics |99 |
|little |2014010208 |female |mathematics |98 |
|Zhang San |2014010201 |male |English |88 |
|Li Si |2014010202 |female |English |99 |
|Wang Wu |2014010203 |male |English |78 |
|Jia |2014010204 |female |English |60 |
|Primary One |2014010205 |male |English |96 |
|Xiaoice |2014010206 |female |English |95 |
|Xiaoding |2014010207 |male |English |98 |
|little |2014010208 |female |English |85 |


**Processing example**


1. Add a column transition node after the model

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55bdd5cba2904a6d8f9e985d126348b0~tplv-goo7wpa0wc-image.image) </span>

2. Check the fields that need to be converted, and select "Chinese", "Mathematics", "English" in this case.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb9909cf6d5d888f72a7af6f2e36812a.png) </span>

3. Set the converted column names for the original field names and field values, in this case "discipline" and "achievement" respectively.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74f11233f349b7bf7de35d0dc6f73ba6.png) </span>

4. Execute the node to preview the data.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_339549b25a1c9a7bd361637e1a71ffc7.png) </span>


<span id="da03a39d"></span>
### **8. Row and column conversion**

One\-click to convert a column of data into multiple columns of data based on enumeration values, each enumeration value corresponds to a column, and the number of data rows will be reduced according to the enumeration value, such as the student's subject score table, with subject and grade fields, recording the grades of each course


|student name |Student ID |Gender |subject |score |
|---|---|---|---|---|
|Zhang San |2014010201 |male |Chinese |88 |
|Li Si |2014010202 |female |Chinese |87 |
|Wang Wu |2014010203 |male |Chinese |79 |
|Jia |2014010204 |female |Chinese |60 |
|Primary One |2014010205 |male |Chinese |90 |
|Xiaoice |2014010206 |female |Chinese |80 |
|Xiaoding |2014010207 |male |Chinese |90 |
|little |2014010208 |female |Chinese |78 |
|Zhang San |2014010201 |male |mathematics |88 |
|Li Si |2014010202 |female |mathematics |76 |
|Wang Wu |2014010203 |male |mathematics |75 |
|Jia |2014010204 |female |mathematics | |
|Primary One |2014010205 |male |mathematics |97 |
|Xiaoice |2014010206 |female |mathematics |100 |
|Xiaoding |2014010207 |male |mathematics |99 |
|little |2014010208 |female |mathematics |98 |
|Zhang San |2014010201 |male |English |88 |
|Li Si |2014010202 |female |English |99 |
|Wang Wu |2014010203 |male |English |78 |
|Jia |2014010204 |female |English |60 |
|Primary One |2014010205 |male |English |96 |
|Xiaoice |2014010206 |female |English |95 |
|Xiaoding |2014010207 |male |English |98 |
|little |2014010208 |female |English |85 |


Through row and column conversion, subject grades can be divided into three fields: "Chinese grades", "Mathematics grades", and "English grades", which become a wide table of students' granularity


|student name |Student ID |Gender |Chinese |mathematics |English |
|---|---|---|---|---|---|
|Zhang San |2014010201 |male |88 |88 |88 |
|Li Si |2014010202 |female |87 |76 |99 |
|Wang Wu |2014010203 |male |79 |75 |78 |
|Jia |2014010204 |female |60 | |60 |
|Primary One |2014010205 |male |90 |97 |96 |
|Xiaoice |2014010206 |female |80 |100 |95 |
|Xiaoding |2014010207 |male |90 |99 |98 |
|little |2014010208 |female |78 |98 |85 |


**Processing example**


1. Add row\-to\-column nodes after the model

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/353e53ce74a1406c9111cfeb89752fd8~tplv-goo7wpa0wc-image.image) </span>

2. Select the fields that need to be row\-to\-column and the corresponding value fields, and put the other reserved fields into the Reserved Fields column. Then, click Configure to add a new column, that is, which fields need to be split into "Disciplines", and fill in the corresponding "Disciplines" values.

   This step also supports simultaneous aggregation of value fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9faefc38d66449a8947d27a2ac15d40b~tplv-goo7wpa0wc-image.image) </span>

3. The content of the red box in the figure above is the table structure after row conversion. Execute the node to preview the data.


<span id="87849152"></span>
### **9. Data breakdown**

The breakdown operator splits the operator into two pieces of data according to this ratio, which represents the proportion of the first piece of data to the input data. After that, the two data breakdowns proportionally can proceed to the next step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b85a1e07bf44d10a3fe6fe6a48747c2~tplv-goo7wpa0wc-image.image) </span>

<span id="c46925d2"></span>
### **10. String index**

A type conversion operator that maps the value of a specified property to a numeric index, allowing operators that can only process numeric data to also process properties. This operator is generally used for data preprocessing, and is not suitable for performing the operator on columns containing continuous data, such as ID columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b549f6b6f6eb454a9cd3184419518519~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Configuration paraphrase</strong> maps the value of the specified attribute to a numeric index, so that operators that can only process numeric data can also process attributes.</div>


<div data-tips="true" data-tips-type="tip"><strong>Parameter settings</strong> Select all string type properties and index: After clicking this parameter, there is no need to manually set the columns that need to be indexed, and the system will automatically select all string type property values to index; if you do not click this parameter, you need to set the inputColumns (input column) parameter, click Select Properties, add the property name that needs to be indexed to the selected property, and click Apply to select a subset of properties.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a93e55590fff421c842e951072df87d0~tplv-goo7wpa0wc-image.image) </span>

**Invalid data processing method** You can choose to ignore invalid data (skip), or error (error), or you can do no processing (keep)

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31774e48f0604f5b9ad8e57a677807bd~tplv-goo7wpa0wc-image.image) </span>

**Index order:** 

Index order indicates the rules for string indexing, which are divided into four categories: frequencyDesc, frequencyAsc, alphabetDesc, and alphabetAsc.


* FrequencyDesc and frequencyAsc represent a string type column that is sorted by the frequency of a string, in descending and ascending order, respectively.

* alphabetDesc and alphab etAsc represent a sort in the encoded order of a string type column, descending and ascending, respectively.


<span id="828befbb"></span>
### **11. Replace missing values**

In the data model, there may be some fields with null values. The replacement missing value operator supports replacing missing data with the maximum/minimum/average, highest frequency, or custom value of the column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fce7ddaa21345d4b7764ac358a0fb1f~tplv-goo7wpa0wc-image.image) </span>

**Configuration paraphrase** : Replace missing data with the maximum/minimum/average, highest frequency, or custom value of the column

**Field settings:** 


* Fields to be filled: Missing value filling will fill the selected fields with missing values

* Parameter Settings \- Padding Rules: Execute the corresponding execution rules for the selected column. Numeric columns support: 0, minimum, maximum, median, average, mode, and custom values. Character types support minimum, maximum, and custom values


**Processing example**

As shown in the figure, there is data with empty subject grades in the model

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9d1dd1dea0f46b78a627ee35cfb815c~tplv-goo7wpa0wc-image.image) </span>

Add a replacement missing value node, select the fields and filling rules that need to be filled with missing values in the node settings below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcd056a0d80b4834a6aba1abb18550e6~tplv-goo7wpa0wc-image.image) </span>

If the field type is selected as Numeric, the padding rule can be selected as 0, Min, Max, Median, Average, Mode, Custom. Character types support minimum, maximum, and custom values; other types support custom value padding, such as "other".

Click Execute to preview the processed data.

<span id="ab83579e"></span>
### **12. Free sorting**

Select a sorting field to sort all the data or some combination dimension, and you can choose to intercept the data of the previous K value according to the sorting. K is the sorting number of the interception. If you take the top 100 according to the score, 100 is the K value. Group sorting function is equivalent to the process of setting partition and sorting by window function.

**Processing example**

There are data including shopping malls, sales personnel, sales dates, and sales. First, sort the sales records of Top100 by sales as a whole, select Sales as the sorting field, and take the top 100 values in reverse order; if the sales of each salesperson in each shopping mall are sorted, and the sales records of Top100 are taken out separately, then add the selected shopping malls and sales personnel as the grouping fields

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f9513261a184a75a4899a42fed5d7ea~tplv-goo7wpa0wc-image.image) </span>

**The configuration item description is as follows:** 


* **Sorting mode:**  Support global sorting and group sorting. Global sorting is to sort all the data according to the sorting field, and group sorting is to set different combinations according to the grouping field to sort the data in each combination.

* **Grouping fields:**  Set the type of sorting, that is, sort the content under each category, such as selecting multiple fields, then define different classes for sorting according to the combined results of multiple fields.

* **Sorting field:**  The judgment condition of sorting, such as sorting according to the score, the score is the sorting field, and two sorting methods are supported: descending/ascending:

* Descending, that is, in reverse order according to the results of the sorting field

* Ascending, that is, sort according to the result order of the sort field

* **If you open the [Sort Only] button** , you only need to sort the data according to the sorting method and the sorting field, and mark the specific sequence number value.

* **Serial number field name:**  According to the sorting method, the specific serial number is stored, and the specific function of the serial number can be defined, such as the score ranking field.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Number of K values: the default is 1000, only integers are supported, and the minimum cannot be less than 1;</div>


2. <div data-tips="true" data-tips-type="warning">Group fields and sort fields cannot be repeated.</div>


3. <div data-tips="true" data-tips-type="warning">Grouping fields and sorting fields are only supported for numeric (integer, floating\-point, etc.), string, date, time, timestamp, and special types such as arrays and maps are not supported.</div>



<span id="9a91f2e1"></span>
### **13. Deduplicate**

To remove duplicate rows from a dataset

**field settings**

Fields to be deduplicated: deduplicate according to the selected field, if the number of rows of the selected field is duplicated, randomly keep one row, if multiple fields are checked, multiple fields need to be the same before deleting the piece of data.

**Processing example**

As an example, the upstream data contains 6 pieces of data, three of which have the name "Zhang San", and two pieces of data have the same user name and phone number;

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23729d0b9ec24c76be3d3a3e3b13722a~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d70855898d4cbfa9c84b1d81cba2f9~tplv-goo7wpa0wc-image.image) </span>

When we add the deduplicate operator and add the deduplicate fields for name and phone and execute the current node;

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89541424eaa541bdab31236369af5236~tplv-goo7wpa0wc-image.image) </span>

We can find that the deduplicated data contains a total of 5 pieces, of which the data with serial number 2 is deleted because the name and phone number of 1 are the same.

When we add the deduplicate operator and add the deduplicate fields for name and phone and execute the current node;

We can find that the deduplicated data contains a total of 3 pieces, of which the data with serial number 2 and 3 are deleted because they have the same name as 1. The details are as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d412d513106f4239982808a659caf16f~tplv-goo7wpa0wc-image.image) </span>

<span id="cd953ac0"></span>
### **14. Split fields**


1. Create a new Split Field operator and select Edit.

2. Select the field type to split.

3. Supports splitting **by delimiter** and **by JSON format** .

4. When selected **by delimiter** :

   * The separator supports multiple selection: after multiple selection, it is divided into multiple fields in sequence according to the matching order.

   * Split up to 10 columns.

   * New columns defined in sequence according to the position of the separator need to redefine the field names of the columns.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb4b0d92aa14ce1886391214a58fef6~tplv-goo7wpa0wc-image.image) </span>

5. When selected **in JSON format** , the JSON format contains the following three:

   * Map ({key: value}): such as city

   * Array [{key: value}]: such as city [{"city name": "Shanghai"}, {"city name": "Beijing"}]

   * Array [value]: e.g. city ["Shanghai", "Beijing"]

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Array type field splits are tiled into multiple rows based on content, and the amount of data may increase   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0304be8afb1c41239f955eddd18737cc~tplv-goo7wpa0wc-image.image) </span>


**Define the name of the column generated after splitting:**  You can define the fields in the nest that need to be parsed and extracted according to the content of the nest


* Map ({key: value})/array [{key: value}] splitting method follows the Json_path syntax function: original field name. Nested field name, where the dot represents the nested level, if there are multiple layers, you can continue to append, such as, city {"city name 1": {"city name 2": "Shanghai", "city code": "123"}, "city code": "123"} Get, the content of city name 2 is, city. City name 1. City name 2

* Array [value]: Array splitting only involves tiling multiple rows of content. At this time, it is automatically returned to a new field, and only the field name needs to be defined.


<span id="886b5d98"></span>
### **15. ID\-Mapping operator**

Depending on the selected ID\-Mapping type, transform the query to an existing OneID through the ID\-Mapping service:


1. According to the entered ID type, query the OneID corresponding to the ID. If the ID contains pure new IDs, it may be filtered.

2. Convert to another ID according to the input ID type. At this time, the amount of data may increase due to the data mapping relationship. Please choose according to your needs. For example, check the device number through the mobile phone number. The mobile phone number: device number is 1: N. At this time, the original 1 line of data may become multiple lines of data

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/679ba3becd42405bb0332d37b568211f~tplv-goo7wpa0wc-image.image) </span>

   **Parameter setting**

   * **Subject: The** subject of the portrait in CDP, that is, the target object of ID\-Mapping OneID

   * **Input:**  Select the input ID type and its input field, which is the data input condition for the conversion between IDs

   * **Output:**  Select the output ID type and define the field name, which is used to save the OneID or other ID data obtained by the exchange ( **for example:**  if the mobile phone number is converted to OneID, the mobile phone number is input and OneID is output)

   * **Whether to participate in OneID correction:**  The IDMapping graph configuration has turned on the OneID correction brush back function, which supports the correction of OneID data in the last 2 days. After turning it on, the system will brush back regularly every day according to the correction configuration, which may occupy certain computing resources. Please set it as needed.


<span id="4e8105e1"></span>
### 16. Encryption and decryption

Refers to the data security management function that encrypts or decrypts the specified field data in the data source according to a specific encryption or decryption algorithm.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Keys are not managed at the system level. If the key is automatically generated or manually entered, please manage it properly by yourself.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9aa359c3399439e9c91827e6c58faa3~tplv-goo7wpa0wc-image.image) </span>


* **Operation type: The** type of operation that needs to be performed on the field, that is, whether to encrypt or decrypt the data.

* **Encryption/decryption algorithm:**  Select the type of algorithm for data encryption or decryption. The encryption and decryption algorithms have differences. They can be divided into symmetric encryption and decryption (such as AES/DES) and asymmetric encryption and decryption (RSA). There are public and private keys in asymmetric encryption. You need to enter them at the same time to encrypt or decrypt. Please choose different algorithms according to your needs.

* **Key:**  Enter or select an encrypted or decrypted key to use as a password for encryption or decryption.

* **Manual input:**  Custom key content is supported, or generated directly through the key generation tool.

* **Field Settings:**  Select the fields that need to be encrypted or decrypted, and select the storage method of the encrypted or decrypted data content as needed.

* **Cover the original field:**  The name of the original field of encryption or decryption remains unchanged, and the data content is updated into encrypted ciphertext or decrypted plaintext according to the operation of multi\-type overlay

* **New field:**  The original field name and data content remain unchanged, and the field name can be customized for newly encrypted or decrypted fields according to the operation type.


<span id="5a5eb5d2"></span>
### 17. Sampling

Sampling selects a subset of the total data for analysis to uncover useful information applicable to a larger dataset. Common sampling is divided into three categories: random sampling, hierarchical sampling, and downsampling.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f1cf4a004664f34ae48bf92e5b7a924~tplv-goo7wpa0wc-image.image) </span>

**Sampling Type:**  Currently supports three sampling types, namely random sampling, hierarchical sampling and downsampling


* **Random sampling:**  Random sampling of the input according to a given ratio or number

* **Hierarchical sampling:**  Divide the input data into different groups and randomly sample each group separately

* **Downsampling:**  also known as undersampling, mainly to solve the problem of data imbalance and reduce the amount of data in excess of the value


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Examples of application scenarios:</strong></div>


<div data-tips="true" data-tips-type="tip">Customer research has obtained a large amount of behavioral data, but it does not require so much data in actual analysis. Therefore, it is hoped that the data will be sampled and analyzed without ensuring the uniformity of the sampling results. It is hoped that a certain proportion of data will be extracted according to different ages. Therefore, classification sampling can be performed through this operator, such as sampling and analyzing 50% of the data based on the sample data according to the "age" setting, and the output result will only leave 50% of the data and be applied to subsequent operators.</div>
