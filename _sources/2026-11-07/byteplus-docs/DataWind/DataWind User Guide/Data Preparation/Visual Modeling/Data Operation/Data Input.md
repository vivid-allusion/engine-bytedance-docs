---
title: "Data Input"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Input"
---

<span id="_1-概述"></span>
# 1. Overview

Data input is the starting point for task processing in visual modeling. Users need to select a data connection to obtain data input from a data source, after which they can choose data cleansing operators or other processing methods.

<span id="_2-功能详解"></span>
# 2. Functional details

<span id="_2-1-数据输入处理"></span>
## 2.1 Data input processing

For example, when using a MySQL data connection for data input, drag the input dataset onto the canvas and click the input operator. You can view the data source information, set the extraction method, and filter by non\-partition fields. Currently, both 'AND' and 'OR' filtering logic are supported, allowing users to further filter data as needed based on the data source. In addition, extraction parameters and the amount of data to preview can also be set.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2ebce0120d04d729ff14f4524b47365~tplv-goo7wpa0wc-image.image) </span>

After completing the basic data input processing, users can further select data cleansing or feature engineering operators to perform diverse data processing and transformation.

<span id="_2-2-自定义sql"></span>
## 2.2 Custom SQL

Visual modeling supports custom SQL for data input from most offline storage, enabling basic data processing. During the data connection step when creating a task, if the user selects a dataset, the left canvas will display: Custom SQL (available for offline tasks), visual modeling dataset, intelligent data insight dataset, and customer data platform dataset (if the product is also purchased and deployed). The introduction to custom SQL is as follows:


* **Hive**/**ClickHouse** custom SQL:

   * Hive: When visual modeling outputs and stores data as a Hive\-type dataset, you can write SQL as long as it complies with Hive syntax.

   * ClickHouse: When visual modeling outputs and stores data as a ClickHouse dataset, you can write SQL as long as it complies with ClickHouse syntax.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3427b9185b624e29a77bc938793d9fd6~tplv-goo7wpa0wc-image.image) </span>

In the custom SQL configuration interface of visual modeling, users can rename, add descriptions, copy, and delete. When used as the first operator node, 'Execute this node' and 'Execute to this point' are not supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87362ef2f2f643bd85e2cebbd942282b~tplv-goo7wpa0wc-image.image) </span>

A library of common functions has been prepared for you in the editing area, including usage instructions, command formats, examples, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a64f1a8aa3b4733bb295b71ff3b0217~tplv-goo7wpa0wc-image.image) </span>

After editing is complete, the user can set the amount of data to preview for calculation, customize the data to preview by selecting either row data or all data, and then click “Data Preview” on the far right to view the results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87a6c569b80249d88c725cca9ea656b3~tplv-goo7wpa0wc-image.image) </span>
