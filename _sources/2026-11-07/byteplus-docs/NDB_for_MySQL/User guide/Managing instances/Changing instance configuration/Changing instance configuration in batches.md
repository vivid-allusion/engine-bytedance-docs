---
title: "Changing instance configuration in batches"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_instance_configuration_in_batches"
---

NDB for MySQL supports batch modification of instance configuration, which allows you to modify instance configurations for instances with consistent business requirements, and improve the efficiency of instance management. This article describes how to batch modify instance configuration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* The instance currently has no **pending** configuration change events. You can search and view them by instance ID in the **Planned event** list. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During the node specification change process, the instance will be restarted and the primary node will be switched.

   * Change order: First make configuration changes to the read\-only nodes, then make configuration changes to the primary node.

   * Impact: During the configuration change, the database may experience a 20\-30 second disconnection. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism.

* The time required to change node specifications mainly depends on the number of nodes in the instance. Under normal circumstances, the time required for each computing node to change is approximately 5 minutes. For example, when an instance with 2 nodes is upgraded from 4C to 8C, the total time taken is about 10 minutes.

* No primary node switching occurs during a change in the number of primary instance nodes.

* When increasing or decreasing the number of nodes, the services on that node may experience a brief connection interruption of 20 to 30 seconds. Therefore, it is recommended to perform configuration changes during off\-peak hours and ensure that the application has an automatic reconnection mechanism.

* The time required to change the number of primary instance nodes is independent of the number of nodes to be changed. Normally, changes can be completed within 5 minutes.

* Before changing the configuration, check whether there is an Online DDL task in progress on the instance. Changing the configuration will interrupt the task, so proceed with caution. For more information, see [Viewing ticket](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V)s.

* A single support to select up to 50 **computing billing type** and **storage billing type** are the same instance batch change configuration.

* Before changing the instance configuration, confirm if any scheduled auto\-scaling rules exist. If so, manually changing the instance configuration may invalidate these rules. For details about scheduled scaling, refer to [Scheduled scaling management](https://docs.byteplus.com/en/docs/DBW/scheduled-scaling-management?lang=zh).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance list** page, select multiple target instances.

4. Select **Instance list** at the bottom of the page  **...**   **\> Modify configuration**.

5. On the **Batch modify configuration** page, reset the following parameters according to business requirements.

   
   |Name |Description |
   |---|---|
   |Specification type |Please select the specification type.<br><br><br>* **Exclusive type**: Completely exclusive CPU and memory, long\-term stable performance, will not be affected by the behavior of other instances on the physical machine. The top of the exclusive specification is exclusive TCE\-metal, completely monopolizing all the resources of a TCE\-metal.<br><br>* **General type**: Exclusive access to allocated memory, sharing CPU resources with other generic instances on the same physical machine. Enjoy scale dividends through resource reuse, with high cost performance. |
   |Node specification |Each specification has a corresponding number of cores and memory, and you can choose according to your business requirements. |
   |Unified number of nodes |* Select **No** (default) to not change the number of nodes for the instance.<br><br>* Select **Yes** to change the number of nodes for all target instances. |
   |Number of primary instance nodes |Select the number of nodes to change, with each instance supporting 2 to 16 nodes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When reducing nodes, the system will first delete nodes with larger node ID numbers. Different node types have different effects on connection endpoints:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The target delete node is the primary node</div><br><br><br>   <div data-tips="true" data-tips-type="tip">When the target deletion node is the primary node, you need to switch the primary node first. It is recommended to switch the node with the smallest node ID number to the primary node, and then reduce the number of nodes. For operation details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node">Switching to primary node</a>.   </div><br>   <br><br>* <div data-tips="true" data-tips-type="tip">The target delete node is a read\-only node</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the custom read\-only endpoint only associates the read\-only nodes that need to be deleted, you need to first associate other read\-only nodes for the read\-only endpoint. When not in use, you can directly delete the read\-only endpoint and then reduce the number of nodes. For operation steps, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Managing_connection_endpoints">Managing connection endpoints</a>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Custom read and write connection endpoint: If the custom read/write endpoint is associated with the primary node and the read\-only node to be deleted, after reducing the read\-only node, the read/write endpoint will not be able to read\-write separation, resulting in an increase in pressure on the primary node. It is recommended to associate other read\-only nodes for the read\-write endpoint before reducing the number of nodes. For operation details, please refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints">Editing connection endpoints</a>.</div><br> |
   |Storage space |* If the storage billing type is pay\-as\-you\-go, you do not need to select storage capacity. The storage capacity will automatically scale up and down as the amount of data increases or decreases, and will be billed on an hourly basis based on actual usage.<br><br>* If the storage billing type is yearly or monthly subscription, you need to enter the changed storage space size in steps of 10 GiB.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When scaling down, if the input storage space capacity is less than the storage space capacity used by the instance, the excess storage capacity will be charged on a usage\-based basis.   </div><br>    |
   

6. Click **Confirm order**.

7. On the **Confirm orde**r page, after confirming that the instance is configured correctly, check the **Database Products and Services Terms**, and then click **Buy now** to change the instance configuration.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |Version |
|---|---|---|
|[ModifyDBInstanceName](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceName) |Call ModifyDBInstanceName to modify the instance name. |2022\-01\-01 |
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2) |Call the ModifyDBInstanceSpec to modify the node configuration of the instance. |2024\-01\-01 |
