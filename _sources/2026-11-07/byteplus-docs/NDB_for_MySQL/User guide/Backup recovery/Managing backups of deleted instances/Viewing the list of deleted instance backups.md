---
title: "Viewing the list of deleted instance backups"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_backups_of_deleted_instances"
---

After an instance is deleted, the system automatically creates a final backup by default and keeps it in the deleted instance backup list. This article describes how to view a list of deleted instances.

<span id="背景信息"></span>
## Background

The deleted instance backup list retains the basic information of all released instances under the primary account and the final backup information of the instances. You can restore the data of the terminated instance to a new instance by using the retained backup files.


|Information classification |Description |
|---|---|
|Summary |This includes Instance name/ID, State, Primary instance availability zone, Virtual private cloud, Compatible version, Used storage space, Affiliated project, Creation time, and Delete time. |
|Backup information |Includes information such as backup ID, backup status, backup file size, backup method, executor, backup type, consistent backup time, backup time, estimated backup deletion time, and supported operations.<br><br>The **Operation** column of the deleted instance backup list provides a quick entry for the **Restore** operation. For detailed steps, see [Recovering a backup of a deleted instance to a new instance](https://www.byteplus.com/en/docs/NDB_for_MySQL/Recovering_a_backup_of_a_deleted_instance_to_a_new_instance).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Backup files do not support manual deletion. By default, the backup will be automatically deleted by the system after 7 days, depending on the completion time of the backup.</div><br> |


<span id="操作步骤"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region to which the target deleted instance belongs.

3. Click **Backup management** in the left\-side navigation bar.

4. In the **Backups of deleted instances**, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d49982417cacf0cf34ca1b2a4fdf0c89.png) </span>in front of the target deleted instance name to view the backup information of the instance.
