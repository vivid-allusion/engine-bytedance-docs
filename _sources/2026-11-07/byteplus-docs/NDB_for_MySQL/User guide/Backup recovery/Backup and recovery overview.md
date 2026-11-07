---
title: "Backup and recovery overview"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Backup_and_recovery_overview"
---

NDB for MySQL has a personalized instance backup and recovery strategy, supports instance backup during instance operation, and can restore data at any time after the instance is released.

<span id="数据备份"></span>
## Data backup

NDB for MySQL supports full physical backup of instances. By default, a full backup is automatically created within a specified time period. You can also perform manual backups at any time according to business needs.


* Automatic backup: The instance automatically performs backup according to the system's preset backup strategy. Automatic backup files cannot be deleted while the instance is running. You can customize the backup strategy based on your business needs. For more information, see [Modifying basic backup policies](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies).

* Manual backup: Instant manual backups can be initiated at any time during the running of the instance, and backup files can be deleted at any time. How to create a manual backup, see [Creating a data backup manually](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_a_data_backup_manually).


Automatic backup and manual backup are compared as follows:


|Backup type |Manual backup |Automatic backup |
|---|---|---|
|Number of days to retain backup |Keep it forever. |The default is 7 days, and customization is supported. For detailed instructions, see [Modifying basic backup policies](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies). |
|Backup time window |Execute immediately. |By default, three days (one day apart) are randomly selected in each week, and the backup task is executed in the same time period of these three days, such as Monday, Wednesday, and Friday from 02:00 to 04:00 every week.<br><br>You can customize the time window for automatic backup. For detailed instructions, see [Modifying basic backup policies](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies). |
|Full backup cycle |Execute immediately. |The frequency of performing full backup is set by default to randomly select three days (one day apart) every week to perform backup, such as Tuesday, Thursday, and Saturday. The full backup cycle can be modified by using **backup settings**, as detailed in [Modifying basic backup policies](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_basic_backup_policies). |
|Backup file |* Supports manual deletion.<br><br>* The maximum number of backup files is 10. |* The instance will be automatically deleted when it expires during operation and manual deletion is not supported.<br><br>* No quantity limit. |
|Create type |User, which means it is created manually by the user. |System, which means it is created automatically by the system. |
|Backup type |Full backup |Full backup |
|Backup method |Physical backup |Physical backup |


<span id="数据恢复"></span>
## Data recovery

NDB for MySQL supports data recovery for running or released instances. Data can be restored to a new instance using a backup set or a specified time point. The supported scenarios are as follows.


|Recovery type |Scene description |
|---|---|
|[Recovering to the new instance from a backup set](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_from_a_backup_set) |Restore the full backup data to a new instance through the files automatically or manually backed up by the system, including all database accounts and other data. Suitable for instance\-level data recovery scenarios. |
|[Recovering to the new instance by time point](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_to_the_new_instance_by_time_point) |Within the log backup retention period, restore the data at a certain point in the past to a new instance, including all database accounts and other data. Suitable for instance\-level data recovery scenarios. |
|[Recovering database and table from a backup set](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_backup_set) |Restoring some databases or tables in a backup set of an instance to the original instance will not affect the existing data. It is suitable for scenarios where part of the data needs to be restored in the business. |
|[Recovering database and table by time point](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_database_and_table_by_time_point) |Restoring some databases or tables in an instance at a certain point in the past to the original instance will not affect the existing data. It is suitable for scenarios where part of the data needs to be restored in the business. |
|[Recovering a backup of a deleted instance to a new instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_a_backup_of_a_deleted_instance_to_a_new_instance) |Data can be restored to the new instance through backup files retained by deleted instances, including data such as all database accounts. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">NDB for MySQL supports cross\-zone recovery, which means that you can restore a backup of an instance in zone A to a new instance in zone B.</div>


<span id="已删除实例备份"></span>
## Backups of deleted instances

After an instance is deleted or unsubscribed, the system automatically creates and retains a final backup in the **Backups of deleted instances**. You can restore data by restoring as a backup set, see [Recovering a backup of a deleted instance to a new instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Recovering_a_backup_of_a_deleted_instance_to_a_new_instance) for activity details.

The final backup file of a deleted instance cannot be manually deleted. It will be automatically deleted by the system after 7 days by default based on the completion time of the backup. You can view the estimated deletion time of the target instance backup in the **Backups of deleted instances** list. For details, see [Viewing the list of deleted instance backups](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_backups_of_deleted_instances).
