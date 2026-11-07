---
title: "Switching to primary node"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Switch_to_primary_node"
---

NDB for MySQL provides switching between primary and secondary nodes functions. When an instance fails, the system will immediately trigger the primary node switching to restore the instance to normal operation in time to ensure the high availability of the instance. You can also manually switch the primary node. This article introduces the operation steps for manually switching the primary node.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* There are currently no backup tasks.


<span id="GyGKlcyx"></span>
## Failover mechanism

In the event of a system failure, failover will automatically occur between the instance's primary node and read\-only nodes. Supports setting a priority for each node. This priority can determine the probability of each node being elected as the primary node when the primary node is switched occurs. When multiple nodes have different priorities, they will be switched in the set priority order. When multiple nodes have the same priority, the node with the larger LSN is selected first.

The steps to switch the primary node are as follows:


1. The system finds all read\-only nodes that are currently eligible for election.

2. Select one or more read\-only nodes with the highest priority.

3. If switching the first node fails (such as due to network problems or abnormal replication status), the next node will be tried until the switch is successful.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Switching time and impact**


* Switching the primary node normally takes about 30 seconds. During this period, the database may experience one or two disconnections. Please ensure that your application has an automatic reconnection mechanism to reduce the impact of disconnections on your business.

* Before switching, check whether there are any Online DDL tasks running on the instance. Switching the primary node will interrupt the task, so proceed with caution. For more information, see [Viewing tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets#.5p-l55yL5bel5Y2V).

* When switching the primary node, the node associated with the custom connection endpoint will change according to the read\-only node switched to, as shown below:

   
   |Endpoint type |Custom read\-only endpoint |Custom read/write endpoint |
   |---|---|---|
   |**Switch effect** |* If the read\-only node switched to is not associated with the current custom read\-only endpoint, the node associated with the custom read\-only endpoint remains unchanged.<br><br>* If the switched read\-only node is associated with the current custom read\-only endpoint, after switching the primary node, the custom read\-only endpoint will be unassociated with the node and automatically associated with the original primary node.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If there is a custom read\-only endpoint associated with only one read\-only node, at this time due to the primary node failure caused by the primary and standby switch, the read\-only node becomes the new primary node, after the switch, the original primary node is still faulty, at this time the flow is not forwarded, the read\-only endpoint address is not available before the original primary node recovery.   </div><br>    |* If the switch to the read\-only node associated with the current custom read and write endpoint, the custom read and write endpoint associated node unchanged.<br><br>* If the switch to the read\-only node is not associated with the current custom read and write endpoint, after switching the primary node, the current custom read and write endpoint will be associated with the newly switched primary node, the original primary node will become a read\-only node, and cancel the custom read and write endpoint association. |
   |**Switch example** |The four nodes of an instance are node0 (primary), node1, node2, and node3, respectively. There is a custom read\-only endpoint associated with nodes node1 and node2. When switching the primary node, the situation is as follows:<br><br><br>* Switch node1 to the primary node, and the node associated with the read\-only endpoint is node0 and node2.<br><br>* Switching node3 to the primary node does not affect the endpoint, and the associated nodes are still node1 and node2. |The four nodes of an instance are node0 (primary), node1, node2, and node3, respectively. There is a custom read and write endpoint, and the nodes node0 (primary) and node1 are associated. When switching the primary node, the situation is as follows:<br><br><br>* Switch node1 as the primary node, and the node associated with the read and write endpoint is still node1 (primary) and node0.<br><br>* Switch node2 as the primary node, and the node associated with the read and write endpoint is node2 (primary) and node1. |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Manually switch the primary node


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. Click the **Connectivity** tab, point the mouse to the target read\-only node in the Instance Topology area, and click **Switch to primary node** in the pop\-up operation box.

5. In the confirmation dialog box that pops up, confirm the scope of influence of switching the primary node and click **OK**.


<span id="7nPylgyO"></span>
## Switch to primary node priority


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

4. Click the **Connectivity** tab, point the mouse to the target read\-only node in the instance topology area, and click **Modify** in the pop\-up operation box.

5. In the pop\-up dialog box, enter the priority value, ranging from 0 to 15. The larger the value, the higher the priority.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the instance is created successfully, the priority of each node defaults to 1, and the priority of the newly added read\-only node also defaults to 1.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Supports dynamic modification of the priority of each node (including the current primary node priority). Modifying the priority will not cause the primary node to switch.   </div>
   

6. Click OK.


<span id="snaXdYmJ"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBNodeConfig](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBNodeConfig) |Call the ModifyDBNodeConfig interface to set the priority of the specified node to be selected as the primary node during primary node switching. |
