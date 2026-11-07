---
title: "Dataset"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_"
---

A dataset is a data model composed of one or more tables, which is the basis for creating labels, groupings, and insights. Before applying data, it is necessary to connect the source data information of the data and output it into a dataset through the visual modeling function.

<span id="8c27d561"></span>
# **Operation steps**

<span id="6b4ea057"></span>
## The first step is to create a dataset

The sources of the dataset are as follows:


1. Datasets accessed through the Enterprise Knowledge Engine data access function, see for details [Dataset Output](https://docs.byteplus.com/docs/dataagent/Dataset_Output).

2. Customer data platform: that is, the CDP system dataset, the dataset output by the system through visual modeling tasks or system interfaces, such as label datasets, the system dataset does not support human deletion and secondary editing.

3. Datawind: If you purchase Datawind and mix it with CDP, you can share the use of datasets under the same project on both platforms (excluding directly connected datasets in Datawind).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Datasets sourced from Datawind are only allowed for use and are not allowed to be edited or deleted.   </div>
   

<span id="06140d27"></span>
## **Step 2: Filtering the dataset**

In the **Data Access** \> **Datasets** module, you can view the information of all datasets in the project and filter according to different indicators, including dataset source, type, total storage, life cycle, update time, etc.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39df9955b3f04722bac553e75b315e8e~tplv-goo7wpa0wc-image.image) </span>

<span id="a698154b"></span>
## **Step 3: Manage the dataset**


1. Click to **view blood information** to display the **blood view,**  help users visually track the source and flow of data, and enhance the transparency and traceability of data management.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7865c5b16d2d40b6a42edaaf5a734266~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25fc02bf51364cd388eca943dd2ccc99~tplv-goo7wpa0wc-image.image" width="1996px" /></div>



2. Click **Edit** to modify the name, description, and lifecycle days of the current dataset.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The TTL (Time to Live) of the dataset is the life cycle of the dataset, that is, the data storage time of the dataset. If you save all the data every day, it is recommended to keep the data within 7 days to reduce storage pressure; if you save new data or non\-partitioned tables every day, it is recommended to customize the lifecycle according to the commonly used data range.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7861fa880c2a4a9489612a9372efcf8f~tplv-goo7wpa0wc-image.image) </span>

3. Click on the **registration data file**, jump to the new data file page, the data registered as the corresponding type of data file, detailed data operations see [4.2 Create New Data Archive](https://docs.byteplus.com/docs/undefined/6968d1606c0b37097f59c1e0#_4-2-%E6%96%B0%E5%BB%BA%E6%95%B0%E6%8D%AE%E6%A1%A3%E6%A1%88).

4. Click **Delete** to delete the current data source. Attention: The deletion operation may affect upstream and downstream use, please proceed with caution.


<span id="8b92c042"></span>
## **Step 4: Dataset Authorization**

In the **Project Center \- Permissions \- Manage by Content \- Resources** page, authorization of **data sets** is supported. Select the resource of type "Dataset".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2687bf3a25cb4b11b72839f152d19ac8~tplv-goo7wpa0wc-image.image) </span>

Support single/batch authorization, support for granting viewing, editing, and administrative permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ef3712151090430d81563063cfe94249~tplv-goo7wpa0wc-image.image) </span>

<span id="bf142159"></span>
## **Step 5: Visual Knowledge Processing**


* Input: Support for selecting the form of **dataset** joins when visualizing build knowledge processing new tasks.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03a7b049fc2f4a378e6bb610c1e217a7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a725e412e91e4e8caf653676ec021e93~tplv-goo7wpa0wc-image.image) </span>


* Output: Support for outputting data to datasets, support for outputting to hive/clickhouse.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/255b4445d71f4caf96a39cc8277f827b~tplv-goo7wpa0wc-image.image) </span>

&nbsp;
