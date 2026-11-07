---
title: "Managing background tasks"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/managing-background-tasks"
---

Operations such as modifying instance configurations run in the background. You can view the status, start time, and end time, and more information about these background tasks on the **Background Task Management** tab of your Kafka instance.

<span id="注意事项"></span>
## Precautions


* Important, non\-immediate instance operations such as modifying instance configurations are displayed as background tasks on the **Background Task Management** tab. Immediate operations such as modifying an instance description are not listed in background tasks.

* If the task status is **Execution failed**, you can view the specific error information in the **Task details** column. If the task status remains **In progress** for an extended period, contact technical support for troubleshooting.


<span id="操作步骤"></span>
## Procedure


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region. In the left\-side navigation pane, click **Instance**.

3. Click the name of the target instance.

4. On the **Background Task Management** tab, view all background tasks for the current instance.

5. Filter tasks. You can filter background tasks by task time, task type, and task source.

   * Filtering by task time: Select the start and end dates of the task at the top of the tab to filter tasks. Background tasks that fall within or overlap with this range are displayed in the results.

   * Filtering by task type: In the **Type** column, select the type of the background task you want to view, such as **Instance configuration modification**, then click **OK** to view the list of background tasks of the specified type.

   * Filtering by task source: In the **Task source** column, select the source of the task you want to view, such as **Open API Call** or **Console operation**, then click **OK** to view the list of background tasks from the specified source.


<span id="后台任务列表"></span>
## Background task list

The **Background Task Management** tab displays the list of all background tasks for the current instance by default. You can filter tasks by task time, task type, and task source. The background task list displays items including task ID, type, status, task details, task source, start time, and end time.
