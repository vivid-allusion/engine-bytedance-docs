---
title: "Configuring migration delay isolation"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_migration_delay_isolation"
---

During the incremental data migration process, if the database experiences a large volume of DML operations (e.g., ` UPDATE`), causing data backlog and increased task latency, you can configure delay isolation for the lagging tables by splitting them into independent lanes for data migration. This topic introduces how to configure a delay isolation migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A BytePlus account has been registered with real name authentication completed. For more information, refer to [Create account](https://docs.byteplus.com/en/docs/6261/64925) and [Verify account](https://docs.byteplus.com/en/docs/6261/64935).

* A data migration task has been created, and the delay time of the migration object exceeds 60 seconds. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This feature applies only to incremental migration tasks for RDS for MySQL, veDB for MySQL, and RDS for PostgreSQL.

* After configuring latency isolation for the lagging table, you must merge it into the main lane before configuring latency isolation again.

* When the latency of tables in the lagging lane reaches 0 seconds or gradually approaches that of the main lane, the lagging tables will be automatically merged into the main lane.

* Tasks configured with delay isolation do not support changing synchronization objects.

* After some lagging tables in the task are split into independent lanes, you can continue to split the remaining unsplit lagging tables.

* Currently, only RDS for MySQL migration tasks support the full\-incremental feature. Once enabled, full and incremental data are deduplicated and concurrently migrated to the destination, which means configuring migration task delay separately will no longer be supported. For more information about the full\-incremental feature of DTS, refer to [What is the full-incremental feature](https://docs.byteplus.com/en/docs/DTS/architecture_principles).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. In the left navigation bar, click **Data migration**.

3. On the **Migration task list** page, click the target task name.

4. On the target instance page, click **Task progress**.

5. On the **Task progress** page, click **Incremental migration**.

6. On the **Incremental migration** tab, click **Enable isolation migration** in the **Actions** column of the target migration object.

7. In the **Latency isolation configuration** dialog box, click **Confirm**.


<span id=".5omn6KGM57uT5p6c"></span>
### Execution result

After configuration succeeds, the delay table will be migrated in separate lanes from other tables, and the latency displayed on the task list page will disappear. Simultaneously, the migration status of this table will be displayed as **Isolation migration in progress** under the **Incremental migration** tab on the **Task progress** page. Isolation automatically lifts when the lagging table's delay time falls below 60 seconds.

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[SpawnSwimmingLane](https://docs.byteplus.com/en/docs/DTS/SpawnSwimmingLane) |Call SpawnSwimmingLane API to configure latency isolation. |
