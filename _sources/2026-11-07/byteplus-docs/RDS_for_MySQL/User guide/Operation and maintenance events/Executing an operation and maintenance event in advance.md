---
title: "Executing an operation and maintenance event in advance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_an_operation_and_maintenance_event_in_advance"
---

RDS for MySQL supports executing Not executed operation and maintenance events in advance. This topic describes how to execute an operation and maintenance event in advance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The operation and maintenance event is in the **Not executed** state.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left\-side navigation pane, click **Operation and maintenance event** to go to the **Operation and maintenance event** list.

4. In the **Operation and maintenance event** list, click **Execute now** in the **Actions** column of the target event.

5. In the popped\-up **Confirm to execute immediately?**  dialog, select as needed whether to "Switch now" after completing preparations and click **OK**.

   * If "Yes" is selected: After clicking **OK**, the entire task, including the preparation and transition phases of the task, will begin immediately.

   * If "No" is selected: After the preparation work is completed, the task will enter the "To be switched" state, and you can choose the switch time yourself or automatically switch during the specified scheduled switch time period.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Operation and maintenance events of type node reconstruction, SSL certificate update, and startup of stopped instance do not support unbinding of immediate execution to immediate switch.</div>


* <div data-tips="true" data-tips-type="tip">To execute multiple <strong>Not executed</strong> operation and maintenance events in advance, select them in the <strong>Operation and maintenance event</strong> list, click <strong>Execute/Switch now</strong> at the bottom\-left of the <strong>Operation and maintenance event</strong> list, and confirm the summary in the <strong>Batch execution</strong> window. Once confirmed, click <strong>Start</strong>. In the pop\-up <strong>Batch tasks have been initiated</strong> dialog box, view <strong>Task progress</strong>, and click <strong>OK</strong> after a task is completed.</div>


   * <div data-tips="true" data-tips-type="tip">When multiple operation and maintenance events are executed in a batch ahead of schedule, the system processes them asynchronously in smaller batches based on resource availability.</div>


   * <div data-tips="true" data-tips-type="tip">You can click the <strong>Terminate</strong> button in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not yet started changes will no longer be executed and cannot be recovered. If you want to make changes again, you need to re\-initiate the batch task.</div>


   * <div data-tips="true" data-tips-type="tip">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason.</div>



<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyplannedeventexecutetime) |Call the ModifyPlannedEventExecuteTime API to change the execution of scheduled operations events. |
