---
title: "About backup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_backup"
---

<span id=".5aSH5Lu9566A5LuL"></span>
## Introduction

Backups are important runtime files for a database that enable features like disaster recovery and restoration. RDS for MySQL provides two backup capabilities, data backup and log backup. Data backup restores your database to a backup set, while log backup restores it to a specific point in time.


* Data backup


RDS for MySQL provides three types of data backups depending on the storage type: physical, logical, and snapshot. The differences are as follows.


   * Storage type is Local SSD:

      * Physical backup supports both full and incremental backups, and its backup object is the entire instance.

      * Logical backup supports backing up the entire database or specified databases and tables.

   * Storage types are Cloud ESSD FlexPL and Cloud ESSD PL0:

      * Snapshot backup only supports full backup, and the backup object is the entire instance.


RDS for MySQL performs automatic backups based on the backup cycle defined in the backup policy. You can also create data backups manually.


* Log backup


RDS for MySQL supports both automatic log backups based on a backup policy and manual log backups.

<span id=".5a2Y5YKo5L2N572u"></span>
## Storage location

Data backups and log backups are stored in the backup space provided by BytePlus and do not occupy the storage space of the instance. The backup file is stored in the region of the MySQL instance by default.

When the MySQL instance is running, a certain number of local binlog files are generated, which uses the storage space of the instance. You can set the corresponding log backup policy to manage the use of the instance storage space by local binlog files.

<span id=".5aSH5Lu95aSn5bCP"></span>
## Backup size

In the **Usage statistics** area of the **Summary** page, the backup usage information of the MySQL instance is provided. This information includes the usage of data backup and log backup.Data backup

To save the backup storage space and shorten the transfer time of backup files during recovery, RDS for MySQL introduced data backup file compression in January 2024.

<span id=".5LiL6L295aSH5Lu9"></span>
## Download backup

You can download data backups and log backups from the local region.

<span id=".5Y-C6ICD5paH5qGj"></span>
## Reference document


* [Creating a data backup manually](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup)

* [Manually backup binlog](https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_backing_up_binlog)

* [Modifying backup policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies)

* [Download data backup files](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_data_backup_files)

* [Download binlog backup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups)
