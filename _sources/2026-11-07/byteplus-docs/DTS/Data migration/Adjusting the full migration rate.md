---
title: "Adjusting the full migration rate"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/adjusting_full_migration_rate"
---

You can adjust the full migration rate during the data migration process based on business data pressure. This topic introduces how to adjust the full migration rate on the DTS console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A full migration task has been created and started. For instructions on how to create and start a migration task, refer to [Creating and starting a migration task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The full migration rate can only be adjusted when the migration has progressed to the full migration. For methods of viewing migration progress, refer to [Viewing migration progress](https://docs.byteplus.com/en/docs/DTS/viewing_migration_progress).

* If the migration rate is too high, it may affect the performance of the source database. You can appropriately adjust the migration rate based on the read and write pressure of the source and target databases.

* Only tasks with instance types of RDS for MySQL, Document Database for MongoDB, and RDS for PostgreSQL support setting the full migration rate.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. On the **Migration task list** page, find the target task and click the task ID.


4. On the data migration page, click the **Monitor** tab.

5. On the **Monitor** tab, click **Adjust full migration rate**.

6. In the **Adjust full migration rate** dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Rows migrated per second** |Enable and set rows migrated per second as needed to prevent excessive migration speed from affecting the performance of the source database. You can adjust the number based on the read and write pressure of the source and target databases. The default value is 100000, and the value range is 1\-100000. |
   |**Data migration volume per second** |Enable and set the data volume migrated per second (Unit: KB) as needed to prevent excessive migration speed from affecting the performance of the source database. You can adjust the data volume based on the read and write pressure of the source and target databases. The default value is 25,000, and the value range is 1 to 25,000. |
   |**Migration task concurrency** |Set the concurrency of the migration task as needed. This concurrency can improve the performance and efficiency of the migration task, ensuring it completes quickly and stably. The default value is 8, and the valid range is 1 to 64. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">An excessively high migration rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases.   </div>
   

7. Click **OK**.
