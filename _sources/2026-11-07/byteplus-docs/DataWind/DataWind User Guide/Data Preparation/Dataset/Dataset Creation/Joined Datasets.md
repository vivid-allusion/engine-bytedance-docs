---
title: "Joined Datasets"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Joined_Datasets"
---

<span id="_1-概述"></span>
# 1. Overview

A joined dataset allows you to match and join fields between two datasets, making it easier to use multiple datasets together based on your business scenarios, and thereby create a dataset that meets your specific data requirements.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c66e366cf68482db119fd28ad8821aa~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="创建关联数据集"></span>
## Create a joined dataset

Step 1: Go to the dataset module, click "New" in the upper left corner, and select "New joined dataset"

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c66e366cf68482db119fd28ad8821aa~tplv-goo7wpa0wc-image.image) </span>

Step 2: After clicking "New joined dataset", you will enter the dataset creation page, where the list of datasets you have permission to access will be displayed on the left

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19916eeddb5a439483be9add3c31aa60~tplv-goo7wpa0wc-image.image) </span>

Step 3: After selecting the required datasets on the left, drag them into the blank area in the middle and select the join fields

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de72cf6e68bb4a569d3aac6463172a8f~tplv-goo7wpa0wc-image.image) </span>

Step 4: After adjusting the field configuration, click "Save" to create the dataset

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-创建关联数据集所需权限"></span>
## 3.1 Permissions required to create a joined dataset

On the model configuration page for creating a joined dataset, only datasets **under the current project** that you own and for which you have **view or higher permissions** are displayed and available on the left


* You can filter the dataset list by clicking the filter button in the upper right corner of the list

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19916eeddb5a439483be9add3c31aa60~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-2-数据集关联所需条件"></span>
## 3.2 Conditions required for dataset joining


|**Extracted dataset** |* Datasets used for association must be created under **the same cluster**.<br><br>* **Extracted** datasets can be associated with **datasets under the same cluster** that are **directly connected to the built\-in ClickHouse**. |
|---|---|
|**Direct connection dataset** |* **ClickHouse direct connection datasets under the same cluster** support mutual association.<br><br>* Direct connection datasets from **the same data connection** support mutual association.<br><br>* Local file direct connection datasets from **the same data connection** support mutual association. |



* The storage method of the datasets must be the same (for example, both must be ClickHouse; if one is ClickHouse and the other is Hive, Join is not supported). If the datasets you want to join do not meet these conditions, the following prompt will appear on the page:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be406430458d4769a6c6f393c96bd62a~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-支持的数据类型"></span>
## 3.3 Supported data types


* Offline extracted datasets (for example, extracted datasets with Hive or ClickHouse as the data source)

* Real\-time extracted datasets (for example, Kafka datasets)

* Direct connection datasets

* Direct connection ClickHouse/ByteHouse datasets (the data tables must come from the same cluster)


<span id="4dd9bd10"></span>
## 3.4 Join field expressions


* If the fields to be joined cannot be directly joined due to inconsistent formats or other reasons, you can select "Expression" when choosing the join fields to process the fields, reducing the amount of secondary processing required.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f286f74e4721480d9fddeb219cb682c7~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-4-权限说明"></span>
## 3.5 Permission description

<span id="5109e3ce"></span>
### 3.5.1 Resource permissions


* Users can create associated datasets using datasets for which they have "view or higher permissions".

* Datasets for which the user has "no permission" or only "view only" permission cannot be selected.


The editor of a dataset can only use datasets for which the "dataset owner" or themselves have "view or higher permissions" to modify the associated dataset.

<span id="_3-4-2-行列权限"></span>
### 3.5.2 Row and column permissions

Scenario: After dataset 1 joins dataset 2 to generate dataset X through a logical association, the rules for row and column permissions on dataset X are as follows:

(1) When a user queries this dataset on the visualization page, resource permissions for dataset X are required. The specific rows and columns that can be queried depend on the row and column permissions the user has for dataset 1 and dataset 2.

(2) When a user views a chart created from dataset X on a dashboard, in addition to dashboard permissions, row and column permissions for dataset 1 and dataset 2 are also required; permissions for dataset X are not required.


|Dimensions for determining row and column permissions |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |Condition |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|Does the user have resource permissions for dataset X |Yes |Yes |Yes |Yes |Yes |Yes |No |No |No |No |No |No |
|Does the user have resource permissions for dataset 1 |Yes |Yes |Yes |No |No |No |Yes |Yes |Yes |No |No |No |
|Is row and column permission control enabled for dataset 1 |Not enabled |Enabled |**Enabled** |Not enabled |Enabled |**Enabled** |Not enabled |Enabled |Enabled |Not enabled |Enabled |Enabled |
|Does the user have row and column permissions for dataset 1 |NA |Yes |**No** |NA |Yes |**No** |NA |Yes |No |NA |Yes |No |
| | | | | | | | | | | | | |
|Can the user query dataset X on the visualization page<br><br>&<br><br>Can the user view the detailed preview of dataset X in the dataset details page \- Preview |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**N** |**N** |**N** |**N** |**N** |**N** |
|Visible rows |All |Permitted rows and columns |None |All |Permitted rows and columns |None |None |None |None |None |None |None |
| | | | | | | | | | | | | |
|If the user has dashboard permissions, can they view charts created from dataset X on the dashboard |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**Y** |**Y** |**N** |**Y** |**Y** |**N** |
|Visible rows |All |Permitted rows and columns |None |All |Permitted rows and columns |None |All |Permitted rows and columns |None |All |Permitted rows and columns |None |
