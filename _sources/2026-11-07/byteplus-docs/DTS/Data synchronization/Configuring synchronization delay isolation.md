---
title: "Configuring synchronization delay isolation"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_synchronization_delay_isolation"
---

During the incremental data synchronization process, if the database experiences a large volume of DML operations (e.g., `UPDATE`), causing data backlog and increased task delay, you can configure delay isolation for the delay tables by splitting them into independent lanes for data synchronization. This topic introduces how to configure delay isolation synchronization on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data synchronization task has been created, and the delay of synchronization objects is more than 60s. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions) for detailed operations.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* This feature applies only to incremental data synchronization tasks between MySQL and PostgreSQL.

* After configuring latency isolation for the lagging table, you must merge it into the main lane before configuring latency isolation again.

* When the latency of tables in the lagging lane reaches 0 seconds or gradually approaches that of the main lane, the lagging tables will be automatically merged into the main lane.

* After some lagging tables in the task are split into independent lanes, you can continue to split the remaining unsplit lagging tables.

* Tasks configured with delay isolation do not support changing synchronization objects.

* Currently, only RDS for MySQL synchronization tasks support enabling the full\-incremental feature. After enabling, full and incremental data are deduplicated and concurrently synchronized to the destination. Therefore, configuring delay for synchronization tasks separately is not supported. For more information about the full\-incremental feature of DTS, refer to [What is the full-incremental feature](https://docs.byteplus.com/en/docs/DTS/architecture_principles).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. In the left navigation bar, click **Data synchronization**.

3. On the **Synchronization task list** page, click the target task name.

4. On the target instance page, click **Task progress**.

5. On the **Task progress** page, click **Incremental synchronization**.

6. On the **Incremental synchronization** tab, click **Enable isolated synchronization** in the **Action** column of the target migration object.

7. In the **Latency isolation configuration** dialog box, click **Confirm**.


<span id=".5omn6KGM57uT5p6c"></span>
### Execution result

After configuration succeeds, the delay table will be synchronized in separate lanes from other tables, and the delay displayed on the task list page will disappear. At the same time, on the **Task progress** page, the sync status of the table on the **Incremental synchronization** tab is **Isolating synchronization**.

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[SpawnSwimmingLane](https://docs.byteplus.com/en/docs/DTS/SpawnSwimmingLane) |Call SpawnSwimmingLane API to configure latency isolation. |
