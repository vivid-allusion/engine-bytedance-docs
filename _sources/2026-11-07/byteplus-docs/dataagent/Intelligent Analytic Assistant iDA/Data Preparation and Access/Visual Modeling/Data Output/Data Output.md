---
title: "Data Output"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/DataOutput"
---

<span id="_1-概述"></span>
# 1. Overview

Data output refers to the stage of outputting and saving data during the process of creating a visual modeling task. After completing data input and data processing, the task results need to be saved as a dataset to facilitate subsequent visual queries and presentation. There are three types of output operators: output, real\-time label output, and split output. This article introduces the first type, the standard output operator.

<span id="_2-功能介绍"></span>
# 2. Function overview

<span id="_2-1-输出方式选择"></span>
## 2.1 Selecting the output method

In the visual modeling editing interface, click the Add operator button, and in the output type section, select the first "Output" option.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7114b551c363401d90d905f42bd78623~tplv-goo7wpa0wc-image.image" width="610px" /></div>


For modeling tasks where each node has already been processed, you can click "Create dataset" or write to an existing dataset in the "Output dataset" section at the bottom of the task interface.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0448c746d3154fbdb46c99ba447ddfa5~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* When creating a new dataset, you need to fill in the dataset name and description.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aaeec68ea1463ab6602b8a7d5e3cc6~tplv-goo7wpa0wc-image.image) </span>

The output node in visual modeling supports field adjustment. If there is a compatibility issue between the field format of the upstream node and the target storage, you can click "One\-click fix". After clicking, a [Field settings] operator will be added before the current node and the fix will be performed automatically.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bb72fb1b0e5419bb91953903f600fed~tplv-goo7wpa0wc-image.image) </span>


* Database selection: The system supports two storage methods, Hive and ClickHouse, which you can choose as needed.

   * Hive: Partition selection is required.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdf955b7f470460eacca4628e29a3581~tplv-goo7wpa0wc-image.image) </span>

   * ClickHouse: You need to select the cluster, sort key, shard field, sampling field, lifecycle, and partition. (For detailed function explanations, click the question mark to view.)

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6cc8aa51bba4025ab37a255753b5da8~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   


<span id="_2-2-依赖配置"></span>
## 2.2 Configuring dependencies

This product provides users with flexible task scheduling dependency configuration capabilities. Scheduling dependencies generally refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development processes. By configuring dependencies between nodes, tasks can be scheduled to run in an orderly manner. That is, the downstream node will only start running after the upstream node has successfully run, ensuring timely production of valid business data.

This product's dependency configuration provides two main methods: automatic detection of whether upstream data has been produced, and custom dependency configuration. This section provides a detailed introduction to these two methods. Users can establish dependencies on data sources, so that when the data source is updated or executed, the current visual modeling task is triggered to run.


* **Configuration methods**: There are two types—system automatic configuration and custom configuration.

* **Note**: When selecting the third\-party API configuration method, you must first configure the API in the Task Management module under System Management, and then complete the dependency configuration for task scheduling in the dependency configuration modules of Visual Modeling and Datasets.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d039e38490d14f318ba605b2fa2b8342~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-1-系统自动构建数据源分区探测任务"></span>
### 2.2.1 System automatic construction of data source partition detection tasks


* **Usage restrictions:**  Only supports some partitioned data sources (Hive/MaxCompute/LAS) and partitioned tables. \*\*\*In the *SaaS environment, LAS currently only supports built\-in data connections and does not support custom connections*

* **Special statement:**  To avoid inaccurate dependencies caused by incomplete data production during partition detection, please complete data production before creating partitions.


 **(1) System automatic configuration**

For data sources such as Hive, MaxCompute, and LAS, the system can automatically obtain and display the dependency information configured upstream.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If generated, the current task will be executed immediately. If the partition is not produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: Sensor tasks mainly refer to scheduled tasks generated by the system to detect partitions, not the current task. For user\-defined settings, the system will automatically **detect** and **probe** whether the required partition table for the task exists in the user's data source. If it exists, it means that the preparation of upstream data is complete and downstream data can start running.


Based on the data source type of the node table dragged in and the project space, if the system matches a dependency rule, the interface will automatically recommend a "system auto\-configuration" dependency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d172ac84af984202b927b6664257c6cb~tplv-goo7wpa0wc-image.image) </span>

 **(2) Custom configuration**

This product also allows users to modify dependency offsets and add dependencies through custom configuration. The specific steps are as follows:

**Step 1**: Click Custom configuration, then click "Add dependency" to open the configuration interface. In this interface, you can click Variable description to view prompts related to dynamic time, or enter a table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff7e76c080b64d97922e56d2daaec726~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click "Create system custom dependency" to open the specific configuration window. At this point, you need to fill in the content shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/392ddd39226b4f53a1305c080a66c9d4~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: After clicking Confirm, this means the custom dependency configuration is successful.

<span id="_2-2-2-三方api依赖"></span>
### 2.2.2 Third\-party API dependencies

If there is already a scheduling platform for data development or data processing tasks within the enterprise, and it can be configured according to this product's API specifications, then it can be integrated and linked with this product to establish task status dependencies for the scheduling platform.


* **Note:**  All data sources supported for extraction by this product also support building API dependencies.


 **(1) Create a new API task dependency**

Create a new API task dependency in System Management \- Task Management. For details, refer to [Task Management](https://docs.byteplus.com/docs/dataagent/Task_Management____).

 **(2) System auto\-configuration**

For data sources covered by the API dependency rules created by the user, the system can automatically obtain upstream configuration dependency information and display it.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If it has been generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

Based on the data source type of the node table dragged in and the project space, if the system matches a dependency rule, the interface will automatically recommend a "system auto\-configuration" dependency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d672521ef63341e099520d0b69feef98~tplv-goo7wpa0wc-image.image) </span>

 **(3) Custom configuration**

This product also supports users in modifying dependency offsets and adding dependencies through custom configuration. The specific steps are as follows:

**Step 1:**  Click custom configuration, then click "Add dependency" to open the configuration interface. In this interface, you can click variable description to view information related to dynamic time, or enter a table name to search and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d172ac84af984202b927b6664257c6cb~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Click "Create system custom dependency" to open the detailed configuration window. At this point, you need to fill in the information shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff7e76c080b64d97922e56d2daaec726~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  After clicking confirm, the custom dependency configuration is successfully completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/392ddd39226b4f53a1305c080a66c9d4~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-3-其他情况"></span>
### 2.2.3 Other situations

**Situation 1**

If there is already a scheduling platform for relevant data development or data processing tasks within the enterprise, users can also manually execute tasks based on the task status in their own scheduling platform.

**Special note:**  Users need to specify the exact task ID, and if the original task is a manually executed task, users can trigger manual execution through OpenAPI.


* First, set the task update method to manual execution.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb57cbd5ac7a48d092616d2511865a8e~tplv-goo7wpa0wc-image.image) </span>


* Second, locate the task ID and project ID (Appid); the task URL contains the task ID and project ID.

> Project refers to the project space of this product.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8c9b7eec00d468fbb01caf3dd1dcd87~tplv-goo7wpa0wc-image.image) </span>


* Finally, users can run the task by manually triggering the interface.


**Situation 2**

If the user's data development or data task management scheduling platform cannot be configured in this product's task management through the standard API method, it is necessary to develop and configure the interface via an intermediate layer, and then adapt this product to build task dependencies. For this situation, we recommend that enterprises adopt the ISV development service approach. For specific solutions, please consult Volcano staff.

<span id="_2-3-高级配置"></span>
## 2.3 Advanced configuration

For datasets from HIVE data sources, you need to select the execution queue and the execution priority within the queue. Select a queue. The corresponding HIVE query will be executed on the specified queue before importing the dataset. The queue selection affects the duration of dataset synchronization but does not affect the results of visualization queries.

**Running parameters:**  You can configure the running parameters for dataset synchronization as needed to ensure successful synchronization or optimize synchronization performance. For details, see: @运行参数

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7deb8ec2c32849c29e0664db4c9e0b84~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-监控配置"></span>
## 2.4 Monitoring configuration

**Alert conditions:**  You can add monitoring alerts to promptly notify relevant users in case of dataset synchronization exceptions. Multiple alert rules can be configured. The system provides three types of alert conditions


* Failure alert: A notification will be triggered if dataset synchronization fails

* Timeout alert: Three types of timeout definitions are supported


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/412019dd332d4a29bd72c3651ad8761d~tplv-goo7wpa0wc-image.image) </span>


* Result anomaly alert: Monitors the number of data rows and triggers an alert when the row count is abnormal. Common use cases include the following:

   * To prevent synchronization exceptions or upstream data anomalies that result in no synchronized data, you can set an alert when the number of data rows equals 0.

   * To prevent incomplete data synchronization when upstream data is updated multiple times, you can set an alert when the number of data rows is less than the expected count. For example, if the expected dataset synchronizes 100,000 rows per day and less than 80,000 rows are synchronized, data may be incomplete. In this case, you can set an alert when the number of data rows is less than 80,000.

   * Difference percentage alert: To monitor changes in the number of data rows in a timely manner, you can set a difference percentage compared to the previous day, the same period last week, the same period last month, or the average of the previous seven days. For example, if you set an alert for a difference percentage (compared to the previous day) of 10%, an alert will be triggered when the number of data rows changes by more than 10% compared to the previous day.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d16ecc2932f455baceb8885c61aa008~tplv-goo7wpa0wc-image.image) </span>

Notification methods: Email, Feishu, WebEx, DingTalk, WeCom, email groups, and Feishu groups are supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35f3ec480b6b41f49f73605f44e364ea~tplv-goo7wpa0wc-image.image) </span>
