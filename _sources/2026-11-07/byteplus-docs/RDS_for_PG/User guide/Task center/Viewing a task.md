---
title: "Viewing a task"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_historical_events"
---

This topic describes the procedure for viewing tasks in RDS for PostgreSQL.

<span id="0kGO3tqh"></span>
## Background information

To facilitate instance management and improve operation and maintenance efficiency, RDS for PostgreSQL provides a task center that records and displays various management operations performed on PostgreSQL instances. These operations are named tasks in the task center with the corresponding Open API name of the operation.

In the task list, you can view the instance associated with the task, task name, task state, task progress, task creation time, task start and end times, and elapsed time. In the task list, you can view detailed information about the task. For tasks in the Waiting for execution or To be switched State, you can perform immediate execution, Modify execution time or Modify switch time, and Cancel operations.

<span id="UCjxef0d"></span>
### Task state description


|**Task status** |**Status description** |
|---|---|
|Succeeded |The task has succeeded, and all operations were executed as expected. |
|Failed |The task failed to complete successfully due to an error or abnormal termination. |
|Running |The task is executing the operation and has not yet completed. |
|Waiting for execution |The task has been created but has not started execution and is waiting to start. |
|To be switched |The task has completed the current operation and is waiting to switch to the next stage or status. |
|Cancelled |The task has been manually or automatically cancelled and will not continue. |
|Running \- before switching |The task is running, and the system will decide whether to switch based on the specific situation after completion. |
|Running \- switching |The task is running and is in the switching phase. |
|Running \- after switching |The task is running and the switch has been completed. |
|Rolling back |The task is rolling back. |
|Failed to rollback |Failed to rollback the task. |
|Timeout |Task execution timeout. |
|Suspended |Task paused. |


<span id="ZRd09k56"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task Center** to enter the **Task** list.

4. The **Tasks list** displays information related to tasks such as instance ID, task name, task state, creation time, start/end time/duration, and actions.

   * Tasks can be filtered for viewing as needed, and the task list can also be screened for display.

      * Filter view: supports filtering tasks by instance ID, task name, and creation time.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The task center by default displays tasks from 00:00:00 on the previous day to 23:59:59 today, with a maximum view of tasks from the last 30 days. When filtering tasks by creation time, the maximum filtering period can be set to 7 days.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">After entering the instance, click the instance task at the top right corner on any page to quickly jump to the task center and view tasks related to the current instance.         </div>
         

      * Filter view: supports filtering the task list by task status.

   * Click the task name of the target task to view information such as the instance ID, task name, task status, creation time, start and end time, task duration, and task parameters.


<span id="nZqoGXWV"></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeTasks](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeTasks) |Call the DescribeTasks API to query tasks. |
