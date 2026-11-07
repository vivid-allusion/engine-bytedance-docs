---
title: "Field Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Fields_Configuration"
---

<span id="_1-概述"></span>
# 1. Overview

Since visual queries retrieve only the fields that are actually visible, after [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL) and completing [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration), you may need to add complex calculated fields based on the model fields or perform other configurations.

<span id="_2-功能介绍"></span>
# 2. Modify fields

After clicking Modify Fields, you will enter the modification page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13fdeebde6c0486081eb7d7dde853c9a~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4c59a5fd1fb4c969f542e26d5b80d88~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-添加-修改字段"></span>
## 2.1 Add/modify fields


* Similar to the add/modify field functionality in the visual query interface, click "Add Field" to go to the Add Field page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2f71d2267e944c68c683b514cd3f3fb~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a62833e1775e445194d9ab4e70643630~tplv-goo7wpa0wc-image.image) </span>


* Alternatively, under the field expression, click the following button to expand the editing box. A pop\-up window as shown above will appear for field editing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5346bbcd82e409ca1b5b5a10e172561~tplv-goo7wpa0wc-image.image) </span>

> The difference between data source fields and dataset fields can be simply understood as follows. For a detailed explanation, see [Data source fields and dataset fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields#d510d1e1)

> * Data source fields are the fields that are actually stored in the table and imported.

> * Dataset fields are logical fields that have been processed and modified from the original fields.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c887061660a441d39c650cff1ccec418~tplv-goo7wpa0wc-image.image) </span>

For a detailed introduction to this feature, see: [Add or Modify Fields](https://docs.byteplus.com/docs/DataWind/Add_or_Modify_Fields)

<span id="_2-2-修改维度指标"></span>
## 2.2 Modify dimensions and measures

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62d305ec43d746a5aaa2bc4c8e84f6aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-排序字段"></span>
## 2.3 Sort fields

Supports seamless switching between ordering by data source and by dimensions first, then measures.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62534ef89b454abba9980d733a239ad5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-字段批量操作"></span>
## 2.4 Batch operations on fields

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86373ec6fe2046b3859519e746bfbacf~tplv-goo7wpa0wc-image.image) </span>


* Batch set aggregation method


If a field is an aggregation function, the field is shown as aggregated. If the aggregation method can be modified, use the drop\-down box to make changes. The drop\-down box contains the available aggregation methods. After modification, the field names will be updated accordingly.

If there are non\-aggregated items among the selected measures, when you click Batch Set Aggregation Method, a settings panel appears below, and the default aggregation method is empty (not selected). After confirming, the aggregation method for non\-aggregated measures among the selected items will be modified and the field names will be updated accordingly.


* Batch set visual style


For chart types that support visual style configuration, after selecting multiple fields, you can click Batch Set Visual Style to configure them.


* Batch set display fields


After selecting multiple fields, if none of the selected items are restricted from being shown or hidden, you can click Batch Set Display Fields. After clicking, a settings panel appears below. The default aggregation method is empty (not selected), and the dropdown allows you to choose whether to show or hide it. After confirmation, the hidden status of multi\-select fields will be updated in sync.

<span id="89beeb7e"></span>
## 2.5 Category settings

Supports categorizing fields, making it easier to search during visual queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ece3ba7a8fb24f648ba803eeaaea7734~tplv-goo7wpa0wc-image.image) </span>

Click "Manage" to add categories. After adding a category, you can select a category in the category column of the field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c5fde9103f34c16905b0c9d0624ddb1~tplv-goo7wpa0wc-image.image) </span>

In category management, you can set categories to be collapsed or expanded by default, which affects how dimensions and metrics with configured categories are displayed in Visual Query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b58f00761f6442159a2cfecb0e912241~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-更多配置"></span>
## 2.6 Field description

Supports adding and modifying field descriptions to help users understand the fields. After enabling the custom button, field descriptions can be customized by the user. When the custom button is disabled, field descriptions are synchronized with upstream table fields, making it easier for users to manage field descriptions across multiple downstream datasets of the same data table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92162661130d4c1db85c1930298875fe~tplv-goo7wpa0wc-image.image) </span>

<span id="9ab21579"></span>
## 2.7 **Support one\-click update of downstream fields**

When a field is modified and there are downstream fields that depend on it, the system allows users to "one\-click synchronize and modify downstream fields" or manually modify erroneous fields as prompted, ensuring data consistency and efficient updates.

<span id="33918e43"></span>
## 2.8 More configuration options


* Supports previewing the total number of fields, as well as the number of dimensions and metrics in the current dataset.

* Supports searching by field name keywords, which is suitable for scenarios with many fields.

* Supports deleting fields that do not need to be imported.

* Supports adjusting the order of fields and quickly moving fields to a specified row number.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05473666718843759afaab508a5b70a5~tplv-goo7wpa0wc-image.image) </span>

<span id="7bcff2cf"></span>
# 3. Field mapping

When configuring a chart to replace a dataset, you need to configure a mapping relationship for each data source field. If the current chart has many fields and you frequently need to replace datasets for charts,

configuring field mappings one by one each time you replace a dataset can be very cumbersome and time\-consuming.

To this end, a field mapping configuration is provided, allowing the mapping relationships between fields of datasets to be preconfigured. When performing dataset replacement operations for charts involving these mapped datasets, the matching relationships will be automatically populated according to the mapping configuration, reducing operational costs.

**Step 1**: The configuration entry is located on the dataset details page. In the options at the top right corner, you can find "Field Mapping Configuration".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90db2012b04044c89e3dbd7e7bcd7ef6~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: First, add the target dataset for which you need to configure the mapping relationship.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec95b2a37c6043a4bf897d02d31dc011~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: Configure the mapping relationships between fields in the two datasets. Both data source matching and dataset matching are supported. For the effects of matching here, see [Replace Dataset](https://docs.byteplus.com/docs/DataWind/Replace_Dataset).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51dfcb5e5bac4a0a81f990c15c796f61~tplv-goo7wpa0wc-image.image) </span>

**Step 4**: Finally, click Save to complete the configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a8c6d3dbd0d44619ef8d0352ba522be~tplv-goo7wpa0wc-image.image) </span>

**Step 5**: After the field mapping configuration is completed, when replacing the chart of the current dataset with the target dataset, the mapped fields will be automatically populated in the matching relationships.

<span id="2908042d"></span>
# 4. Best practice


* When the partition field in the source table data of a dataset is of text or numeric type, you can modify the partition field settings to avoid full table scans during subsequent data queries and improve data query efficiency. For details, see [Practice for Configuring Partition Field Filtering in Direct Connection Datasets](https://docs.byteplus.com/docs/DataWind/Practice_for_Configuring_Partition_Field_Filtering_in_Direct_Connection_Datasets).
