---
title: "Customizing backup policies"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/customizing_backup_policies"
---

This topic introduces the procedure for customizing the backup strategy.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Recovery of read\-only nodes is not currently supported.

* Do not perform DDL operations during the backup period to avoid table locks that may cause a backup failure.

* Try to choose the business off\-peak period for backup.

* The incremental backup method with high\-frequency increments is a new feature launched on October 13, 2025. Instances created before October 13, 2025 will continue to use the previous incremental backup configuration.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Click the **Backup policy** sub\-tab, then click **Edit** to the right of **Basic backup policy** and the **Local WAL retention policy**, and customize the related policies in the popped\-up settings page. The specific configuration items are shown in the following table.

   
   |**Policy category** |Parameters |Note |
   |---|---|---|
   |Basic backup policy |Backup retention days |The retention period of backup files in the backup space. Backup retention days supports settings between 7 and 365. |
   ||Full backup cycle |The dates for executing full backup weekly; by default, full backups are performed on Monday, Wednesday, Friday, and Sunday each week. It supports adjustment to other dates, but at least one day should be retained. |
   ||Backup time window |The time period for full backup on the specified full backup date, the default time period is 02:00~03:00. Can be adjusted to another time period of 1 hour in length. |
   ||Incremental backup method<br><br> |You can set incremental backups to **High frequency** or **Normal frequency**. The default is that incremental backup is not enabled.<br><br><br>* When **High frequency** is selected, **Incremental backup frequency** needs to be set. After setting, incremental backups can be performed according to the set frequency.<br><br>* **Normal**: When selecting normal incremental, you need to set **Incremental backup cycle**. If the incremental backup cycle is not set, incremental backups will not actually be enabled. |
   ||Incremental backup frequency |The frequency for executing incremental backups can be set to perform an incremental backup every 1 hour, every 2 hours, every 4 hours, every 6 hours, or every 12 hours. The default is to perform an incremental backup every 12 hours.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">There is no need to set a backup cycle for incremental backups. After the instance is created, incremental backups will be continuously created according to the set incremental backup frequency.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Full backup has a higher priority than incremental backup. If an incremental backup is still in progress when the start time window for full backup arrives, the incremental task will be terminated and full backup will start.</div><br> |
   ||Incremental backup cycle |When normal incremental backup is selected, the frequency of performing incremental backups. The frequency of normal incremental backup is selected weekly and cannot conflict with the full backup cycle. According to the setting of the full backup cycle, up to 6 days per week can be selected for incremental backup. If not selected, the instance will not perform incremental backups. |
   ||WAL backup |Enabled by default and cannot be disabled. |
   ||WAL backup retention days |By default, it follows the same policy as data backup and cannot be modified. |
   |Local WAL retention policy |Local remaining available space protection |after enabling this feature, the instance automatically clears the earliest local WAL log when storage usage exceeds 80% or remaining space is less than 5 GB, until usage drops below 80% and remaining space exceeds 5 GB, preventing abnormalities such as instance read\-only due to high storage usage. |
   

7. After setting, click **OK**.
