---
title: "Synchronization Settings"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Synchronization_Settings__"
---

<span id="e4fa2fce"></span>
# 1. Overview

The product supports multiple forms of [Data Connection Overview](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview), and you can configure whether the data in the product and the original data source are connected via extraction or direct connection. For [Dataset Overview](https://docs.byteplus.com/docs/dataagent/Dataset_Overview_) that use extraction, you can adjust the data synchronization frequency and timing, dependency configuration, synchronization monitoring, performance settings, and more.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/795f0ada068443c39b522a6db65c693f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-同步状态设置"></span>
## 2.1 Synchronization status configuration


* **Dataset editing status**

   * When creating a new dataset, click the "Synchronization settings" button in the navigation bar at the top of the new dataset interface.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34431e28f734df78778a9a14ebde773~tplv-goo7wpa0wc-image.image) </span>

   * For existing datasets, click "Edit" to enter the same interface as above.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b3d5b50ec1041faabc41b20d4512fbc~tplv-goo7wpa0wc-image.image) </span>

* **Dataset save preview status**

   * When in the dataset save preview status, click Dataset \-\- Synchronization status to see the "Synchronization configuration" and "Data synchronization" buttons.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a70d56f7127943148b5c65114710e8bc~tplv-goo7wpa0wc-image.image) </span>

   * Click the "Synchronization configuration" button to display synchronization configuration information. Click the pencil\-shaped edit icon on the right side of each feature to enter the settings for that feature.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68d242cb9fd84d83863638f343328906~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-同步状态设置操作指引"></span>
## 2.2 Synchronization status configuration operation guide


|**Functions** |**Required or optional** |**Function overview** |
|---|---|---|
|Configure synchronization frequency |Required |Set the update synchronization time for the dataset based on the update frequency of the data source and the required data granularity. Users can modify the synchronization type, synchronization frequency and time, write partition, data lifecycle, synchronization of historical data, and other options according to business needs.<br><br><br>* **Initial configuration**<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8822633a56274a068b389e416eaaa816~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Subsequent modification**<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94c09cda2f245e596b6eef2d9376492~tplv-goo7wpa0wc-image.image) </span> |
|Dependency configuration |Optional |Dependency configuration means users can set associations between a dataset and other data sources, enabling updates to dataset A to trigger updates to dataset B. By using dependency configuration, the readiness status of upstream data can be considered to determine and initiate scheduled synchronization tasks. When the user\-defined synchronization time is reached, the system checks the status of dependency tasks. The synchronization task for this dataset will only start after all corresponding dependency tasks are ready (that is, after the upstream datasets have been updated). If the synchronization task for this dataset is not executed due to dependencies, it is usually because there are no data updates in the upstream dataset or modeling task within the business date range configured for the dependent upstream task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/557f9325d6374be7bf7d0ab5b9d3d098~tplv-goo7wpa0wc-image.image) </span> |
|Monitoring configuration |Optional |When dataset synchronization is abnormal, relevant personnel must be notified immediately to prevent issues with data results. The product supports failure alerts, timeout alerts, and result anomaly alerts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da8a6c5e5a3645ca92a7f78f4c2bfe6f~tplv-goo7wpa0wc-image.image) </span> |
|Performance settings |Optional |Performance settings may affect the synchronization and query performance of the dataset. Once saved, performance settings cannot be modified again.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c98ea0512d7d44cda118f54ac8414492~tplv-goo7wpa0wc-image.image) </span> |
|Advanced settings |Optional |Supports setting task synchronization priority. Tasks with higher priority will be synchronized first during system synchronization peaks.<br><br>Runtime parameters can help improve synchronization success rate. For more information, refer to [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters__).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fc7df5c4184446fbd34574e44946452~tplv-goo7wpa0wc-image.image) </span> |


<span id="_2-3-同步状态预览"></span>
## 2.3 Synchronization status preview

When in the dataset save preview status, click Dataset \-\- Synchronization status. Below, you can view the historical synchronization status of the dataset, as well as the historical data synchronization list, logs, and data synchronization/rollback operation buttons.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21e4f9c271fe4775a1ca4bc3eebff67c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-同步状态设置"></span>
## 3.1 Synchronization status configuration

<span id="_3-1-1-同步频率-同步类型"></span>
### 3.1.1 Synchronization frequency \- synchronization type

<span id="（1）概览"></span>
#### (1) Overview

The synchronization types in synchronization frequency are divided into two: scheduled synchronization and manual synchronization.


* When performing synchronization configuration for the first time, the information is displayed as follows:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2512a8ad9a674547b18cceef55300ec9~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* Subsequent configuration changes are displayed as follows:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a5dd50ab275484e9d1672d0678ea9d1~tplv-goo7wpa0wc-image.image" width="666px" /></div>


Therefore, the following introduction to synchronization types will cover synchronization types, synchronization frequency, historical synchronization data, and selection of the historical data time range.

<span id="（2）功能详细介绍"></span>
#### (2) Detailed feature introduction

**Scheduled synchronization**: Supports data synchronization at the monthly, weekly, daily, hourly, and minute levels, and allows you to set the start time.


* Synchronization time (precise timing): Supports specifying precise timing for synchronization at the minute, hour, day, week, and month frequencies. For example, 09:00 every day, 09:00 on Monday, Tuesday, and Wednesday each week, 09:00 on the 1st, 15th, and 30th of each month, and so on.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d5e4fa058c4599934afb64f5b07b94~tplv-goo7wpa0wc-image.image" width="666px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c858ca2be81a425b9387f3fb1a5e81a6~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* Synchronize historical data: Enabled by default. Once enabled, you can choose to synchronize historical data within the selected time range after creating the dataset. This synchronization for the specified time range is performed only during the initial synchronization and will not take effect during subsequent data synchronizations. Additionally, selecting a backtracking queue is supported. The backtracking queue only applies to historical data synchronization, while the queue for scheduled synchronization tasks is configured in advanced settings.


**Manual synchronization**: Only performed during the initial synchronization and will not be automatically updated thereafter. To synchronize, click the dataset, then in the synchronization status, click the operation bar corresponding to a specific business date, and click the [Synchronize] button to perform synchronization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/452988e273f4473f859985b5c2ddb0f5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-同步频率-写入分区"></span>
### 3.1.2 Synchronization frequency \- write partitions


* Scheduled synchronization with hourly or minute\-level frequency supports two write partition modes: by hour and by day.

* Scheduled synchronization with daily, weekly, or monthly frequency supports only the day write partition mode.

> Write partitions cannot be modified after creation.


**Scenario 1:** 

MySQL incremental synchronization: Select scheduled synchronization as the synchronization type, choose hourly synchronization frequency, and select day as the write partition.

Synchronization: Each hourly task synchronizes all data for the day.

Query: In visual queries, select to query data by day.

**Scenario 2:** 

MySQL incremental synchronization: Select scheduled synchronization as the synchronization type, choose minute\-level synchronization frequency, and select hour as the write partition.

Synchronization: Each minute\-level task synchronizes data for the corresponding hour.

Query: In visual queries, you can choose to query data by hour or by day.

<span id="_3-1-3-同步频率-数据生命周期"></span>
### 3.1.3 Synchronization frequency \- data lifecycle

Users can customize the data lifecycle to retain data from the most recent x days, or use advanced settings to specify which data to retain when the limit is exceeded. If the lifecycle is set to 1 day, only data from yesterday is retained.

Suppose a dataset is created on July 1, the lifecycle is set to 7 days, and data is synchronized daily:

(1) Synchronizing historical data/retrospective data is limited to data from the past 7 days only. For example, if today is February 8, only historical data from February 2 to February 7 will be synchronized.

(2) After data synchronization, data can only be retained for 7 days. For example, data for February 7 (business date) is synchronized on February 8, and data for January 31 will be deleted; after synchronization, only data from February 1 to February 7 within these 7 days is available.

<span id="_3-1-4-依赖配置"></span>
### 3.1.4 Dependency configuration

This product provides users with flexible task scheduling dependency configuration capabilities. Scheduling dependencies typically refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development processes. By configuring dependencies between nodes, tasks are scheduled to run upstream and downstream nodes in order—that is, downstream nodes are triggered only after upstream nodes run successfully, ensuring timely production of valid business data.

The dependency configuration of this product offers two main methods: automatic detection of upstream data output and custom dependency configuration. This section provides a detailed introduction to these two methods. Users can establish dependencies on data sources so that when a data source is updated or executed, it triggers synchronization of the dataset.


* **Configuration methods**: Dependency configuration can be set up in two ways: system automatic configuration and custom configuration.

* **Note**: If you choose to configure via a third\-party API, you must first configure the API in the task management module under system management, and then complete the dependency configuration for task scheduling in the dataset's dependency configuration module.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7e8817d5be54ba8a0817892ba1596f3~tplv-goo7wpa0wc-image.image) </span>

 **(1) System automatically builds data source partition detection tasks**


* **Usage restrictions**: Only supported for certain partitioned data sources (Hive/MaxCompute/LAS) and partitioned tables.

* **Special statement**: To avoid inaccurate dependencies caused by incomplete data output during partition detection, please ensure data output is completed before building partitions.


**Method 1: System automatic configuration**

For data sources such as Hive, MaxCompute, and LAS, the system can automatically obtain and display dependency information configured upstream.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it will check every 5 minutes whether the specified partition table of the data source has been generated. If the partition is generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: Sensor tasks mainly refer to scheduled tasks generated by the system script to discover partitions, rather than the current task. For user\-configured scenarios, the system will automatically **sense and investigate** whether the required partition table for the task exists in the user's data source. If it exists, this indicates that the upstream data preparation is complete and the downstream data can start running.


The system will automatically discover Sensor dependency tasks that have already been created for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and the user can choose to configure dependencies manually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ce90d09d501498a9f4564c39b34728e~tplv-goo7wpa0wc-image.image) </span>

**Method 2: Custom configuration**

This product also supports users in modifying dependency offsets and adding dependencies through custom configuration. The specific steps are as follows:

**Step 1**: Click Custom Configuration, then click "Add Dependency" to open the configuration interface. In this interface, you can click Variable Description to view dynamic time\-related prompts, or enter the table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/419d628b2cbc415ea5668f7da05f0f18~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click "Create Custom Dependencies" to open the specific configuration window. At this point, you need to fill in the content shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43861e89113440d7849c78d1ab8e5a98~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911fe0043372485091a6298d1be1278a~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: After clicking Confirm, the custom dependency configuration is considered successful.

 **(2) Third\-party API dependency**

If there is already a scheduling platform for data development or data processing tasks within the enterprise, and it can be configured according to this product's API specifications, then integration and linkage with this product can be achieved to establish task status dependencies for the scheduling platform.


* **Special statement:**  All data sources that can be extracted by this product also support building API dependencies


**Step 1**: **Create a new API task dependency**

Create a new API task dependency in System Management \- Task Management [Data Operation and Maintenance Configuration](https://docs.byteplus.com/docs/dataagent/Data_Operation_and_Maintenance_Configuration).

**Step 2**: **Dependency configuration**

**Method 1**: System automatic configuration

For data sources covered by the API dependency rules created by the user, the system can automatically obtain upstream dependency information and display it.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If generated, the current task will be executed immediately. If the partition is not produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: At the time set by the user, the system automatically detects whether the partition table required by the task exists in the user's data source. If it exists, it means that the preparation of upstream data is complete and downstream data can start running.

> The Sensor task refers to the scheduled task generated by the system script to discover partitions, not the current task.


The system will automatically detect Sensor dependency tasks that have already been created for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and the user can choose to configure custom settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5430312cb3c546c489dbfb71b6492706~tplv-goo7wpa0wc-image.image) </span>

**Method 2**: Custom configuration

This product also supports users in modifying dependency offsets and adding dependencies through custom configuration. The specific steps are as follows:

First, click Custom Configuration, then click "Add Dependency" to open the configuration interface. In this interface, you can click Variable Description to view dynamic time\-related prompts, or enter the table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/419d628b2cbc415ea5668f7da05f0f18~tplv-goo7wpa0wc-image.image) </span>

Next, click "Create System Custom Dependency" to open the specific configuration window. At this point, you need to fill in the contents shown in the figure below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911fe0043372485091a6298d1be1278a~tplv-goo7wpa0wc-image.image" width="1800px" /></div>


As shown above, a custom dependency configuration has been performed for the data table. Relevant term explanations:


|Term |Description |Example |
|---|---|---|
|Data source type |The data source types of the dependency table include [Hive](https://docs.byteplus.com/docs/dataagent/Hive__), [MaxCompute](https://docs.byteplus.com/docs/dataagent/MaxCompute__) , and [LAS](https://docs.byteplus.com/docs/dataagent/LAS___). |Hive indicates that a Hive data type data source has been selected based on data requirements. |
|Database name |The name of the database corresponding to the dependent table. |database_1 indicates that the database named database_1 in the Hive data source has been selected. |
|Table name |The name of the data table corresponding to the dependent table. |dim.user_basic_info_1d_a\-\-user information table indicates that the table dim.user_basic_info_1d_a under this database has been selected (here, \-\-user information table is used as an example). |
|Table type |There are two types: partitioned and non\-partitioned. |For an incremental table, selecting non\-partitioned means selecting all historical data in the data table. Selecting partitioned means selecting all data within the specified partition range. |
|Partition settings |Partition settings are a method for dividing data into different subsets according to specific rules. The dropdown fields for partition settings include all fields in the dependent table you have selected. You can select the partition field based on your table's field types. After selecting the partition field of the data table, choose the corresponding partition. |For example, in the figure above, the partition of the dependent table is p_date (representing a time partition). According to business requirements, we set p_date='20250317' (the partition for March 17, 2025), which means viewing all data within this partition. |
|Dependency type |Data source partition detection dependency, API dependency |By default, data source partition detection dependency is selected. If API dependency is configured in the system, you can choose either data source partition detection dependency or API dependency as needed. |


Finally, after clicking Confirm, the custom dependency configuration is considered successful.

 **(3) Other situations**

**Situation 1**

If a relevant scheduling platform for data development or data processing tasks already exists within the enterprise, users can also choose to manually run tasks based on the status of tasks in their own scheduling platform.

**Special statement:**  Users need to specify the task ID, and if the task is set for manual execution, users can trigger manual execution through OpenAPI.


* First, set the task synchronization type to manual synchronization.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7040c9abb33148a08be8a57ceb818b36~tplv-goo7wpa0wc-image.image) </span>


* Next, find the task ID and project ID (Appid). The task URL contains both the task ID and project ID (the project refers to this product's project space).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb3782b4c11d5386d8b242fa28315f74.png) </span>


* Finally, users can manually trigger the interface to run the task.


**Scenario 2**

If the user's scheduling platform for data development or data task management cannot be configured in this product's task management settings through a standard API, it is necessary to develop and configure an interface via an intermediate layer, so that this product can adapt to build task dependencies. For this situation, we recommend that enterprises adopt the ISV\-developed service approach. For specific solutions, please consult BytePlus staff.

<span id="_3-1-5-监控配置"></span>
### 3.1.5 Monitoring configuration

**Alert conditions:**  The system supports adding monitoring alerts to promptly notify relevant users when data set synchronization is abnormal. Multiple alert rules can be configured. The system provides three types of alert conditions


* Failure alert: A notification will be triggered if data set synchronization fails.

* Timeout alert: Four types of timeout definitions are supported.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12110cc02f49497683c18c472de80fca~tplv-goo7wpa0wc-image.image) </span>


* Absolute time (by Beijing time): An alert will be triggered if synchronization is not completed by the specified time

* Synchronization duration exceeded: An alert will be triggered if data set synchronization exceeds the specified duration. For example, if a 2\-hour duration alert is set and the data set starts synchronizing at 7:00, an alert will be triggered if synchronization is not completed by 9:00

* Exceeding the set synchronization time: Applicable to scheduled synchronization. After setting the synchronization time in the synchronization frequency, if synchronization has not started or has not completed within the specified timeout, an alarm will be triggered. For example, if the synchronization time is set to 7 o'clock and the timeout is "not started within 1 hour after the set synchronization time," then if the dataset has not started synchronization at 8 o'clock (in unsynchronized/not ready status), an alarm will be triggered.

* Synchronization duration fluctuation: An alarm will be triggered if the synchronization process duration for the dataset exceeds the specified time.

* Result anomaly alarm: Monitors the number of data rows and triggers an alarm when the row count is abnormal. Commonly used in the following scenarios

   * Prevent synchronization anomalies or upstream data anomalies that result in no data being synchronized: An alarm can be set when the number of data rows equals 0.

   * Upstream data may be updated multiple times; to prevent incomplete synchronized data, an alarm can be set when the number of data rows is less than the expected row count. For example, if the expected dataset synchronizes 100,000 rows daily and less than 80,000 rows are synchronized, data may be incomplete. In this case, an alarm can be set when the number of data rows is less than 80,000.

   * Abnormal fluctuation rate alarm: The fluctuation rate can be set, and an alarm will be triggered when the fluctuation rate of the number of data rows compared to the previous day or within 7 days exceeds the specified value.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6986f5822c4e48e388501b243c5cbf2c~tplv-goo7wpa0wc-image.image) </span>

Notification methods: Supports Lark, Lark group, Webhook alarms and General IM.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38c4987d80424ac2b08e704cdaa58335~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-6-性能设置"></span>
### 3.1.6 Performance settings

Performance settings may affect the synchronization and query performance of the dataset. Performance settings cannot be modified after the dataset is saved.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4ad54ecfa5249e4a047402b1829d228~tplv-goo7wpa0wc-image.image" width="666px" /></div>


**Sort key:** 

Setting the fields most commonly used as filter conditions as sort keys can make queries faster. Multiple fields can be set as sort keys. The first field has the greatest effect, and the others decrease in effect sequentially. It is recommended not to exceed three fields.

**Shard field:** 

Used to ensure that data is evenly distributed across all storage nodes. If the daily data volume does not exceed 20 million rows, please retain the system default settings. Only one field can be set as the sharding field. You can select the field most commonly used as a dimension (set this field only if its enumeration values exceed 100), or the field most commonly used as a deduplication counting metric (set this field only if its enumeration values exceed 10,000, such as user_id, device_id, item_id, and so on).

> For usage scenarios of sort keys and partition fields, click the button above to view.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05a9d5d699d84a6a9ad99b5acd014d1f~tplv-goo7wpa0wc-image.image) </span>

**Sampling field:** 

When querying, random sampling can be performed based on the sampling field to improve query speed. The sampling field must be specified when creating the table, and only fields of type int, float, or string are supported.

The system defaults to the first primary key field; this is optional.

**Sampling ratio:** 

By default, 100% of the data is sampled according to the sampling field. The smaller the ratio, the less data is sampled, and the faster the visualization query speed.

The system defaults to 100%. The ratio can be adjusted during actual visualization queries.

**Partition:** 

Specify the partition of the dataset. The default is p_date.

**Query consistency assurance:** 

When this feature is enabled, the results of multiple queries on the dataset will be consistent, which can prevent extreme cases such as discrepancies between primary and backup data. However, query performance will decrease accordingly.

<span id="_3-1-7-高级设置"></span>
### 3.1.7 Advanced settings

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/509b6cf4090e40f7bf19f541f3d2ea63~tplv-goo7wpa0wc-image.image" width="666px" /></div>


**Queue and priority:** 

This feature only supports extracting datasets, affecting extraction speed but not query speed.

The default settings do not need to be changed.

**Retry count and retry interval for failures:** 

When dataset synchronization fails, the system will initiate one retry by default. You can customize the number of retries and the retry interval for dataset synchronization failures to improve the success rate of synchronization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b8a84674d0c41c889c2be7f71bf31d2~tplv-goo7wpa0wc-image.image) </span>

**Steps for configuring existing datasets**:

On the dataset "Synchronization Status" page, click Synchronization Configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3048b5d1180947a7ba99566861e0e8ab~tplv-goo7wpa0wc-image.image) </span>

Edit advanced settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed80673f7a24a2e8e0478cb9f154f84~tplv-goo7wpa0wc-image.image) </span>

Adjust the retry count and retry interval in the pop\-up sidebar.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12194fef09154cc7af2887e1fd58773d~tplv-goo7wpa0wc-image.image) </span>

**Multi\-day synchronization:** 

If the data synchronized each day needs to be refreshed multiple times, multi\-day synchronization can be configured. Supports refreshing data from specified N days ago (multiple selections allowed) or the most recent N days. This feature must be used together with [Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL_).

**Runtime parameters:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c954639afe04e3f9b0df0b0f16dddfd~tplv-goo7wpa0wc-image.image) </span>

You can configure dataset synchronization runtime parameters as needed to ensure successful synchronization, optimal performance, and more. For details, see [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters__)

<span id="_3-2-同步状态预览"></span>
## 3.2 Synchronization status preview

When previewing a saved dataset, click Dataset \-\- Synchronization Status to view the historical synchronization details of this dataset in the area below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aaad1ff2ccd43758a8528b8808d3118~tplv-goo7wpa0wc-image.image) </span>


* The upper left area allows you to quickly filter historical data synchronization results by business date, synchronization status, or filter for results where the row count is 0.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96013c1574e64625983518ea651a94de~tplv-goo7wpa0wc-image.image) </span>


* The upper right has the "Synchronization Configuration" and "Data Synchronization" buttons.

   * Click the "Synchronization Configuration" button to display the synchronization configuration information. Click the pencil\-shaped edit icon to the right of each function to enter the settings for that function.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/151f01dfe2294593815bad0793fbc879~tplv-goo7wpa0wc-image.image) </span>


* Click the "Data Synchronization" button to open the synchronization settings dialog box. Select the required business date start and end times from the selection range to immediately batch synchronize the data within that business date range.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/885d6405fe4842b8957152b829584318~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  Select "After enabling synchronization, the synchronization status list displays this time range" to show the execution information for this period in the list. For example, if you select the time period from 2-1 to 2-3 and enable synchronization, the following synchronization information will be displayed in the synchronization status.
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99568f4dc8504015bbbb4d34205f592c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40174238bb9747fc9f0824b320d2a64c~tplv-goo7wpa0wc-image.image) </span>


* In the data backtracking settings, you can choose to execute based on dependencies or ignore dependencies and execute backtracking directly.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77125ad1508744f18b52fa54bcae74d7~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* The list at the bottom displays all synchronized and updated data by business date, synchronization status, scheduled time, synchronization start time, synchronization end time, execution duration, data row count, and operations (Run View, Log, Synchronize).

   * Run View: After clicking, a pop\-up will appear in the lower right corner, presenting the run records of this dataset as a view.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc5d77d1fe6247f796d9aa274dd9e5e1~tplv-goo7wpa0wc-image.image" width="1468px" />   </div>
   

   * Log: After clicking, a new page will open, listing the run log records for this dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f874d52529941bdaf65ced6704a1b4a~tplv-goo7wpa0wc-image.image) </span>


* Synchronize: Click Synchronize to open the backtracking settings. Click Confirm to immediately synchronize the data for that business date range.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbb0d78b9cd74d43a9cf479f0f3add32~tplv-goo7wpa0wc-image.image" width="666px" /></div>
