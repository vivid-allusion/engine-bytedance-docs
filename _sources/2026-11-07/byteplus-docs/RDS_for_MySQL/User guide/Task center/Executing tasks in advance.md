---
title: "Executing tasks in advance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_tasks_in_advance"
---

RDS for MySQL supports executing tasks in advance that are in the `Waiting for execution` or `Waiting for switch` state. This article describes the procedure for executing tasks in advance.

<span id="前提条件"></span>
## Required

The task is in the **Waiting for execution** or **Waiting for switch** state.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. In the left navigation pane, click **Task center** to go to the **Task** list.

4. In the **task** list, click **Execute now** in the **Actions** column of the target task.

5. In the pop\-up **Confirm to execute immediately?**  **dialog box, click OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you confirm the immediate execution, the entire task will start, including its preparation and switching stages.   </div>
   

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To execute multiple tasks in the <strong>Waiting for execution</strong> state in advance, select them in the <strong>task</strong> list. Click <strong>Execute/Switch now</strong> at the lower\-left corner of the list. In the <strong>Batch Execution</strong> pop\-up window, confirm the Summary. After confirmation, click <strong>Start</strong>. In the pop\-up Batch tasks have been initiated dialog box, view Task progress, and click OK after a task is completed.</div>



* <div data-tips="true" data-tips-type="tip">When you execute multiple tasks early in a batch, the system runs them asynchronously in batches based on resource availability.</div>


* <div data-tips="true" data-tips-type="tip">You can click the Terminate button in the Batch tasks have been initiated dialog box. If you want to make changes again, you need to re\-initiate the batch task.</div>


* <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on Failure in the Execution result column to view the failure reason.</div>



<span id="相关-api"></span>
## Related API


|API |description |
|---|---|
|[ModifyTask](https://www.volcengine.com/docs/6313/1213146) |Call the ModifyTask API to modify the task. |
