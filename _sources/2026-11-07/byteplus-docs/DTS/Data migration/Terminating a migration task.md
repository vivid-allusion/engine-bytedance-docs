---
title: "Terminating a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/terminating_a_migration_task"
---

You can terminate the tasks that must be stopped or have been paused to avoid overwriting the source data into the target database. This topic describes how to terminate a migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data migration task has been created, and the task status is **In progress** or **Paused**. For details about migration task status, refer to [Instructions on migration task status](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions#.5Lu75Yqh54q25oCB6K-05piO).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If source and target instances are in different regions, you need to terminate the task at the destination.

* After termination, the task status will change to completed.

* Restart is not supported after task termination, and executed operations will not rollback. Proceed with caution.

* If you terminate a data migration task of the RDS for SQL Server instance, DTS will automatically clean up the source CDC table and release the occupied storage space after the task is terminated. If the source end is executing other migration tasks, it is recommended to terminate after all tasks are completed to avoid affecting other tasks.


<span id=".6LS555So"></span>
## Description


* When terminating a migration task, you can also terminate the data verification task associated with this task at the same time.

* If only the migration task is terminated, terminating the task will not affect the execution of the data verification task.


<span id=".6LS555So"></span>
## Billing

Data migration tasks currently only support pay\-as\-you\-go billing. Terminating the task does not involve unsubscribing fees and will be billed based on the actual resource usage.

<span id=".57uI5q2i5oyH5a6a5Lu75Yqh"></span>
## Terminate a specified task


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select **More operations** \> **Terminate** at the upper right of the target task.

5. In the **Terminate selected migration task?**  pop\-up, choose whether to terminate the data verification tasks associated with this task as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks.</strong> is checked, meaning that terminating the migration task also terminates all its associated data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Uncheck <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks</strong> to terminate only the migration task without affecting the data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The pop\-up displays up to 5 associated verification tasks. Selecting this option will terminate all verification tasks linked to this task.   </div>
   

6. Click **Terminate**.


<span id=".5om56YeP57uI5q2i5Lu75Yqh"></span>
## Batch terminate tasks


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, check the tasks to be terminated. In the bottom menu bar, select **More operations** \> **Batch terminate**.

5. In the **Terminate task** pop\-up, choose whether to terminate the related data verification tasks of the selected tasks as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks</strong> is checked, meaning that terminating the selected migration task also terminates all its associated data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Uncheck <strong>Terminate the selected task and simultaneously terminate the associated data verification tasks</strong> to terminate only the selected migration tasks without affecting the execution of their related data verification tasks.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Confirm the tasks to terminate in the <strong>Terminate task</strong> dialog box. To exclude tasks from termination, click <strong>Remove</strong> in the <strong>Actions</strong> column to delete them.   </div>
   

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[StopTransmissionTask](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTask) |Call the StopTransmissionTask API to terminate a transmission task. |
|[StopTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/StopTransmissionTasks) |Call the StopTransmissionTasks API to batch terminate transmission tasks. |
