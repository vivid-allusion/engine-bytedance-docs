---
title: "Manage scheduled SQL analysis tasks"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_scheduled_sql_analysis_tasks"
---

After a scheduled SQL task is created, you can start or pause the task and view its basic configuration information in the console. This topic describes how to manage a scheduled SQL task.

<span id=".5p-l55yL5Lu75Yqh6K-m5oOF"></span>
## View task details

To view detailed information such as specified task status and a task list:


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Schedule SQL**.

   You can view brief information on each task in your task list, such as task status and source topics. For more information on tasks status, refer to [Task status description](https://docs.byteplus.com/docs/tls/manage_scheduled_sql_analysis_tasks#.5Lu75Yqh54q25oCB6K-05piO).

4. Click the target task name.

   You can view basic information on and information on the task execution of the task on the task details page. For more information, refer to [Basic information](https://docs.byteplus.com/docs/tls/manage_scheduled_sql_analysis_tasks#.5Z-65pys5L-h5oGv) and [Instance scheduling results](https://docs.byteplus.com/docs/tls/manage_scheduled_sql_analysis_tasks#.5a6e5L6L6LCD5bqm57uT5p6c6K-05piO).


<span id=".5Z-65pys5L-h5oGv"></span>
### Basic information

This area displays basic information and SQL scheduling information on the current task. The basic information includes the name, ID, and scheduling time range of the task.

The following table describes the configuration items.


|Parameter |Description |
|---|---|
|Task name |The name of a scheduled SQL task. |
|Task ID |The unique identifier of the scheduled SQL task. |
|Description |The description of the scheduled SQL task. |
|Source topic |The source topic of the scheduled SQL task, or the topic in which the original log data is. |
|Target project |The target project of the scheduled SQL task, or the project corresponding to the processed log data. |
|Target topic |The target topic of the scheduled SQL task, or the topic in which the processed log data is stored. |
|Recent update |The last update time of the configuration for the scheduled SQL task. |
|Scheduling scope |The period that indicates the start and end time of the scheduled SQL task. During this period, Torch Log Service (TLS) continuously initiates instance scheduling based on the scheduling cycle. |
|Scheduling cycle |The scheduling cycle of the scheduled SQL task. The scheduling cycle specifies the interval at which each instance performs scheduling. |
|SQL time window |The time range for log query and analysis used when the scheduled SQL task is running. |
|SQL statement |The query and analysis statements that the scheduled SQL task executes. |
|delayed execution |The latency for each scheduling operation. |
|Created on |The creation time of the scheduled SQL task. |


<span id=".5Lu75Yqh5omn6KGM5oOF5Ya1"></span>
### Information on task execution

By default, this area displays a list of instances used within the last five minutes. The instance list displays basic information on instance scheduling, such as scheduling results and the number of instances in the **Dispatch successful**, **Scheduling failure**, and **Running** status respectively.

The following table describes the configuration items.


|Parameter |Description |
|---|---|
|Instance ID |The unique identifier of an instance. |
|Dispatch result |The scheduling result related to the instance. For more information, refer to [Task status description](https://docs.byteplus.com/docs/tls/manage_scheduled_sql_analysis_tasks#.5Lu75Yqh54q25oCB6K-05piO). |
|Scheduling time |The time when the scheduled instance starts execution in the default situation. The time is determined by the scheduling cycle. It is not affected when the previous instance has latency, encounters a timeout, or executes analysis as a supplement. |
|Execution time |The actual execution time of instance scheduling, including the start time and end time. |
|SQL time window |The time range for log query and analysis used when the scheduled SQL task is running. |
|Processing data volume |The number of log entries processed by the scheduled SQL task. |


<span id=".5Lu75Yqh54q25oCB6K-05piO"></span>
### Task status description

The task status and instance status are described as follows.


|Status |Description |
|---|---|
|Running |The scheduled SQL task is running. |
|Suspended |The scheduled SQL task is paused. To restart a task, refer to [Pause or start a task](https://docs.byteplus.com/docs/tls/manage_scheduled_sql_analysis_tasks#.5pqC5YGc5oiW5ZCv5Yqo5Lu75Yqh). |


<span id=".5a6e5L6L6LCD5bqm57uT5p6c6K-05piO"></span>
### Instance scheduling results


|Scheduling Result |Description |
|---|---|
|Running |The instance is scheduling and running. |
|Dispatch successful |The instance performs successful scheduling and the calculation results are successfully written to your target topic. |
|Scheduling failure |Instance scheduling fails. Possible factors include:<br><br><br>* The source topic or target topic does not exist. We recommend that you re\-create a topic, modify the scheduled SQL task configuration, and associate the configuration with the topic.<br><br>* Required permissions are not granted. We recommend that you verify whether the source topic or target topic has the query and data write permissions.<br><br>* The query times out. The query statement is complex. Simplify it. |


<span id=".5p-l55yL5omn6KGM57uT5p6c"></span>
## View execution results


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Schedule SQL**.

4. Click the target task name.

   In the **Task implementation** area of the task details page, find the target instance ID, then click **View execution results** in the action column. This way, you can go to the query and analysis page corresponding to the instance.


<span id=".5pqC5YGc5oiW5ZCv5Yqo5Lu75Yqh"></span>
## Pause or start a task


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Schedule SQL**.

4. Find the target task, then click **Pause** or **start** in its corresponding action column.

5. In the dialog box, click **OK**.


<span id=".5L-u5pS55Lu75Yqh6YWN572u"></span>
## Modify task configurations

After a task is created, you can modify the task configuration as needed. Perform the following steps:


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Schedule SQL**.

4. Find the target task, then click **Edit** in its corresponding action column.

   For more information on task configurations, refer to [Create a scheduled SQL task](https://docs.byteplus.com/docs/tls/create_a_scheduled_sql_task).


<span id=".5Yig6Zmk5Lu75Yqh"></span>
## Delete tasks

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After a scheduled SQL task is deleted, you cannot restore the task. Exercise caution.</div>


* <div data-tips="true" data-tips-type="tip">Deleting a task does not affect the log data saved in the target topic.</div>


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Schedule SQL**.

4. Find the target task, then click  **...**  \> **Delete** in its corresponding action column.

5. In the dialog box, click **OK**.
