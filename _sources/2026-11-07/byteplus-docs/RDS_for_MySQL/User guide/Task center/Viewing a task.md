---
title: "Viewing a task"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_a_task"
---

This topic describes the steps to view tasks for RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

To facilitate instance management and improve operation and maintenance efficiency, RDS for MySQL provides a task center to record and display various management operations performed on MySQL instances. These operations are named tasks in the task center with the corresponding Open API name of the operation.

In the task list, you can view the instance associated with the task, task name, task category, task status, task progress, creation_time, start and end time, and elapsed time. In the task list, you can view detailed information about the task. For tasks in the Waiting for execution or To be switched State, you can perform immediate execution, Modify execution time or Modify switch time, and Cancel operations. For multiple tasks in the Waiting for execution state, you can perform batch operations to execute them now, modify their execution/switching time, or cancel them.

<span id=".5Lu75Yqh54q25oCB6K-05piO"></span>
### Task state description


|Task status |Status description |
|---|---|
|Execution successful |The task has succeeded, and all operations were executed as expected. |
|Execution failed |The task failed to complete successfully due to an error or abnormal termination. |
|Executing |The task is executing the operation and has not yet completed. |
|Waiting for execution |The task has been created but has not started execution and is waiting to start. |
|Waiting for switch |The task has completed the current operation and is waiting to switch to the next stage or status. |
|Cancelled |The task has been manually or automatically cancelled and will not continue. |
|Running (before switching) |The task is running, and the system will decide whether to switch based on the specific situation after completion. |
|Terminating |The task is being terminated. After entering this state, the system will complete the current work and then perform the termination operation. There may be a delay before the termination process actually starts. |
|Terminated |The task was terminated during execution, and the operation has ended. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The primary account can view all tasks in the task center, while sub\-users cannot view some batch operation tasks involving multiple instances in the task center.

* The instance name displayed in the task list is the real\-time name of the instance. If you delete the instance, only its corresponding instance ID is displayed.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task center** to enter the **Task** list.

4. The **Tasks** list displays task\-related information such as the instance name/ID, task name, task category, task status, creation time, start and end time/time consumption, and actions.

   * Tasks can be filtered for viewing as needed, and the task list can also be screened for display.

      * Filter view: supports filtering tasks by instance name/ID, task name, and creation time.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The task center by default displays tasks from 00:00:00 on the previous day to 23:59:59 today, with a maximum view of tasks from the last 30 days. When filtering tasks by creation time, the maximum filtering period can be set to 7 days.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">After entering the instance, click the instance task at the top right corner on any page to quickly jump to the task center and view tasks related to the current instance.         </div>
         

      * Filter view: You can filter the task list by task category and task status.

   * Click the task name of the target task to view information such as the instance ID, task name, task status, creation time, start and end time, task duration, and task parameters, task progress, and configuration comparison. For tasks such as switching the availability zone and recovery to a new instance, you can view the task's progress stage and its progress percentage on the task details page. For modification tasks such as modifying the backup policy, modifying the instance parameter, modifying the instance configuration, modifying the endpoint, and modifying the connection pool mode, you can also view the task's progress stage, overall progress, and a before\-and\-after parameter comparison (configuration comparison) on the task details page **.** 

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The stages displayed for tasks such as modifying instance configuration, switching availability zones, and recovering to a new instance vary depending on the instance specifications.      </div>
      

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DescribeTasks](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describetasks) |Call the DescribeTasks API to query tasks. |
