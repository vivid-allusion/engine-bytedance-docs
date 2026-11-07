---
title: "Ending a migration task"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/ending_a_migration_task"
---

You can end the tasks that must be stopped or have been suspended, to avoid overwriting the source data into the destination database. This topic describes how to end a migration task through the DTS console.

<span id="prerequisites"></span>
## Prerequisites

A data migration task is in the status of **In progress** or **Pausing**. For more information on the migration task status, refer to [Migration Task Statuses](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions).

<span id="procedure"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts).

2. In the upper\-left corner of the top menu bar, select the target region.

3. On the **Migration task list** page, find the target migration task, and click **Terminate** in the **Action** column.

4. Click **OK** in the pop\-up dialog box.

   ::: Warning

   A task that ended cannot be recovered, and operations that have been executed cannot be rolled back. Please proceed with caution.

   :::
