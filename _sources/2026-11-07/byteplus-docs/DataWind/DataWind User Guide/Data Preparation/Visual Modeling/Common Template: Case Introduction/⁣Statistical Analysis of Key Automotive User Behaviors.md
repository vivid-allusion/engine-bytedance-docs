---
title: "⁣Statistical Analysis of Key Automotive User Behaviors"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Statistical_Analysis_of_Key_Automotive_User_Behaviors"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

Common data collection methods in automotive sales are mainly divided into online (APP/WeChat Mini Program) and offline (store registration/offline QR code scanning). When conducting user behavior statistics, it is often necessary to integrate information from different data tables and combine the basic attributes of user id\-mapping to calculate key user metrics.

This case comprehensively considers both online and offline user behaviors, taking into account the time when users enter the configuration package, the time they access the Mini Program, and their visits to offline stores. By integrating these factors, key user behaviors are calculated to assist in determining whether users are interested in purchasing a car, and ultimately, the CDP platform is used to support user marketing decisions.

<span id="_2-能力概述"></span>
# 2. Capability overview

The system provides convenient interactive data processing capabilities. With features such as data exploration and result preview, users can easily process data while viewing results, lowering the threshold for traditional data processing. Even without professional SQL skills, users can get started easily.

<span id="_2-1-数据源接入"></span>
## **2.1 Data source integration**

The product currently supports integration with more than 20 mainstream data sources, enabling data sampling, filtering, partial column reading, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a2bbb31eac54f51b46f18884c9b0679~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-数据处理"></span>
## **2.2 Data processing**

Provides a variety of data processing operators, such as:


|Processing method |Explanation |
|---|---|
|Field settings |Column name/Column type/Column filter |
|Join |Data join, supports left and right inner/outer joins, supports cross\-source joins |
|Aggregation |Select aggregation fields and methods, aggregation method can be changed, and the name of the aggregated field can be set |
|Calculate columns |Use Spark functions to process upstream fields to add new fields. Business date fields can also be added to tables without business dates. |
|Filter rows |Select fields and confirm filter conditions, supports two layers of and/or logical relationships. |
|String index |A type conversion operator that maps the value of a specified attribute to a numeric index, allowing operators that only process numeric data to also handle attributes. This operator is generally used for data preprocessing. Additionally, it is not suitable for columns containing continuous data, such as ID columns. |
|Replace missing values |Replace null values, supports replacement with min/max/avg/fixed value |


<span id="_3-建模过程"></span>
# 3. Modeling process

By aggregating both online and offline tables to calculate the duration of browsing the configuration package page, the time of entering the Mini Program, and the number of offline store visits, and combining the user's basic attributes, the user's active duration is calculated. This metric is then connected to the CDP or output to Hive/ClickHouse for subsequent processing.

<span id="_3-1-数据描述"></span>
## **3.1 Data description**

Online behavior data table (user unique identifier id and device id):


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Data tracking is partitioned by date and stored daily |
|tenant_id |int |Tenant ID |Channel access method |
|device_id |string |Device ID |The user's device ID |
|user_id |string |User ID |Used to uniquely identify the user |
|app_id |int |App ID |The client app's ID |
|event |string |Behavior event |enter_mp: Enter the WeChat Official Account<br><br>enter_car_optical_pack: Enter the optional package page<br><br>close_car_optical_pcak: Close the optional package page |
|string_params |map |Event details, stores character behaviors |enter_from: WeChat Official Account/Offline QR code scan<br><br>enter_from: Mini program homepage/WeChat Official Account push |
|decimal_params |map |Event details, stores numeric values |stay_time: Duration of stay |
|time |bigint |Occurrence time, timestamp |The event occurrence time, timestamp type |


Offline behavior data table (registered username and phone number):


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Data tracking is partitioned by date and stored daily |
|tenant_id |int |Tenant ID |Channel access method |
|name |string |User name |The user's name, which will be matched with id\-mapping |
|phone |string |User phone number |User's registered phone number |
|app_id |int |App id |Client app id |
|event |string |Behavior event |enter_mp: Enter WeChat Official Account<br><br>enter_car_optical_pack: Enter optional package page<br><br>close_car_optical_pack: Close optional package page |
|string_params |map |Event details, stores character\-based actions |enter_from: WeChat Official Account/offline QR code scan<br><br>enter_from: Mini program homepage/WeChat Official Account push |
|decimal_params |map |Event details, stores numeric values |stay_time: Dwell time |
|time |bigint |Occurrence time, timestamp |Event occurrence time, timestamp type |


ID_Mapping table:


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|date |string |Partition field, date |Date of user information update, full update daily |
|uid |bigint |User id |Used to uniquely identify the user |
|nickname |string |User name |User's registered name on the platform |
|name |string |User name |User's name, will be matched with id\-mapping |
|phone |array |User's phone number |User's registered phone number, multiple numbers possible |
|carnumber |array |User's license plate number |User's registered license plate number, multiple plates possible |
|did |array |Device id |User's mobile device id, multiple devices possible |
|mail |string |Email |User's registered email |


<span id="_3-2-数据准备"></span>
## **3.2 Data preparation**

<span id="_3-2-1-线上数据处理"></span>
### **3.2.1 Online data processing**

Online behavior mainly collects visit counts (number of times entering the configuration package plus number of times entering the Mini Program) and statistics of visit duration based on exit time.


* Use filter and aggregation operators to filter events for entering the optional package and entering the mini program, then aggregate them together (count the number of entries).

* Use event filtering and calculated columns (extracting the value from map type), then aggregate and sum to calculate a user's dwell time.

* Finally, merge the two sets of data to obtain the final effective user access metrics (number of visits and dwell time).


<span id="_3-2-2-线下数据和-id-mapping-处理"></span>
### **3.2.2 Offline data and id\-mapping processing**

Offline behavior mainly collects the number of store visits, usually recording the username and phone number, so it needs to be merged with the id table.


* Use filter and aggregation operators to filter events of entering the store and aggregate the count.

* Merge with the id\-mapping table to obtain the user's unique id.


<span id="_3-2-3-数据整合统计-数据生产应用"></span>
### **3.2.3 Data integration statistics & data production application**

Finally, use the join operator to merge online and offline data, and the processed data results can be output to hive/clickhouse. Subsequently, visual queries or dashboard creation can be performed on the DataWind platform. It can also be combined with CDP products for label insights, marketing applications, user segmentation, and more.
