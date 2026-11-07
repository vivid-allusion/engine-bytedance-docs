---
title: "Modifying the switching time of the operation and maintenance event"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Modifying_the_switching_time"
---

RDS for PostgreSQL supports modifying the execution time of unexecuted operation events. This topic describes how to modify the switching time of operation and maintenance events.

<span id="b1OXpe1U"></span>
## Prerequisites


* The status of the operation and maintenance event is Waiting for execution.

* The scheduled execution time for the operations event is more than 24 hours.


<span id="yMywsO4N"></span>
## Precautions


* Support changing the switching time of the operation and maintenance event to 24 hours after the current time to the latest postponement time. The latest postponement time for an operation and maintenance event is displayed in the operation and maintenance event list.

* If the switch cannot be completed within the specified time period, the switch will be postponed to the next maintenance window.

* The point at which the operation and maintenance event starts is automatically specified based on the instance and the selected switch time.


<span id="VOjoAaKa"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Operation and maintenance event** in the left navigation bar to enter the **Operation and maintenance events** list.

4. In the **Operation and maintenance events** list, click the **Modify the switching time** in the target operation and maintenance event **Actions** column.

5. In the pop\-up **Modify the switching time** window, after completing the following settings, click **OK**.

   
   |Parameter |Note |
   |---|---|
   |Switching time |Select the execution time for the operation and maintenance event. You can choose **Specific time period** or **Maintenance window** to execute.<br><br><br>* **Specific time period**: Switch within the specified time period.<br><br>* **Maintenance window**: Switch within the maintenance window of the instance. You can view the currently set maintenance window for your instance on the Summary page. To adjust, see [Setting maintenance window](https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period). |
   |Specific time period |Select the execution time for the operation and maintenance event.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Setting time periods across days is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The minimum time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Set the time period within the time range prompted by the console.</div><br> |
   |Maintenance window |If you choose to switch within the **Maintenance window**, you need to confirm the **Maintenance window** of the instance. |
   


<span id="IHLruuea"></span>
## Related APIs


|API |Note |
|---|---|
|[ModifyPlannedEventExecuteTime](https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyPlannedEventExecuteTime) |Calling the ModifyPlannedEventExecuteTime API to delay the execution of scheduled operations events. |
