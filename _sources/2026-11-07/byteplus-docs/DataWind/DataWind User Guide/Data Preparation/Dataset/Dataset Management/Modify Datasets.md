---
title: "Modify Datasets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Modify_Datasets"
---

<span id="_1-概述"></span>
# 1. Overview

The dataset module supports modifying dataset\-related configurations. Upstream tables allow you to add new fields, modify the data types of existing fields, and delete fields. In the data preview interface, you can quickly modify model fields. Modifying models and customizing SQL for SQL\-based charts are also supported.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-上游表新增-修改-删除字段"></span>
## 2.1 Add, modify, or delete fields in upstream tables

If "Auto\-refresh fields" is not enabled, you need to add fields manually. See below for details:

For example: Add a field xx to a MySQL table. On the preview page, click "Edit" to enter the model modification mode. Click the capsule at "Model configuration." The model list will display the new field as a gray, unchecked item. Select the field to add it.

For example: Modify the data type of an existing field in a MySQL table. On the preview page, click "Edit" to enter the model modification mode. After confirming the data type change, save it. The historical data corresponding to the original field type will be deleted.

Modifications do not change the data that has already been synchronized. To update the data, please resynchronize.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4849bfa9d0554e189c66e2f287b5f23d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-修改字段"></span>
## 2.2 Modify fields

In the data preview interface, you can quickly modify model fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b7741f337f04c6b9e31a85efddb63aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-修改模型"></span>
## 2.3 Modify models

Click the "Edit" button to enter the edit mode, where you can adjust the model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75e1c728ce184dafada94bd04ba73743~tplv-goo7wpa0wc-image.image) </span>

When modifying a model, replacing the underlying data table is supported. Modifying the primary key, sharding fields, partition fields, or sampling fields is not supported. To modify the above items, create a new dataset.

<span id="模型配置替换底表"></span>
### Replace the underlying table in model configuration

The product supports editing datasets and replacing the underlying table on the model configuration page. Currently, replacing the underlying table for direct\-connection datasets is not supported.

Right\-click the data table card, click the "Replace" button, and drag a data table from the left onto the card to complete the replacement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69167228925d4ee1bbf4c760e656bc8b~tplv-goo7wpa0wc-image.image) </span>

Note the following when using this feature:


* Fields with the same name in the new and original tables will directly replace the corresponding model fields, without affecting dataset fields. After saving, visual queries are not affected.

* For fields that exist in the new table but not in the original table, you can choose to add them to the model fields. By default, they will be added to the dataset fields.

* For fields that exist in the original table but not in the new table, please delete the corresponding fields on the field configuration page. If you save and retain only the fields that exist in the original table, the system will prompt the user that the corresponding fields cannot be found. If you confirm the replacement, the corresponding fields in the original dataset will be permanently deleted.

* Replacing the data table does not affect historical data. To import the replaced data table into the system, you need to resynchronize historical data by date.


<span id="_2-4-自定义-sql-修改"></span>
## 2.4 Custom SQL modification

Routine SQL\-based charts can be modified.

Click "Edit" to enter the modification interface. Click the "Edit" button in the interface to modify the SQL.

<span id="_2-5-调整生命周期"></span>
## 2.5 Adjust lifecycle

Click synchronization status to view the current dataset's lifecycle. Lifecycle: The retention period for data synchronized in the dataset. If the lifecycle is 3 days, then partitioned data generated on January 25 will be cleared on January 28. If the data is synchronized daily, only data synchronized within the past 3 days can be queried.

Click the pencil\-shaped edit button and confirm the changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90ea3edd834c481b8b8fc10e2cd461de~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-类目管理"></span>
## 2.6 Category management

**Dataset categories**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b960fc40d8c7436f8c6ac84a77e858b2~tplv-goo7wpa0wc-image.image) </span>

**Project\-level categories**

Unified management of dataset field categories within the project is supported. You can choose not to allow the creation of dataset categories.

<span id="_2-7-同步类型和-sla-更改"></span>
## 2.7 Synchronization type and SLA changes

Click synchronization status to view the current dataset's synchronization type. Synchronization types: Automatic synchronization—synchronizes automatically during system off\-peak hours each day, aiming to complete synchronization before the SLA; Scheduled synchronization—including synchronization at hourly, daily, weekly, or monthly intervals; Paused synchronization—the dataset will no longer synchronize automatically.

Click the pencil\-shaped edit button and confirm the changes. If the data source used by the dataset is a hive table, the editor must also have permission to view the hive table in order to successfully edit.
