---
title: "Migrating availability zones"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/availability_zone_migration"
---

RDS for PostgreSQL supports migrating instances and nodes across availability zones (AZs) within the same region. This topic describes the steps to migrate availability zones.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The region where the instance is located has multiple AZs.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* Only migrating a single\-availability\-zone instance to a multi\-availability\-zone instance is supported.

* Only support migrating secondary nodes or read\-only nodes, and support migrating secondary nodes and read\-only nodes simultaneously.

* You can migrate 20 instances at the maximum at the same time.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Migrating instances across AZs will not change the node ID.

* When migrating the availability zone of secondary nodes or read\-only nodes, 1 to 2 brief service interruptions may occur (each lasting 30 to 60 seconds). Avoid migrating during peak business hours to prevent unnecessary impact on the business.

* The time required for migration depends on the data volume and the number of nodes to be migrated; the larger the data volume and the more nodes to be migrated, the longer the migration takes. To ensure smooth migration, minimize data writes during the migration period.

* During migration, the instance's available storage space may decrease; monitor the instance's disk usage during this period. After migration completes, the storage space occupied by the migration will be released. Disk usage can be monitored through the monitor indicator **Disk usage**. For more details, refer to [Viewing monitoring information](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_monitoring_information).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the Instances page, click on the target instance name.

4. Go to the **Summary** tab and click on the edit icon after **Availability zone**.

5. Select the target availability zone of each node in the **Migrate availability zones** pop\-up dialog box and click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During the migration, the instance state is <strong>Modifying</strong>. You can view the migration progress of the instance in the historical event. For more details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_historical_events">Viewing historical event</a>.</div>
