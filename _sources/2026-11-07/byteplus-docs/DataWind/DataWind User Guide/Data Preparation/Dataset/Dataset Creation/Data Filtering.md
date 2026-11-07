---
title: "Data Filtering"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Filtering"
---

<span id="_1-概述"></span>
# 1. Overview

After [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL) and [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration) are completed, you can filter the data to ensure the dataset is accurate, queries are efficient, and avoid wasting unnecessary space. This section will introduce how to perform data filtering with the product.

DataWind supports filtering data from data sources, retaining only the data that meets specified criteria.

<span id="_2-功能介绍"></span>
# 2. Feature introduction


* You can configure multiple conditions as needed, supporting two levels of AND/OR logic, and configure both field conditions and expression conditions.

* As shown in the figure, the filtering logic configured for this dataset is: (app_version is between 2.21.0 and 2.26.0 and local_time_ms=server_time) or (app_version is 2.20.0 and app_language is cn)

> local_time_ms=server_time is the second condition in the figure below: local_time_ms=server_time is true


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/248eb539305242bb815dadf32b2920b9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-多层且或条件配置"></span>
## 2.1 Multi\-level AND/OR condition configuration

After adding a filter condition, click "+Field Condition" or "+Expression Condition" below to add a parallel condition.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72eea92aa9a44d65ae4ffa29ffc4e85f~tplv-goo7wpa0wc-image.image) </span>

When there are multiple filter conditions, click the outer "+Field Condition" or "+Expression Condition" to add a parallel condition group.

Click the AND/OR icon on the left side of the condition group to change the logic between conditions.

<span id="_2-2-字段条件与表达式条件"></span>
## 2.2 Field conditions and expression conditions

Field condition: After selecting a field, filter by the field value.

Expression condition: Write an expression to filter data where the expression equals a specified value. For example:

a. To filter data where the sum of two metrics is greater than 100: write the expression as Field A + Field B, and select \>100 as the value.

b. To filter data where the values of two metrics are equal: write the expression as Field A = Field B, and select true as the value.

<span id="_2-3-批量录入属性值"></span>
## 2.3 Batch entry of attribute values

When you need to enter a large number of attribute values in the filter attribute value section, you can click the batch upload field on the right and enter the list of attribute values in the following format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f1b651a39fa40fd8f4a11edc4c10d39~tplv-goo7wpa0wc-image.image) </span>
