---
title: "Data Filtering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Filtering_"
---

<span id="_1-概述"></span>
# 1. Overview

[Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL_)After completing [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration_), you can filter the data to ensure the dataset is accurate, queries are efficient, and unnecessary space is saved. This section will introduce how the product performs data filtering.

DataAgent supports filtering data from data sources, retaining only the data that meets specified criteria.

<span id="_2-功能介绍"></span>
# 2. Features


* You can configure multiple conditions as needed, supporting two layers of AND/OR logic, and configure both field conditions and expression conditions.

* As shown in the figure, the filtering logic configured for this dataset is: (app_version between 2.21.0 and 2.26.0 AND local_time_ms=server_time) OR (app_version is 2.20.0 AND app_language is cn)

> local_time_ms=server_time is the second condition in the figure: local_time_ms=server_time is true


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbcab76abb50450fad3c8b5b0076c16f~tplv-goo7wpa0wc-image.image" width="2132px" /></div>


<span id="_2-1-多层且或条件配置"></span>
## 2.1 Multi\-layer AND/OR condition configuration

After adding a filtering condition, click the “+ Field condition” or “+ Expression condition” button below to add additional conditions at the same level.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bcc593834154272b3b7c46c7f74ecbd~tplv-goo7wpa0wc-image.image" width="610px" /></div>


When multiple filtering conditions exist, click the outer “+ Field condition” or “+ Expression condition” button to add additional condition groups at the same level.

Click the AND/OR icon on the left side of the condition group to change the logical relationship between conditions.

<span id="_2-2-字段条件与表达式条件"></span>
## 2.2 Field conditions and expression conditions

Field condition: After selecting a field, filter by the field value.

Expression condition: Write an expression to filter data where the expression equals a specified value. For example:

a. To filter data where the sum of two metrics is greater than 100: write the expression as Field A + Field B, and set the value to \>100

b. To filter data where two metric values are equal: write the expression as Field A = Field B, and set the value to true

<span id="_2-3-批量录入属性值"></span>
## 2.3 Batch entry of attribute values

When you need to enter a large number of attribute values in the attribute value filtering section, you can click the batch upload field on the right and enter the list of attribute values in the format shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/720532ccc6074df3bed9023c00bfc534~tplv-goo7wpa0wc-image.image) </span>
