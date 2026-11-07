---
title: "Dataset List Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_List_Management"
---

<span id="_1-数据集列表管理概述"></span>
# 1. Overview of dataset list management

The entire dataset interface can be divided into three modules: 1. dataset creation, 2. dataset management, and 3. dataset list. As shown in the figure below, area 3 is the dataset list. In the list area, users can perform multiple operations on datasets, including viewing basic information, moving, deleting, copying, and more. This article provides a detailed explanation of these features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdd49aac48cf4ab39ad03de9e9c532b6~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-功能介绍"></span>
# 2. Features

<span id="_2-1-基础信息"></span>
## 2.1 Basic information

Click "Basic Information" to configure the dataset's information, including the dataset name and description.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a67c5570f0b4fed8fcdd53c677d400d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edba67e6a3754240a3281b1bd0441e2c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-移动数据集"></span>
## 2.2 Move dataset

After clicking "Move", the dataset will be moved to another path (folder), allowing for better dataset management.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4668bebd4ff0457492161f60ede7f9a0~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-复制数据集"></span>
## 2.3 Copy dataset

Based on an existing dataset, users can quickly create a new dataset by cloning similar model configurations, filter conditions, and other settings, then modifying them as needed. This enables rapid batch setup of similar data models. Only extraction\-type datasets are supported for quick copying.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5daa7f2ad95148b7902418bf4a4e70a7~tplv-goo7wpa0wc-image.image) </span>

**Dataset copying principles**


* Copying dimensions and metrics only supports copying basic information; copying hierarchy and category is not supported.

* Synchronization task configurations of extraction\-type datasets can be copied.

* Permission configurations and the physical data of extraction\-type datasets are not copied.


**Common error messages**

If an exclamation mark appears on the dataset model configuration page after copying, it may indicate the following issues. The user can modify the configuration based on the cause to complete dataset creation.


* The user does not have permission for the model table.

* When copying across projects, the data connection does not exist or has been deleted.


<span id="_2-4-删除数据集"></span>
## 2.4 Delete dataset

The operation to delete a dataset can be accessed from the right side of the dataset on the dataset overview page, or by clicking the delete icon on the right side of the target dataset in the dataset preview interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eee32f053d1e4c178b39845b61648231~tplv-goo7wpa0wc-image.image) </span>

After clicking Delete, a corresponding pop\-up dialog will appear, prompting you to confirm whether you want to proceed with the deletion. You can click to view the lineage diagram to determine whether resources that use this dataset downstream are important and should not be deleted; you can also directly click Delete. In the privatized version, the pop\-up dialog provides an impact analysis, listing the number of charts and dashboards associated with this dataset and their access counts to help users assess the downstream impact after deletion.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68fcc617249e4c1296b61b7fe1676d6d~tplv-goo7wpa0wc-image.image) </span>

For deleted datasets, you can restore them directly from the Recycle Bin within 15 days; after 15 days, you can query the data model to reconstruct the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a24a9d542366465d85c1682b1099c2c5~tplv-goo7wpa0wc-image.image) </span>

To permanently delete this resource or restore it, click the "Recycle Bin" in the lower left corner to perform the operation. In the dataset interface within the Recycle Bin, there are two tabs: Restorable and Data Model Reconstruction.

To avoid negative impacts caused by accidental deletion, the "Data Model Reconstruction" option is provided, which supports querying model information for datasets deleted for more than 15 days (permanently deleted), making it easier for users to reconstruct them.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d017fd67a84418ab856e840214a4390~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-7-设置标签"></span>
## 2.5 Set tags

For details, see: [Tag Management](https://docs.byteplus.com/docs/dataagent/Tag_Management)

<span id="_2-8-授权"></span>
## 2.6 Authorization

In addition to the entry mentioned above, you can also click the dataset and then use the "Permission Assignment" button in the upper right corner of the details preview page to authorize the dataset. For details on authorization capabilities, see [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7cbba3d5674807955508072cbd34cb~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-9-转移所有者"></span>
## 2.7 Transfer ownership

After clicking "Transfer Ownership", the system will automatically redirect and display a pop\-up dialog prompting you to transfer ownership. Enter the recipient of the permissions in the dialog and click Confirm; the management permissions for this dataset will be transferred to the recipient.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bff5f9b974d42d7ad10cea55f133db9~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c818a00747b4b0c90f7ed42208bcfbd~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e668c81b7fcf4300ab9d31a6719ba439~tplv-goo7wpa0wc-image.image) </span>
