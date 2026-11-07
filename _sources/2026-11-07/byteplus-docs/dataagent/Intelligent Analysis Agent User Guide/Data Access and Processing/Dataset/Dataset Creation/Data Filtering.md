---
title: "Data Filtering"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Filtering"
---

<span id="_1-概述"></span>
# 1. Overview

After [Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL) and [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration) are completed, data can be filtered to ensure the dataset is accurate, queries are efficient, and unnecessary space is saved. This section describes how the product performs data filtering.

DataAgent supports filtering data from data sources, retaining only the data that meets the specified criteria.

<span id="_2-功能介绍"></span>
# 2. Feature introduction


* Multiple conditions can be configured as needed, supporting two\-level AND/OR logic, as well as field conditions and expression conditions.

* As shown in the figure, the filtering logic configured for this dataset is: (app_version between 2.21.0 and 2.26.0 and local_time_ms=server_time) or (app_version is 2.20.0 and app_language is cn)

> local_time_ms=server_time is the second condition in the figure below: local_time_ms=server_time is true


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbcab76abb50450fad3c8b5b0076c16f~tplv-goo7wpa0wc-image.image" width="2132px" /></div>


<span id="_2-1-多层且或条件配置"></span>
## 2.1 Multi\-level AND/OR condition configuration

After adding a filter condition, click "+Add" below to add additional conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bcc593834154272b3b7c46c7f74ecbd~tplv-goo7wpa0wc-image.image" width="610px" /></div>


When multiple filter conditions exist, click the outer "+Field Condition" or "+Expression Condition" to add additional condition groups.

Click the AND/OR icon on the left side of the condition group to change the AND/OR logic between conditions.

<span id="_2-2-字段条件与表达式条件"></span>
## 2.2 Field conditions and expression conditions

Field condition: After selecting a field, filter by the field value.

Expression condition: Write an expression to filter data where the expression equals a specified value. For example:

a. To filter data where the sum of two metrics is greater than 100: write the expression as Field A + Field B, and select \>100 as the value.

b. To filter data where two metric values are equal: write the expression as Field A = Field B, and select true as the value.

<span id="_2-3-批量录入属性值"></span>
## 2.3 Batch entry of attribute values

When you need to enter a large number of attribute values in the attribute value filtering section, you can click the batch upload field on the right and enter the list of attribute values in the following format.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/720532ccc6074df3bed9023c00bfc534~tplv-goo7wpa0wc-image.image) </span>
