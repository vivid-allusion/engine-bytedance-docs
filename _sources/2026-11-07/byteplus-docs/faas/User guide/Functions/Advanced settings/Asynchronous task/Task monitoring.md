---
title: "Task monitoring"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Task_monitoring"
---

This article introduces metrics for monitoring asynchronous tasks, including statistics on task execution, logs, monitoring metrics, and more.

<span id="task-execution-statistics"></span>
## Task Execution Statistics

On the current function details page, click **Async task** to jump to the asynchronous task tab and view the task execution details.

<span id="task-count-statistics"></span>
### Task Count Statistics

The default display on the dashboard shows the overall task execution for the past 7 days, and you can also customize the query period, with a maximum look\-back of 30 days or 10000 tasks (**logical 「OR」** ). FaaS will clear tasks that are in a completed state (Succeeded, Failed, Unknown, Terminated) and only retain records for the most recent 30 days or 10000 entries. The dashboard displays content including the total number of tasks, the number of tasks in each state, and the proportion of tasks in each state.

<span id="task-execution-record-list"></span>
### Task Execution Record List

Displays detailed information about each task in a table format, including task ID, current task status, task submission/end time, and the total duration of the task. For tasks in **Pending** or **Running** states, you can also manually **Terminate invocation**.

<span id="logs"></span>
## Logs

For asynchronous tasks, FaaS provides observation logs at the task, instance, and function levels, facilitating function debugging and fault analysis.

<span id="task-logs"></span>
### Task logs

Supports querying the execution logs of each task. In the **async task** tab of the target function, select the target task ID from the task list, then click on the **Actions** column under **Loging** to jump to the log tab, where you can view the execution logs of the current task and obtain execution records.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Task logs are retrieved and matched through the instance name (pod_name) and task start/end times.</div>


<span id="instance-logs"></span>
### Instance logs

For tasks in Running status, support viewing live logs of the instance.


1. In the **Async task** tab of the target function, select the task ID which is in Running status under the task list, and click on the **Instance name** to view the current task's instance log.

2. (Optional) Click on the top right corner **Instance list** to jump to the instance list page. Partial operational tasks on instances can be performed via Webshell.


<span id="function-logs"></span>
### Function logs

Supports viewing all the execution logs of the current async task function. In the current function details page, click on **Logs** to jump to the log tab, where you can query all execution logs of the current async task function.

<span id="monitoring-metrics"></span>
## Monitoring metrics

On the current function details page, click **Monitoring** to jump to the monitoring tab and view the monitoring metrics of the current async task function.
