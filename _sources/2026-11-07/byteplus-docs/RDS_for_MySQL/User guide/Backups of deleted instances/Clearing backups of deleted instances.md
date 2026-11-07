---
title: "Clearing backups of deleted instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Clearing_backups_of_deleted_instances"
---

This topic describes how to delete backups of deleted instances for RDS for MySQL.

<span id="注意事项"></span>
## Precautions

If the backup retention policy is set to create and retain only the final backup when an instance is deleted, RDS for MySQL keeps only this backup. As the sole backup for the instance, it cannot be deleted directly from the list of backups of deleted instances. To delete it, modify the backup retention policy for the deleted instance to "Do not retain backups". For more information, refer to [Modify the retention policy for backups of deleted instances](https://www.volcengine.com/docs/RDS_for_MySQL/modifying_retention_policy_for_deleted_instances_backups).

<span id="前提条件"></span>
## Required

In the list of backups of deleted instances, the target backup is not the only backup of the instance, and its Status is **Recycled**.

<span id="操作步骤"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar on the upper left, select the region.

3. On the left navigation bar, select MySQL \\> Backups.

4. Click the **Backups of deleted instances** tab at the top of the page.

5. On the **Backups of deleted instances** page, click **Delete** in the **Actions** column for the target backup file, and in the dialog box that appears, click **OK**.
