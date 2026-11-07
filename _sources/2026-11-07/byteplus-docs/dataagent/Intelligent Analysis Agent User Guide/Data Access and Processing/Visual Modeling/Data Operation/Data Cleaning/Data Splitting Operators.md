---
title: "Data Splitting Operators"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Splitting_Operators"
---

<span id="_1-数据拆分概述"></span>
# 1. Overview of data splitting

Data splitting operators include: data splitting, split field operators, and more. These operators enable splitting a single dataset into multiple datasets based on specified conditions.

<span id="_2-算子介绍"></span>
# 2. Operator introduction

<span id="_2-1-数据拆分"></span>
## 2.1 Data splitting

**Data splitting** operator splits the data into two datasets according to the specified ratio.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd4b2c3b909a4c72a7b69f77c332c535~tplv-goo7wpa0wc-image.image) </span>

First, in the configuration interface, users can set parameters by entering the split ratio and the maximum limit. The value entered in the input box represents the proportion of the first dataset relative to the input data. After splitting according to the ratio, the two resulting datasets can proceed to the next step.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ded954b3e0f94bc9adb8c945a1b4bf51~tplv-goo7wpa0wc-image.image) </span>

Next, in the preview area on the right, click "Data 1" and "Data 2" to preview the data. The preview data is generated based on sampling results from the original data. If multiple tables are involved in a join query, the results after sampling and then joining may differ from the actual results (this only affects the preview display and does not impact the final calculation; you can set a larger preview quantity). For example, if Table A and Table B store Chinese and math scores respectively and need to be merged, during preview, Table A may sample Xiao Zhang's Chinese score and Table B may sample Xiao Li's math score. After merging, the preview data will show Xiao Zhang's math score as empty and Xiao Li's Chinese score as empty.

<span id="_2-2-拆分字段"></span>
## 2.2 Split field

**Split field** operator splits a field into multiple fields (columns) based on the field's format or content. It supports splitting by delimiter, parsing and splitting nested Map JSON fields, parsing and splitting nested array JSON fields, and also supports expanding the contents of pure array fields into multiple rows. Note that after parsing nested array JSON fields, the data will be expanded into multiple rows according to the array contents, which may increase the data volume. Please confirm the data content in advance.

**Scenario explanation** :

a. Split by delimiter: When the city field stores content in the format "city\-Code", it is necessary to split it into two fields, city name and city code, based on the '\-' delimiter. In this case, you can select the delimiter splitting method to generate two fields.

b. Split by JSON format: When the city field stores data in a JSON structure, such as city{"城市名": "Shanghai","城市code": "123"}, and you need to extract only the city name, you can select the JSON format splitting method to extract the nested field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ca95b5c29b2414f97823bc2fda681d2~tplv-goo7wpa0wc-image.image) </span>

**Operation steps** :


1. Create a new "Split field" operator and select it for editing.

2. Select the type of field to be split.

3. Supports splitting by **delimiter** and **JSON format**.

4. When **delimiter** is selected:

* Delimiters support multiple selections: When multiple delimiters are selected, fields are split sequentially according to the order in which they are matched.

* Up to 10 columns can be split.

* You need to redefine the column names for the new columns, which are defined sequentially based on the position of the delimiter.

5. When **JSON format** is selected, the JSON format includes the following three types:

* Map({key:value}): For example, city

* Array[{key:value}]: For example, city[{"城市名": "Shanghai"},{"城市名": "Beijing"}]

* Array[value]: For example, city["上海","北京"] \*


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Splitting array\-type fields will flatten the content into multiple rows, which may increase the amount of data.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcf769a115af40f88f76299e1c970722~tplv-goo7wpa0wc-image.image) </span>

**Define the names of columns generated after splitting:** 

You can define which nested fields to parse and extract based on the nested content.


* Map({key:value})/ Array[{key:value}] splitting methods follow the Json_path syntax function: original field name.nested field name, where the dot represents the nesting level. If there are multiple levels, you can continue to append. For example, city{"城市名1": {"城市名2": "Shanghai","城市code": "123"},"城市code": "123"} to obtain the content of 城市名2, use city.城市名1.城市名2

* Array[value]: Array splitting only involves flattening the content into multiple rows, which will automatically be assigned to a new field. You only need to define the field name.
