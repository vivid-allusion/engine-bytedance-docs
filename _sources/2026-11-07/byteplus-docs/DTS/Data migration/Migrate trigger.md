---
title: "Migrate trigger"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_a_trigger"
---

When creating a MySQL data migration task, and the migration method of the pre\-migration trigger is configured as manually trigger migration, you can manually migrate trigger before the incremental migration is started. This topic describes how to manually migrate trigger.

<span id="agY01tDr"></span>
## Prerequisites

A MySQL data migration task has been created, and the migration method of the pre\-migration trigger in the data migration task is manually trigger migration. For the method to create a migration task, refer to [Creating a migration task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

<span id="IQy2sFWe"></span>
## Precautions


* This feature is released in allowlist. To use it, [submit tickets](https://console.byteplus.com/workorder/create/) to contact technical support.

* Manual migration trigger is supported only when the migration task progresses to the incremental migration stage.

* When the task is in the paused state, manual migration trigger is supported if the task is in the incremental migration stage.


<span id="a2LLZikf"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, select **More operations \> Migrate trigger** on the right of the target migration task.

5. In the migrate trigger pop\-up window, click **OK**.


<span id="QdI9Luy7"></span>
### Execution result

You can view the task progress of the target migration task in the data migration list.
