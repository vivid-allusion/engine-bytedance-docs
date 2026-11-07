---
title: "Data Output"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Output_"
---

<span id="_1-概述"></span>
# 1. Overview

Data output refers to the stage of data output and saving during the process of creating a visual modeling task. After completing data input and data processing, the task results need to be saved as a dataset for subsequent visual queries and presentation. There are three types of output operators: output, output real\-time labels, and split output. This article will introduce the first type, the regular output operator.

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-输出方式选择"></span>
## 2.1 Output method selection

In the visual modeling editing interface, click the Add Operator button, and in the output type section, select the first "Output" option.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7114b551c363401d90d905f42bd78623~tplv-goo7wpa0wc-image.image" width="610px" /></div>


For modeling tasks where each node has been processed, you can click "Create dataset" or save to an existing dataset in the "Output dataset" section at the bottom of the task interface.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0448c746d3154fbdb46c99ba447ddfa5~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* To create a new dataset, you need to enter the dataset name and dataset description.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07aaeec68ea1463ab6602b8a7d5e3cc6~tplv-goo7wpa0wc-image.image) </span>

The output node in visual modeling supports field correction. If there is a compatibility issue between the field format of the upstream node and the target storage, you can click "One\-click correction". After clicking, a [Field settings] operator will be added before the current node and the correction will be applied automatically.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bb72fb1b0e5419bb91953903f600fed~tplv-goo7wpa0wc-image.image) </span>


* Database selection: The system supports two storage methods, Hive and ClickHouse, which you can choose as needed.

   * Hive: Partition selection is required.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdf955b7f470460eacca4628e29a3581~tplv-goo7wpa0wc-image.image) </span>


* ClickHouse: You need to select the cluster, sort key, shard field, sampling field, lifecycle, and partition. (Click the question mark for detailed feature explanations.)


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6cc8aa51bba4025ab37a255753b5da8~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_2-2-依赖配置"></span>
## 2.2 Dependency configuration

This product provides users with flexible task scheduling dependency configuration capabilities. Scheduling dependencies usually refer to the upstream and downstream relationships between periodic scheduling nodes during data synchronization and data development processes. By configuring node dependencies, tasks are scheduled to run upstream and downstream nodes in order. That is, after the upstream node runs successfully, the downstream node will start, ensuring timely production of valid business data.

The dependency configuration of this product provides two main methods: automatic detection of whether upstream data has been produced and custom dependency configuration. This section provides a detailed introduction to these two methods. Users can establish dependencies on data sources, so that when a data source is updated or run, the current visual modeling task is triggered.


* **Configuration methods**: There are two types—system automatic configuration and custom configuration.

* **Note**: If you choose to configure a third\-party API, you must first configure the API in the task management module under system management, and then complete dependency configuration for task scheduling in the dependency configuration modules of visual modeling and datasets.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8cffb3299d045499d4bc6c1fbfad4ae~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-1-系统自动构建数据源分区探测任务"></span>
### Automatically constructing data source partition detection tasks


* **Usage restrictions:**  Only supports certain partitioned data sources (Hive/MaxCompute/LAS) and partitioned tables. \*\*\*LAS in *SaaS environments currently only supports built\-in data connections and does not support custom connections*

* **Special statement:**  To avoid inaccurate dependencies caused by incomplete data production during partition detection, please complete data production before constructing partitions.


 **(1) System automatic configuration**

For Hive, MaxCompute, and LAS data sources, the system can automatically obtain and display upstream dependency information.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partitioned table of the data source has been generated. If the partition is generated, the current task will be executed immediately. If the partition is not produced for more than 50 hours, the Sensor task will be marked as failed.

> Sensor definition: A Sensor task mainly refers to a scheduled task generated by the system script to detect partitions, not the current task. For user\-configured scenarios, the system will automatically **detect** and **check** whether the required partitioned table for the task exists in the user's data source. If it exists, it means that the upstream data preparation is complete and downstream data processing can begin.


Based on the data source type of the node table that is dragged in and the project space, if the system matches a dependency rule, the interface will automatically recommend a "system auto configuration" dependency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d039e38490d14f318ba605b2fa2b8342~tplv-goo7wpa0wc-image.image) </span>

 **(2) Custom configuration**

This product also allows users to modify dependency offsets and add dependencies through custom configuration. The specific steps are as follows:

**Step 1**: Click Custom configuration, then click "Add dependency" to open the configuration interface. In this interface, you can click Variable description to view dynamic time\-related notes, or enter a table name to search for and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d172ac84af984202b927b6664257c6cb~tplv-goo7wpa0wc-image.image) </span>

**Step 2**: Click "Create system custom dependencies" to open the specific configuration window. At this point, you need to fill in the content shown in the following figure

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff7e76c080b64d97922e56d2daaec726~tplv-goo7wpa0wc-image.image) </span>

**Step 3**: After clicking Confirm, the custom dependency will be configured successfully.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/392ddd39226b4f53a1305c080a66c9d4~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-三方api依赖"></span>
### 2.2.2 Third\-party API dependency

If there is already a scheduling platform for data development or data processing tasks within the enterprise, and it can be configured according to this product's API specification, then integration with this product can be achieved to establish task status dependencies for the scheduling platform.


* **Special note:**  All data sources that can be extracted by this product also support building API dependencies.


 **(1) Create an API task dependency**

Create an API task dependency in System Management \- Task Management. For details, refer to [Task Management](https://docs.byteplus.com/docs/dataagent/Task_Management).

 **(2) System auto configuration**

For data sources covered by the API dependency rules created by the user, the system can automatically obtain upstream configuration dependency information and display it.

**Note:**  After the system wakes up the Sensor task at the scheduled time, it checks every 5 minutes whether the specified partition table of the data source has been generated. If it has been generated, the current task will be executed immediately. If the partition has not been produced for more than 50 hours, the Sensor task will be marked as failed.

Based on the data source type of the node table that is dragged in and the project space, if the system matches a dependency rule, the interface will automatically recommend a "system auto configuration" dependency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d672521ef63341e099520d0b69feef98~tplv-goo7wpa0wc-image.image) </span>

 **(3) Custom configuration**

This product also supports users in modifying dependency offsets and adding dependencies through custom configuration. The specific steps are as follows:

**Step 1:**  Click Custom Configuration, then click "Add Dependency" to open the configuration interface. In this interface, you can click Variable Description to view prompts related to dynamic time, or enter a table name to search for and view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d172ac84af984202b927b6664257c6cb~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Click "Create System Custom Dependencies" to open the specific configuration window. At this point, you need to fill in the content shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff7e76c080b64d97922e56d2daaec726~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  After clicking Confirm, the custom dependency configuration is successfully configured.

<span id="_2-2-3-其他情况"></span>
### 2.2.3 Other scenarios

**Scenario 1**

If there is already a scheduling platform for relevant data development or data processing tasks within the enterprise, users can also manually run tasks based on the task status in their own scheduling platform.

**Special note:**  Users need to specify the exact task ID, and if the original task is a manually executed task, users can trigger manual execution via OpenAPI.


* First, set the task update method to manual run.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb57cbd5ac7a48d092616d2511865a8e~tplv-goo7wpa0wc-image.image) </span>


* Second, locate the task ID and project ID (Appid); the task URL contains the task ID and project ID.

> Project refers to this product's project space.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8c9b7eec00d468fbb01caf3dd1dcd87~tplv-goo7wpa0wc-image.image) </span>


* Finally, users can run the task by manually invoking the interface.


**Scenario 2**

If the user's data development or data task management scheduling platform cannot be configured in this product's task management via standard API methods, it is necessary to develop and configure interfaces through an intermediate layer, after which this product adapts to build task dependencies. For this scenario, we recommend that enterprises adopt the ISV development service approach. For specific solutions, please consult Volcano support staff.

<span id="_2-3-高级配置"></span>
## 2.3 Advanced configuration

For datasets from HIVE data sources, you need to select the run queue and the run priority within the queue. Select a queue. The corresponding HIVE query will be executed on the specified queue before importing the dataset. The queue selection affects the duration of dataset synchronization, but does not impact the results of visualization queries.

**Runtime parameters:**  Supports configuring runtime parameters for dataset synchronization as needed to ensure successful synchronization or optimize performance. For details, see: [Extraction Parameters](https://docs.byteplus.com/docs/dataagent/Extraction_Parameters).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7deb8ec2c32849c29e0664db4c9e0b84~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-监控配置"></span>
## 2.4 Monitoring configuration

**Prerequisites:**  Notification methods require completion of [Office Platform Integration](https://docs.byteplus.com/docs/dataagent/Office_Platform_Integration) prerequisite configuration before they can be set.

**Alert conditions:**  Supports adding monitoring alerts to promptly notify relevant users when dataset synchronization encounters exceptions. Multiple alert rules can be configured. The system provides three types of alert conditions


* Failure alert: A notification message is triggered if dataset synchronization fails

* Timeout alert: Supports selection of three types of timeout definitions


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/412019dd332d4a29bd72c3651ad8761d~tplv-goo7wpa0wc-image.image) </span>


* Result anomaly alert: Monitors the number of data rows and triggers an alert when the row count is abnormal. Commonly used in the following scenarios:

   * To prevent synchronization exceptions or upstream data anomalies resulting in no synchronized data: An alert can be set when the number of data rows equals 0

   * Upstream data may be updated multiple times. To prevent incomplete synchronized data: An alert can be set when the number of data rows is less than the expected row count. For example, if the expected dataset synchronizes 100,000 rows daily and less than 80,000 rows are synchronized, data may be incomplete. In this case, an alert can be set when the number of data rows is less than 80,000

   * Percentage difference alert: To monitor changes in the number of data rows in a timely manner, a percentage difference can be set compared to the previous day, the same period last week, the same period last month, or the average of the previous seven days. For example, if the percentage difference (compared to the previous day) is set to 10%, an alert will be triggered when the number of data rows changes by more than 10% compared to the previous day


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d16ecc2932f455baceb8885c61aa008~tplv-goo7wpa0wc-image.image) </span>

Notification methods: Supports alerts via email, 飞书, WebEx, DingTalk, WeCom, email groups, and 飞书 groups

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35f3ec480b6b41f49f73605f44e364ea~tplv-goo7wpa0wc-image.image) </span>
