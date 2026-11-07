---
title: "Modify a Dataset"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Modify_a_Dataset_"
---

<span id="_1-概述"></span>
# 1. Overview

The dataset module supports modifying dataset\-related configurations. Upstream tables support adding fields, modifying the data types of existing fields, or deleting fields. In the data preview interface, you can quickly modify model fields. Modifying the model is also supported.

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-上游表新增-修改-删除字段"></span>
## 2.1 Add, modify, or delete fields in upstream tables

If "Auto refresh fields" is not enabled, you must add fields manually. See the following method:

For example: Add a field named xx to a MySQL table. On the preview page, click "Edit" to enter model modification. Click the capsule\-shaped button at "Model configuration"; a gray, unchecked field will appear in the model list. Select to retain the field, which will add it.

For example: Modify the data type of an existing field in a MySQL table. On the preview page, click "Edit" to enter model modification. After confirming the data type change, save your changes. The historical data corresponding to the original field type will be deleted.

After modification, previously synchronized data content will not be changed. To update the data, please synchronize again.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a60a267ae49412a86314f021546c2f7~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-修改字段"></span>
## 2.2 Modify fields

In the data preview interface, you can quickly modify model fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15a3c9e14f6d40b4b68176fa7c4d53a9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-修改模型"></span>
## 2.3 Modify the model

Click the "Edit" button to enter the global modification interface, where you can adjust the model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9881d051a1fe4963a4090d3f9d0465b1~tplv-goo7wpa0wc-image.image) </span>

Model modification supports replacing the underlying data table, but does not support modifying the primary key, shard, partition, or sampling fields. To modify the above items, create a new dataset.

<span id="模型配置替换底表"></span>
### Replace the underlying table in model configuration

The product supports editing datasets and replacing the underlying table on the model configuration page. Currently, directly connected datasets do not support replacing the underlying table.

Right\-click the data table card, click the "Replace" button, and drag the data table from the left onto the card to complete the replacement.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1216282267cb4d6d953bbcbdb8b8a42e~tplv-goo7wpa0wc-image.image) </span>

Note the following when using this feature:


* Fields with the same name in the new and original tables will directly replace the model fields without affecting dataset fields. Saving will not affect visual queries.

* For fields that exist in the new table but not in the original table, you can choose to add them to the model fields; by default, they will be added to the dataset fields.

* For fields that exist in the original table but not in the new table, please delete the corresponding fields on the field configuration page. If you save and retain only the fields that exist in the original table, the system will prompt the user that the corresponding fields cannot be found. If you confirm the replacement, the corresponding fields in the original dataset will be permanently deleted.

* Replacing the data table does not affect historical data. To import the replaced data table into the system, you need to resynchronize historical data by date.


<span id="_2-4-自定义-sql-修改"></span>
## 2.4 Custom SQL modification

Charts generated from routine SQL queries support modification.

Click "Edit" to enter the modification interface. Click the "Edit" button in the interface to modify SQL.

<span id="_2-5-调整生命周期"></span>
## 2.5 Adjust lifecycle

Click synchronization status to view the current dataset's lifecycle. Lifecycle: The retention period for data synchronized in the dataset. If the lifecycle is 3 days, partitioned data generated on January 25 will be cleared on January 28. If the data is synchronized daily, only data synchronized within the past 3 days can be queried.

Click the edit button (pencil icon) and confirm the changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63944a4730c4483b9ccbe6e81aa7c728~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-类目管理"></span>
## 2.6 Category management

**Dataset categories**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ccda03bc04b437384a299ddbfb334d6~tplv-goo7wpa0wc-image.image) </span>

**Project\-level categories**

Unified management of dataset field categories within the project. You can choose to disallow the creation of dataset categories.

<span id="_2-7-同步类型和-sla-更改"></span>
## 2.7 Synchronization type and SLA changes

Click synchronization status to view the current dataset's synchronization type. Synchronization type: Automatic synchronization—automatically synchronizes daily during system off\-peak hours, aiming to complete synchronization before the SLA; Scheduled synchronization—including synchronization at hourly, daily, weekly, or monthly intervals; Paused synchronization—the dataset will no longer synchronize automatically.

Click the edit button (pencil icon) and confirm the changes. If the data source used by the dataset is a hive table, the editor must also have permission to view the hive table in order to edit successfully.
