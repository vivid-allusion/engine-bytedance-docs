---
title: "Viewing backup lists"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_data_backup_list"
---

This topic describes how to view data backups and log backups for an instance.

## Background

The data backup list for RDS for MySQL lists all existing backups for the instance and displays their basic information. In the actions column of the backup list, you can also restore from a backup (data backups only) and download backup files.

## Precautions

After you perform operations such as modifying the configuration, upgrading the version, or restoring to the original instance, RDS for MySQL may reset the Binlog number and restart from 000001. If you have configured Binlog monitoring, check the Binlog after these operations to prevent service impact from monitoring failures.

## Procedure

1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. On the **Backups** tab, click **Basic backup list** and **Cross\-regional backup list** to view the data backup and log backup lists for the instance in the local region and cross\-regions.

   > **tip**

   * > In the upper\-right corner of the **Basic backup list** and **Cross\-regional backup list** pages, you can view the storage space occupied by local and cross\-regional backup files.

   * > In the **Data backup** list and **Binlog backup** list, you can sort and view backup files by file size and backup start time.

   ## Related API

|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebackups) |Call the DescribeBackups API to query the backup file list. |
|[DescribeBinlogFiles](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describebinlogfiles) |Call the DescribeBinlogFiles API to query Binlog backup files. |
