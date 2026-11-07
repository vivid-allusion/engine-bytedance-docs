---
title: "Dataset Output"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_Output"
---

<span id="83eccd9d"></span>
# Feature Overview

Data output refers to the data output and storage in the process of creating visual knowledge processing tasks. After completing data access \- data processing, the task results need to be saved in the form of a dataset for subsequent visualized queries and displays.

Output class operators include six categories: output data set, output label, split output, external output, output data file, import knowledge engine.

This article will introduce you to the first general output operator, which is **to output data to a dataset, supporting output to the hive/clickhouse engine.** 

<span id="31e96b5d"></span>
# Usage Restrictions

The user needs to complete **data processing** to output the dataset.

<span id="7dcebfa7"></span>
# Operation Steps

<span id="3a944d39"></span>
## **Offline task output**

<span id="5218b806"></span>
### Output dataset


1. In the editing interface of visual knowledge processing, click the Add button of the operator, and in the output type, click Select the first "**output dataset**".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a192822da4444f1890a503ac560173f~tplv-goo7wpa0wc-image.image) </span>

2. For modeling tasks that have been processed by each node, you can click **New Data Set** or Write to Existing Data Set in the "Output Data Set" section at the bottom of the task interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/256b1de1092c48f1a573663c7ad34e63~tplv-goo7wpa0wc-image.image) </span>

   1. To create a new dataset, fill in the dataset name and dataset description.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3a004ba57cf440cbb8f6ba36ff04247~tplv-goo7wpa0wc-image.image) </span>

   2. Set up storage configuration: The system supports Hive and Clickhouse storage methods, and users can choose on demand.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb84bdb9b90243a7a64b87b55cb58dde~tplv-goo7wpa0wc-image.image" width="600px" />      </div>
      

      * Hive: You need to select **Lifecycle Days (required)**  and **Partition (optional)** 

         Data life cycle: The effective storage days of the data. If 7 days are selected, up to 7 days of data will be saved according to the data update time. Data beyond 7 days will be regularly cleared according to the data update time. Recommendation: If you save all the data every day, it is recommended to keep the data within 7 days to reduce storage pressure, such as saving new data or non\-partitioned tables every day. It is recommended to customize the lifecycle according to the commonly used data range. Optional 1 day/7 days/30 days/365 days/permanent.

      * Clickhouse: **Select clusters, sort keys, sharding keys, sample fields, lifecycle days** and **partitions**.

      
      |parameter |explain |
      |---|---|
      |**cluster** |Select the cluster where the dataset is stored. |
      |**sort key** |Setting the field that is most often used as a filter to the sort key makes the query faster. You can set multiple fields as sorting keys, with the first field having the greatest effect, and the rest decreasing in turn. It is recommended that there be no more than three. You cannot use a partition field as a sort key. |
      |**sharding key** |It is used to ensure that data is evenly distributed across storage nodes. If the data volume does not exceed 2000w rows per day, please keep the system default settings. Only one field can be set as sharding key, you can choose the field that is most commonly used as a dimension (this field enumerates more than 100 values to be set), or the field that is most commonly used as a deduplicate count indicator (this field enumerates more than 1w values to be set, such as user_id, device_id, item_id, etc.). |
      |**sample field** |In the visualized query module, you can sample and query according to this field, and only fields of type int, float, and string are supported. |
      |**data lifecycle** |The valid storage days of the data, if 7 days is selected, the data will be saved for up to 7 days according to the data update time, and the data beyond 7 days will be regularly cleared according to the data update time. Recommendation: If you save all the data every day, it is recommended to keep the data within 7 days to reduce storage pressure, such as saving new data or non\-partitioned tables every day. It is recommended to customize the lifecycle according to the commonly used data range. Optional 1 day/7 days/30 days/365 days.<br><br>Data Lifecycle supports **advanced configuration of the lifecycle** . Allows users to customize data retention rules, such as "Retain the last XX days" and "Retain ${specific days} per ${period}".<br><br><br>* **Example: Data retention on the last day of each month for 40 to 50 days.** <br><br>   *This function is controlled by the product switch and is turned off by default. If necessary, you can contact your account manager.* <br><br>* Note: Add condition upper limit is two layers |
      |**partition** |Optional date or other fields with enumerable values are used as partitions. The first\-level partition must be of date type. If there is no suitable field, you can select "System Default Partition" (the value of routine synchronization tasks at the day, week, and month levels is the day before the routine execution of the task, and the value of routine synchronization tasks at the hour and minute levels is the day of routine execution of the task. The value of manually run tasks is the business time selected at runtime) |
      

3. In the offline visual knowledge processing task, when the upstream table structure changes, users are supported to update the table structure of the real\-time dataset.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1e593c08c01e4dcd3a9d8bf9c2f1051.png) </span>


<span id="7a6b4c24"></span>
### **Dependency configuration**

**Data source dependency**

Dependent on the configuration, the upstream data can be combined with the ready state, determine and start timing synchronization tasks. In [Dependency Configuration], for Hive and Clickhouse data sources, the system can automatically obtain the dependency information of the upstream configuration and display it. If you need to modify or customize the configuration dependencies, you can choose a custom configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fdbf4eef5fc466f85b61babb7c669a0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a053522f9d748f7b8bdfa55b477c903~tplv-goo7wpa0wc-image.image) </span>

Supports detection of dependencies on common data sources (Hive JDBC, Maxcompute). Fill in the dependency table, partition information, and dependency type. You can choose a reasonable dependence method according to the situation of the data table in the current task logic, and the system recommends [task dependence \> system custom dependence \> data source partition detection dependence] by default:


* Task dependence: Establishing dependencies based on visual modeling of the output data table or dataset task state

* Data source partitioning detects dependencies: establishes dependencies based on the partitioned data output of the data source

* System custom dependencies: create dependencies through system admin by creating dependency APIs, which are usually used to establish dependencies for tasks related to third\-party data platforms. The logic of the API is defined by system admin. For details, please consult system admin.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For non\-partitioned tables, the system is temporarily unable to recommend dependency system custom dependencies and data source partition probe dependencies.</div>


**Data synchronization task dependence**

It supports the dependency on the task execution status of the three\-party platform by establishing an HTTP API.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ef23bc6f88a47b29b90dea7bcdea13f~tplv-goo7wpa0wc-image.image) </span>

**API configuration**


* Request method: GET

* Sample URL: https://restapi.amap.com/v3/weather/weatherInfo

* Parameters in Params are automatically spliced into custom URLs



|type |explain |
|---|---|
|request parameter description: |The Key and Value in Params will be automatically spliced into a custom URL, where the name of the Key can be customized, and the format of the Value parameter remains unchanged. The system automatically passes in specific task parameters according to the content of the parameters. You can choose to use them as needed |
|parameter Params |* `${dataSourceType}`data source types such as hide\-jdbc, maxcomputer<br><br>* `${dbName}`Library name of data source in task<br><br>* `${tableName}`table name of data source in task<br><br>* `${taskTime}`business date, that is, the date of execution of the specific task, usually the business date is consistent with the partition date<br><br>* `${partition}`value of the partition of the data source in the task |
|custom parameters |If the above system parameters cannot be located to the specific scheduling information, a parameter information that can be identified by a third\-party platform can be defined. The newly added custom parameter information will add a required parameter component to the task configuration. Please define the name reasonably for easy understanding. |
|interface successfully returns structure |API interface call successful, please define the structure returned successfully: JSON structure returns `{"status": "success"}`or `{'status ": 0}` |


<span id="118f2f57"></span>
### **Advanced configuration**

The dataset of the HIVE data source needs to select the run queue and the run priority in the queue. Select a queue, and the corresponding HIVE query will be executed on the specified queue before importing the dataset. Queue selection affects dataset synchronization time, but does not affect visualized query performance.

**Operating parameters:**  Support setting the running parameters of data set synchronization according to requirements to ensure successful synchronization or synchronization performance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fd6e61e1bc64c6cacbb248893d5d4cf~tplv-goo7wpa0wc-image.image) </span>

<span id="f74081d8"></span>
### **Monitoring configuration**

**Pre\-requirements: The** notification method needs to complete the pre\-configuration of **office software integration** before it can be set.

**Alarm conditions:**  Support to add monitoring alarms, notify the corresponding users in time when the data set synchronization is abnormal, and can configure multiple alarm rules. The system provides three types of alarm conditions


* Failure alarm: If the dataset synchronization fails, a message notification will be triggered.

* Timeout alarm: support the selection of three types of timeout definitions

   1. **Deadline Beijing time alarm** : Refers to the system triggering an alarm when the specified Beijing time (UTC + 8) reaches a preset time point.

   2. **Synchronization process time\-consuming alarm** : refers to the calculation from the start of the task, if the task execution time exceeds the preset duration threshold, the alarm is triggered.

   3. **Synchronization time from the set exceeds the alarm** : refers to the task is calculated from a predetermined execution time, if the actual execution time is later than the predetermined time, and exceeds the set time threshold, the alarm is triggered.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/583e77fc5caa4479abc88c7924e56e18~tplv-goo7wpa0wc-image.image) </span>

* Results Abnormal alarm: monitor the number of data lines, alarm when the number of lines is abnormal. It is often used in the following scenarios:

   * To prevent abnormal synchronization or abnormal upstream data, resulting in no data synchronization: alarm when the number of data rows = 0 can be set

   * The upstream data will be updated multiple times to prevent incomplete synchronization data: an alarm can be set when the number of data lines is < the expected number of lines; if the expected data set synchronizes 10w lines of data per day, if the data is < 80000, the data may be incomplete, and the number of data lines can be set. Alarm when the number of lines is < 80000


Notification method: Support email, Feishu, WebEx, DingTalk, WeCom, mail group, Feishu group alarm.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/221a75d843734660aa683ef1e9706b3f~tplv-goo7wpa0wc-image.image) </span>

<span id="e7b9c401"></span>
## **Real\-time task output**

<span id="c1fdaf48"></span>
### Output dataset

Real\-time tasks only support output of clickhouse type.


1. In the editing interface of visual knowledge processing, click the Add button of the operator, and in the output type, click Select the first " **output dataset** ".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a192822da4444f1890a503ac560173f~tplv-goo7wpa0wc-image.image) </span>

2. For modeling tasks that have been processed by each node, you can click **New Data Set** or Write to Existing Data Set in the "Output Data Set" section at the bottom of the task interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4aa0739cdb3946a4a283e4a0c51bdf67~tplv-goo7wpa0wc-image.image) </span>

   1. To create a new dataset, fill in the dataset name and dataset description.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f87c879071934df0afc3ff201f6a1461~tplv-goo7wpa0wc-image.image) </span>

   2. Configuration storage:

      \*\*Support for configuring the data lifecycle, \*\*that is, the valid retention days extracted from the data in the system storage, the non\-partitioned table retains the data according to the data update time, the date partition retains the data according to the partition date, and the data outside the lifecycle will be automatically cleared at 0 o'clock every day.

      \*\*Advanced settings for data lifecycle: \*\*that is, on the basis of the number of retention days, you can selectively retain historical data.

      * Example 1: If the last 7 days are selected, the data of the last 7 days will be retained, and the data beyond 7 days will be cleared according to the data update time.

      * Example 2: (Advanced function): If you select the last 7 days + keep the data of the last day of the month when it expires, the data of the last day of the month in the historical data will also be retained in addition to the last 7 days data

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Quarterly is the natural quarter (e.g. January\-March is the first quarter)      </div>
      

      <span id="44c57510"></span>
      ###### <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Suggestion:      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The longer the retention period, the more system storage resources will be occupied. Please choose a reasonable lifecycle range according to your needs      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><strong>Sort key:</strong> Setting the field most often used as a filter to sort key makes queries faster. You can set multiple fields as sorting keys, with the first field having the greatest effect, and the rest decreasing in turn. It is recommended that there be no more than three.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><strong>Sampling Fields:</strong> Setting the field that is most often used as a filter to the sort key makes queries faster. You can set multiple fields as sorting keys, with the first field having the greatest effect, and the rest decreasing in turn. It is recommended that there be no more than three.      </div>
      

   3. Advanced configuration:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b2302d8443348a6bdc14d27288af9a2~tplv-goo7wpa0wc-image.image) </span>

      
      |parameter |explain |
      |---|---|
      |cluster |Select cluster |
      |sort key |Setting the field that is most often used as a filter to the sort key makes the query faster.<br><br>You can set multiple fields as sorting keys, with the first field having the greatest effect and the rest decreasing in turn. It is recommended that there be no more than three. |
      |sample field |In the visual direct inquiry module, you can sample and query according to this field, and only fields of type int, float, and string are supported. |
      


<span id="5b604943"></span>
### **Advanced configuration**

Support for configuring advanced parameters to ensure stable output for real\-time tasks.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f1b9114342b46b099c4f627f0019330~tplv-goo7wpa0wc-image.image) </span>

The currently supported parameters and descriptions are as follows:


|parameter name |explain |
|---|---|
|parallelism.default |default parallelism |
|taskmanager.memory.process.size |Total process memory size of taskmanager |
|yarn.containers.vcores |Virtual cores per yarn container |
|taskmanager.numberOfTaskSlots |Number of slots provided by taskmanager |
|jobmanager.memory.process.size |Total process memory size of jobmanager |
|yarn.appmaster.vcores |Virtual cores of appmaster in yarn |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Advanced parameters are valid only if there is a "data cleaning" operator in the leading node or if the output dataset is configured with a "CDP Reference ID Field".</div>


<span id="01b77aad"></span>
### Dirty data setup

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1df918d89b4431fb6799fb4eb63b52a~tplv-goo7wpa0wc-image.image) </span>


|parameter |explain |
|---|---|
|whether to enable dirty data collection |Enable or disable dirty data collection |
|dirty data collection per second |No numbers indicate no sampling |
