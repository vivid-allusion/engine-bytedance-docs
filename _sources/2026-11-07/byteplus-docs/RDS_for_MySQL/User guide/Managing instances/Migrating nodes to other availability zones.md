---
title: "Migrating nodes to other availability zones"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/availability_zone_migration"
---

RDS for MySQL supports migrating the nodes of an instance to other availability zones in the same region. This topic describes the steps to migrate availability zones.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The region where the instance is located has multiple AZs.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Only double\-node instance types support migrating nodes. A classic architecture with one primary node and one secondary node, and multiple read\-only nodes can be added.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Migrating the availability zone will migrate the entire instance. The database will experience 1 to 2 flash breaks during the migration. Proceed with caution. Migrate availability zones during off\-peak business hours and ensure your application has an automatic reconnection mechanism.

* MySQL instances can only use subnets located in the same availability zone as the primary or secondary node. You cannot migrate both the primary and secondary nodes to an availability zone that does not contain their subnet.


<span id=".6L-B56e75Zy65pmv"></span>
## Migration scenarios


|Migration scenarios |Description |
|---|---|
|Change a single\-availability zone instance to a multiple\-availability zone instance. |When migrating, select different availability zones for the primary and secondary nodes.<br><br>For example: In the Beijing region, migrate an instance from availability zone A (primary) + availability zone A (secondary) to availability zone A (primary) + availability zone B (secondary). |
|Change the availability zones for nodes in a multi\-availability\-zone instance. |During migration, change the availability zone of the primary node, the secondary node, or a read\-only node. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Migrating an availability zone will not change the node IDs of any nodes.</div>


<span id=".6LS555So6K-05piO"></span>
## Billing

The availability zone migration feature is free, and no fees are charged for any migration scenario.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the Instances page, click the target instance name.

4. Go to the **Summary** tab and click on the edit icon after ** Availability zone**.

5. In the **Migrate availability zones** dialog box, select the target availability zone and execution time for each node, and click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Modify availability zone |The following rules apply when you modify the availability zone of a node:<br><br><br>* You can specify different availability zones in the same region for the primary node and the secondary node.<br><br>* Nodes can be distributed in up to three availability zones. |
   |Switch time |Select an execution time for the availability zone migration.<br><br><br>* **Switch now**: Execute the migration immediately after clicking OK.<br><br>* **Specific time**: Execute the migration within the specified time period.<br><br>* **Maintenance window**: Execute the migration within the instance's maintenance window. |
   |Specific time period |If you select to perform the migration within a **specific time**, set a time period for the migration.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Time periods cannot be set across days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The shortest time period is two hours.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the time period within the time range indicated in the console.</div><br> |
   |Maintenance window |If you choose to perform the migration within the **maintenance window**, you need to confirm the instance's **maintenance window**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can click <strong>Edit</strong> to modify the maintenance window of the instance. For detailed rules on setting maintenance window, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_a_maintenance_period">Configuring maintenance window</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is initiated, you can still modify the instance's maintenance window, but the execution time of the initiated task will not be automatically adjusted with the modification of the maintenance window. If you need to adjust the execution time of a task, you need to manually schedule and adjust it at Task center. For more information about modifying tasks execution time, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_the_execution_time_of_a_task">Changing the execution time of a task</a>.</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[MigrateToOtherZone](https://docs.byteplus.com/en/docs/RDS_for_MySQL/migratetootherzone) |Call the MigrateToOtherZone API to migrate nodes of a specified instance to another availability zone within the same region. |
