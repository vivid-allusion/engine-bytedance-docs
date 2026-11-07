---
title: "Operation and Maintenance Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Operation_and_Maintenance_Management"
---

Operations and maintenance management is an operations and maintenance tool provided by this product. It helps users efficiently manage and maintain various tasks. This document describes how to use the specific features of operations and maintenance management.

<span id="5b844de9"></span>
# Prerequisites

Please ensure that your account has **operations or management permissions**.

<span id="73d130e8"></span>
# Usage restrictions

This feature is supported starting from version V2.64.0 in SaaS deployment mode.

<span id="1d78e9a5"></span>
# Feature overview

Users can use features such as the task dashboard, intelligent diagnostics, and resource governance to monitor the progress and status of tasks in real time, standardize task process management, and quickly identify and resolve issues encountered during task operations and maintenance.

Currently, operations and maintenance management includes three main features: task dashboard, task operations, and resource governance.


* **Task dashboard**: Serves as the "data cockpit" of operations and maintenance management, providing real\-time visualization of task statuses and insights into historical data, helping users intuitively understand the overall situation of tasks.

* **Task operations**: Focuses on controlling the task execution process, supports multi\-dimensional queries of task instances, custom batch reruns, termination of abnormal tasks, and more. It is the core tool for handling task exceptions and restoring task execution.

* **Resource governance**: Identifies and cleans up idle data resources (datasets, Excel/CSV files) to avoid storage resource waste and ensure efficient use of system resources.


<span id="97c9de91"></span>
# Quick start


1. Please use the BytePlus Console (Portal) login page. You need to ensure your account has **operations or management permissions**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f70795c8a604e15bc8ab4a438244c02~tplv-goo7wpa0wc-image.image) </span>


2. Task dashboard, task operations, or resource governance. After logging in, you can go to the operations and maintenance management page by clicking "System Management" in the upper right corner of the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dab1f66a511f4335b778e3a316585fd2~tplv-goo7wpa0wc-image.image) </span>

<span id="7429a9ce"></span>
# Task dashboard

<span id="f6932afc"></span>
## Today's task overview

Today's Task Overview page includes the following information:


* Statistics of today's task instances by status

* Today's task overview (hourly statistics)


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cc1fdc31a664310a6e56ba461fc9649~tplv-goo7wpa0wc-image.image) </span>

<span id="8588e996"></span>
## Historical task insights

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d1269a558c24072adbfb12f2e50839d~tplv-goo7wpa0wc-image.image) </span>

The historical task insights page includes the following information:


* Details of yesterday's tasks

   * Number of tasks triggered in the past 48 hours

   * Top 20 tasks by duration yesterday: This section displays required metadata, such as the dataset or visual modeling task name, dataset or visual modeling task ID, owner, project ID, duration of this task instance, output data volume of this instance, and the corresponding average task duration.

   * Top 20 tasks by output data volume yesterday: This section displays required metadata, such as the dataset or visual modeling task name, dataset or visual modeling task ID, owner, project ID, name of the output table, TTL of the output base table, and output data volume of this instance.

* Task insights from the past two weeks (up to one month can be selected)

   * Statistics on the number of successful tasks

   * Statistics on task instance runtime duration

   * Statistics on data source synchronization task runtime duration


<span id="22ca7a12"></span>
# Task operations and maintenance


* Task operations and maintenance includes multi\-dimensional queries, rerunning, and terminating task instances.

* Abnormal task instances are highlighted: consecutive failures are shown with a red background, slow tasks are shown with a blue background.

* Task operations and maintenance supports custom batch reruns, typically used for cluster migration or missing instances.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/349c74c7df44488583d7c18f9046f0c1~tplv-goo7wpa0wc-image.image) </span>

Explanation of search criteria:


|Search criteria |Note |
|---|---|
|ID / Name |Enter the unique identifier (ID) or name of the task instance for an exact search. |
|Project |Select or enter the project name to filter task instances belonging to a specific project. |
|Owner |Select or enter the username of the task owner to filter their task instances. |
|Source |Select the task source. Options: dataset, visual modeling. |
|Instance status |The default status is failure.<br><br><br>* Succeeded: The task instance completes the entire process from triggering to execution without any exceptions, successfully processes data, and outputs valid results. This is the normal end state.<br><br>* Failed: The task instance is interrupted during execution due to data anomalies, code errors, insufficient resources, or other issues, and does not generate valid results. These instances require priority troubleshooting. Includes initial failure and consecutive failures, which can be distinguished by whether they are highlighted in red.<br><br>   * Initial failure: Not highlighted. Tasks that fail on their first run.<br><br>   * Consecutive failures: Displayed with red highlight. Tasks whose latest instance failed yesterday and continue to fail today.<br><br>* Queued: The task instance has been triggered but is waiting for execution due to insufficient queue resources, low priority, or other reasons. This is a transitional state and will eventually change to running or failed. Includes routine trigger and backtracking trigger.<br><br>   * Routine: Instances automatically scheduled by the system.<br><br>   * Backtracking: Instances manually backtracked or rerun through the page.<br><br>* Running: The task instance has acquired resources and entered the data processing workflow but has not yet completed execution. Monitor resource usage and execution progress, paying attention to slow tasks. A slow task is an instance that has been running for more than one hour, highlighted with a blue background in the filter results.<br><br>* Terminated: Terminated tasks include those terminated manually by the user and those terminated abnormally during system operation. |
|Data connection |Filter based on the data connection resources used by the task. |
|Trigger method |Select or enter the trigger type to filter task instances, including routine triggers and retrospective triggers.<br><br><br>* Routine: Instances automatically scheduled by the system.<br><br>* Retrospective: Instances that are manually backfilled or rerun through the page. |
|Scheduling frequency |Select the scheduling cycle for the task. Options include: minute\-level, hour\-level, day\-level, week\-level, month\-level, day\-level (based on trading calendar), and day\-level (the day after each trading calendar day).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The trading calendar feature is currently supported only for products deployed privately with version V2.83.0 or above. To enable this feature, contact BytePlus technical support.</div><br> |
|Start time |Specify a time range to filter task instances that start running within this period. The default is the full day range for the current date. For example, if today is 2025\-09\-12, the default start time is 2025\-09\-12 00:00:00 to 2025\-09\-12 23:59:59. |
|Business date |Filter based on the business date (data date) of the data processed by the task. The default is from seven days prior to the current date up to the current date. For example, if today is 2025\-09\-05, the default business date is 2025\-09\-05 00:00:00 to 2025\-09\-12 23:59:59\*\*.\*\* |
|Queue |Select the resource queue specified when the task runs to filter tasks that consume specific computing resources. For an introduction to queues, see [Queue Configuration](https://docs.byteplus.com/docs/DataWind/109964).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Starting from version V2.87.0, filtering by "Queue" is supported.</div><br> |


<span id="7c0eb8f9"></span>
# Resource governance

<span id="3d0fae21"></span>
## Idle dataset governance

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dfe5c7dd05f470bb10f0646a68b1c72~tplv-goo7wpa0wc-image.image) </span>

The idle dataset governance page includes the following information:


* Supports selecting "project name", entering "number of idle days", and selecting "most recent synchronization time" to locate the target idle dataset.

* Supports batch pause synchronization and batch deletion. Batch deletion moves datasets to the recycle bin, and recovery is supported via the recycle bin.


<span id="3b608e7d"></span>
## Idle Excel/CSV file governance

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73fe562b7f95498dad8b58b432f8d39d~tplv-goo7wpa0wc-image.image) </span>

The idle Excel/CSV file governance page includes the following information:


* Supports selecting "project name", entering "number of idle days", and selecting "most recent synchronization time" to locate the target idle Excel/CSV file.

* Supports "multi\-select results" and "batch deletion" of idle Excel/CSV files for which the user has permission.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After deletion, downstream resources associated with these data connections will be unavailable. To restore these data connections, you must re\-upload the Excel/CSV file.</div>


<span id="cb610d15"></span>
# Usage scenarios

<span id="73497d05"></span>
## Troubleshooting

 **(1) Check logs after receiving an alert**

First, navigate to the task board page and click the failed card. The system will automatically redirect to the task operations page and search for failed instances.

Next, select the failed instance and click the Log button to view the detailed log of the failed task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c942daf7e4f4695a2e929ad8c0dfea2~tplv-goo7wpa0wc-image.image) </span>

 **(2) Determine whether the accumulation alert is caused by a large task**

First, click the running card on the task board page, then check the resources used by the running instance.

If the resource usage accounts for a significant portion of the entire queue, check the execution duration of the instance. If the duration is long, it indicates that the alert is caused by this task instance, and you need to adjust the task model accordingly.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e020db02d1f460eb31642145379812d~tplv-goo7wpa0wc-image.image) </span>

 **(3) Determine whether the accumulation alert is caused by excessive backtracking**

If there are many backtracking tasks in your task board and the number of slow tasks is zero, you can confirm that the alert is caused by excessive backtracking.

In this case, go to the task operations page, select Backtracking as the trigger method, and select Queued as the instance status to locate the details of specific backtracking task instances.

 **(4) View detailed information of running tasks**

To view detailed information of running tasks, such as dataset, project, owner, and more, simply click the running card on the task board to access the detailed metadata of the running instance. You can also click the Jump button to go directly to the dataset or visual modeling task page, and click the Log button to view the task execution log.

<span id="b940a984"></span>
## Recover tasks

 **(1) Complete instance records and rerun tasks**

When instances are missing or clusters are migrated, complete the instance records and rerun the tasks. This can be accomplished through customized rerun.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99f9f4ae5e5747b9b59f0be9406383fb~tplv-goo7wpa0wc-image.image) </span>

 **(2) Recover projects by priority**

When a task fails, you need to first recover the tasks of project 1 with high priority, and then recover the tasks of project 2. Follow the steps below to complete this operation.

**Step 1:**  Click Custom Rerun, select the business date, set the rerun type to Project, enter 1 for Id, select [high\-quality], and then submit.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2280f3abf5bc4745b3ad2101bf1b2284~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Click Custom Rerun, select the business date, set the type to Project, select Project 2 for Id, select [Ordinary], and then submit.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/322fcc1d13f84738b674785a47a3165c~tplv-goo7wpa0wc-image.image) </span>

 **(3) Batch rerun**

To perform a batch rerun for a specific dataset or visual modeling task. First, click the [Custom Rerun] button, select the business date, and set the type to Dataset or Visual Modeling Task. Then, enter the batch Ids separated by **commas** in the Id column, and finally click OK.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51ecdd9d87794e59bcfe4e4b470de6cc~tplv-goo7wpa0wc-image.image) </span>

 **(4) Terminate backtracking tasks**

When task resources are limited, it may be necessary to prioritize routine tasks and terminate all backtracking tasks at once. You can complete this operation by following these steps.

**Step 1:**  On the Task Operations page, set the trigger method to [Backtracking], set the instance status to [Queued], select all instances, and click Terminate.

**Step 2:**  On the Task Operations page, set the trigger method to [Backtracking], set the instance status to [Running], select all instances, and click Terminate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6eb812a68b324dada50fa0601a3107f3~tplv-goo7wpa0wc-image.image) </span>

 **(5) View the time for queued consumption tasks**

When task queuing is normal, you can view the [Queued] card on the Task Dashboard page, which displays the estimated time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d3009713e3f4fdab60f492526d2570a~tplv-goo7wpa0wc-image.image) </span>

 **(6) Rerun all failed tasks**

First, click the Run Failed button on the Task Dashboard page. The system will redirect to the Task Operations page and display all failed tasks for today.

Next, select all failed tasks, and then choose Batch Rerun.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b7da550f26b43e79336ad390f9e91b2~tplv-goo7wpa0wc-image.image) </span>

<span id="c697296a"></span>
## Clean up tasks

**Scenario: Clean up datasets that have been idle for more than 90 days when disk space is limited.** 

First, on the Idle Datasets page, enter 90 for idle days, and then filter the results. Next, select all, and you can choose to pause synchronization.

Finally, refresh the page. The scheduling type for all previously selected tasks on the page has been changed to Manual.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2134787fc36e49129f8d6e4c0ea51175~tplv-goo7wpa0wc-image.image) </span>
