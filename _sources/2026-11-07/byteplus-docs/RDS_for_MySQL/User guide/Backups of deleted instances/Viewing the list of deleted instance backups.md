---
title: "Viewing the list of deleted instance backups"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/view_the_list_of_deleted_instance_backups"
---

This topic introduces the operation steps for viewing the backup list of deleted instances.

<span id="background"></span>
## Background

Instances that are manually deleted or unsubscribed, or recovered due to arrears or expiration will retain the backup files of the instance according to the set retention policy when they are deleted, unsubscribed, or recovered. These backup files will be displayed in the **Backups of deleted instances** list. For more information about the retention policy, refer to [Modifying backup policies](https://www.volcengine.com/docs/6313/97306).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">When manually deleting an instance, you can also modify the retention policy for retaining backup files after the instance is released.</div>


In the **Backup of Deleted Instances** list, the backup ID, the name and ID of the instance to which the backup belongs, the backup status, the size of the backup file, the start and end time of the backup, the backup method, the running status of the instance, the database version, and the project to which the instance to which the backup belongs are displayed. In the **Operation** column of the **Backup of Deleted Instances** list, you can rebuild an instance based on the backup file. For detailed information about rebuilding an instance, see [Rebuilding an instance](https://www.volcengine.com/docs/6313/75400).

<span id="steps"></span>
## Steps


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the top menu bar on the upper left, select the region.

3. On the left navigation bar, select **MySQL** \> **Backups**.

4. Click the **Backups of deleted instances** tab at the top of the page to view the **Backups of deleted instances** list.
