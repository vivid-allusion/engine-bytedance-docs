---
title: "Field Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Field_Configuration_"
---

<span id="_1-概述"></span>
# 1. Overview

After [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation_) and completing [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration_), you may need to add complex calculated fields based on the model fields or perform other configurations.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-添加-修改字段"></span>
## 2.1 Add/modify fields


* For the field settings of [Dimensions and Metrics](https://docs.byteplus.com/docs/dataagent/Dimensions_and_Metrics_), follow the steps below to click "Expand edit box" and open a pop\-up window for field editing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70b727d723724505ad837b6e4ea41bd4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2c81a4d67f34757aa5771c1f9debf63~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51b844f2fe4940eba0d2f022925863c5~tplv-goo7wpa0wc-image.image) </span>

> The difference between data source fields and dataset fields can be simply understood as follows:

> * Data source fields are the actual fields written to the table and imported.

> * Dataset fields are logical fields that have been processed and modified from the original fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a186343b411e45d79615561ed1bc4c8d~tplv-goo7wpa0wc-image.image) </span>

For a detailed introduction to this feature, see: [Add or Modify Fields](https://docs.byteplus.com/docs/dataagent/Add_or_Modify_Fields_).

<span id="_2-2-修改维度指标"></span>
## 2.2 Modify dimensions and measures

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68be42a3d9f04bad8e83b3b779f2e382~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-排序字段"></span>
## 2.3 Sort fields

Supports flexible switching between two rules: data source order, and dimension\-first then measure order.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b762c4a73e0480ca279bb631c5b6cba~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-字段批量操作"></span>
## 2.4 Batch field operations

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c380b82197d04ca583f978231cb04311~tplv-goo7wpa0wc-image.image) </span>


* Batch synchronize part of the field description to the field name.

* Delete: Batch delete fields.

* Switch measure: Batch switch between dimension and measure types. If originally a dimension, switch to measure; if originally a measure, switch to dimension.

* Add category: Batch add to project\-level categories or dataset\-level categories.

* Set data format: Batch set data format. Options include auto, number, percentage, per mille, raw value, pp, and custom.

* Set data type: Batch set data type. Options include text, numeric, date, or datetime format.

* Move selected rows to specified row: Batch move selected rows to the specified row

* Set as hidden: After selecting multiple fields, if all selected items can have their visibility set, you can batch set the display fields to be clickable. After clicking, a settings panel appears below. The default aggregation method is unset (not selected), and you can select show or hide from the dropdown. After confirming, the hidden field status of the selected fields will be updated simultaneously.

* Add table name to field name: After selecting multiple fields, add their table names to the field names.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/284e738848664357965becdd027bb973~tplv-goo7wpa0wc-image.image) </span>


* Add table names to categories: Select multiple fields, and add their table names to categories


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca0f1636bfb142dfaef41b46dcfe8c58~tplv-goo7wpa0wc-image.image) </span>

<span id="89beeb7e"></span>
## 2.5 Category settings

Supports categorizing fields by setting categories, making it easier to search for them during visual queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5bf7233af15740269894d1a145f3c911~tplv-goo7wpa0wc-image.image) </span>

Click "Manage" to add categories. After adding categories, you can select a category in the category column of a field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fb89ce593d046e3baa10c0abc8dc2ea~tplv-goo7wpa0wc-image.image) </span>

In category management, you can set categories to be collapsed or expanded by default, which affects how dimensions and metrics configured with categories are displayed in Visual Query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35e75441db7e4f369719c2b52f816c53~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-更多配置"></span>
## 2.6 Field description

Supports adding and modifying field descriptions to help users understand fields. After enabling the custom button, users can customize field descriptions. When the custom button is disabled, field descriptions are synchronized with upstream table fields, making it easier to manage field descriptions across multiple downstream datasets of the same data table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/294fc8918421439a86aa227dc14ac8dd~tplv-goo7wpa0wc-image.image) </span>

<span id="9ab21579"></span>
## 2.7 More configurations


* Supports previewing the total number of fields, as well as the number of dimensions and metrics in the current dataset.

* Supports searching by field name keywords, suitable for scenarios with many fields.

* Supports deleting fields that do not need to be imported.

* Supports adjusting the order of fields and quickly moving fields to specified positions by row number.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28f500b12b37496ab1461e5ab422e06b~tplv-goo7wpa0wc-image.image) </span>
