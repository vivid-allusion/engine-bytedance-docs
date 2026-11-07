---
title: "Changing the number of primary instance nodes"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_the_number_of_primary_instance_nodes"
---

You can change the instance configuration according to business needs. This article describes how to change the number of nodes in the primary instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* No primary node switching occurs during a change in the number of primary instance nodes.

* When increasing or decreasing the number of nodes, the services on that node may experience a brief connection interruption of 20 to 30 seconds. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism.

* The time required to change the number of primary instance nodes is independent of the number of nodes to be changed. Normally, changes can be completed within 5 minutes.

* Before changing the number of nodes in the primary instance, please check whether there is an ongoing Online DDL task in the instance. Changing the configuration operation will cause the task to be interrupted. Please proceed with caution. For more information, see [Viewing ticket](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V)s.

* Before changing the instance configuration, confirm if any scheduled auto\-scaling rules exist. If so, manually changing the instance configuration may invalidate these rules. For details about scheduled scaling, refer to [Scheduled scaling management](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management?lang=zh).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, select **Modify configuration \> Change the number of Primary instance nodes** for the Target Instance **Actions** column.

4. Reset the following parameters according to business requirements.

   
   |Name |Description |
   |---|---|
   |Number of primary instance nodes |Select the number of nodes to change, with each primary instance supporting 2 to 16 nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When reducing nodes, the system will first delete nodes with larger node ID numbers. Different node types have different effects on connection endpoints:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The target delete node is the primary node When the target deletion node is the primary node, you need to switch the primary node first. It is recommended to switch the node with the smallest node ID number to the primary node, and then reduce the number of nodes. For operation details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node">Switching to primary node</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The target delete node is a read\-only node</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the custom read\-only endpoint only associates the read\-only nodes that need to be deleted, you need to first associate other read\-only nodes for the read\-only endpoint. When not in use, you can directly delete the read\-only endpoint and then reduce the number of nodes. For operation steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Managing_connection_endpoints">Managing connection endpoints</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Custom read and write connection endpoint: If the custom read/write endpoint is associated with the primary node and the read\-only node to be deleted, after reducing the read\-only node, the read/write endpoint will not be able to read\-write separation, resulting in an increase in pressure on the primary node. It is recommended to associate other read\-only nodes for the read\-write endpoint before reducing the number of nodes. For operation details, please refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Editing connection endpoints</a>.</div><br> |
   |Execution method |Select the execution method and choose the value:<br><br><br>* **Execute now** (default): Deduct or refund the fee immediately and perform the configuration change operation. The instance enters the **Configuration modifying** state. At this time, other operations are not allowed on the instance.<br><br>* **Execute during maintainable window**: Deductions or refunds are made during the maintenance time period, and configuration changes are performed. For details about the maintenance time window, see [Configuring maintenance window](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Configuring_maintenance_window). |
   

5. Click **Confirm order**.

6. On the **Confirm order** page, after confirming that the instance configuration is correct, read and check the **Database Products and Services Terms**.  If you choose to **Execute during maintainable window**, you also need to check the fee description.

7. Then click **Buy now**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |Version |
|---|---|---|
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceName) |Call ModifyDBInstanceName to modify the instance name. |2022\-01\-01 |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |2024\-01\-01 |
