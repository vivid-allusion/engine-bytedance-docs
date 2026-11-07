---
title: "Overview of Dataset Creation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Overview_of_Dataset_Creation_"
---

<span id="_1-数据集创建概述"></span>
# 1. Overview of dataset creation

Dataset creation consists of three parts: creating a new dataset, creating an associated dataset, and creating a new folder.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-新建数据集"></span>
## 2.1 Create a new dataset

<span id="_2-1-1-入口"></span>
### 2.1.1 Entry point


* Click the plus sign to create a dataset


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fab4d41974794a5a91b34dd072944484~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-2-选择数据源"></span>
### 2.1.2 Select a data source

 **(1) Directly connect to an existing data source**

Users can create a new dataset from an existing data connection. First, select the target connection from the data connections, then click Confirm.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f49caa11de843eaacbabb083b2566d8~tplv-goo7wpa0wc-image.image" width="610px" /></div>


 **(2) Create a new data connection**

The pop\-up window for creating a new dataset provides an entry point for permission requests.

When the user has the "Project Edit" permission, the pop\-up window for creating a new dataset appears as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92ef4fdf265f4c94858311a2ce144b53~tplv-goo7wpa0wc-image.image" width="610px" /></div>


When the user does not have the "Project Edit" permission, there are usually two possible situations:

**Situation 1:**  For users whose system includes a permission request module, "Project Edit" permission can be enabled by clicking "Notify administrator via system email".

**Situation 2:**  For users whose system does not include a permission request module, please contact the project administrator to request the "Project Edit" permission.

After enabling the above "Project Edit" permission, follow the instructions in [Data Connection Overview](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview) to create a new data connection. Once completed, proceed directly to the next step to configure the model.

<span id="_2-1-3-数据集具体配置"></span>
### 2.1.3 Dataset configuration details


* On the model configuration page, first select either Custom SQL or a table from the database on the left, then drag and drop it onto the canvas on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ad48d781cb84b1a8e714abe296b3a4b~tplv-goo7wpa0wc-image.image) </span>


* You can click "Custom SQL" under the data connection on the left, drag it to the canvas on the right, and then write your own SQL to create a dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/691d53c75642417d948f0741d7d37982~tplv-goo7wpa0wc-image.image) </span>

* You can also click a table on the left, drag it to the canvas on the right, and create a dataset directly from the table.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c54a82e7308d4641a125652b041f17dc~tplv-goo7wpa0wc-image.image) </span>

Users can also perform additional configurations. For details, see:


|**Operation item** |**Detailed explanation of operation items** |
|---|---|
|1 |[Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL_) |
|2 |[Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration_) |
|3 |[Data Filtering](https://docs.byteplus.com/docs/dataagent/Data_Filtering_) |
|4 |[Synchronization Settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Settings__) |
|5 |[Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration_) |


<span id="_2-1-4-预览与保存"></span>
### 2.1.4 Preview and save

Click the "Preview" button on the right to preview and confirm the data. After confirming there are no issues, click the "Save" button to save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1898f63b5724c42a9541afc19dafd82~tplv-goo7wpa0wc-image.image) </span>


* Set the dataset name and description in the pop\-up window, select the save path, and configure the usage instructions during dataset creation.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfaaa6731402493792187200ead01a5d~tplv-goo7wpa0wc-image.image" width="630px" /></div>



* After saving, you can view the details of this dataset and click "Edit" to enter the above [Model Configuration](https://docs.byteplus.com/docs/dataagent/Model_Configuration_) step.

> Caution: After creating a dataset, you need to wait for a certain period before the dataset can be previewed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9cb5446a2bb46b396e5d0af99cb77bc~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-新建关联数据集"></span>
## 2.2 Create an associated dataset

An associated dataset allows you to match and associate fields between two datasets, making it easier to use multiple datasets together according to your business scenario, thereby forming a dataset that meets your data requirements.

**Entry point:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5e26b77807e48dd9ae5a4c2f7b68782~tplv-goo7wpa0wc-image.image) </span>

**Detailed explanation:**  [Linked Datasets](https://docs.byteplus.com/docs/dataagent/Linked_Datasets_).

<span id="_2-3-新建文件夹"></span>
## 2.3 Create a folder

Click the plus sign to create a folder, and fill in the name, remarks, and folder address.

**Entry point:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16965ffd4163424d86be7243b3a65f54~tplv-goo7wpa0wc-image.image) </span>

**Specific content to fill in:** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af0478891b8141cb8b97f38407eb1bcf~tplv-goo7wpa0wc-image.image" width="673px" /></div>


<span id="b0ce6350"></span>
## 2.4 More configurations


* After the user uploads an Excel or CSV local file, the system will perform a "file merge" operation to reduce the number of base tables created and alleviate cluster pressure.

* For redshift and las_jdbc direct connection datasets within the dataset, the "insert parameter" feature has been added, allowing users to embed relevant parameters in the dataset according to specific requirements.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cdeabf7d0fa40cfa7213ae7b92dbeaa~tplv-goo7wpa0wc-image.image) </span>
