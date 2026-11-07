---
title: "Dataset List Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_List_Management_"
---

<span id="_1-数据集列表管理概述"></span>
# 1. Overview of dataset list management

The entire dataset interface can be divided into three modules: 1 dataset creation, 2 dataset management, and 3 dataset list. As shown in the figure below, area 3 is the dataset list. In the list area, users can perform various operations on datasets, including viewing basic information, moving, deleting, copying, and other operations. This article provides a detailed explanation of these features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdd49aac48cf4ab39ad03de9e9c532b6~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-基础信息"></span>
## 2.1 Basic information

Click Basic Information to configure the dataset's information, including the dataset name and a description of the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a67c5570f0b4fed8fcdd53c677d400d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edba67e6a3754240a3281b1bd0441e2c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-移动数据集"></span>
## 2.2 Move dataset

After clicking Move, the dataset will be moved to another path (folder) under datasets, allowing users to manage the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4668bebd4ff0457492161f60ede7f9a0~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-复制数据集"></span>
## 2.3 Copy dataset

Based on an existing dataset, quickly create a new dataset by cloning similar model configurations, filter conditions, and other settings, then modifying them as needed. This enables rapid batch creation of similar data models. Only extraction\-type datasets are supported for quick copying.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5daa7f2ad95148b7902418bf4a4e70a7~tplv-goo7wpa0wc-image.image) </span>

**Dataset copy principles**


* Copying dimension metrics only supports copying basic information and does not support copying hierarchies or categories.

* Copy synchronization task configurations of extraction\-type datasets

* Do not copy dataset permission configurations or the physical data of extraction\-type datasets


**Common error messages**

If an exclamation mark appears indicating an exception on the model configuration page of the copied dataset, it may be due to the following reasons. The user can modify the configuration according to the reason to complete dataset creation.


* The user does not have permission for the model table

* When copying across projects, the data connection does not exist or has been deleted


<span id="_2-4-删除数据集"></span>
## 2.4 Delete dataset

The operation to delete a dataset can be accessed from the right side of the dataset on the dataset overview page, or by clicking the delete icon on the right side of the target dataset in the dataset preview interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eee32f053d1e4c178b39845b61648231~tplv-goo7wpa0wc-image.image) </span>

After clicking Delete, a corresponding pop\-up will appear to confirm whether you want to proceed with the deletion. You can click to view the lineage view to determine whether the resources that use this dataset downstream are important and should not be deleted; you can also click Delete directly. In the privatized version, the pop\-up will provide an impact analysis, listing the number of charts and dashboards associated with this dataset and their access counts to help users assess the downstream impact after deletion.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68fcc617249e4c1296b61b7fe1676d6d~tplv-goo7wpa0wc-image.image) </span>

For deleted datasets, you can restore them directly from the Recycle Bin within 15 days; after 15 days, you can query the data model to reconstruct the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a24a9d542366465d85c1682b1099c2c5~tplv-goo7wpa0wc-image.image) </span>

To permanently delete or restore this resource, click the "Recycle Bin" in the lower left corner and proceed with the operation. On the dataset page in the Recycle Bin, there are two tabs: Restorable and Query Data Model Reconstruction.

To avoid negative impacts caused by accidental deletion, the "Query Data Model Reconstruction" option is provided, which allows users to query the model information of datasets deleted for more than 15 days (permanently deleted) to facilitate reconstruction.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d017fd67a84418ab856e840214a4390~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-设置标签"></span>
## 2.5 Set tags

For details, see [Tag Management](https://docs.byteplus.com/docs/dataagent/Tag_Management_).

<span id="_2-8-授权"></span>
## 2.6 Authorization

In addition to the above entry, you can also click the dataset and then click the "Permission Assignment" button in the upper right corner of the details preview page to authorize the dataset. For details on authorization capabilities, see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7cbba3d5674807955508072cbd34cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-9-转移所有者"></span>
## 2.7 Transfer owner

After clicking "Transfer Owner", the system will automatically redirect and display a pop\-up to prompt for ownership transfer. Enter the permission recipient in the box and click Confirm to transfer the management permissions of this dataset to the recipient.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bff5f9b974d42d7ad10cea55f133db9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c818a00747b4b0c90f7ed42208bcfbd~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e668c81b7fcf4300ab9d31a6719ba439~tplv-goo7wpa0wc-image.image) </span>
