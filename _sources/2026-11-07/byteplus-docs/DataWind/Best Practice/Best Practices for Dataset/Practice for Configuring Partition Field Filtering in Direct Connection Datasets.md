---
title: "Practice for Configuring Partition Field Filtering in Direct Connection Datasets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Practice_for_Configuring_Partition_Field_Filtering_in_Direct_Connection_Datasets"
---

After creating a direct connection dataset, to avoid full table scans on partitioned tables during subsequent dataset queries, you need to filter data based on partition fields when querying. This article describes how to configure partition fields for direct connection datasets that are based on partitioned tables, in order to improve filtering efficiency during subsequent data queries.

<span id="ecb4360c"></span>
# Prerequisites

A direct connection dataset has been created, and the data table in the source data engine is a partitioned table. For details on how to create a dataset, see [Dataset Creation Overview](https://docs.byteplus.com/docs/DataWind/Dataset_Creation_Overview).

<span id="dbd99fd0"></span>
# Configure dataset partition fields


1. After creating the corresponding direct connection dataset, go to the dataset details page and click the "Edit" button in the upper right corner to enter the dataset editing page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/879f6be5a83e4366a4db50599145defd~tplv-goo7wpa0wc-image.image) </span>


2. On the dataset editing page, click the "Field settings" button in the upper right corner to go to the field settings page, and then modify the partition fields of text or numeric type.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b9a1ec105dd4082a0bbc35c04a4afe0~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration description |
|---|---|
|Data type |Change the data format of partition fields of text or numeric type to "Date" type. |
|Expression |Modify the expression of partition fields of text or numeric types to convert the field to a date type. The expression configuration for conversion formats varies between different types of engines. Refer to the documentation for the corresponding engine for configuration details. The following are configuration examples for some common engines (in the examples, `order_date` is a sample partition field name; you need to replace it with the actual field name).<br><br><br>* clickhouse: `cast(order_date as Date)`, or `toDate(order_date)`<br><br>* hetu：`cast(order_date as date)`<br><br>* doris: `cast(order_date as date)`, or `date(order_date)`<br><br>* opengauss：`cast(order_date as date)`<br><br>* gaussdws：`CAST( order_date AS DATE FORMAT 'YYYY-MM-DD' )` |
|Set partitions |Set the corresponding field as a partition field in the operation column. |



3. (Optional) Modify the field name. Since the above operation involves converting the field type using a field expression, it is recommended to modify the field name.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9388995e71c4a20bc09c1008c79f2c7~tplv-goo7wpa0wc-image.image) </span>

If you do not modify the field name, when saving the dataset, the interface will prompt a field name exception. You can also choose not to modify the field name and select "Save anyway" at this point.

<span id="0f5e06b4"></span>
# Application example: Quickly filter partition fields

After completing the above configuration, you can conveniently filter data based on the configured partition fields when querying the corresponding dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b3812bbc84944038fe347e34abdc713~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, on the visual query page, the configured partition fields are automatically added to the filter configuration results, and you can conveniently select the date range to filter using the date component.
