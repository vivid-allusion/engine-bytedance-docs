---
title: "Dataset List Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_List_Management"
---

<span id="_1-数据集列表管理概述"></span>
# 1. Overview of dataset list management

The entire dataset interface can be divided into three modules: 1, dataset creation; 2, dataset management; and 3, dataset list. As shown in the figure below, area 3 is the dataset list. In the list area, users can perform many operations on datasets, including viewing basic information, moving, deleting, copying, and more. This document provides a detailed explanation of these features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8233558533b442e6a9fca659f2610f61~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-基础信息"></span>
## 2.1 Basic information

Click Basic Information to set the dataset's information, including the dataset name and description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6493c4071f4b4df4ac915d567b213e5d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0907029c14104865a03abfe8d9d08069~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-移动数据集"></span>
## 2.2 Move dataset

After clicking Move, the dataset will be moved to another path (folder) within the dataset structure, allowing users to manage the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22b3296f8417438aa627e9e49445ae55~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-复制数据集"></span>
## 2.3 Copy dataset

Based on an existing dataset, users can quickly create a new dataset by cloning similar model configurations, filter conditions, and other settings, then modifying them as needed. This enables rapid batch setup of similar data models.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ace4bf2ab214126b29fda75cf9410fd~tplv-goo7wpa0wc-image.image) </span>

**Dataset copy principles**


* Copying dimension metrics only supports copying basic information and does not support copying hierarchies or categories.

* When copying an extraction\-type dataset, only the synchronization task configuration of the extraction\-type dataset is copied; the dataset's permission configuration and the physical data of the extraction\-type dataset are not copied.


**Common error messages**

If an exclamation mark appears on the model configuration page of the copied dataset, it indicates an error, which may be caused by the following reasons. The user can modify the configuration according to the cause to complete dataset creation.


* The user does not have permission for the model table

* When copying across projects, the data connection does not exist or has been deleted


<span id="_2-4-删除数据集"></span>
## 2.4 Delete dataset

The operation to delete a dataset can be accessed from the right side of the dataset on the dataset overview page, or by clicking the delete icon on the right side of the target dataset in the dataset preview interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1015c42fa3614a87a417233e374d0f18~tplv-goo7wpa0wc-image.image) </span>

After clicking Delete, a corresponding pop\-up prompt will appear to confirm whether to proceed with deletion. You can click [Lineage View](https://docs.byteplus.com/docs/DataWind/Lineage_View) to check whether the resources used by subsequent applications of this dataset are important and cannot be deleted. Alternatively, you can directly click Delete. In the private deployment version, a pop\-up window will provide an impact analysis, listing the number of charts and dashboards associated with this dataset as well as their access counts, to help users assess the downstream impact after deletion.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f30ed637ced4134875782264c7656f0~tplv-goo7wpa0wc-image.image) </span>

Deleted datasets can be restored directly from the Recycle Bin within 15 days; after 15 days, the dataset can be rebuilt by querying the data model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a32dfcc46a154e48a70117edef0b98ba~tplv-goo7wpa0wc-image.image) </span>

To permanently delete or restore this resource, click the "Recycle Bin" in the lower left corner and proceed with the operation. On the dataset page in the Recycle Bin, there are two tabs: Recycle Bin_Restore and Query Data Model_Rebuild.

To avoid negative impacts caused by accidental deletion, version V2.58.0 and later added the "Query Data Model_Rebuild" option, which supports querying model information for datasets deleted for more than 15 days (permanently deleted), making it easier for users to rebuild them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c076ab6d13c46a59767ce2b7ed505f6~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-可视化查询配置"></span>
## 2.5 Visual query configuration

For details, see: [Visual Query Configuration for Datasets](https://docs.byteplus.com/docs/DataWind/Visual_Query_Configuration_for_Datasets).

<span id="_2-7-设置标签"></span>
## 2.6 Set tags

For details, see: [Tag Management](https://docs.byteplus.com/docs/DataWind/Tag_Management).

<span id="_2-8-授权"></span>
## 2.7 Authorization

In addition to the above entry, you can also authorize this dataset by clicking the "Permission Assignment" button in the upper right corner of the details preview page after selecting the dataset. For details on authorization capabilities, see [Detailed Explanation of Permission Features](https://docs.byteplus.com/docs/DataWind/Detailed_Explanation_of_Permission_Features).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ed7be6e29504dc0933bd4c6422e58ca~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-9-转移所有者"></span>
## 2.9 Transfer ownership

After clicking, the system will automatically redirect and display a pop\-up window prompting you to transfer ownership. Enter the new owner's information in the box and click Confirm to transfer the management permissions of this dataset to the new owner.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b255f826937a41c5a04f74ee8bdbfd9b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42eecabe819f4fbf946ce59801ba3659~tplv-goo7wpa0wc-image.image) </span>
