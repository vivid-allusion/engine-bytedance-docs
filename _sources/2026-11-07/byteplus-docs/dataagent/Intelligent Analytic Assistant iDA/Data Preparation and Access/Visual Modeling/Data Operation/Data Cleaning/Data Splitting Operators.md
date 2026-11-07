---
title: "Data Splitting Operators"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Splitting_Operators_"
---

<span id="_1-数据拆分概述"></span>
# 1. Overview of data splitting

Data splitting operators include data splitting, split field operators, and more. These operators enable splitting a single dataset into multiple datasets based on specified conditions.

<span id="_2-算子介绍"></span>
# 2. Introduction to operators

<span id="_2-1-数据拆分"></span>
## 2.1 Data splitting

**Data splitting** operator splits the dataset into two datasets according to the specified ratio.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd4b2c3b909a4c72a7b69f77c332c535~tplv-goo7wpa0wc-image.image) </span>

First, in the configuration interface, users can set parameters by specifying the split ratio and maximum limit. The value entered in the input box represents the proportion of the first dataset relative to the input dataset. After splitting according to the ratio, the two resulting datasets can proceed to the next operation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ded954b3e0f94bc9adb8c945a1b4bf51~tplv-goo7wpa0wc-image.image) </span>

Next, in the preview area on the right, click "Data 1" and "Data 2" to preview the datasets. The preview data is generated based on sampling results from the original data. If multiple tables are joined for queries, the results after sampling and joining may differ from the actual results (this only affects the preview display and does not impact the final calculation; a larger preview quantity can be set). For example, Table A and Table B respectively store Chinese and mathematics scores. If the two tables need to be merged, but during preview, Table A samples Zhang's Chinese score and Table B samples Li's mathematics score, the merged preview data will show Zhang's mathematics score as empty and Li's Chinese score as empty.

<span id="_2-2-拆分字段"></span>
## 2.2 Split fields

**Split fields** operator splits a field into multiple fields (columns) based on the field's format or content. It supports splitting by delimiter, parsing and splitting nested Map JSON fields, parsing and splitting nested array JSON fields, and also supports expanding the contents of pure array fields into multiple rows. Note that after parsing nested array JSON fields, the data will be expanded into multiple rows according to the array contents, which may increase the data volume. Please confirm the data content in advance.

**Scenario explanation**:

a. Split by delimiter: When the city field contains content in the format "city\-Code", it is necessary to split it into two fields, city name and city code, based on the '\-' delimiter. In this case, you can choose the delimiter splitting method to generate two fields.

b. Split by JSON format: When the city field is stored as a JSON structure, such as city {"city name": "Shanghai", "city code": "123"}, and you need to extract only the city name, you can select the JSON format splitting method to extract the nested field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ca95b5c29b2414f97823bc2fda681d2~tplv-goo7wpa0wc-image.image) </span>

**Operation steps**:


1. Create a new "Split Field" operator and select it for editing.

2. Select the type of field to be split.

3. Supports splitting by **delimiter** and by **JSON format**.

4. When **delimiter** is selected:

* Multiple delimiters are supported. After selecting multiple delimiters, the field will be split into multiple fields sequentially, based on the order in which the delimiters appear.

* A maximum of 10 columns can be split.

* The new columns created according to the positions of the delimiters need to have their field names specified.

5. When **JSON format** is selected, the JSON format includes the following three types:

* Map ({key:value}): for example, city

* Array [{key:value}]: for example, city [{"city name": "Shanghai"}, {"city name": "Beijing"}]

* Array [value]: for example, city ["Shanghai", "Beijing"] \*


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Splitting array\-type fields will flatten the content into multiple rows, which may increase the amount of data.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcf769a115af40f88f76299e1c970722~tplv-goo7wpa0wc-image.image) </span>

**Define the names of the columns generated after splitting:** 

You can define the fields to be parsed and extracted from the nested content.


* The splitting method for Map ({key:value}) / Array [{key:value}] follows the Json_path syntax function: original field name.nested field name, where the dot represents the nesting level. If there are multiple levels, you can continue to append them. For example, for city {"city name 1": {"city name 2": "Shanghai", "city code": "123"}, "city code": "123"}, to obtain the value of city name 2, use city.city name 1.city name 2.

* Array [value]: Splitting the array only involves flattening the content into multiple rows, which are automatically placed into a new field. You only need to define the field name.
