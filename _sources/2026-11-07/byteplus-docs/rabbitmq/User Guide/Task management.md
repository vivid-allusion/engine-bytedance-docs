---
title: "Task management"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Background_task_management"
---

When opening or closing extensions or changing instances, the server creates corresponding background tasks and visually displays their status and basic information in the console. You can check the status, start time, and end time of background tasks on the **Task management** tab of the instance.

<span id="注意事项"></span>
## Notes


* Important instance actions that can not be completed immediately, like opening and closing extensions and restarting instances, show as background tasks on the **Task Management** tab. Immediate actions, such as modifying instance descriptions, are not recorded as background tasks.

* If the task status shows **execution failed**, please contact technical support to troubleshoot the issue.


<span id="操作步骤"></span>
## Operation steps


1. Log in to the [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region from the top menu bar and click **Instances** in the left navigation menu.

3. Find the target instance and click the instance name.

4. Under the **Task Management** tab, you can view all background tasks for the current instance.

5. Filter tasks.

   You can filter background tasks by task time, task type, and task source.

   * Filter by task time: select the task start and end dates at the top of the tab. Tasks overlapping with this period will show in the results.

   * Filter by task type: select the background task type to view in the **Type** column, such as **Instance restart** or **Extension change**, then click **Apply** to see the list of tasks of the specified type.

   * Filter by task source: select the task source to view in the **Task source** column, such as **Open API Call** or **Console actions**, then click **Apply** to see the list of tasks from the specified source.


<span id="后台任务列表"></span>
## Background task list

The **Task Management** tab displays all background tasks for the current instance by default. You can filter tasks by task time, type, and task source. The background task list shows the task ID, type, status, details, source, execution start time, and execution end time.
