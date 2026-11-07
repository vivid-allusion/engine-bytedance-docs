---
title: "Field Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Field_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

After [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation) and completing [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration), you may need to add complex calculated fields based on the model fields or perform other configurations.

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-添加-修改字段"></span>
## 2.1 Add or modify fields


* To configure fields for [Dimensions and Metrics](https://docs.byteplus.com/docs/dataagent/Dimensions_and_Metrics), click "Expand edit box" as shown below to open a pop\-up window for field editing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70b727d723724505ad837b6e4ea41bd4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a186343b411e45d79615561ed1bc4c8d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbad2315d4c444f8927e3b371964f511~tplv-goo7wpa0wc-image.image) </span>

> The difference between data source fields and dataset fields can be simply understood as follows:

> * Data source fields are the actual fields stored in tables and imported.

> * Dataset fields are logical fields that have been processed or modified from the original fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e47bf94e7fa74e9797437cdac943a768~tplv-goo7wpa0wc-image.image) </span>

For a detailed introduction to this feature, see: [Add or Modify Fields](https://docs.byteplus.com/docs/dataagent/Add_or_Modify_Fields).

<span id="_2-2-修改维度指标"></span>
## 2.2 Modify dimensions and measures

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68be42a3d9f04bad8e83b3b779f2e382~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-排序字段"></span>
## 2.3 Sort fields

Supports flexible switching between data source order and the rule of dimensions first, then measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b762c4a73e0480ca279bb631c5b6cba~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-字段批量操作"></span>
## 2.4 Batch field operations

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c380b82197d04ca583f978231cb04311~tplv-goo7wpa0wc-image.image) </span>


* Sync description to field name: Batch sync part of the field description to the field name.

* Delete: Batch delete fields.

* Switch measure: Batch switch between dimension and measure types. If the original type is dimension, switch to measure; if the original type is measure, switch to dimension.

* Add category: Batch add to project\-level categories or dataset\-level categories.

* Set data format: Batch set data format. Options include auto, number, percentage, per mille, raw value, pp, and custom.

* Set data type: Batch set data type. Options include text, numeric, date, or datetime format.

* Move selected rows to specified row: Batch move selected rows to the specified row

* Set as hidden: After selecting multiple fields, if none of the selected items are restricted from showing or hiding, you can batch set the display status of the fields. After clicking, a settings panel appears below. The default aggregation method is empty (not selected). You can select show or hide from the dropdown. After confirming, the hidden field status of the selected fields will be updated synchronously.

* Add table name to field name: After selecting multiple fields, add their table names to the field names.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/284e738848664357965becdd027bb973~tplv-goo7wpa0wc-image.image) </span>

* Add table names to categories: Select multiple fields to add their table names to categories

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca0f1636bfb142dfaef41b46dcfe8c58~tplv-goo7wpa0wc-image.image) </span>


<span id="89beeb7e"></span>
## 2.5 Category settings

Fields can be grouped by category, making them easier to retrieve during visual queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bf7233af15740269894d1a145f3c911~tplv-goo7wpa0wc-image.image) </span>

Click "Manage" to add categories. Once categories are added, you can select a category in the category column for each field.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fb89ce593d046e3baa10c0abc8dc2ea~tplv-goo7wpa0wc-image.image" width="2684px" /></div>


In category management, you can set categories to be collapsed or expanded by default, which affects how dimensions and metrics with assigned categories are displayed in Visual Query.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35e75441db7e4f369719c2b52f816c53~tplv-goo7wpa0wc-image.image" width="2686px" /></div>


<span id="_2-5-更多配置"></span>
## 2.6 Field description

You can add or modify field descriptions to help users understand each field. When the custom button is enabled, field descriptions can be customized by users. When the custom button is disabled, field descriptions are synchronized with upstream table fields, making it easier to manage field descriptions across multiple downstream datasets from the same data table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/294fc8918421439a86aa227dc14ac8dd~tplv-goo7wpa0wc-image.image) </span>

<span id="9ab21579"></span>
## 2.7 More configuration options


* You can preview the total number of fields, as well as the number of dimensions and metrics in the current dataset.

* You can search for fields by entering keywords in the field name, which is useful when there are many fields.

* Fields that do not need to be imported can be deleted.

* You can adjust the order of fields and quickly move fields to a specified position by row number.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e51a0ca119d4d92ac29c9db49628f27~tplv-goo7wpa0wc-image.image) </span>
