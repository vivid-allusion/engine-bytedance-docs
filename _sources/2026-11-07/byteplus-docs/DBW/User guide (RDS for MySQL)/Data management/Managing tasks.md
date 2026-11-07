---
title: "Managing tasks"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/task-management-for-mysql"
---

Database Workshop (DBW) supports task management by executing SQL statements at a fixed time or in cycles. This topic describes how to create and manage tasks on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance and account for RDS for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

<span id=".5LyY5Yq_"></span>
## Advantages


* **Automation and timing**: Through task management, you can set SQL statements to be executed automatically at specific times without manual operation. It is helpful for scheduled tasks, such as updating data or generating reports on a regular basis.

* **Improve efficiency**: You can schedule time\-consuming SQL tasks to be executed during system idle times (such as off\-peak business periods), maximizing the use of system resources without affecting normal business operations.

* **Avoid human error**: Automated task scheduling can reduce errors caused by human error.

* **Improve data consistency**: If there are multiple tasks that need to run on the same or similar data sets, task scheduling can ensure that all tasks run in a predetermined order immediately after the data is updated, ensuring the data consistency processed by each task.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can create up to 10 tasks per instance.

* In a cyclic task, if the execution time exceeds the set cycle, up to 3 executing subtasks can exist under a task at the same time. If 3 tasks are already in progress, subsequent subtasks scheduled for execution will be automatically skipped.

* The `select `keyword can not appear in SQL statements, but you can use `select sleep`.


<span id=".5Yib5bu65Lu75Yqh"></span>
## Create a task


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Task management**.

4. On the **Task management ** page, click **Create task**.

5. In the Create task dialog box, set the parameters described in the following table.

   
   |**Parameter** |||**Description** |
   |---|---|---|---|
   |**Task name** |||Customize the task management name. |
   |**Task type** |||Only **single instance** is supported. **SQL**, and modification is not supported. |
   |**Execution time** |**Fixed time** |**Fixed time** |Set the time point for task execution as needed. After the task is executed at the set time point, the **Task status** will become **Expired**. |
   ||**Cycle time** |**Start time** |Set the time when the task starts to be executed cyclically as needed. |
   |||**End time** |Optional. Set the time when the task ends the loop execution as needed.<br><br><br>* Set end time: If the end time is earlier than the last time the task was executed plus the period, the task will expire.<br><br>* Not set end time: If the execution time of a task exceeds the set period, the next execution time will be the execution end time of this task plus the period. |
   |||**Execution interval** |Set the execution interval of the task as needed, and support the selection of execution intervals in **seconds**, **minutes**, **hours**, and **days**. At the same time, it supports setting the execution cycle. |
   |||**When there are tasks in progress** |When a task is being executed within the loop execution period, you can choose to **Skip**, **Execute after the previous task completes**, or **Ignore the previous task and execute it directly**. |
   |**Database type** |||Select database type from the drop\-down list. Currently, only **RDS for MySQL** is supported. |
   |**Select instance** |||From the drop\-down list, select the target instance to be managed.<br><br>If security control is enabled on the target instance, you do not need to enter the database account and password, and vice versa. For information on how to enable security control for an instance, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql). |
   |**Select database** |||From the drop\-down list, select the target database. |
   |**Execute SQL** |||Enter the SQL statement to be executed. |
   |**Remarks** |||(Optional) It is used to describe the reason or goal for changes to create SQL tasks, reducing communication costs. |
   |**Advanced configuration** |||Optional. Check whether to enable transactions and ignore errors as needed, as shown below:<br><br><br>* **Enable transaction**: If a transaction is enabled and the executed SQL contains multiple SQL statements, then the multiple SQL statements will be treated as a transaction for operation.<br><br>* **Ignore error**: When an unexpected alarm or exception is encountered in the execution of a SQL statement, if the ignore error is enabled, the SQL statement will continue to execute without stopping due to the alarm. |
   


<span id=".5byA5ZCvLeWFs-mXreS7u-WKoQ=="></span>
## Enable/Disable a task

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Closing expired tasks is not supported.</div>


* <div data-tips="true" data-tips-type="tip">After the task is disabled, the task will not be executed at the next execution time.</div>


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Task management**.

4. On the **Task management ** page, click the button under the **Task status** column of the target task.

5. Are you **sure you want to disable?**  Or, **are you sure you want to enable?**  dialog box, click **OK**.


<span id=".57yW6L6R5Lu75Yqh"></span>
## Modify a task


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Task management**.

4. On the **Task management ** page, click **Edit** in the **Actions ** column of the target task.

5. In the Edit task dialog box, modify the **Task name**, **SQL text**, and **Remarks**.

6. Click **OK**.


<span id=".5Yig6Zmk5Lu75Yqh"></span>
## Delete a task


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Task management**.

4. On the **Task management** page, click **Delete** in the **Actions** column of the target task.

5. In the **Confirm deletion** dialog box, click **OK**.


<span id=".5p-l55yL5Lu75Yqh5omn6KGM6K6w5b2V"></span>
## View task execution records


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Task management**.

4. On the **Task management** page, you can view the basic information of the task, including **Task ID**, **Task name**, **Owning instance**, **Task status**, **Database type**, **Lastest execution status**, **Last execution time**, **Creation time**, and **Execution status**. At the same time, you can also view the following information:

   * Task information: Click the target task name, and on the **Task information** tab of the **Task details** panel, view the **Task name**, **Task type**, **Execution time**, **Database type**, **When there are tasks in progress**, **Database instance**, **Database**, **Execute SQL**, **Remarks**, **Enable transaction?**  and **Whether to ignore errors**.

   * Task execution record: Click the **Execution record** in the **Actions** column of the target task, and on the execution record tab of the task details panel, view all execution records, including **Task execution ID**, **Execution start time**, **Execution status**, **Task failure reason**, **Task end time**, and Execution log.
