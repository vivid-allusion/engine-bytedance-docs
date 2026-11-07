---
title: "[Case] Key Behavior Statistics of Automobile Users"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Case_Key_Behavior_Statistics_of_Automobile_users"
---

<span id="09bf5f12"></span>
## I. Overview

The common data collection methods for car sales are mainly divided into online (APP/WeChat Mini Program) and offline (store registration/offline scan code). When counting user behavior, it is often necessary to integrate information from different data tables, and combine the basic attributes of the user's id\-mapping to count the key indicators of the user.

This case comprehensively considers the user's online behavior/user's offline behavior, combined with the user's time to enter the optional package, the time to enter the Mini Program, and the situation of entering the offline store, and comprehensively considers these factors to calculate the user's key behavior to assist in judging whether the user is interested in buying a car, and finally combines the CDP platform to assist in decision\-making user marketing.

<span id="565f9966"></span>
## II. Processing process

The data preparation module provides convenient interactive data processing, combined with exploration/data result preview, which can facilitate data processing while viewing the results, lowering the threshold of traditional data processing. It can be easily started without professional SQL skills.

<span id="c2736d11"></span>
### 1. Data source access

Currently, data preparation integrates Hive, MySQL, Clickhouse, Kafka, HttpApi, Feishu, Csv/Excel, Oracle, Impala, PostgreSql, Hbase, SqlServer, MaxCompute, ADB, MongoDb, Hana, teradata, Db2, Vertica, GreenPlum and other 20 mainstream data source access capabilities, supporting data sampling/full/filtering/partial reading

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e1e97186ce74421ad1b8727d3c935fa~tplv-goo7wpa0wc-image.image) </span>

<span id="8ca0f6a2"></span>
### 2. Data processing

The data preparation module contains a variety of data processing operators


|processing method |Explanation |
|---|---|
|field settings |Column Name/Column Type/Column Filter |
|connect |Data Join, support left and right internal connection/external connection, support cross\-origin connection |
|polymerization |Select the aggregation field and method to change the aggregation method and set the aggregated field name |
|calculated column |Use Spark functions to process upstream fields to add new fields. You can also add a business date field for a table with no business date. |
|filter row |Select a field, confirm the filter criteria, support two layers and/or logical relationships. |
|String index |A type conversion operator that maps the value of a specified property to a numeric index so that an operator that can only process numeric data can also process the property. This operator is generally used for data preprocessing. Additionally, it is not suitable for performing this operator on columns containing continuous data, such as ID columns |
|Replace missing values |Replace null values with min/max/avg/fixed values |


<span id="5637e218"></span>
## III. Problem modeling

Count the time to browse the optional package page/the time to enter the Mini Program/the number of times to enter the store offline, combine the basic attributes of the user, calculate the active time of the user, and connect it to the CDP or output hive/clickhouse as an indicator for subsequent processing

<span id="43cc5123"></span>
### 1. Data description

Online behavioral data table (user unique ID and device ID):


|field name |field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Tracking events are partitioned by date and stored by day |
|tenant_id |int |tenant id |How to access the channel |
|device_id |string |Device ID |The ID of the user's device. |
|user_id |string |user id |Used to uniquely identify users |
|app_id |int |App ID |Client side app id |
|event |string |behavioral event |enter_mp: Enter WeChat official account<br><br>enter_car_optical_pack: Go to the optional package page<br><br>close_car_optical_pcak: Close the Options page |
|string_params |map |Event details, character save behavior |enter_from: official account/offline scan code<br><br>enter_from: Mini Program Home/official account push |
|decimal_params |map |Event details, save numbers |stay_time: Duration of stay |
|time |bigint |Occurrence time, timestamp |The event at which the event occurred, timestamp type |


Offline behavior data table (registered username and phone number):


|field name |field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Tracking events are partitioned by date and stored by day |
|tenant_id |int |tenant id |How to access the channel |
|name |string |user name |The user's name will match id\-mapping |
|phone |string |user phone |User registered phone |
|app_id |int |App ID |Client side app id |
|event |string |behavioral event |enter_mp: Enter WeChat official account<br><br>enter_car_optical_pack: Go to the optional package page<br><br>close_car_optical_pcak: Close the Options page |
|string_params |map |Event details, character save behavior |enter_from: official account/offline scan code<br><br>enter_from: Mini Program Home/official account push |
|decimal_params |map |Event details, save numbers |stay_time: Duration of stay |
|time |bigint |Occurrence time, timestamp |The event at which the event occurred, timestamp type |


ID_Mapping table:


|field name |field type |Field meaning |Field description |
|---|---|---|---|
|date |string |Partition field, date |Date of user information update, full daily update |
|uid |bigint |user id |Used to uniquely identify users |
|nickname |string |user name |The user's name registered on the platform |
|name |string |user name |The user's name will match id\-mapping |
|phone |array |user phone |The phone number registered by the user has multiple calls. |
|carnumber |array |User's license plate number |The license plate number registered by the user has multiple license plates. |
|did |array |Device ID |The user's mobile device id, there are multiple devices |
|mail |string |email |User registered email address |


<span id="6b14e79e"></span>
### 2. Data preparation

<span id="f02ea83d"></span>
#### 2.1 Online data processing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a45bde9065d47d59f38f0bfef27e213~tplv-goo7wpa0wc-image.image) </span>

Online behavior mainly collects the number of visits (the number of times entering the optional package + the number of times entering the Mini Program) and the statistics of the visit duration (exit time).


* Using filter and aggregation operators, filter the events entering the optional package and entering the Mini Program, and then do an aggregation with each other (count the number of entries).

* Use filter events and computed columns (to extract value values of type map), summed in aggregates, to calculate a user dwell time

* The last two data are merged to obtain the effective metrics of end\-user visits (number of visits and duration of stay).


<span id="a439107c"></span>
#### 2.2 Offline data and id\-mapping processing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b335774989d54648ac568455f6c311f1~tplv-goo7wpa0wc-image.image) </span>

The offline behavior mainly collects the number of visits to the store, the general registered username and phone number, so it needs to be merged with the id table.


* Filter the number of store entries with filter and aggregation operators

* Merge with the id\-mapping table to get the user's unique id.


<span id="62cff0ad"></span>
#### 2.3 Data Integration Statistics & Data Production Applications

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cbb737e1eb544fba7ac56595f8d3256~tplv-goo7wpa0wc-image.image) </span>

Finally, the connection operator is used to merge the online and offline data, and the data processing results can be output to hive/clickhosue, which can be combined with ABI for analysis and processing later. At the same time, it can also be connected to the CDP platform, and the indicator can be put into production for label insight/marketing application/user grouping

<span id="96b7d29f"></span>
## IV. Summary

The data preparation platform includes rich data access capabilities and simple and easy\-to\-use data processing capabilities, which makes it convenient for users to handle different data tables/cross\-source data processing/interactive visualization data processing, greatly reducing output cleaning costs and allowing users to easily solve data problems.
