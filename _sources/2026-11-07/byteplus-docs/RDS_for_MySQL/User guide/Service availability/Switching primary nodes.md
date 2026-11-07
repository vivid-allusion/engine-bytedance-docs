---
title: "Switching primary nodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_primary_nodes"
---

RDS for MySQL supports switching between primary and secondary nodes. When the system detects an instance failure, it immediately triggers a switch between the primary and secondary nodes to restore normal operations and ensure instance high\-availability. This topic describes the steps to manually switch the primary node.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If there is no primary\-secondary replication latency, the switchover succeeds within 5 seconds.

* Switching a primary node usually takes 30 to 60 seconds and the database may experience 1 to 2 transient disconnections. Proceed with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.

* After a primary node switchover, read\-only or secondary nodes attached to the instance will experience data latency for several minutes due to the rebuilding of replication links and synchronization of incremental data.

* When switching the primary node of a multiple\-node instance, MySQL prioritizes selecting the secondary node with the lowest replication latency. If multiple secondary nodes have the same latency, the secondary node in the same availability zone as the primary node is prioritized.

* Single node instances do not support switching the primary node.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* No migration tasks are ongoing.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the instance name of the target instance to enter the **Summary** page.

5. Click the **Service availability** tab at the top of the page to go to the **Service availability** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <strong>Service availability</strong> page displays information about each instance node, including Node ID, Availability zone, Node status, Storage usage, CPU/Memory usage, Synchronized latency, Slave_IO status, and Slave_SQL status. You can use this information to select a suitable secondary node as the new primary node.   </div>
   

6. On the **Service availability** page, click **Switching between primary and secondary nodes** in the **Instance availability** section.

7. In the **Switching between primary and secondary nodes** dialog box, select a secondary node to become the new primary node, and then click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[SwitchDBInstanceHA](https://docs.byteplus.com/en/docs/RDS_for_MySQL/switchdbinstanceha) |Call the SwitchDBInstanceHA API to manually switch the primary and secondary nodes of a specified MySQL instance. |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

**Note For more details on primary/secondary switchover, refer to [Switching primary nodes](../6438/79278).** 


* Please make sure that your applications have automatic reconnection mechanisms.

* If a read\-only node is mounted under the instance, the data of the read\-only node can be delayed for several minutes after primary/secondary switchover, because it must rebuild the replication link and synchronize the incremental data.

* Switchover can be completed within 5 seconds without a delay in primary/secondary replication.


**Do I need to update the connection address in my service after a primary/secondary switchover?** 

The primary and secondary addresses are the same. You do not need to change the address after a primary/secondary switchover, but be aware that a transient disconnection may occur during the process.
