---
title: "Data Archive Management"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Data_Archive_Management_"
---

<span id="_1-功能概述"></span>
# 1. Overview of Functions

In the Data Archive Management functional module, support registering and managing **underlying data** as **business\-readable and understandable business data content** according to different business types and formats. Downstream applications can efficiently call data based on agreed formats, businesses can quickly understand data based on redefined names and interpretations, achieving fast data recognition and application.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the data registered in data file management can be used for subsequent tasks such as creating labels and selecting groups.</div>


<span id="f49d176a"></span>
# 2. Prerequisites for Use


* Only administrators and those with the permission to view or add, delete, and modify data archives in the project center\-module\-data archive management, can use this module.

* Before building data archives, data sets need to be cleaned and associated with the configuration One ID in visual modeling. Only **datasets containing One ID and partition fields can be registered in this module.** 


<span id="b9497130"></span>
# 3 Data file format requirements

<span id="f7c1425a"></span>
## 3.1 Subject attributes

<span id="4dd1059f"></span>
#### **Overview**

Around the attributes of the subject, each subject ID (OneID) definitely has only one line of data

<span id="e41805b3"></span>
#### Data sample


|**OneID Field** |**Partition Date** |**Attribute 1** |**Attribute 2** |**Attribute 3** |**Attribute 4** | **...**  |
|---|---|---|---|---|---|---|
|10001 |2022/1/1 |Male |mac |Shanghai |Sports |... |
|10002 |2022/1/1 |Male |mobile |Beijing |Art |... |
|10003 |2022/1/1 |Female |mac |Beijing |Music |... |


<span id="3a47e07c"></span>
#### Data structure and field requirements


|Field |Field Type |Description |
|---|---|---|
|* OneID Field |Numeric (int/long/bigint) |* Mandatory Field<br><br>* The OneID field is a primary key that is recognizable across all platforms, such as the OneID obtained through IDM conversion, also known as the baseline BaseID<br><br>* The OneID field must be of numeric type and when stored as a dataset, must be a sharding key (storage setting) for fast queries<br><br>* The OneID field must be the unique key of the table (storage setting). If duplicate data exists, data deduplication can be performed in advance or a unique key sorting field can be set to deduplicate logic |
|* Partition Date |Date Type |* Required field<br><br>* The system automatically generates or designates the partition field, and no manual configuration is required. |
|Attribute Field |Numerical/Text/Time/Array multiple values, does not support map type |* Optional Field<br><br>* The attribute field revolves around the attributes of OneID, such as age/gender, used to directly generate the user's portrait.<br><br>* Property fields support numerical/text/date/array values, and the text type supports setting enumeration fields, such as configuring city names in city codes.<br><br>* The attribute field does not support special fields like map. |


<span id="896a07eb"></span>
#### Selection component usage logic

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2cdcd9fe75b6b8f800ae40c09871610.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">OneID must be generated through the IDMapping conversion operator</div>


2. <div data-tips="true" data-tips-type="tip">OneID definitely conducted data deduplication or set a unique key for storage, which can be processed using deduplication operators</div>


3. <div data-tips="true" data-tips-type="tip">It must be a partitioned table, <strong><ins>and the latest partition stores full data,</ins></strong> the full data refers to syncing all user OneIDs to the latest partition daily.</div>



<span id="ba7726e6"></span>
## 3.2 Business details

<span id="352c4c3d"></span>
#### Overview

Around the business factual data of the subject, each ID may have multiple lines of data, often recording business factual records or statistical data, such as aggregated consumption amount data

<span id="72ba437a"></span>
#### Sample data


|**OneID Field** |**Statistics Date** |**Total Consumption Amount** |**Consumption City** |**Consumption Type** | **...**  |
|---|---|---|---|---|---|
|10001 |2022/1/1 |100 RMB |Shanghai |Sports |... |
|10001 |2022/1/2 |200 RMB |Hangzhou |Music |... |
|10002 |2022/1/2 |300 RMB |Beijing |Art |... |
|10003 |2022/1/3 |100 RMB |Beijing |Music |... |


<span id="e073587a"></span>
#### Data structure and field requirements


|**Field** |**Field Type** |**Description** |
|---|---|---|
|OneID Field |Numeric (int/bigint/long) |* Required field.<br><br>* Duplicate OneIDs are allowed.<br><br>* The OneID field must be numeric and set as the shard key when stored in a dataset for fast queries. |
|Statistics Date |Date (date/datetime) |* Required field.<br><br>* Defaults to the partition date. By default, the table is treated as an incremental table, meaning each partition contains newly added data. If the business data is a full table, it can be transformed into an incremental one via visual modeling.<br><br>* The date must have incremental business significance (e.g., creation or update time). |
|Detail Fields |Numeric / Text / Time / Array (multi\-valued), Map type not supported |* Optional fields.<br><br>* These contain detailed business fact data around the OneID, often used for statistical information. |


<span id="c80c402d"></span>
#### Logic of selection component usage

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_853190e1cdcead817df7dc6106e64adb.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">OneID is definitely generated through the IDMapping operator.</div>


2. <div data-tips="true" data-tips-type="tip">OneID can be duplicated, meaning the same OneID can have multiple rows of data.</div>


3. <div data-tips="true" data-tips-type="tip">Must be a partitioned table, where the partition date must possess some incremental business significance, with each latest partition being new business factual data by default as an incremental table.</div>



<span id="9a8ef92a"></span>
## 3.3 Behavioral Events

<span id="99030f69"></span>
#### Overview

Around the behavior logs of the subject, namely who (OneID) did what at what time (behavior time) resulting in what event outcome (attribute), the subject ID, behavior event, and behavior time together form a unique key.

<span id="7e287886"></span>
#### Sample data


|* OneID field |* Statistical date<br><br>> Default to use partition date |* Action time |* Action event |* Property (Numeric Type \- Integer) |* Property (Numeric Type \- Decimal) |* Property (Text Type) |
|---|---|---|---|---|---|---|
|10001 |2023\-9\-7 |1694075399 |clickbutton |{"cost":200 ，<br><br>"click_cnt": 100} |{"balance": 100.11，<br><br>"mileage": 100.11} |{"buttonname": "Test"，<br><br>"city": "Shanghai"} |
|10001 |2023\-9\-7 |1694075392 |pageview |{"cost":200 ，<br><br>"click_cnt": 100} |{"balance": 100.11，<br><br>"mileage": 100.11} |{"buttonname": "Test"，<br><br>"city": "Shanghai"} |
|10002 |2023\-9\-7 |1694075395 |pageview |{"cost":200 ，<br><br>"click_cnt": 100} |{"balance": 100.11，<br><br>"mileage": 100.11} |{"buttonname": "Test"，<br><br>"city": "Shanghai"} |
|10003 |2023\-9\-7 |1694075397 |pageview |{"cost":200 ，<br><br>"click_cnt": 100} |{"balance": 100.11，<br><br>"mileage": 100.11} |{"buttonname": "Test",<br><br>"city": "Shanghai"} |


<span id="4a806dd7"></span>
#### Data structure and field requirements


|Field |Field Type |Description |
|---|---|---|
|* OneID Field |Numerical (int/bigint/long) |* Required Field<br><br>* OneID allows duplicate data<br><br>* The OneID field must be of numerical type and must be sharded key (storage setting) when stored as a dataset for fast queries |
|* Statistical Date |Date type (date) |* Required field<br><br>* Using date partition as the statistical date keeps consistent with the behavior time, that is, incrementally storing data according to the time of data generation |
|* Behavior Time |Numerical type (int/bigint/long) |* Required field<br><br>* Numerical type timestamp, with 11 digits or 13 digits timestamp |
|* Behavior Event |Text type (string) |* Required field |
|* Attribute (integer type) |Map integer type Map (string, bigint) |* Required field<br><br>* Key in the map is the attribute name<br><br>* Value in the map is the attribute value<br><br>> Such as: {"cost": 200,<br><br>> "click_cnt": 100}<br><br>> Cost is the attribute name for expenses, 200 is the attribute value |
|* Attribute (Numerical Type \- Decimal) |Map integer type Map (string, bigint) |* Required field.<br><br>* The key in the map represents the attribute name,<br><br>* and the value in the map represents the attribute value. |
|* Attribute (Numeric Type \- Text) |Map integer type Map (string, bigint) |* Required field.<br><br>* The key in the map represents the attribute name,and the value represents the attribute value. |


<span id="e1519faf"></span>
#### Logic of selection component usage

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9b2c6c44852a84e5cabfcb894bc6f9a.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">OneID must be generated through the IDMapping operator transformation.</div>


2. <div data-tips="true" data-tips-type="tip">The property must be a map structure, which can be converted into the desired format through visual modeling.</div>


3. <div data-tips="true" data-tips-type="tip">It can be a partitioned table, but it must be incremental partition logic, that is, behavioral events are always up to date every day.</div>



<span id="cfd4391d"></span>
# 4. Operation Instructions

<span id="718b25a5"></span>
## **4.1 View Data Archive List**

Display information about the created data profiles, including data profile name, type, creator, data production tasks, data update frequency, and the latest update time; Users can search for data profile names/creators in the top left corner to quickly find the corresponding data profiles.

If users want to edit or delete the data profile, click on the **operation** location.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cdad90a766a7b57ee19b02743e18a335.png) </span>


* Profile Types: Include main properties, behavioral events, business details, and business dimensions, with support for quick filtering.

* Update Frequency: Includes two update frequencies: real\-time and offline, with support for quick filtering.

* Latest Update Time: Records the latest update time of the data source, and supports sorting in ascending/descending order.


<span id="7a2d5160"></span>
## **4.2 Create New Data Profile**

**Step One: Configure Basic Information**

1.Click **Create Data Profile;** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2dc0a9c0a9644f264431f6048cfbaae.png) </span>

2.Choose **Data Profile** type, including main properties, behavioral events, business details, and business dimensions.


* Caution:

   * Subject Attributes: The subject attributes obtain the data of the latest partition in the dataset every day. It is necessary to ensure that the latest 【dataset partition】 contains all the attribute features of the subjects.

   * Business Details: When users use business details, they will first select data from the latest N days. At this time, the latest N days are filtered by 【dataset partition】= latest N days. Therefore, it is necessary to define the dataset partition based on a certain business date, such as order creation time.

   * Business Dimensions: The business dimensions obtain the data of the latest partition in the dataset every day. It is necessary to ensure that the latest 【dataset partition】 contains all the attribute features of all business dimensions.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c9af3cdfe85fc4b86aed9d2bb02e5b1.png) </span>

<span id="357666fb"></span>
### 4.2.1 Creating New Subject Attribute Data Archive


1. Select **Dataset**. The datasets that can be selected have the following requirements:

* Default support for datasets stored in ClickHouse/ByteHouse

* Allow regular scheduled updates/real\-time updates of datasets

* Support binding with Hive datasets, which can be used when creating import tags later (Note: This feature is turned off by default. To enable it, please inform and activate the corresponding feature switch during deployment)


The system will automatically associate lifecycle, update frequency, and OneID primary key fields based on the selected dataset, and manual changes are not supported.

Define **data archive** and fill in basic information.


* Data archive name: allows Chinese, English, numbers, and underscores.

* Data archive description: support supplementary descriptions for the data archive for better business understanding.

* Associated subject: simply select the relevant subject.


At the data archive registration position, check the dataset fields that need to be registered (OneID field and partition field will be checked by default), support changing the field display name, and adding archive field descriptions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/877d913d0f5d4c68a7a9004c82d49a74~tplv-goo7wpa0wc-image.image) </span>

<span id="138727e5"></span>
### 4.2.2 Create a new business detail data archive.


1. Select **dataset**, the selected dataset must meet the following requirements:

* Only datasets stored in ClickHouse/ByteHouse are allowed.

* Only datasets that are regularly or real\-time updated are allowed.


Based on the selected dataset, the system will automatically associate lifecycle, update frequency, and OneId primary key fields. Manual changes are not supported.

Define **data archive** and fill in the basic information.


* Data archive name: Allows Chinese, English, numbers, and underscores.

* Data archive description: Support adding supplementary descriptions for the data archive to facilitate business understanding.

* Associated subject: Simply choose the subject to be associated with.

* Archive update type: Support dropdown selection of **partition incremental update, partition full update**.

> \*After the upgrade, the subject property data archives of existing customers default to full update, while behavioral & detailed data archives default to incremental update.


At the location to register archive information, select the dataset fields that need to be registered (OneID field and partition field are selected by default), support modifying field display names, and adding archive field descriptions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5d9ce5963f843f483081dce4d797ddc~tplv-goo7wpa0wc-image.image) </span>

Subject property data archives, business detailed data archives' attribute fields, support **attribute classification**.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a3b22f3556f4be59b100a086010aac6~tplv-goo7wpa0wc-image.image" width="1884px" /></div>


<span id="a70c2bb3"></span>
### 4.2.3 Create new behavioral event data archives


1. Select **dataset**, which must meet the following requirements:

* Only datasets stored in ClickHouse/ByteHouse are allowed

* Only datasets that are regularly scheduled/real\-time updates are allowed


The system will automatically associate lifecycle, update frequency, and OneId primary key fields based on the selected dataset and does not support manual changes.

2. Define **data archive**, and fill in the basic information.


* Data archive name: allows Chinese, English, numbers, and underscores;

* Data archive description: support adding a supplementary description for better understanding of the data archive;

* Associated subject: Select the subject to be associated with.

* Behavioral event configuration: Configure the event time, event action, and action attribute fields sequentially

   * Event time field: Event_time, usually a 13\-digit timestamp, restricted field type to int/long or other numerical types;

   * Event action field: Event_type, field storing the event names such as 'page_view', 'Clickbutton', restricted field type to string string types;

   * Behavior attribute field: Event_params, usually stored in JSON format, contains the content of click events, such as the information/buttons/devices related to "Clickbutton." The field type is restricted to Map type, which can include Map{String,String}/Map{String,Float}/Map{String,Int32}/Map(String, Array(String))/Map(String, Datetime) types.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daf53998a8fe40ff8ef433068918aefc~tplv-goo7wpa0wc-image.image) </span>

<span id="861cf626"></span>
### 4.2.4 Create New Business Dimension Data Archives


1. Select **Dataset** with the following requirements:

* Only datasets stored in ClickHouse/ByteHouse are allowed.

* Only datasets with scheduled/real\-time updates are allowed.


The system will automatically associate lifecycle, update frequency, and the OneId primary key field based on the selected dataset, without support for manual changes.

2. Define **Data Archive** and fill in the basic information.


* Data Archive Name: Allow Chinese, English, numbers, and underscores.

* Data Archive Description: Support supplementary descriptions for better business understanding.

* Associated Subject: Simply select the relevant subject.

* Update Type: Support drop\-down selection for **partition incremental updates, partition full updates**.

   Partition Incremental Update: Incremental data is stored in partitions daily. If you need to query data with a certain business meaning date within the last 7 days (e.g., partition date like order creation time), you need to perform cross\-partition queries.

   Partition Full Update: Full data is stored in partitions daily. If you need to query data with a certain business meaning date within the last 7 days (e.g., order creation time), you can query the latest partition.

> 1. After the upgrade, the main attributes data files of existing customers default to full updates, while behavior and detailed data files default to incremental updates.


When registering archive information, select the dataset fields to be registered (dimension primary key and partition fields are selected by default), support modifying field display names, and adding archive field descriptions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e1ab76283e74b30bc78cff7a99d2858~tplv-goo7wpa0wc-image.image) </span>

**Attention:**  Only business details & behavior events support real\-time datasets, while main attributes do not support real\-time datasets.

<span id="bba65b91"></span>
## **4.3 View Data Archive Details Page**

Click on the data archive name to access the data archive details page, support modifying data archive name and description, modifying archive field display names and descriptions.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_78ecb262e86610b2d92c6bca606b7a16.png) </span>

<span id="27f550a1"></span>
## **4.4 Delete Data Archive**

Support deletion of data archives. When deleting, the system will display downstream dependencies such as tags, please delete with caution.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad7d0342641dfaf65571250cd83b3a28.png) </span>

<span id="9f1fad3f"></span>
# 5. Frequently Asked Questions

<span id="73e04216"></span>
### Q: What real\-time scenarios are currently not supported when users import real\-time data from DataFinder to CDP and automatically create them as data archives?

Some special events or properties in DataFinder may not be supported in real\-time scenarios, mainly including:


* Arbitrary events, arbitrary active events, virtual events (identified as $_vp), virtual properties: Currently not supported;

* Dimension tables and dictionaries: Currently, neither DataFinder nor other regular data sources support them;

* Real\-time signals: Real\-time signals do not support custom multi\-attribute operations.


It is recommended to carefully read the system prompts when using the above functions to ensure data accuracy and system stability.
