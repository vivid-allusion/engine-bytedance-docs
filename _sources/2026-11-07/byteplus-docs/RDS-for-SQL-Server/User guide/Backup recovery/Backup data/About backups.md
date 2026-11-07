---
title: "About backups"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/about-backup"
---

This topic describes the backup information of RDS for SQL Server.

<span id="brief-introduction"></span>
## Brief introduction

Backup is the core guarantee for database disaster recovery and restoration. RDS for SQL Server provides two backup capabilities: data backup and log backup. Through data backup, the database can be restored to a state consistent with the data in the backup file; based on data backup, log backup enables the database to be restored to a specified point in time.


* Data backup

   For data backup, RDS for SQL Server currently only supports physical backups, which include two types: System backup and User backup.

   * System backup: The system performs automatic backups according to the backup policy and the set backup cycle. A full backup will be executed during the specified full backup cycle, while differential backups will be performed at all other times.

   * User backup: Data backups created manually by users. You can perform full backups on demand and choose to back up the entire instance or specific databases.

* Log backup

   The log backup of RDS for SQL Server can effectively improve the disaster tolerance and data protection level of the database, and ensure business continuity and data security. When an instance fails, you can effectively restore the database to the most recent point in time before the failure using log backup information.

   Log Backup for RDS for SQL Server supports automatic backups based on backup policies.


<span id="storage-location"></span>
## Storage location

Data backups and log backups are stored in the backup space provided by BytePlus and do not consume the storage space of the instance. Backup files are stored by default in the region where the SQL Server instance is located. RDS for SQL Server also provides the ability to back up across geographies, i.e. store backup files in geographies other than the one where the SQL Server instance is located. By backing up across geographies, SQL Server instances can gain the ability to recover from disasters across geographies. The cross\-regional backup function is turned off by default. To enable it, please refer to [Setting up cross-regional backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy).

<span id="backup-size"></span>
## Backup size

In the usage statistics area of the instance in page, you provide backup usage information for your SQL Server instance, which contains usage for both data and log backups.

<span id="download-backup"></span>
## Download backup

Both data backup and log backup in the local domain support downloading to the local area, and downloading cross\-regional backup files is not supported for the time being.

<span id="related-documentation"></span>
## Related Documentation


* [Custom backup strategy](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy)

* [Create a manual backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-data-backup-manually)

* [View backup](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-backup-details)

* [Download the data backup file](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-data-backup-files)

* [Download log backup file](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/downloading-log-backups-files)

* [Delete manual data backup files](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/deleting-manual-data-backup-files)
