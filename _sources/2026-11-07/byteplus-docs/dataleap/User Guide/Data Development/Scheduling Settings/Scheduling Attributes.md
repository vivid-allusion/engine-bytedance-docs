---
title: "Scheduling Attributes"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/scheduling_attributes"
---

<span id="73e3f463"></span>
## 1 Overview

Scheduling attributes are the necessary configurations required during the execution of DataLeap tasks. Here, you can configure the schedule type, effective date, execution frequency, failed rerun count, and other properties relevant to either periodic or manual execution.

This article will introduce the specific configuration descriptions during task execution.

<span id="5d67b225"></span>
## **2 Function Entry**


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc) **.** 

2. In the **Overview** interface, display the joined projects and click on **IDE development** to enter the corresponding project.

3. In the **Task Development** interface, on the left navigation bar, double\-click to open a batch task and enter the node's edit interface.

4. Click the **Schedule** button on the right navigation bar to enter configuration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/185c08a9d4b7466791786a4429362044~tplv-goo7wpa0wc-image.image) </span>

<span id="74d5241b"></span>
## 3 Scheduling Properties

The scheduling attributes during task execution are introduced in the table below:


|Parameters |Description |
|---|---|
|Scheduling State |Divided into On and Off, On by default.<br><br>On indicates that the task can be scheduled, Off indicates that the task cannot be scheduled.<br><br>You can go to **Operations Center** to turn off or enable task scheduling. |
|Schedule Type |* Periodic scheduling: After the success of upstream tasks, the task automatically starts based on the set frequency and execution time.<br><br>* Manual scheduling: The system will not schedule automatically; it requires manual execution. Manual execution entry point is **Operations Center \> Batch Task Maintenance \> Deploy Task \> Data Backfill**. |
|Scheduling effective date |**When the schedule type is set to periodic scheduling**, you can set the effective time range for the schedule. When not within the effective date range, task instances will not be created. |
|Execution frequency & Execution time |Select task execution frequency and corresponding execution times based on the actual scenario.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After a task is deployed, if the instance corresponding to that day's task has been generated or completed, any adjustments to the task's execution time will only take effect in the instance generated on Day 2.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The mapping methods between business time and the timing of tasks vary depending on the execution frequency of different tasks. For details, see <a href="https://docs.byteplus.com/docs/undefined/689d96727654f3051453d252">Description of platform time variables and constants</a></div><br><br><br>* Minute level: Setting the time interval and execution moment is required for execution time. Time intervals currently support choices of 5 minutes, 10 minutes, 15 minutes, 20 minutes, and 30 minutes levels; the execution moment should be less than the granularity of the interval, for example, for a 10 minutes level schedule, the execution moment supports choices from 0 to 9 minutes.<br><br>* Hourly level: Execution time requires setting multiple selectable execution hours and execution moments.<br><br>* Per Day: Specific time needs to be set for execution time.<br><br>* Weekly: Execution date needs to be set on specific days of the week, supporting multiple selections and a specific execution time.<br><br>* Monthly: Execution date needs to be determined by the specific days of the month, supporting multiple selections along with a specific execution time. |
|Hour interval & range |**When the schedule type is set to periodic scheduling and the execution frequency is set to minute level,**  you can optionally enable the hour interval setting.<br><br>Once the hourly interval settings are enabled, the range of hours for minute\-level task execution needs to be specified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The start time set for hourly intervals must be less than the end time, and time settings that span days are not yet supported.</div><br> |
|Schedule Settings & Scheduling Period |**When the Schedule Type is set to periodic scheduling and the Execution Frequency is chosen as minute level or hour level**, time\-sharing scheduling properties are introduced.<br><br>Enable time\-sharing scheduling. Instances set to run outside the time\-sharing scheduling period will only be submitted for scheduling at the start of the next period, thus alleviating execution pressure during unspecified times.<br><br>Schedule period settings, Example:<br><br><br>1. The time\-sharing scheduling period is from 6:00 to 22:00. If an instance is set to run at 23:00, it will be delayed and submitted for scheduling at 6:00 the next day.<br><br>2. The time\-sharing scheduling period is from 22:00 to 6:00 (from 10 PM on the current day to 6 AM the following day). If an instance is set to run at 7:00, it will be delayed and submitted for scheduling at 22:00 on that day. |
|Earliest Backfill Time |The earliest time for rerunnable historical data. Once set, instances before the earliest backfill time will not be generated. |
|Idle exec settings |When a task's logic temporarily does not need to run but altering the entire data link relationship is not desired, it can be set to idle execute, during which the task will be marked as successful.<br><br>In the overall DAG workflow, setting subnodes to idle execute can temporarily remove the subnodes. |
|Retry trigger conditions |The system provides two types of retry trigger conditions: failure and single run timeout.<br><br><br>* Failed: If the task fails to run and there are remaining retry attempts, it will automatically retry.<br><br>* Single run timeout: If the task running time exceeds the set threshold and there are remaining retry attempts, it will automatically retry. |
|Failed rerun count |The number of retries after a task fails. If the retry running time exceeds 48 hours, the system will automatically end the instance. |
|Rerun interval |Retry time interval after task failure. |
|Maximum concurrency control |This refers to the maximum concurrency for a single task, i.e., the maximum number of instances that a task can run simultaneously. The actual number of executable instances is affected by both the concurrency limit of the task and the total number of concurrent instances of the system. |
|Data backfill suggestions |Indicate whether the task supports data backfill, including **allowed backfill** and **cautious backfill**.<br><br>If you choose **cautious backfill**, enter the reason for caution and set the type of cautious backfill:<br><br><br>* Pop\-up secondary confirmation: When performing backfill/rerun operations on tasks, a pop\-up confirmation prompt will appear.<br><br>* Owner approval:<br><br>   * When an owner initiates backfill or rerun, the owner must confirm the operation in the pop\-up that appears.<br><br>   * When a non\-owner initiates backfill or rerun, the owner must confirm the user's task. |


<span id="d1a7e674"></span>
## 4 Subsequent Actions

After configuring the task scheduling attribute information, you can continue to configure the task scheduling dependencies. See details [Task scheduling depends on](https://docs.byteplus.com/docs/dataleap/scheduling_dependencies).
