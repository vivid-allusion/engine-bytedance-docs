---
title: "Dataset Creation Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Creation_Overview"
---

<span id="_1-数据集创建概述"></span>
# 1. Overview of dataset creation

Dataset creation consists of three parts: creating a new dataset, creating a new associated dataset, and creating a new folder.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-新建数据集"></span>
## 2.1 Create a new dataset

<span id="_2-1-1-入口"></span>
### 2.1.1 Entry point


* Click the plus sign to create a dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e446266837240f3a10d63323c17ab86~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-1-2-选择数据源"></span>
### 2.1.2 Select a data source

 **(1) Directly connect to an existing data source**

Users can create a new dataset from an existing data connection. First, select the target connection from the data connections, then click Confirm.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b37738b27a446af8bde5b9d9c2aa5ce~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* **Before version V2.50.0,**  as shown in the figure below


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ac864ce93f147b4ad0a7fb3158e47a0~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* **From version V2.50.0 onwards,**  as shown in the figure below

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ac8a1725fa244d3aefd3decb96c6cf2~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   


 **(2) Create a new data connection**

**From version V2.62.0 onwards,**  a permission application entry has been added in the pop\-up window for creating a new dataset.

When the user has the "Project Edit" permission, the pop\-up window for creating a new dataset appears as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ac864ce93f147b4ad0a7fb3158e47a0~tplv-goo7wpa0wc-image.image" width="610px" /></div>


When the user does not have the "Project Edit" permission, there are usually two scenarios:

**Scenario 1:**  For users whose system has a permission application module, click "System email notification to administrator" to enable the "Project Edit" permission.

**Scenario 2:**  For users whose system does not have a permission application module, please contact the project administrator to request the "Project Edit" permission.

After the above "Project Edit" permission is enabled, follow the [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview)instructions to create a new data connection. Once completed, proceed directly to the next step to configure the model.

<span id="_2-1-3-数据集具体配置"></span>
### 2.1.3 Dataset configuration details


* On the model configuration page, first select either Custom SQL or a table from the database on the left, then drag and drop it onto the canvas on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c471164e7b3d4f4886e51fe77fa7f854~tplv-goo7wpa0wc-image.image) </span>

   * You can click "Custom SQL" under the data connection on the left, drag it to the canvas on the right, and then write your own SQL to create a dataset.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7459bd529ba400e95b1fb2a6aa5174f~tplv-goo7wpa0wc-image.image) </span>

   * You can also click a table on the left, drag it to the canvas on the right, and create a dataset directly from the table.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/061780ee16054c71bcb8656a308a144a~tplv-goo7wpa0wc-image.image) </span>


Users can also perform more configurations. For details, see


|**Actions** |**Detailed description of actions** |
|---|---|
|1 |[Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL) |
|2 |[Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration) |
|3 |[Data Filtering](https://docs.byteplus.com/docs/DataWind/Data_Filtering) |
|4 |[Synchronization Settings](https://docs.byteplus.com/docs/DataWind/Synchronization_Setting) |
|5 |[Field Configuration](https://docs.byteplus.com/docs/DataWind/Fields_Configuration) |


<span id="_2-1-4-预览与保存"></span>
### 2.1.4 Preview and save

Click the "Preview" button on the right to preview and confirm the data. If there are no issues, click the "Save" button to save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/935da32d9ee54ce7b25797845f98eb52~tplv-goo7wpa0wc-image.image) </span>


* Set the dataset name and description in the pop\-up window, select the save path, and starting from V2.50.0, you can configure during dataset creation.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a36503bd1fad46578cce49c61f94e9a2~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* After saving, you can view the details of the dataset. You can click "Visual Query" in the upper right corner to use this dataset [Visual Query Overview](https://docs.byteplus.com/docs/DataWind/Visual_Query_Overview), or click "Edit" to go to the above [Model Configuration](https://docs.byteplus.com/docs/DataWind/Model_Configuration) step.

> Caution: After creating a dataset, you need to wait for a certain period before the dataset can be previewed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb54b3cb93f14a97bbeee950279280ce~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-新建关联数据集"></span>
## 2.2 Create an associated dataset

An associated dataset allows you to match and associate fields between two datasets, making it easier to use multiple datasets together for your business scenarios, thereby forming a dataset that meets your data requirements.

**Entry point:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba93ae7db9f24da8a002bc9cd32f948c~tplv-goo7wpa0wc-image.image) </span>

**For detailed description, see** [Joined Datasets](https://docs.byteplus.com/docs/DataWind/Joined_Datasets).

<span id="_2-3-新建文件夹"></span>
## 2.3 Create a folder

Click the plus sign to create a folder, and fill in the name, description, and folder address.

**Entry point:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3f683abe85c4dca9011472933b8e31b~tplv-goo7wpa0wc-image.image) </span>

**Fields to fill in:** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/024a6ede0d45417081108fdd0d72d479~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="b0ce6350"></span>
## 2.4 More configurations


* **V2.74.0 and later**, after users upload Excel/CSV local files, the system will perform a "file merge" operation to reduce the number of base tables created and alleviate cluster pressure.

* **V2.74.0 and later**, for redshift and las_jdbc direct connection datasets within the dataset, the "Insert Parameter" feature has been added, allowing users to embed relevant parameters in the dataset according to specific requirements.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79c095af4cb5411d8679081908dd0b90~tplv-goo7wpa0wc-image.image" width="2562px" /></div>
