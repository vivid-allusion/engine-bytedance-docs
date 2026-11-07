---
title: "Synchronization Settings"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Synchronization_Setting"
---

<span id="e4fa2fce"></span>
# 1. Overview

The product supports multiple forms of [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection), and you can configure whether the data in the product is extracted from or directly connected to the original data source. For extracted [Dataset Overview](https://docs.byteplus.com/docs/dataagent/Dataset_Overview), you can adjust the synchronization frequency/time, dependency configuration, synchronization monitoring, performance settings, and other settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/795f0ada068443c39b522a6db65c693f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-同步状态设置"></span>
## 2.1 Synchronization status settings


* **Dataset editing status**

   * When creating a new dataset(see [Overview of Dataset Creation](https://docs.byteplus.com/docs/dataagent/Overview_of_Dataset_Creation)), click the "Synchronization settings" button in the navigation bar at the top of the new dataset interface.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34431e28f734df78778a9a14ebde773~tplv-goo7wpa0wc-image.image) </span>

   * For an existing dataset, clicking "Edit" also allows you to access the same environment.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b3d5b50ec1041faabc41b20d4512fbc~tplv-goo7wpa0wc-image.image) </span>

* **Dataset save preview status**

   * In the dataset save preview status, click Dataset\-\-Synchronization status to see the "Synchronization configuration" and "Data synchronization" buttons.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a70d56f7127943148b5c65114710e8bc~tplv-goo7wpa0wc-image.image) </span>

   * Click the "Synchronization configuration" button to display synchronization configuration information. Click the pencil\-shaped edit icon on the right side of each feature to enter the settings for that feature.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68d242cb9fd84d83863638f343328906~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-同步状态设置操作指引"></span>
## 2.2 Synchronization status settings operation guide


|**Feature items** |**Required or optional** |**Function overview** |
|---|---|---|
|Configure synchronization frequency |Required |Set the update synchronization time for the dataset based on the update frequency of the data source and the required data granularity. Users can modify the synchronization type, synchronization frequency and time, write partition, data lifecycle, synchronization of historical data, and many other settings according to business needs.<br><br><br>* **Initial configuration**<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8822633a56274a068b389e416eaaa816~tplv-goo7wpa0wc-image.image) </span><br><br><br>* **Subsequent changes**<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e94c09cda2f245e596b6eef2d9376492~tplv-goo7wpa0wc-image.image) </span> |
|Dependency configuration |Optional |Dependency configuration allows users to establish associations between a dataset and other data sources, so that dataset B is updated only when dataset A is updated. By using dependency configuration, the readiness status of upstream data can be checked to determine and initiate scheduled synchronization tasks. When the user\-defined synchronization time is reached, the system checks the status of dependency tasks. The synchronization task for this dataset will only start after all corresponding dependency tasks are ready (that is, after the upstream dataset has been updated). If the synchronization task for this dataset is not executed due to dependencies, it is usually because there is no data update in the upstream dataset or modeling task within the business date range configured for the dependent upstream task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/557f9325d6374be7bf7d0ab5b9d3d098~tplv-goo7wpa0wc-image.image) </span> |
|Monitoring configuration |Optional |When a dataset synchronization error occurs, relevant personnel must be notified immediately to avoid issues with data results. The product supports failure alerts, timeout alerts, and result anomaly alerts. Notification methods must be configured in advance via [Office Platform Integration](https://docs.byteplus.com/docs/dataagent/Office_Platform_Integration) before they can be set.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da8a6c5e5a3645ca92a7f78f4c2bfe6f~tplv-goo7wpa0wc-image.image) </span> |
|Performance settings |Optional |Performance settings may affect the synchronization and query performance of the dataset. Once the dataset is saved, performance settings cannot be modified again.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c98ea0512d7d44cda118f54ac8414492~tplv-goo7wpa0wc-image.image) </span> |
|Advanced settings |Optional |Supports setting task synchronization priority. Tasks with higher priority will be synchronized first during system synchronization peak periods.<br><br>Runtime parameters can help improve synchronization success rate. For more explanation, refer to [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters)<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fc7df5c4184446fbd34574e44946452~tplv-goo7wpa0wc-image.image) </span> |


<span id="_2-3-同步状态预览"></span>
## 2.3 Synchronization status preview

In the dataset save preview status, click Dataset\-\-Synchronization status. You can view the historical synchronization status of the dataset, as well as the historical data synchronization list, logs, and data synchronization/rollback operation buttons below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21e4f9c271fe4775a1ca4bc3eebff67c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-同步状态设置"></span>
## 3.1 Synchronization status settings

<span id="_3-1-1-同步频率-同步类型"></span>
### 3.1.1 Synchronization frequency \- synchronization type

<span id="（1）概览"></span>
#### (1) Overview

The synchronization types in synchronization frequency are divided into two: scheduled synchronization and manual synchronization.


* The information displayed when performing synchronization settings for the first time is as follows:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2512a8ad9a674547b18cceef55300ec9~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* The information displayed when changing the configuration later is as follows:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a5dd50ab275484e9d1672d0678ea9d1~tplv-goo7wpa0wc-image.image" width="666px" /></div>


Therefore, the following introduction to synchronization types will cover synchronization types, synchronization frequency, historical synchronization data, and the selection of the time range for historical data.

<span id="（2）功能详细介绍"></span>
#### (2) Detailed feature introduction

**Scheduled synchronization**: Supports data synchronization at the month, week, day, hour, and minute levels. You can set the start time.


* Synchronization time (precise time): Supports specifying the precise time for synchronization at minute, hour, day, week, and month intervals. For example, 09:00 every day, 09:00 on Monday, Tuesday, and Wednesday each week, 09:00 on the 1st, 15th, and 30th of each month, and so on


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d5e4fa058c4599934afb64f5b07b94~tplv-goo7wpa0wc-image.image" width="666px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c858ca2be81a425b9387f3fb1a5e81a6~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* Synchronize historical data: Enabled by default. Once enabled, you can choose to synchronize historical data within the selected time range after creating the dataset. Synchronization for this time range only occurs during the initial synchronization and will not take effect in subsequent data synchronizations. Additionally, selecting a backtracking queue is supported. The backtracking queue is only effective for synchronizing historical data, while the queue for scheduled synchronization tasks is configured in advanced settings.


**Manual synchronization**: Only performed during the initial synchronization and will not be automatically updated thereafter. To synchronize, click the dataset, then in the synchronization status, click the operation bar corresponding to a specific business date, and click the [Synchronize] button to perform synchronization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/452988e273f4473f859985b5c2ddb0f5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-2-同步频率-写入分区"></span>
### 3.1.2 Synchronization frequency \- write partitions


* Scheduled synchronization at hourly and minute frequencies supports two write partition methods: by hour and by day.

* Scheduled synchronization at daily, weekly, and monthly frequencies only supports the write partition method by day.

> Write partitions cannot be modified after creation.


**Scenario 1:** 

MySQL incremental synchronization: Select scheduled synchronization as the synchronization type, select hourly synchronization as the frequency, and choose day as the write partition.

Synchronization: Each hourly task synchronizes all data for the day.

Query: In visual queries, select to query data by day.

**Scenario 2:** 

MySQL incremental synchronization: Select scheduled synchronization as the synchronization type, select minute\-level synchronization as the frequency, and choose hour as the write partition.

Synchronization: Each minute\-level task synchronizes data for the corresponding hour.

Query: In visual queries, you can choose to query data by hour or by day.

<span id="_3-1-3-同步频率-数据生命周期"></span>
### 3.1.3 Synchronization frequency \- data lifecycle

Users can customize the data lifecycle, set to retain data from the most recent x days, or use advanced settings to specify which data to retain when the limit is exceeded. If the lifecycle is set to 1 day, only yesterday's data is retained.

Assume the dataset is created on July 1, the lifecycle is set to 7 days, and data is synchronized daily:

(1) When synchronizing historical data or backtracking data, only data from the past 7 days can be synchronized. For example, if today is February 8, only historical data from February 2 to February 7 will be synchronized.

(2) After data synchronization, data can only be retained for 7 days. For example, data for February 7 (business date) is synchronized on February 8, and data for January 31 will be deleted; after synchronization, only data from February 1 to February 7 within these 7 days will be available.

<span id="_3-1-4-依赖配置"></span>
### 3.1.4 Dependency configuration

This product provides users with flexible options for configuring task scheduling dependencies. Scheduling dependencies typically refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development processes. By configuring dependencies between nodes, tasks are scheduled to run in an orderly manner between upstream and downstream nodes. That is, downstream nodes will only start running after upstream nodes have successfully run, ensuring timely production of valid business data.

The dependency configuration of this product offers two main approaches: automatic detection of upstream data output and custom dependency configuration. This section provides a detailed introduction to these two approaches. Users can establish dependencies on data sources so that when a data source is updated or runs, it triggers synchronization of the dataset.


* **Configuration method**: Dependency configuration can be set up in two ways: system automatic configuration and custom configuration.

* **Note**: To configure using a third\-party API, you must first set up the API in the task management module under system management, and then complete the dependency configuration in the dataset's dependency configuration module.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7e8817d5be54ba8a0817892ba1596f3~tplv-goo7wpa0wc-image.image) </span>

**Step 1: System automatically constructs data source partition detection tasks**


* **Usage restrictions**: Only certain partitioned data sources (Hive/MaxCompute/LAS) and partitioned tables are supported.

* **Special statement**: To avoid inaccurate dependencies caused by incomplete data output during partition detection, please ensure data output is complete before constructing partitions.


**Method 1: System automatic configuration**

For Hive, MaxCompute, and LAS data sources, the system can automatically obtain dependency information configured upstream and display it.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If the partition table is generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: Sensor tasks mainly refer to scheduled tasks generated by the system script to detect partitions, rather than the current task. For user\-configured scenarios, the system will automatically **sense and probe** whether the required partition table for the task exists in the user's data source. If it exists, this indicates that the preparation of upstream data is complete and downstream data can start running.


The system will automatically discover Sensor tasks that have already been created as dependencies for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and users can choose to configure custom settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ce90d09d501498a9f4564c39b34728e~tplv-goo7wpa0wc-image.image) </span>

**Option 2: Custom configuration**

This product also supports users in modifying dependency offsets and adding dependencies through custom configuration. The specific steps are as follows:

**Step 1**: Click Custom Configuration, then click “Add Dependency” to open the configuration interface. In this interface, you can click Variable Description to view dynamic time\-related prompts, or enter the table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/419d628b2cbc415ea5668f7da05f0f18~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click “Create System Custom Dependency” to open the specific configuration window. At this point, you need to fill in the content shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911fe0043372485091a6298d1be1278a~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: After clicking Confirm, the custom dependency configuration is considered successful.

 **(2) Third\-party API dependency**

If there is already a scheduling platform for relevant data development or data processing tasks within the enterprise, and it can be configured according to this product's API specifications, then integration and linkage with this product can be achieved to establish task status dependencies for the scheduling platform.


* **Special statement:**  All data sources supported for extraction by this product also support building API dependencies


**Step 1**: **Create an API task dependency**

Create an API task dependency in System Management \- Task Management, See [Data Operation and Maintenance Configuration](https://docs.byteplus.com/docs/dataagent/Data_Operation_and_Maintenance_Configuration).

**Step 2**: **Dependency configuration**

**Method 1**: System automatic configuration

For data sources covered by the API dependency rules created by the user, the system can automatically obtain upstream dependency information and display it.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: At the time set by the user, the system automatically detects whether the partition table required by the task exists in the user's data source. If it exists, it means that the upstream data preparation is complete and the downstream data can start running.

> Sensor task refers to the scheduled task generated by the system script to discover partitions, not the current task.


The system will automatically detect Sensor dependencies that have already been created for the current table and recommend them for selection. If there are no recommendations, the list will be empty, and the user can choose to configure them manually.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5430312cb3c546c489dbfb71b6492706~tplv-goo7wpa0wc-image.image) </span>

**Method 2**: Custom configuration

This product also allows users to modify dependency offsets and add dependencies through custom configuration. The specific steps are as follows:

First, click Custom Configuration, then click "Add Dependency" to open the configuration interface. In this interface, you can click Variable Description to view dynamic time\-related prompts, or enter the table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/419d628b2cbc415ea5668f7da05f0f18~tplv-goo7wpa0wc-image.image) </span>

Next, click "Create System Custom Dependency" to open the specific configuration window. At this point, you need to fill in the contents shown in the figure below:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911fe0043372485091a6298d1be1278a~tplv-goo7wpa0wc-image.image" width="1800px" /></div>


As shown above, a custom dependency configuration has been performed for the data table. Relevant term explanations:


|Term |Description |Example |
|---|---|---|
|Data source type |The data source types for the dependency table include [Hive](https://docs.byteplus.com/docs/dataagent/Hive), [MaxCompute](https://docs.byteplus.com/docs/dataagent/MaxCompute), and [LAS](https://docs.byteplus.com/docs/dataagent/LAS). |Hive: Indicates that a Hive\-type data source was selected based on data requirements. |
|Database name |The name of the database corresponding to the dependency table. |database_1 indicates that the database named database_1 in the Hive data source has been selected. |
|Table name |The name of the data table corresponding to the dependency table. |dim.user_basic_info_1d_a\-\-user information table: Indicates that the table dim.user_basic_info_1d_a under this database has been selected (here, \-\-user information table is used as an example). |
|Table type |There are two types: partitioned and non\-partitioned. |Using an incremental table as an example, if non\-partitioned is selected, it means all historical data in the data table is selected. If partitioned is selected, it means all data within the specified partition range is selected. |
|Partition settings |Partition settings are a method for dividing data into different subsets according to specific rules. The dropdown fields for partition settings are all fields in the dependency table you selected. You can select the partition field based on your table's field types, and then choose the corresponding partition. |For example, in the diagram above, the partition for the dependency table is p_date (representing a time partition). According to business requirements, we set p_date='20250317' (the partition for March 17, 2025), which means viewing all data within this partition. |
|Dependency type |Data source partition detection dependency, API dependency |By default, data source partition detection dependency is selected. If the system is configured with API dependency, you can choose either data source partition detection dependency or API dependency as needed. |


Finally, after clicking Confirm, the custom dependency configuration is considered successful.

 **(3) Other situations**

**Situation 1**

If a relevant data development or data processing task scheduling platform already exists within the enterprise, users can also choose to manually run tasks based on the status of tasks in their own scheduling platform.

**Special statement:**  Users need to specify the exact task ID, and if the original task is a manually executed task, users can trigger manual execution through OpenAPI.


* First, set the task synchronization type to manual synchronization.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7040c9abb33148a08be8a57ceb818b36~tplv-goo7wpa0wc-image.image) </span>


* Next, locate the task ID and project ID (Appid). The task URL contains both the task ID and project ID (the project refers to the project space of this product).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb3782b4c11d5386d8b242fa28315f74.png) </span>


* Finally, users can run the task by manually calling the interface.


**Scenario two**

If the user's data development or data task management scheduling platform cannot be configured in this product's task management settings via the standard API, it is necessary to develop and configure an interface through an intermediate layer. This product will then adapt to build task dependencies. For this situation, we recommend that enterprises adopt the ISV development service model. For specific solutions, please contact Volcengine staff.

<span id="_3-1-5-监控配置"></span>
### 3.1.5 Monitoring configuration

**Prerequisite:**  The notification method must first complete [Office Platform Integration](https://docs.byteplus.com/docs/dataagent/Office_Platform_Integration) and be pre\-configured before it can be set.

**Alarm conditions:**  You can add monitoring alarms to promptly notify relevant users when data set synchronization is abnormal. Multiple alarm rules can be configured. The system provides three types of alarm conditions.


* Failure alarm: A notification message is triggered if data set synchronization fails.

* Timeout alarm: Supports four types of timeout definitions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12110cc02f49497683c18c472de80fca~tplv-goo7wpa0wc-image.image) </span>

   * Absolute time (Beijing time deadline): An alarm is triggered if synchronization is not completed by the set time.

   * Synchronization duration exceeded: An alarm is triggered if data set synchronization exceeds the set duration. For example, if a 2\-hour duration alarm is set and synchronization starts at 7 o'clock, an alarm will be triggered if synchronization is not completed by 9 o'clock.

   * Exceeding the scheduled synchronization time: Applicable to scheduled synchronization. After setting the synchronization time in the synchronization frequency, if synchronization has not started or completed within the specified timeout period, an alarm will be triggered. For example, if the synchronization time is set to 7 o'clock and the timeout is "exceeding the scheduled synchronization time by 1 hour without starting," then if the dataset has not started synchronization at 8 o'clock (in unsynchronized or not ready status), an alarm will be triggered.

   * Synchronization duration fluctuation: If the synchronization process of the dataset exceeds the specified duration, an alarm will be triggered.

* Result anomaly alarm: Monitors the number of data rows and triggers an alarm when the row count is abnormal. Commonly used in the following scenarios

   * Prevent synchronization anomalies or upstream data anomalies that result in no data being synchronized: An alarm can be set when the number of data rows equals 0.

   * Upstream data may be updated multiple times; to prevent incomplete synchronized data, an alarm can be set when the number of data rows is less than the expected row count. For example, if the expected dataset synchronizes 100,000 rows daily and less than 80,000 rows are synchronized, data may be incomplete. In this case, an alarm can be set when the number of data rows is less than 80,000.

   * Abnormal fluctuation rate alarm: The fluctuation rate can be set, and when the number of data rows fluctuates beyond the specified value compared to the previous day or within seven days, an alarm will be triggered.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6986f5822c4e48e388501b243c5cbf2c~tplv-goo7wpa0wc-image.image) </span>

Notification methods: Supports Lark, Lark group, Webhook alarms and General IM.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38c4987d80424ac2b08e704cdaa58335~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-6-性能设置"></span>
### 3.1.6 Performance settings

Performance settings may affect the synchronization and query performance of the dataset. Once saved, performance settings cannot be modified again.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4ad54ecfa5249e4a047402b1829d228~tplv-goo7wpa0wc-image.image" width="666px" /></div>


**Sort key:** 

Setting the fields most commonly used as filter conditions as sort keys can make queries faster. Multiple fields can be set as sort keys. The first field has the greatest effect, with the others decreasing in order. It is recommended not to exceed three fields.

**Shard field:** 

Used to ensure that data is evenly distributed across all storage nodes. If the daily data volume does not exceed 20 million rows, retain the system default settings. Only one field can be set as the sharding field. You can select the field most commonly used as a dimension (set this only if the field has more than 100 enumerated values), or the field most commonly used as a deduplication count metric (set this only if the field has more than 10,000 enumerated values, such as user_id, device_id, item_id, and more).

> For information on the usage scenarios of sort keys and partition fields, click the button above to view details.

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05a9d5d699d84a6a9ad99b5acd014d1f~tplv-goo7wpa0wc-image.image) </span>


**Sampling field:** 

During queries, random sampling can be performed based on the sampling field to improve query speed. You need to specify this when creating the table. Only fields of type int, float, or string are supported.

The system defaults to the first primary key field. This is optional.

**Sampling ratio:** 

By default, 100% of the data is sampled according to the sampling field. The smaller the ratio, the less data is used, and the faster the visualization query speed.

The system defaults to 100%. You can adjust this during actual visualization queries.

**Partition:** 

Specify the partition of the dataset. The default is p_date.

**Query consistency guarantee:** 

When this feature is enabled, the results of multiple queries on the dataset are guaranteed to be consistent, which can prevent extreme cases such as discrepancies between primary and backup data. However, query performance will decrease accordingly.

<span id="_3-1-7-高级设置"></span>
### 3.1.7 Advanced settings

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/509b6cf4090e40f7bf19f541f3d2ea63~tplv-goo7wpa0wc-image.image" width="666px" /></div>


**Queue and priority:** 

This feature only supports extracted datasets and affects extraction speed, but does not affect query speed.

The default settings do not need to be changed.

**Number of retry attempts and retry interval for failures:** 

When dataset synchronization fails, the system will automatically initiate one retry by default. You can customize the number of retry attempts and the retry interval for dataset synchronization failures to improve the success rate of synchronization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b8a84674d0c41c889c2be7f71bf31d2~tplv-goo7wpa0wc-image.image) </span>

**Steps for configuring existing datasets**:

On the dataset "Synchronization Status" page, click Synchronization Configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3048b5d1180947a7ba99566861e0e8ab~tplv-goo7wpa0wc-image.image) </span>

Edit advanced settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed80673f7a24a2e8e0478cb9f154f84~tplv-goo7wpa0wc-image.image) </span>

In the pop\-up sidebar, adjust the number of retry attempts and the retry interval.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12194fef09154cc7af2887e1fd58773d~tplv-goo7wpa0wc-image.image) </span>

**Synchronize multiple days:** 

If the data synchronized each day needs to be refreshed multiple times, you can set up synchronization for multiple days. Supports refreshing data for a specified N days ago (multiple selections allowed) or for the most recent N days. This feature needs to be used in conjunction with [Custom SQL](https://docs.byteplus.com/docs/dataagent/Custom_SQL).

**Runtime parameters:** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c954639afe04e3f9b0df0b0f16dddfd~tplv-goo7wpa0wc-image.image) </span>

Supports configuring dataset synchronization runtime parameters as needed to ensure successful synchronization, optimize synchronization performance, and so on. For details, see [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters)

<span id="_3-2-同步状态预览"></span>
## 3.2 Synchronization status preview

When the dataset is in the saved preview state, click Dataset \-\- Synchronization Status to view the historical synchronization details of the dataset below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aaad1ff2ccd43758a8528b8808d3118~tplv-goo7wpa0wc-image.image) </span>


* The upper left area allows you to quickly filter historical data synchronization results by business date, synchronization status, or result row count equal to 0.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96013c1574e64625983518ea651a94de~tplv-goo7wpa0wc-image.image) </span>


* The upper right contains the "Synchronization configuration" and "Data synchronization" buttons.

   * Click the "Synchronization configuration" button to display synchronization configuration information. Click the pencil\-shaped edit icon on the right side of each feature to enter the settings for that feature.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/151f01dfe2294593815bad0793fbc879~tplv-goo7wpa0wc-image.image) </span>

   * Click the "Data synchronization" button to open the synchronization settings dialog box. Select the required business date start and end times in the selection range to immediately synchronize data in bulk for the specified business date range.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/885d6405fe4842b8957152b829584318~tplv-goo7wpa0wc-image.image) </span>

      Select "After enabling synchronization, the synchronization status list displays this time range" to show execution information for this time range in the list. For example, when selecting the time period from 2\-1 to 2\-3 and enabling the button, the synchronization status will display the following synchronization information.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99568f4dc8504015bbbb4d34205f592c~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40174238bb9747fc9f0824b320d2a64c~tplv-goo7wpa0wc-image.image) </span>

   * In the data backtracking settings, you can choose to execute according to dependencies or ignore dependencies and execute backtracking directly.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77125ad1508744f18b52fa54bcae74d7~tplv-goo7wpa0wc-image.image" width="666px" />   </div>
   

* The list at the bottom displays all synchronized and updated data by business date of data synchronization, synchronization status, scheduled time, synchronization start time, synchronization end time, execution duration, data row count, and actions (run view, log, synchronization).

   * Run view: After clicking, a dialog box appears in the lower right corner, presenting the dataset's run records in a view format.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc5d77d1fe6247f796d9aa274dd9e5e1~tplv-goo7wpa0wc-image.image) </span>


* Log: After clicking, a new page opens listing the run log records for the dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f874d52529941bdaf65ced6704a1b4a~tplv-goo7wpa0wc-image.image) </span>

* Synchronization: Click Synchronization to open the backtracking settings. Click Confirm to immediately synchronize the data for the specified business date range.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbb0d78b9cd74d43a9cf479f0f3add32~tplv-goo7wpa0wc-image.image" width="666px" /></div>
