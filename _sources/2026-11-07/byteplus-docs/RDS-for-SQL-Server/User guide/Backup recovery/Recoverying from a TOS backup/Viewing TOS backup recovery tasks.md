---
title: "Viewing TOS backup recovery tasks"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/view-tos-backup-recovery-tasks"
---

This topic describes the steps for viewing a TOS backup recovery task.

<span id="background-information"></span>
## Background information

RDS for SQL Server supports convenient migration to cloud operations. Just upload the backup files of the self\-built database to the TOS (Torch Object Storage), and you can restore the backup files to the designated database through the TOS backup recovery function provided by RDS for SQL Server. TOS backup recovery function supports full recovery, differential recovery and log recovery to meet more business scenarios. The TOS backup recovery function adopts Microsoft's official backup recovery solution to strictly ensure stability and compatibility.

<span id="precautions"></span>
## Precautions


* During the TOS backup recovery process, the instance state is migrating.

* You can do the following during the instance migration:

   * Support viewing instance information during the instance migration.

   * Support manually backing up specified databases during the instance migration. For more information, see [Creating a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually).

   * Support downloading backup files during the instance migration. For details, see [Downloading data backup files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files) and [Downloading log backup files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-log-backups-files).


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. In the left navigation bar, click **TOS Backups**.

4. In the **TOS backup recovery list ** page, **Instance Name/ID**, **Task start time**, **Task end time**, **Task status**, **Task type**, **Recovery type**, **Task description** and **Actions** are displayed. You can perform the following actions in this page:

   * Recovery tasks can be filtered and searched by instance name, instance ID, or start\-end time period.

   * Click **View task details** in the **Actions** column of the target recovery task to view the **Backup information** and **Database list** of the task:

      * In the **Backup information** area: You can view the **Backup type** and **Backup files**.

      * In the **Database list** area: You can view the **Original database name**, **New database name**, **Backup file size**, **Recovery status**, **Recovery start time**, **Recovery end time**, **Start LSN**, and **End LSN**.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the backup files to be restored are large, you can monitor the recovery progress in real time in the <strong>Recovery status</strong> column. For example, during the recovery process, the column will display <strong>50%</strong> restored.      </div>
