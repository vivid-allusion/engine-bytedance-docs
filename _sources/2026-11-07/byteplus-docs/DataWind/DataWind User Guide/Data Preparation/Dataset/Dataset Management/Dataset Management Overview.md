---
title: "Dataset Management Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Management_Overview"
---

<span id="_1-数据集管理概述"></span>
# 1. Overview of dataset management

The entire dataset interface is divided into three modules: 1 dataset creation, 2 dataset management, and 3 dataset list. As shown in the figure below, the green area labeled 2 represents dataset management. In the dataset detail management area, users can perform various operations on the dataset, including data preview, synchronization status, model information, lineage view, row and column permissions, and more. This article will provide a detailed explanation of these features.

\**For direct connection dataset data readiness configuration, see section 2.10*

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70934e5e978b4ccaa7591b9d5f6de55c~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-数据集管理说明"></span>
# 2. Dataset management instructions

<span id="_2-1-数据集信息"></span>
## 2.1 Dataset information

Basic dataset information: owner, most recent synchronization time, dataset size, and access popularity.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31145b3ca10942799c965933416fd71f~tplv-goo7wpa0wc-image.image) </span>

The top section supports the following operations:


* Permission assignment: Assign permissions to the dataset.

* Visual query: Quickly navigate to the visual query page to query the current dataset.

* Edit: Edit and modify the dataset configuration.

* More:

   * Cross\-project configuration: Configure mirrored datasets. For more information, see [Mirror Dataset](https://docs.byteplus.com/docs/DataWind/Mirror_Dataset).

   * Attribution analysis configuration: Configure attribution analysis dimensions for the dataset. For more information, see [Intelligent Attribution](https://docs.byteplus.com/docs/DataWind/Intelligent_Attribution).

   * Transfer owner: Allows transferring ownership of the dataset.

   * Transfer alert recipient: Allows transferring the alert recipient of the dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d666a64c17e04989babda0b154e2460e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-数据预览"></span>
## 2.2 Data preview

Supports two preview structures: detailed data and table structure.


* Detailed data (no data preview available when synchronization fails).

   Note: The preview is only a sample result, providing users with an approximate format of the data and does not represent the exact result. To view precise detailed results, please go to [Visual Query Overview](https://docs.byteplus.com/docs/DataWind/Visual_Query_Overview).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e71cfa035934e82b210148380ff47ec~tplv-goo7wpa0wc-image.image) </span>


* Table structure


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b221b876d354b04b3e7f6dcb0fae79a~tplv-goo7wpa0wc-image.image) </span>

Supports editing field information. Click [Edit field] to enter field information editing mode. For more operation guidelines, see [Field Configuration](https://docs.byteplus.com/docs/DataWind/Fields_Configuration).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29e725da5001403b8db59dead9d4b3bd~tplv-goo7wpa0wc-image.image) </span>

Supports entering keywords to search for field names.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2605a45d89444649a713abdd7a4f4c18~tplv-goo7wpa0wc-image.image) </span>

Supports specifying filter conditions to preview target data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1369b36c97d45ffb28a0238e0d05d83~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-同步状态"></span>
## 2.3 Synchronization status

You can view the current status, operation view, and synchronization log to stay updated on specific progress in real time.

Supports filtering tasks by specific business date, synchronization status, and data result equal to 0.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17121feb1422434c8fbaab807d4a5768~tplv-goo7wpa0wc-image.image) </span>

Supports resynchronization for a single instance and batch data synchronization.


* Single instance resynchronization


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/548a3515d28c4f4ca95358c6a5098d35~tplv-goo7wpa0wc-image.image) </span>


* Batch data synchronization


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a22fb114acd14e74b15699ce255c8bc0~tplv-goo7wpa0wc-image.image) </span>

Supports viewing and modifying detailed synchronization configurations. For more operation instructions, see [Synchronization Settings](https://docs.byteplus.com/docs/DataWind/Synchronization_Setting).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98ada20d814c4095ba30659091f39d8f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-模型信息"></span>
## 2.4 Model information

View model settings information: model composition, filter conditions, and performance settings. Click the capsule to view specific field information. For more operation instructions, see [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1184ef14bd245aa88da23c5ae482d61~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-血缘信息"></span>
## 2.5 Lineage information

View the usage of the current dataset, including which dashboards it is used in, which charts it is applied to, and statistical information about related resources.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1da9ecee92264f8da7555e60ce7ea92e~tplv-goo7wpa0wc-image.image) </span>

Supports downloading lineage information as a file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/039f2055b7bf405ea954a18bc4b74689~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-excel-批量修改"></span>
## 2.6 Excel batch editing

Supports one\-click download of the current table structure information as a file, and allows users to batch edit dimensions/metrics, field names, field expressions, remarks, and more. Supports batch addition of new fields.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5ed0ac0385641ea80a18c8ffdbf2ed1~tplv-goo7wpa0wc-image.image) </span>

(1) Click to enter the download page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d37d5e8cffbf41279e5e4798a204a55b~tplv-goo7wpa0wc-image.image) </span>

(2) Download the latest field list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b9a0c568be247b985a84a9ff720b505~tplv-goo7wpa0wc-image.image) </span>

(3) Edit fields in Excel. To add new fields, append them at the bottom of the file.

(4) Upload the modified field list and confirm whether the modification was successful. Click Confirm to proceed.

(5) Confirm whether the automatically filled field information is correct. Click Save to take effect.

<span id="_2-7-跨项目配置"></span>
## 2.7 Cross\-project configuration

After selection, a pop\-up window will appear, making this dataset available for other projects. For details, see: [Mirror Dataset](https://docs.byteplus.com/docs/DataWind/Mirror_Dataset).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cb24a1a013477f80dce8912c61eb88~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-8-归因分析配置"></span>
## 2.8 Attribution analysis configuration

Configure attribution analysis dimensions for the dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2f768efef294d07871b389f44a8de62~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-9-转移所有者与转移告警人"></span>
## 2.9 Transfer owner and transfer alert recipient

Supports transferring the owner and alert recipient of the dataset. Caution: When the dataset owner is transferred, the alert owner created based on this dataset will also be transferred synchronously.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eb036a3878f42a990abbfb846434fc2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b2de8cc437e481f94a5ece281821cb8~tplv-goo7wpa0wc-image.image) </span>

<span id="dc1b9301"></span>
## 2.10 Direct connection dataset data readiness configuration

By default, only extracted datasets support configuring subscription monitoring push notifications triggered when data synchronization is complete. In the on\-premises version, direct\-connect datasets support triggering subscription monitoring notifications upon data synchronization completion through **data readiness configuration**.

For a direct\-connect dataset A, since it does not have synchronization information, it cannot use the "trigger on data synchronization completion" monitoring subscription configuration. Users can maintain a dataset B that stores "upstream data source readiness configuration information." By mapping the upstream database table field names and dates to dataset fields in the system, datasets A and B can be linked. Subsequently, in the monitoring subscription scenario, the system will **query dataset B to determine whether all upstream tables used in dataset A are ready**.

Steps:

**Step 1: Create a "direct\-connect scenario data readiness information table" and a "data readiness information dataset"** 

(1) Create a new "direct\-connect scenario data readiness information table." The following fields are required:


* dbName: Database name

* tableName: Table name

* partDate: Readiness time


Meaning: Records the name of the database table and the date it is ready. The system queries the readiness information table. When it finds that the readiness time for a certain database and table has arrived, it will determine that synchronization is complete and trigger monitoring.


|Field name |Type |Description |
|---|---|---|
|dbName |string |Required |
|tableName |string |Required |
|partDate |string (2024\-01\-01) |Required; data readiness date partition value |


(2) Use the "direct\-connect scenario data readiness information table" to create a "data readiness information dataset," and grant "view" and higher permissions for the "data readiness information dataset" to users who need to use this dataset later.

> The "direct\-connect scenario data readiness information table" and the "data readiness information dataset" are named for convenience in this document; the actual system does not restrict the names of such tables or datasets.


**Step 2: Configure readiness information for the direct\-connect dataset**

In the direct\-connect dataset, under "..." \- "More" \- "Data Readiness Configuration," confirm the upstream database and table information for the current dataset, and configure the database name, table name, and data readiness date partition from the "data readiness information dataset" individually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/987e67ab66c948f1a3c213e91dfe1243~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6f811cea7ab4fbba67245d36775b8e0~tplv-goo7wpa0wc-image.image" width="610px" /></div>


**Step 3: Support monitoring subscriptions for direct connection datasets triggered when data synchronization is complete**

For users with permission to use direct connection datasets, when charts and dashboards configured with direct connection datasets are used in monitoring subscription scenarios, if the system detects that the direct connection dataset is configured with "data readiness information", it will support notifications that are triggered when data synchronization is complete. This prevents downstream users from receiving monitoring subscription notifications before the data in the direct connection dataset is ready.
