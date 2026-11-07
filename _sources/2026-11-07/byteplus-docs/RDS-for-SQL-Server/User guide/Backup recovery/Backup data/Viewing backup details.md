---
title: "Viewing backup details"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-backup-details"
---

This article describes how to view base backup list and cross\-region backup list information.

<span id="prerequisite"></span>
## prerequisite

A basic backup policy or a cross\-region backup policy for the instance has been set up. For more information, see [Custom backup policies](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy).

<span id="view-base-backup-list-information"></span>
## View base backup list information


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. At the top of the page, click the **Backup Recovery** tab.

5. On the **Backup Recovery** tab, click **Base Backup List** to view the data backup and log backup information for the instance:

   * View data backup information

      The Data Backup List for RDS for SQL Server lists all existing data backups of an instance, including full and differential backups, and shows basic information about backups. In the operation column of the backup list, you can also restore and download backup files through backup files. For details, see [Data Recovery](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-recovery) and [Downloading Data Backup Files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files).

   * View log backup information

      The Log Backup List for RDS for SQL Server lists all existing log backup information for an instance, including **backup ID** , **backup status** , **file size** , and **backup start/end time**. In the action column of the log backup list tab, you can download the log backup file from the backup file. For details, see Downloading backup files.


<span id="view-cross-regional-backup-list-information"></span>
## View cross\-regional backup list information


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

   * **Method 1** :

      1. On the **instance list** page, click the target instance name.

      2. At the top of the page, click the **Backup Recovery** tab.

      3. On the **Backup Recovery** tab, click **Cross\-Geographic Backup List** to view the cross\-geographic backup list information for your instance.

         In the Cross\-Geographic Backup list, you can view the **backup ID** , **backup status** , **backup type** , **backup method** , **executor** , **file size** , **backup start/end time** and **backup geography** for cross\-geographic backups.

   * **Method 2**:

      1. In the left navigation bar, click **Backup Management**.

      2. On the **Backup Management** page, click **Cross\-Geographic Backup**.

      3. On the **Cross\-Geo Backup List** tab, view all cross\-geo backup list information under the current geo.

         In Cross\-Geographic Backup, you can view the instances that have enabled and enabled cross\-geographical backup, and display the instance's name and ID, backup ID, backup status, backup method, backup type, executor, file size, backup start and end time, backup region, and other information.
