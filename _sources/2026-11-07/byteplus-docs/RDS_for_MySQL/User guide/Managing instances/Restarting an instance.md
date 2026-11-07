---
title: "Restarting an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance"
---

When an instance experiences full connections or performance issues, you can restart the instance manually. This topic describes the steps to restart a MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The time to restart the instance depends on the load state of the instance, which will cause the business to flash out once or twice. Please operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection flashes on the business.

* Double\-node instances support restarting specific read\-only nodes. During the restart process of a read\-only node, the corresponding nodes will be unavailable, and the load of the current read\-only node will be transferred to other nodes that meet the conditions. Proceed after accurately evaluating the impact of the restart.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click  **...**  \> **Restart instance** in the **Actions** column of the target instance.

5. In the dialog box that appears, configure the following settings and click **OK**.

   
   |Parameter |Details |
   |---|---|
   |Restart scope |You can choose to restart all nodes or specific read\-only nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For single\-node instances, the restart scope can only be <strong>All nodes</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Double\-node instances support restarting all nodes or some read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For multiple\-node instances, selecting a restart scope is not supported. You can only restart the entire instance.</div><br> |
   |Restart time |Select a time to restart the instance.<br><br><br>* **Restart immediately**: restarts the instance immediately after you click OK.<br><br>* **Specific time period**: Restart within the specified time period.<br><br>* **Maintenance window**: Restart within the maintenance window set for the instance. |
   |Specific time period |If you select to restart within a **specific time period**, you must set the restart time period.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting the upgrade time period across days is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the upgrade time period within the time frame prompted by the console.</div><br> |
   |Maintenance window |If you choose to restart during the **Maintenance window**, confirm the instance's **Maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   |Force restart |Select whether to enable force restart. When force restart is disabled, the restart may take too long or even fail due to factors such as high primary\-secondary latency. Once enabled, the system will restart quickly. This may cause data loss or service interruption. Confirm that you accept this risk.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Single\-node instances only support force restart.</div><br> |
   |Restart database proxy |Select whether to restart the database proxy. If you choose not to restart, connections will not be interrupted when Connection persistence is enabled and the session meets the [conditions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_connection_persistence).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This is only supported when the database proxy feature is enabled for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Single\-node instances do not support this feature.</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Note |
|---|---|
|[RestartDBInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restartdbinstance1) |Call the RestartDBInstance API to restart a MySQL instance. |
