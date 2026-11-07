---
title: "Data Splitting Operators"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Splitting_Operators"
---

<span id="_1-数据拆分概述"></span>
# 1. Overview of data splitting

Data splitting operators include: data splitting, split field operators, and more. These operators enable splitting a single dataset into multiple datasets based on specified conditions.

<span id="_2-算子介绍"></span>
# 2. Introduction to operators

<span id="_2-1-数据拆分"></span>
## 2.1 Data splitting

**Data splitting** operator splits the dataset into two datasets according to the specified ratio.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97c42534b83b4d22aa8e83cdc5338f85~tplv-goo7wpa0wc-image.image) </span>

First, in the configuration interface, users can set parameters by entering the split ratio and maximum limit. The value entered in the input box represents the proportion of the first dataset in the input data. After splitting according to the ratio, the two resulting datasets can be used for subsequent operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/446ad3e6da474423adb6a9b29c73acb6~tplv-goo7wpa0wc-image.image) </span>

Next, in the preview area on the right, click "Data 1" and "Data 2" to preview the data. The preview data is generated based on sampling results from the original data. If multiple tables are involved in a join query, the results after sampling and then joining may differ from the actual results (this only affects the preview display and does not impact the final calculation; you can set a larger preview quantity). For example, if Table A and Table B respectively store Chinese and mathematics scores and need to be merged, during preview, Table A may sample Zhang's Chinese score, and Table B may sample Li's mathematics score. After merging, the preview data will show Zhang's mathematics score as empty and Li's Chinese score as empty.

<span id="_2-2-拆分字段"></span>
## 2.2 Split fields

**Split fields** operator splits a field into multiple fields (columns) based on the field format or content. It supports splitting by delimiter, parsing and splitting nested Map JSON fields, parsing and splitting nested array JSON fields, and also supports expanding the contents of pure array fields into multiple rows. Note that after parsing nested array JSON fields, the data will be expanded into multiple rows according to the array contents, which may increase the data volume. Please confirm the data content in advance.

**Scenario description:** 

a. Split by delimiter: Some city fields store content in the format "city\-Code". You need to split this into two fields, city name and city code, based on the '\-' delimiter. In this case, you can use the delimiter splitting method to generate two fields.

b. Split by JSON format: Some city fields are stored as a JSON structure, such as city{"城市名": "Shanghai","城市code": "123"}. To extract the city name separately, you can use the JSON format splitting method to extract the nested field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ee438b074d54e4d8876ac1c7cacbec5~tplv-goo7wpa0wc-image.image) </span>

**Operation steps** :


1. Create a new "Split Field" operator and select it for editing.

2. Select the field type to be split.

3. You can split by **delimiter** or **JSON format**.

4. When **delimiter** is selected:

* Multiple delimiters are supported: when multiple delimiters are selected, the field is split sequentially according to the order in which the delimiters match.

* A maximum of 10 columns can be split.

* The field names of the new columns created according to the positions of the delimiters need to be redefined.

5. When **JSON format** is selected, there are three types of JSON formats:

* Map({key:value}): For example, city

* Array[{key:value}]: For example, city[{"城市名": "Shanghai"},{"城市名": "Beijing"}]

* Array[value]: For example, city["上海","北京"] \*


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Splitting array\-type fields will flatten the content into multiple rows, which may increase the number of rows.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2027a410d0af4d11b66d3d7d0bee65f8~tplv-goo7wpa0wc-image.image) </span>

**Define the names of the columns generated after splitting:** 

You can define the fields to be parsed and extracted from the nested content.


* The splitting method for Map({key:value})/Array[{key:value}] follows the Json_path syntax: original field name.nested field name, where the dot represents the nested level. If there are multiple levels, you can keep appending. For example, for city{"城市名1": {"城市名2": "Shanghai","城市code": "123"},"城市code": "123"}, to obtain the content of 城市名2, use city.城市名1.城市名2

* Array[value]: Splitting an array only involves flattening the content into multiple rows, which are then automatically assigned to a new field. You only need to define the field name.
