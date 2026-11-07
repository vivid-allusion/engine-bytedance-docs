---
title: "⁣Statistical Analysis of Key Behaviors of Automotive Users"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Statistical_Analysis_of_Key_Behaviors_of_Automotive_Users"
---

<span id="_1-场景概述"></span>
# 1. Scenario overview

Common data collection methods in automotive sales are mainly divided into online (APP/WeChat Mini Program) and offline (in\-store registration/offline QR code scanning). When performing user behavior statistics, it is often necessary to integrate information from different data tables and combine the user's id\-mapping basic attributes to calculate key user metrics.

This case comprehensively considers both users' online and offline behaviors, taking into account the time when users enter the optional package, the time they access the Mini Program, and their visits to offline stores. By considering these factors together, key user behaviors are calculated to help determine whether users are interested in purchasing a car, and ultimately, the Customer Data Platform (CDP) is leveraged to assist in user marketing decisions.

<span id="_2-能力概述"></span>
# 2. Capability overview

The system provides convenient interactive data processing capabilities. With exploration features and data result preview, users can process data while viewing results, lowering the barrier to entry for traditional data processing and enabling easy use even without professional SQL skills.

<span id="_2-1-数据源接入"></span>
## **2.1 Data source integration**

The product currently supports integration with more than 20 mainstream data sources, supporting data sampling, filtering, and reading specific columns.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f463dc4c49854c6a96cefc917acf0606~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-数据处理"></span>
## **2.2 Data processing**

Multiple data processing operators are provided, such as:


|Processing method |Explanation |
|---|---|
|Field settings |Column names, types, and filters |
|Join |Data join, supports left join, right join, inner join, outer join, and cross\-source join |
|Aggregation |Select aggregation fields and methods. You can change the aggregation method and set the name of the aggregated field. |
|Calculated column |Use Spark functions to process upstream fields to add new fields. You can also add business date fields to tables that do not have business dates. |
|Filter rows |Select fields and confirm filter conditions. Supports two layers of and/or logical relationships. |
|String index |A type conversion operator that maps the value of a specified attribute to a numeric index, allowing operators that can only process numeric data to handle attributes. This operator is generally used for data preprocessing. Additionally, it is not suitable for columns containing continuous data, such as ID columns. |
|Replace missing values |Replace null values; supports replacement with min, max, avg, or a fixed value |


<span id="_3-建模过程"></span>
# 3. Modeling process

By aggregating the duration of browsing the optional package page, the time of entering the Mini Program, and the number of offline store visits from both online and offline tables, and combining users' basic attributes, the user's active duration is calculated as a metric for connection to the CDP or output to Hive/ClickHouse, facilitating subsequent processing.

<span id="_3-1-数据描述"></span>
## **3.1 Data description**

Online behavior data table (user unique identifier id and device id):


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Data tracking is partitioned by date and stored daily |
|tenant_id |int |Tenant ID |Channel access method |
|device_id |string |Device ID |User's device ID |
|user_id |string |User ID |Used to uniquely identify the user |
|app_id |int |App ID |Client app ID |
|event |string |Behavior event |enter_mp: Enter WeChat Official Account<br><br>enter_car_optical_pack: Enter the optional package page<br><br>close_car_optical_pcak: Close the optional package page |
|string_params |map |Event details, stores string behaviors |enter_from: WeChat Official Account/Offline QR code scan<br><br>enter_from: WeChat Mini Program homepage/WeChat Official Account push |
|decimal_params |map |Event details, stores numeric values |stay_time: Duration of stay |
|time |bigint |Occurrence time, timestamp |Event occurrence time, timestamp type |


Offline behavior data table (registered username and phone number):


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|p_date |string |Partition field, date |Data tracking is partitioned by date and stored daily |
|tenant_id |int |Tenant ID |Channel access method |
|name |string |User name |The user's name, which will be matched with id\-mapping |
|phone |string |User phone number |User's registered phone number |
|app_id |int |App id |Client app id |
|event |string |Behavior event |enter_mp: Enter official WeChat account<br><br>enter_car_optical_pack: Enter optional package page<br><br>close_car_optical_pcak: Close optional package page |
|string_params |map |Event details, stores character actions |enter_from: Official account / offline QR code scan<br><br>enter_from: Mini program homepage / official account push |
|decimal_params |map |Event details, stores numeric values |stay_time: Dwell time |
|time |bigint |Occurrence time, timestamp |Event occurrence time, timestamp type |


ID_Mapping table:


|Field name |Field type |Field meaning |Field description |
|---|---|---|---|
|date |string |Partition field, date |Date of user information update, updated in full every day |
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

Online behavior mainly collects the number of visits (number of times entering the optional package plus number of times entering the Mini Program) and collects statistics on visit duration (based on exit time).


* Use filter and aggregation operators to filter events for entering the optional package and entering the mini program, then aggregate them together (count the number of entries).

* Use event filtering and calculated columns (extracting the value of map type), then aggregate and sum to calculate a user's dwell time.

* Finally, merge the two datasets to obtain the final effective user access metrics (number of visits and dwell time).


<span id="_3-2-2-线下数据和-id-mapping-处理"></span>
### **3.2.2 Offline data and id\-mapping processing**

Offline behavior mainly collects the number of store visits, typically recording the user name and phone number, so it needs to be merged with the id table.


* Use filter and aggregation operators to filter the number of store entries.

* Merge with the id\-mapping table to obtain the user's unique id.


<span id="_3-2-3-数据整合统计-数据生产应用"></span>
### **3.2.3 Data integration statistics & data production application**

Finally, use the join operator to merge online and offline data, and the processed data results can be output to hive/clickhouse. Subsequently, visual queries and dashboard creation can be performed on the DataWind platform. It can also be combined with CDP products for label insights, marketing applications, user segmentation, and more.
