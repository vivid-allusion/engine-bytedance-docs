---
title: "Configuring a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task"
---

Database Transmission Service (DTS) provides various types of database migration services. This topic describes how to create and start a data migration task on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The data migration task is created, and the task status is **to be started**.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Do not manually terminate full data migration tasks, as it may cause data incompleteness. Wait for the migration task to complete. The migration task stops automatically.

* Incremental data migration tasks do not stop automatically and require manual termination. For manual termination methods, refer to [Terminating a migration task](https://docs.byteplus.com/en/docs/DTS/terminating_a_migration_task).

* If a data verification task is enabled in the migration task, the data verification task can be disabled by configuring the migration task before it starts. Once the built\-in data verification task is disabled, it will be removed from the data verification task list. After the migration task is started, the built\-in data verification task can not be disabled.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. Find the target task in the migration task list and select **Configuration** at the top right.

4. For the next steps, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions) and select the operation guide based on your requirements.
