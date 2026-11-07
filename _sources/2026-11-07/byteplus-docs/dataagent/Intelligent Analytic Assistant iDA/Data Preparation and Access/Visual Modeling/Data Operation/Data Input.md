---
title: "Data Input"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Input__"
---

<span id="_1-概述"></span>
# 1. Overview

Data input marks the beginning of the user's task processing for visual modeling. The user needs to select a specific data connection to obtain data input from the data source, and can then choose data cleansing operators or other processing methods.

<span id="_2-功能详解"></span>
# 2. Detailed functions

<span id="_2-1-数据输入处理"></span>
## 2.1 Data input processing

Taking data input via a MySQL data connection as an example, push the input dataset onto the canvas and click the input operator. The data source information will be displayed, and the extraction method can be set. Non\-partition field filtering can be performed. Currently, both "and" and "or" filtering logic are supported, allowing users to freely filter data based on the data source. Additionally, extraction parameters, the amount of preview data, and more can be set.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6c6103cf0aa4dbcb687b2fd2a9403dc~tplv-goo7wpa0wc-image.image) </span>

After completing the basic data input processing, users can further select data cleansing or feature engineering operators to achieve diverse data processing and transformation.

<span id="_2-2-自定义sql"></span>
## 2.2 Custom SQL

Visual modeling supports custom SQL for most offline\-stored data inputs, enabling basic data processing. During the data connection step when creating a task, if the user selects a dataset, the left canvas will display: custom SQL (visible for offline tasks), visual modeling dataset, intelligent data insight dataset, and customer data platform dataset (if the product is purchased and deployed). The introduction to custom SQL is as follows:


* **Hive**/**ClickHouse** custom SQL:

   * Hive: When visual modeling outputs and stores data as a Hive\-type dataset, SQL can be written as long as it complies with Hive syntax.

   * ClickHouse: When visual modeling outputs and stores data as a ClickHouse dataset, SQL can be written as long as it complies with ClickHouse syntax.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d352f8d6bcd4a62889f1528a2bafae7~tplv-goo7wpa0wc-image.image) </span>

In the custom SQL configuration interface of visual modeling, users can rename, add descriptions, copy, delete, and more. When used as the first operator node, "execute this node", "execute to this point", and more are not supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92fd6e7f7e4040a2a11f4624740c4aaf~tplv-goo7wpa0wc-image.image) </span>

In the editing area, a library of common functions is provided for you, including descriptions of function usage, command formats, examples, and so on.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03213a74581d4847a64dbcbbac2b2fe9~tplv-goo7wpa0wc-image.image) </span>

After editing is complete, users can set the amount of data for preview calculation, customize the row data or use all data, and then click the "Data Preview" on the far right to view.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/796b73c91a1e4ac79eb3a5c3abf1ac10~tplv-goo7wpa0wc-image.image" width="2940px" /></div>
