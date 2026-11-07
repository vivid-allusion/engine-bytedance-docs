---
title: "Restarting instances"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Restarting_instances"
---

When the instance reaches full connections or has performance issues, you can manually restart the instance. This article describes how to restart the NDB for MySQL instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 50 instances can be selected for batch restarts at a time.

* Before restarting, please check whether the instance has an ongoing Online DDL task. The restart operation will cause the task to be interrupted. Please proceed with caution. For more information, see [Viewing tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V).


<span id="9oezoKpt"></span>
## Restart impact


|**Restart scope** |**All nodes** |**Specify node** |
|---|---|---|
|Restart sequence |Restart the read\-only node first, then restart the primary node. |Restart only the specified nodes. |
|Restart impact |During the restart of the primary node, only one automatic primary node switch occurs, and the database connection may be briefly interrupted for about 30 seconds. We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism. |When you restart the primary node, the corresponding node will still start as the primary node and will not automatically trigger the primary node switch. |
|Restart time |Under normal circumstances, the restart time for each compute node is approximately 5 minutes. For example, if the instance contains two compute nodes, it takes about 10 minutes to restart the entire instance. |Normally, the restart time is approximately 60 seconds. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only instances with kernel versions <code>3.*.6.1</code> or <code>2.0.6.1</code> and above support restarting a specified node. If the instance does not support the specified restart range, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> and contact technical support to upgrade the instance. For information on how to view the instance version number, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Version_number_management">Version management</a>.</div>


&nbsp;

<span id=".6YeN5ZCv5Y2V5Liq5a6e5L6L"></span>
## Restart a single instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select the target instance **Actions** column for  **...**  \> **Restart instance**.

4. In the dialog box that pops up, set the instance restart information and click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Restart scope |You can choose to restart **All nodes** or **Specify node**. |
   |Node |After selecting specified node in restart range, select the specific node to be restarted in the drop\-down list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you restart a specified node, the node will become unavailable and the request load will be transferred to other nodes that meet the conditions. Please evaluate based on your business situation and proceed with caution.</div><br> |
   |Execution method<br><br> |Select the execution method and choose the value:<br><br><br>* **Execution now** (default): Restart the instance immediately and the instance enters the **Restarting** state. No other operations are allowed in the instance.<br><br>* **Execute during maintainable window**: Restart during the maintenance time window. For details about the maintenance time window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window). |
   


<span id=".5om56YeP6YeN5ZCv5a6e5L6L"></span>
## Batch restart instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instance list** page, select multiple target instances.

5. Confirm the instance information in the **Confirm restart of selected instance** pop\-up dialog box. After confirming that it is correct, click **OK**.

6. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the task execution fails, place the cursor on <strong>Failure</strong> in the <strong>Execution result</strong> column to view the failure reason. You can also click the target instance <strong>Actions</strong> column to <strong>Retry</strong> the task, or click <strong>Batch retry</strong> to retry all failed tasks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can click the <strong>Terminate button</strong> in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, tasks for instances that have not started to restart will no longer be performed and cannot be resumed. If you want to restart again, you need to initiate the restart task again.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[RestartDBInstance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestartDBInstance) |Call the RestartDBInstance to restart the instance. |
