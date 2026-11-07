---
title: "View data transformation progress and status"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/view_data_transformation_progress_and_status"
---

After you create a data transformation task, you can view the configuration and status information on the task by going to the task details page in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After a data transformation task starts running, Torch Log Service (TLS) records the execution status and progress of the task in a service log. You can view and analyze the relevant log data in the corresponding topic. For more information, refer to <a href="https://docs.byteplus.com/docs/tls/service_log_fields">Service log fields</a>.</div>


<span id="操作步骤"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS resides.

3. In the left\-side navigation pane, choose **Data processing** \> **Data transformation**.

   The page that appears displays a list containing data transformation tasks in the current project. The list offers the task names/IDs, status, source topics, and creation time.

4. Find the target task, then click the task name.

   You are redirected to the configuration information tab on the task details page. This page displays the basic information on and transformation rules of the task.


<span id="任务状态说明"></span>
## Task status description

The following table describes the status of data transformation tasks.


|Status |Description |
|---|---|
|Suspended |All consumers corresponding to a transformation task already pause consumption. If the task is not started after you create it for the first time, the task enters the **Suspended** status. |
|In preparation |A transformation task is being started. After all consumers under the consumer group are started successfully, the task enters the **Running** status. |
|Running |A transformation task running as expected. |
|Pause |The background system is pausing a transformation task. After all consumers under the consumer group are stopped, the task enters the **Suspended** status. |
|Restart |A transformation task is being automatically restarted. A task is in this status usually after its rules are modified. During a restart, all consumers are stopped, then started. |
|Completed |A transformation task for data collected within a time period is complete. |
