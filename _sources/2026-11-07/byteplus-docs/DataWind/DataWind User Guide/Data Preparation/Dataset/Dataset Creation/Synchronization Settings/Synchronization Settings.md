---
title: "Synchronization Settings"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Synchronization_Setting"
---

For extracted datasets, the product allows users to configure synchronization frequency/time, dependency configuration, synchronization monitoring, performance settings, and more. This article describes how to configure synchronization settings.

<span id="0f76e8fd"></span>
# Function overview

The product supports multiple forms of data connections, and allows you to set whether the data in the product and the original data source are in an extracted or direct connection relationship. For extracted datasets, you can adjust synchronization frequency/time, dependency configuration, synchronization monitoring, performance settings, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6813ec7c62f40059e9147e3cd5e9ac1~tplv-goo7wpa0wc-image.image) </span>

The specific functional items are described as follows:


|Feature item |Required or optional |Feature description |
|---|---|---|
|Synchronization frequency |Required |Set the dataset's update synchronization time based on the update frequency of the data source and the required data granularity. Users can modify the synchronization type, synchronization frequency and time, write partitions, data lifecycle, synchronization of historical data, and more according to business needs.<br><br><br>* Initial configuration<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a7c6136999e4417b84264b2ef586da8~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Subsequent changes<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6ccddc45b364df98644321941830584~tplv-goo7wpa0wc-image.image) </span> |
|Dependency configuration |Optional |Users can set associations between a dataset and other data sources, so that updates to Dataset B are triggered only when Dataset A is updated.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2903a2f8e3a24163a4d5f16fe50bfcaf~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The readiness status of upstream data can be used to determine and enable scheduled synchronization tasks. When the user\-defined synchronization time is reached, the system will check the status of dependency tasks. The synchronization task for this dataset will only start after all corresponding dependency tasks are ready (that is, after the upstream datasets have been updated).<br><br>* If the synchronization task for this dataset is not executed due to dependencies, it is usually because there is no data update in the upstream dataset or modeling task within the business date range configured for the dependent upstream task in the current business. |
|Monitoring configuration |Optional |When a dataset synchronization exception occurs, relevant personnel must be notified in a timely manner. The product supports failure alarms, timeout alarms, and result exception alarms. Notification methods must be pre\-configured in office platform integration before they can be set.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82cba01c6714441e87b08944594e0eca~tplv-goo7wpa0wc-image.image) </span> |
|Performance settings |Optional |Performance settings may affect the synchronization and query performance of the dataset, including configuring sort keys, shard fields, sample fields, and query consistency guarantees. Performance settings cannot be modified after the dataset is saved.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c5c8b8c9d5a4655a0e09af693334013~tplv-goo7wpa0wc-image.image) </span> |
|Advanced settings |Optional |Supports setting the synchronization priority of tasks. Tasks with higher priority will be synchronized first during system synchronization peaks. Runtime parameters can help improve synchronization success rates. For more information, refer to [Extraction Parameters](https://docs.byteplus.com/docs/DataWind/Extraction_Parameters).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53b53ae26c114a289d018e99f6841e71~tplv-goo7wpa0wc-image.image) </span> |


<span id="aba2d9bb"></span>
# Cautions


* Only extracted datasets have synchronization settings; direct connection datasets do not have the concept of synchronization. For the differences between extraction and direct connection, see [Connection methods](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview#0b15f366).

* Some configurations can only be set during dataset creation and cannot be modified after the dataset is created, such as dependency configuration and performance settings.


<span id="23625d8c"></span>
# Prerequisites

In monitoring configuration, to set notification methods such as email or Lark (Lark, a collaboration platform), you must first complete the prerequisite configuration of platform integration.

<span id="e5ec8d8a"></span>
# Usage restrictions

The trading calendar and multiple synchronization features in synchronization frequency are currently only supported in privatized deployment of version V2.83.0 and above. To use this feature, please contact the Volcano Engine team to enable it for you.

<span id="07243b3d"></span>
# Function entry


|Dataset status |Operation method |
|---|---|
|Dataset editing status |* To create a new dataset: In the navigation bar at the top of the new dataset interface, click the "Sync" button.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d025ccd01f0485ea710ac8386f6f2bf~tplv-goo7wpa0wc-image.image) </span><br><br><br>* To edit an existing dataset: Click Edit to enter the synchronization settings environment.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46643b2a5b0243fdaa5e609b7f7d7a96~tplv-goo7wpa0wc-image.image) </span> |
|Dataset preview status |Click Dataset \- Synchronization Status to see the "Synchronization configuration" and "Data synchronization" buttons. Click the "Synchronization configuration" button to display the synchronization configuration information. Click "Edit" on the right side of each feature to enter the settings for that feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce39287e04e5486a86f0fdbb9ba33aa1~tplv-goo7wpa0wc-image.image) </span> |


<span id="_3-1-同步状态设置"></span>
# Synchronization status settings

<span id="_3-1-1-同步频率-同步类型"></span>
## Synchronization frequency

Supports configuration of synchronization type, synchronization frequency, write partition time, data lifecycle, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1776a6a53d54f2c836163c9ceac5035~tplv-goo7wpa0wc-image.image) </span>

The parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Synchronization type |Synchronization types are divided into scheduled synchronization and manual synchronization.<br><br><br>* Scheduled synchronization: You can set the start time to synchronize data on a schedule. Synchronization of historical data is supported.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/266271d7ee18473095415bb0aee224b8~tplv-goo7wpa0wc-image.image) </span><br><br>* Manual synchronization: Only the initial synchronization is performed; subsequent updates are not automatic. To synchronize, click the dataset, then in the synchronization status, click the operation bar corresponding to a specific business date, and click the [Synchronize] button to perform synchronization.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8e134bcc28e4523a768bd2956485676~tplv-goo7wpa0wc-image.image) </span> |
|Synchronization frequency |Supports specifying the exact time for scheduled synchronization at the minute, hour, day, day (by trading calendar), day (the day after trading calendar), week, and month levels.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For hour\-level, day\-level (based on the trading calendar), and day\-level (the day after the trading calendar), multiple time points can be set.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If a single time is selected, the schedule will execute only once.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If multiple times are selected, the schedule will execute multiple times according to the selected times.</div><br><br><br>* Minute level<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b5083a60d2d4fa9bec126c300a1c191~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Hour level<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b7ce2e6594745e9a3088f1569feeda1~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Day level<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac2367c24167435fb102bfcfce73ee85~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Week level<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e45f3443e8c4c4695156dda81aaf39b~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Monthly frequency<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98abd426cc3f44618e8dc2d201a44a93~tplv-goo7wpa0wc-image.image) </span> |
|Write partition |* Scheduled synchronization with hourly or minutely frequency supports two write partition methods: by hour or by day.<br><br>* Scheduled synchronization with daily, weekly, or monthly frequency supports only the daily write partition method.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once a write partition is created, it cannot be modified.</div><br><br><br>**Scenario 1:** <br><br>For MySQL incremental synchronization, select scheduled synchronization as the synchronization type, hourly synchronization as the frequency, and day as the write partition.<br><br>Synchronization: Each hourly task synchronizes all data for the day.<br><br>Query: In visual queries, select to query data by day.<br><br>**Scenario 2:** <br><br>For MySQL incremental synchronization, select scheduled synchronization as the synchronization type, minutely synchronization as the frequency, and hour as the write partition.<br><br>Synchronization: Each minutely task synchronizes data for the corresponding hour.<br><br>Query: In visual queries, you can select to query data by hour or by day. |
|Data lifecycle |Users can customize the data lifecycle to retain data from the most recent x days, or configure advanced settings to specify which data to retain after the period is exceeded. If the lifecycle is set to 1 day, only yesterday's data is retained.<br><br>Suppose a dataset is created on July 1, the lifecycle is set to 7 days, and data is synchronized daily:<br><br><br>* When synchronizing historical or backdated data, only data from the past 7 days can be synchronized. For example, if today is February 8, only historical data from February 2 to February 7 will be synchronized.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82bb46afe2bb4daca58154845bdafa03~tplv-goo7wpa0wc-image.image) </span><br><br><br>* After data synchronization, data can only be retained for 7 days. For example, if data for February 7 (business date) is synchronized on February 8, data from January 31 will be deleted; after synchronization, only data from February 1 to February 7 within these 7 days is available. |
|Synchronize historical data |This setting is available only for scheduled synchronization and is enabled by default. When enabled, you can choose to synchronize historical data within the selected time range after creating the dataset. Synchronization for this time range is performed only during the initial synchronization and will not take effect during subsequent synchronizations. At the same time, you can select a backtracking queue. The backtracking queue is only effective for synchronizing historical data. The queue for scheduled synchronization tasks is configured in advanced settings. |


<span id="_3-1-4-依赖配置"></span>
## Dependency configuration

This product provides users with flexible configuration options for task scheduling dependencies. Scheduling dependencies usually refer to the upstream and downstream relationships between periodic scheduling nodes in data synchronization and development processes. Tasks are scheduled in an orderly manner based on node dependencies, ensuring that downstream nodes are only triggered to run after upstream nodes have successfully executed, thereby guaranteeing the timely production of valid business data.

The dependency configuration of this product provides two main categories: automatic detection of upstream data output and third\-party API dependencies. For each category, you can choose either system automatic configuration or custom configuration. Users can establish dependencies on data sources, so that when a data source is updated or executed, dataset synchronization is triggered.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you choose to configure using a third\-party API, you must first perform API configuration in the task management module under system management, and then complete the dependency configuration for task scheduling in the dependency configuration module for visual modeling and datasets.</div>


<span id="cd9ecfb5"></span>
### The system automatically constructs partition detection tasks for data sources.


* Usage restriction: Only some partitioned data sources (Hive/MaxCompute/LAS) and partition tables are supported.

* Special statement: To avoid inaccurate dependencies caused by incomplete data output during partition detection, please ensure that data output is completed before constructing partitions.


**Option 1: System automatic configuration**

For data sources such as Hive, MaxCompute, and LAS, the system can automatically obtain and display dependency information configured for upstream nodes.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If the partition is generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: Sensor tasks mainly refer to scheduled tasks generated by the system to detect partitions, not the current task. For user\-configured scenarios, the system will automatically **detect and probe** whether the required partition table exists in the user's data source. If it exists, it means that the upstream data preparation is complete and the downstream data can be triggered to run.


The system will automatically discover Sensor dependency tasks that have already been created for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and users can choose custom configuration at this time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5d5e1db29514cbbb07c2f7d812936e8~tplv-goo7wpa0wc-image.image) </span>

**Option 2: Custom configuration**

This product also allows users to modify dependency offsets and add dependencies through custom configuration. The specific steps are as follows:


1. Click Custom Configuration, then click "Add Dependency" to open the configuration interface. In this interface, you can click Variable Description to view prompts related to dynamic time, or enter a table name to search and view.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43790fe91530487082681f11c84d0532~tplv-goo7wpa0wc-image.image) </span>


2. Click "Create System Custom Dependency" to open the detailed configuration window. At this point, you need to fill in the information shown in the figure below:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/976b4e8903e844009a9ec4d4ccd38088~tplv-goo7wpa0wc-image.image) </span>


3. After clicking OK, the custom dependency configuration is considered successful.


<span id="cce3ce33"></span>
### **Third\-party API dependency**

If a scheduling platform for data development or data processing tasks already exists within the organization and can be configured according to this product's API specifications, it can be integrated and linked with this product to establish task status dependencies for that scheduling platform.


* Special statement: All data sources supported for extraction by this product also support building API dependencies.

1. **Create an API task dependency**

   In System Management \- Task Management, create a new API task dependency.

2. **Dependency configuration**

   **Method 1**: System automatic configuration

   For data sources covered by API dependency rules created by users, the system can automatically obtain and display upstream dependency information.

   **Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If generated, the current task will be executed immediately. If the partition is not produced for more than 50 hours, the Sensor task will be marked as failed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Sensor definition: At the time set by the user, the system automatically detects whether the partition table required by the task exists in the user's data source. If it exists, this means that the preparation of upstream data has been completed and downstream data can begin to run.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A sensor task refers to a scheduled task generated by the system to discover partitions using a script, and is not the current task.   </div>
   

   The system will automatically discover dependency task sensors already created for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and users can choose custom configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af2cc9eeddd541dd8f9880606674dbf8~tplv-goo7wpa0wc-image.image) </span>

**Method 2**: Custom configuration

This product also allows users to modify dependency offsets and add dependencies through custom configuration. The specific steps are as follows:

First, click Custom configuration, then click "Add dependency" to open the configuration interface. In this interface, you can click Variable description to view information related to dynamic time, or enter a table name to search for and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375b586f9816490aa646b6d34b167067~tplv-goo7wpa0wc-image.image) </span>

Next, click "Create system custom dependency" to open the specific configuration window. At this point, you need to fill in the information shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b16deb63457c43e6a0d21d1b27ef467f~tplv-goo7wpa0wc-image.image) </span>

As shown above, a custom dependency configuration has been set for the data table. Relevant terms explained:


|Term |Description |Example |
|---|---|---|
|Data source type |The data source type of the dependency table, including [Hive](https://docs.byteplus.com/docs/DataWind/Hive), [MaxCompute](https://docs.byteplus.com/docs/DataWind/MaxCompute), and [LAS](https://docs.byteplus.com/docs/DataWind/LAS). |Hive indicates that a data source of the Hive data type was selected based on data requirements. |
|Database name |The name of the database corresponding to the dependency table. |database_1 indicates that the database named database_1 in the Hive data source was selected. |
|Table name |The name of the data table corresponding to the dependency table. |dim.user_basic_info_1d_a\-\-user information table, indicating that the table dim.user_basic_info_1d_a under this database was selected (in this example, \-\-user information table is used). |
|Table type |Divided into two types: partitioned and non\-partitioned. |Using an incremental table as an example, if non\-partitioned is selected, this means all historical data in the data table is selected. If partitioned is selected, this means all data within the specified partition range is selected. |
|Partition settings |Partition settings are a method of dividing data into different subsets according to specific rules. The drop\-down fields for partition settings include all fields in the dependency table you selected. You can define the partition field of the data table according to the field types in your table, and after selecting the partition field, select the corresponding partition. |For example, in the figure above, the partition of the dependency table in this example is p_date (representing a time partition). According to business requirements, we set p_date='20250317' (the partition for March 17, 2025), which means viewing all data within this partition. |
|Dependency type |Data source partition detection dependency, API dependency |By default, the data source partition detection dependency is selected. If the system is configured with an API dependency, you can choose either the data source partition detection dependency or the API dependency as needed. |


Finally, after clicking OK, the custom dependency configuration is complete.

<span id="a812ce92"></span>
### **Other scenarios**

**Scenario 1**

If a scheduling platform for data development or data processing tasks already exists within the enterprise, users can also manually run tasks based on the status of tasks in their scheduling platform.

**Note:**  The user needs to specify the task ID, and if the original task is set to manual execution, the user can trigger manual execution through OpenAPI.


* First, set the task synchronization type to manual synchronization.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3bf5701db02401d8dafc51252950ba2~tplv-goo7wpa0wc-image.image) </span>


* Next, find the task ID and project ID (App ID). The task URL contains both the task ID and project ID (the project refers to this product's project space).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb3782b4c11d5386d8b242fa28315f74.png) </span>

* Finally, the user can trigger the task to run by manually calling the interface.


**Scenario 2**

If the user's data development or data task management scheduling platform cannot be configured in this product's task management settings via the standard API method, the interface must be developed and configured through an intermediate layer, and then this product can adapt to build task dependencies. For this scenario, we recommend that enterprises adopt ISV development services. For specific solutions, please consult Volcano Engine staff.

<span id="_3-1-5-监控配置"></span>
## Monitoring configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To set the notification method, you must first complete the pre\-configuration ofoffice platform integration; only then can you proceed with the settings.</div>


Alert conditions\*\*:\*\* You can add monitoring alerts to promptly notify relevant users when data set synchronization is abnormal. Multiple alert rules can be configured.

The system provides three types of alert conditions


* Failure alert: A notification will be triggered if dataset synchronization fails.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5fde04e1529455a94f07f71c2182b4d~tplv-goo7wpa0wc-image.image) </span>


* Timeout alert: Four types of timeout definitions are supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9cbb1e5fb26548859864ce8aeb454cd7~tplv-goo7wpa0wc-image.image) </span>


* Absolute time (based on Beijing Time): An alert will be triggered if synchronization is not completed by the specified time.

* Synchronization duration exceeded: An alert will be triggered if dataset synchronization exceeds the specified duration. For example, if the alert is set for 2 hours and synchronization starts at 7:00, an alert will be triggered if synchronization is not completed by 9:00.

* Exceeding the set synchronization time: Applicable to scheduled synchronization. After setting the synchronization time in the synchronization frequency, if synchronization has not started or is not completed after the specified timeout, an alert will be triggered. For example, if the synchronization time is set to 7:00 and the timeout is set to "not started within 1 hour after the set synchronization time," an alert will be triggered if the dataset has not started synchronization (in unsynchronized/not ready status) by 8:00.

* Synchronization duration fluctuation: An alert will be triggered if the synchronization process duration exceeds the specified threshold.

* Result anomaly alert: Monitors the number of data rows and triggers an alert when the row count is abnormal.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43fe9639f05646ed8b485cffe66a517f~tplv-goo7wpa0wc-image.image) </span>


* To prevent synchronization anomalies or upstream data anomalies resulting in no data being synchronized: An alert can be set when the number of data rows equals 0.

* Upstream data may be updated multiple times. To prevent incomplete synchronization data: An alert can be set when the number of data rows is less than the expected row count. For example, if the expected dataset synchronizes 100,000 rows daily and less than 80,000 rows are synchronized, data may be incomplete. In this case, an alert can be set when the number of data rows is less than 80,000.

* Fluctuation rate anomaly alert: The fluctuation rate can be set, and an alert will be triggered when the number of data rows fluctuates beyond the set value compared to the previous day or within 7 days.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a855e06f6f8424caf7463717d1e0ed5~tplv-goo7wpa0wc-image.image) </span>

Notification methods: Email, Lark, DingTalk, WeCom, email groups, Lark groups, Wehook, and general IM are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5fde04e1529455a94f07f71c2182b4d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-6-性能设置"></span>
## Performance settings

Performance settings may affect dataset synchronization and query performance. Performance settings cannot be modified after the dataset is saved.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9ac285a1314854ac8d7c83d8297ae3~tplv-goo7wpa0wc-image.image) </span>

**Sort key:** 

Set the fields most commonly used as filter conditions as sort keys to speed up queries. Multiple fields can be set as sort keys, with the first field having the highest priority and the others decreasing in order. It is recommended not to exceed three fields.

**Shard field:** 

Used to ensure that data is evenly distributed across all storage nodes. If the daily data volume does not exceed 20 million rows, retain the system default settings. Only one field can be set as the shard field. You can select the field most commonly used as a dimension (set this if the field has more than 100 distinct values), or the field most commonly used as a deduplication count metric (set this if the field has more than 10,000 distinct values, such as user_id, device_id, item_id, and so on).

> For an explanation of the usage scenarios for sort keys and partition fields, click the button above to view more information.

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dc49c0a06ad44e4ab818d41a838e235~tplv-goo7wpa0wc-image.image) </span>


**Sampling field:** 

During queries, random sampling can be performed based on the sampling field to improve query speed. This must be specified when creating the table, and only fields of type int, float, or string are supported.

The system defaults to the first primary key field; this is optional.

**Sampling ratio:** 

By default, 100% of the data is sampled according to the sampling field. The smaller the ratio, the less data is sampled, and the faster the visualization query speed.

The system default is 100%. The ratio can be adjusted during actual visualization queries.

**Partition:** 

Specifies the partition of the dataset. The default is p_date.

**Query consistency assurance:** 

When this feature is enabled, it ensures that the results of multiple queries on the dataset are consistent, which can prevent extreme cases such as discrepancies between primary and secondary data, but query performance will decrease accordingly.

<span id="_3-1-7-高级设置"></span>
## Advanced settings

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba8106164f3c45ddb415cea0aaed920b~tplv-goo7wpa0wc-image.image) </span>

**Queue and priority:** 

This feature only supports extracted datasets and affects extraction speed, but does not affect query speed.

No changes are required for the default settings.

**Number of retry attempts and retry interval for failures:** 

When dataset synchronization fails, the system will initiate one retry by default. You can customize the number of retry attempts and the retry interval for dataset synchronization failures to improve the success rate of synchronization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/910d8aa0f51647fcb67421d8dd8754de~tplv-goo7wpa0wc-image.image) </span>

**Steps for configuring existing datasets**:

On the dataset "Synchronization Status" page, click Synchronization Configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/923a86b6a00345d3bb4cfc3a2517885f~tplv-goo7wpa0wc-image.image) </span>

Edit advanced settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b1983355fa3414d9a44417b8a841354~tplv-goo7wpa0wc-image.image) </span>

Adjust the number of reruns and the rerun interval time in the pop\-up sidebar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c27422824cf246ed876c97bfe4bf1916~tplv-goo7wpa0wc-image.image) </span>

**Synchronize multiple days**:

To refresh synchronized data multiple times each day, configure synchronization for multiple days. Supports refreshing data from specified N days ago (multiple selections allowed) or the most recent N days. This feature must be used together with [Custom SQL](https://docs.byteplus.com/docs/DataWind/Custom_SQL).

**Runtime parameters:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c84587870c1410bb83dcbaf2bb346f0~tplv-goo7wpa0wc-image.image) </span>

Supports configuring runtime parameters for dataset synchronization as needed to ensure successful synchronization or optimize synchronization performance. See [Extraction Parameters](https://docs.byteplus.com/docs/DataWind/Extraction_Parameters) for details.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For synchronization frequency, select a frequency related to trading days; the option for multi\-day synchronization is not displayed.</div>


* <div data-tips="true" data-tips-type="warning">After enabling multi\-day synchronization, only day\-level synchronization frequency can be selected, and the option for trading days is not displayed.</div>



<span id="_3-2-同步状态预览"></span>
# Synchronization status preview

When previewing a saved dataset, click Dataset \- Synchronization Status to view the historical synchronization status of the dataset below, as well as the historical synchronization list, runtime view, logs, and synchronization operation buttons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0085e90fac29447990bf74cbe9475906~tplv-goo7wpa0wc-image.image) </span>

When previewing a saved dataset, click Dataset \-\- Synchronization Status to view detailed historical synchronization information for the dataset below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2544a608f3654fceb7795b1f435e70ad~tplv-goo7wpa0wc-image.image) </span>


* The upper left area allows you to quickly filter historical synchronization results by business date, synchronization status, or when the result row count is 0.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7cb9dbdea06478aba3d1823684b40ba~tplv-goo7wpa0wc-image.image) </span>


* The upper right contains the "Synchronization Configuration" and "Data Synchronization" buttons.

   * Click the "Synchronization Configuration" button to display synchronization configuration information. Click the pencil\-shaped edit icon on the right side of each feature to enter its settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d3f779d43be4189bdced1b5351738a0~tplv-goo7wpa0wc-image.image) </span>


* Click the "Data Synchronization" button to open the synchronization settings pop\-up. Select the required business date start and end times in the selection range to immediately synchronize data in bulk for that business date range.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ee82e3c7af64ec6876196c320b25eb7~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  Select "After enabling synchronization, the synchronization status list displays this time range" to show execution information for this period in the list. For example, select the time period from 2-1 to 2-3 and enable the toggle. The synchronization status will display the following synchronization information.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/566f0d0b62c948dbae3326771cc8fdd8~tplv-goo7wpa0wc-image.image) </span>


* In the data backtracking settings, you can choose to execute according to dependency settings or ignore dependencies and execute backtracking directly.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4b2daf9ce574129be509b8e7d1dfff0~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* The list at the bottom displays all synchronized and updated data by business date, synchronization status, scheduled time, synchronization start time, synchronization end time, execution duration, number of data rows, and operations (Run View, Log, Synchronize).

   * Run View: When clicked, a pop\-up appears in the lower right corner, presenting the execution records of this dataset in a view format.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88d6a3ca43304b95945a1e28705ff84f~tplv-goo7wpa0wc-image.image" width="734px" /></div>



* Log: When clicked, a new page opens, listing the execution logs for this dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73519d771e44414389b2d3523a817d4c~tplv-goo7wpa0wc-image.image) </span>


* Synchronize: Clicking Synchronize will prompt the backfill settings. Click Confirm to immediately synchronize the data for the specified business date.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72313f67498b4defac0e104cb9d2f309~tplv-goo7wpa0wc-image.image" width="610px" /></div>
