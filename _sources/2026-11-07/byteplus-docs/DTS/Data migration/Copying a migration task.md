---
title: "Copying a migration task"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/replicating_a_migration_task"
---

Database Transmission Service (DTS) supports copying migration tasks, meaning it can copy a task with the same configuration as an existing one. At the same time, you can adjust parameters for the successfully copied task. This topic explains how to copy a migration task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A migration task has been created. For details, refer to [Creating a migration task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* During task replication, ensure the availability of the source and target databases, as well as consistency in the migration task user permissions. Otherwise, the task replication may fail.

* If a data verification task was enabled in the original migration task, the built\-in data verification task will not be copied when replicating the task. If you need to perform data verification on the migrated data, you must manually configure the data verification task in the configuration interface.

* The task duplication operation fully preserves all settings, including data validation configurations, ensuring that the new task behaves identically to the source task.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select **More operations \> Copy task** on the right side of the target migration task.

5. In the **Do you want to copy the selected task?**  dialog box, click **Copy**.


<span id=".5omn6KGM57uT5p6c"></span>
### Execution result

After successfully copying the migration task, the copied task will be in the **To be started** state and named **Original task name_bak_random number** To start the task, click **Configure**. After setting the relevant parameters, you can start the task. For details, refer to [Configuring a migration task](https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task).
