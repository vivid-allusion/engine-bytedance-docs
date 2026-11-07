---
title: "Linked Datasets"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Linked_Datasets_"
---

<span id="_1-概述"></span>
# 1. Overview

Linked datasets allow you to match and associate fields between two datasets, making it convenient to use multiple datasets together based on your business scenarios and ultimately create a dataset that meets your data requirements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/179314797a2f4270aa8db77e4a0d6a56~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="创建关联数据集"></span>
## 2.1 Create a linked dataset

Step 1: Go to the dataset module, click "Create" in the upper left corner, and select "Create linked dataset".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/179314797a2f4270aa8db77e4a0d6a56~tplv-goo7wpa0wc-image.image) </span>

Step 2: After clicking "Create linked dataset", you will enter the dataset creation page. The list of datasets you have permission to access will be displayed on the left.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/156d7f25fbdc46e5a854abc69416a482~tplv-goo7wpa0wc-image.image) </span>

Step 3: After selecting the required datasets on the left, drag them into the blank area in the middle and select the fields to associate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48d9dd0ddc024de7975fdefef740dcbe~tplv-goo7wpa0wc-image.image) </span>

Step 4: After adjusting the field configuration, click "Save" to create the dataset.

<span id="_3-功能介绍"></span>
# 3. Feature overview

<span id="_3-1-创建关联数据集所需权限"></span>
## 3.1 Permissions required to create a linked dataset

On the model configuration page for creating a linked dataset, only datasets **under the current project** for which you have **view or higher permissions** are displayed and available on the left.


* You can filter the dataset list by clicking the filter button in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/156d7f25fbdc46e5a854abc69416a482~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-2-数据集关联所需条件"></span>
## 3.2 Conditions required for dataset association


|**Extracted datasets** |* Datasets used for association must be created under **the same cluster**.<br><br>* **Extracted** datasets can be associated with **datasets under the same cluster** that are **directly connected to the built\-in ClickHouse**. |
|---|---|
|**Direct connection datasets** |* **ClickHouse direct connection datasets under the same cluster** support mutual association.<br><br>* Direct connection datasets from **the same data connection** support mutual association.<br><br>* Local file direct connection datasets from **the same data connection** support mutual association. |



* The storage method of the datasets must be the same (for example, both are ClickHouse; if one is ClickHouse and the other is Hive, Join is not supported). If the datasets you want to Join do not meet the above conditions, the following prompt will appear on the page:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6213695fa22f48008e43fb825e808f78~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-支持的数据类型"></span>
## 3.3 Supported data types


* Offline extraction datasets (for example, extraction datasets with Hive or ClickHouse as the data source)

* Real\-time extraction datasets (for example, Kafka datasets)

* Direct connection datasets

* Direct connection ClickHouse/ByteHouse datasets (the data tables must come from the same cluster)


<span id="4dd9bd10"></span>
## 3.4 Associated field expressions


* If the fields to be associated cannot be directly linked due to inconsistent formats or other reasons, you can select "Expression" when choosing the associated fields to process the fields, reducing the need for further processing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67f028b1fec74f2b9b3a63e50a2b7dff~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-权限说明"></span>
## 3.5 Permission description

<span id="5109e3ce"></span>
### 3.5.1 Resource permissions


* Users can create associated datasets using datasets for which they have "view or higher permissions".

* Datasets for which users have "no permissions" or "view only" permissions cannot be selected.


Editors of a dataset can only use datasets owned by the "dataset owner" and those for which they themselves have "view or higher permissions" to modify the associated dataset.

<span id="_3-4-2-行列权限"></span>
### 3.5.2 Row and column permissions

Scenario: After dataset 1 joins dataset 2 to generate dataset X through logical association, the rules for row and column permissions on dataset X are as follows:

(1) When users query the dataset on the visualization page, they need resource permissions for dataset X. The specific rows and columns that can be queried follow the row and column permissions that users have for datasets 1 and 2.

(2) When users view charts created from dataset X on the dashboard, in addition to dashboard permissions, they also need row and column permissions for datasets 1 and 2. Resource permissions for dataset X are not required.


|Dimensions for row and column permission determination |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Does the user have resource permissions for dataset X? |Yes |Yes |Yes |Yes |Yes |Yes |No |No |No |No |No |No |
|Does the user have resource permissions for dataset 1? |Yes |Yes |Yes |No |No |No |Yes |Yes |Yes |No |No |No |
|Is row and column permission control enabled for dataset 1? |Not enabled |Enabled |**Enabled** |Not enabled |Enabled |**Enabled** |Not enabled |Enabled |Enabled |Not enabled |Enabled |Enabled |
|Does the user have row and column permissions for dataset 1? |NA |Yes |**No** |NA |Yes |**No** |NA |Yes |No |NA |Yes |No |
| | | | | | | | | | | | | |
|Can the user query dataset X on the visualization page<br><br>&<br><br>Can the user view the detailed preview of dataset X in the dataset details page \- Preview |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**N** |**N** |**N** |**N** |**N** |**N** |
|Visible rows |All |Rows and columns the user has permission to view |None |All |Rows and columns the user has permission to view |None |None |None |None |None |None |None |
| | | | | | | | | | | | | |
|If the user has dashboard permissions, can they view charts created from dataset X on the dashboard |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**Y** |**Y** |**N** |
|Visible rows |All |Rows and columns the user has permission to view |None |All |Rows and columns the user has permission to view |None |All |Rows and columns the user has permission to view |None |All |Rows and columns the user has permission to view |None |
