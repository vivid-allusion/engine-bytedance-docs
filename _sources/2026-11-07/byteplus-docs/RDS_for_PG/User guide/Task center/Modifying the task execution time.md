---
title: "Modifying the task execution time"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Modifying_the_task_execution_time"
---

Tasks in the Waiting for execution or Waiting for switch state can have their execution/switch time modified. This topic introduces the procedure for modifying the execution/switch time of a task.

<span id="bGhxMdog"></span>
## Prerequisites

Task is in the **Waiting for switch** state.

<span id="nImoCr7B"></span>
## Precautions


* The supported modification time range is from 1 hour later to within 7 days. If the task is expected to complete within 1 hour, you can try to **Execute/Switch immediately**. For more details, see [Executing tasks in advance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Executing_tasks_in_advance).

* If the specified time range cannot complete the switch, the task will be postponed to the instance's next Maintenance window for execution.

* The start time of the task execution will be automatically specified based on the instance situation and the selected switch time.


<span id="ostHST9V"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Task Center** to enter the **Task** list.

4. In the **task** list, click the **Modify execution time** button in the **Actions** column of the target task.

5. In the pop\-up **Modify execution time** window, complete the following settings and then click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Execution time |Select the task execution time. You can choose **Specific time period** or **Maintenance window** to execute.<br><br><br>* **Specified time period**: execute the task within the specified time period.<br><br>* **Maintenance window**: execute the task within the maintenance window set for the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Setting maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period). |
   |Specific time period |If you choose to resize within the **specified time period**, you need to set the time period for task execution.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Setting time periods across days is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Set the time period within the time range prompted by the console.</div><br> |
   |Maintenance window |If you choose to switch within the **Maintenance window**, you need to confirm the **Maintenance window** of the instance. |
   


<span id="soiYh7eO"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyTask](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask) |Call the ModifyTask API to edit the task. |
