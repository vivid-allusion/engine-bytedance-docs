---
title: "Cancelling a task"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/cancelling_a_task"
---

RDS for MySQL supports canceling pending tasks. This topic describes the steps to cancel a task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The task is **Waiting for execution** or **Waiting for switch**.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When the following task is initiated and selected to be executed in the **Specific time period** or **Maintenance window**, the task will enter the **Waiting for execution** state. The cancellation of the task takes effect immediately.

   * Restart instance (RestartDBInstance)

   * Modify proxy configuration (ModifyDBProxySpec)

* When the following task is initiated and selected to be executed in the **Specific time period** or **Maintenance window**, the task will enter the **Running (before switching)**  state, and perform the corresponding resource preparation and background scheduling work. If a task is cancelled during this period, the cancellation is performed after the current phase (resource preparation and background scheduling) is completed.

   * Migrate availability zones (MigrateToOtherZone)

   * Upgrade instance kernel version (UpgradeDBInstanceEngineMinorVersion)

   * Add node (CreateDBNodes)

   * Delete node (DeleteDBNodes)

   * Change specification (ModifyDBNodeSpec)

   * Temporary upgrade (ModifyDBNodeTemporarySpec)

* After the following tasks are initiated, they enter the **Executing** state. If a task is cancelled during this period, the system will complete the current running phase before terminating the task.

   * Restore to source instance (RestoreToExistedInstance)

* When the following task is initiated and selected to be **executed Immediately**, the task can not be cancelled.

   * Change specification (ModifyDBNodeSpec)

   * Temporary upgrade (ModifyDBNodeTemporarySpec)


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task center** to enter the **Task** list.

4. In the **Task** list, click the **Cancel** button in the **Actions** column of the target task.

5. In the pop\-up **Confirm to cancel** dialog box, click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to cancel multiple tasks in the <strong>Waiting for execution</strong> state, you can check these tasks in the <strong>Task</strong> list, click <strong>Cancel</strong> in the lower left corner of the <strong>Task</strong> list, and confirm the instance information in the pop\-up <strong>Batch cancel</strong> window. Once confirmed, click <strong>Start</strong>. In the pop\-up <strong>Batch tasks have been initiated</strong> dialog box, view <strong>Task progress</strong>, and click <strong>OK</strong> after a task is completed.</div>



* <div data-tips="true" data-tips-type="tip">When multiple tasks are cancelled in batches, the background executes them asynchronously in batches based on resource availability.</div>


* <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not yet started changes will no longer be executed and cannot be recovered. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.</div>



<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifytask) |Call the ModifyTask API to edit the task. |
