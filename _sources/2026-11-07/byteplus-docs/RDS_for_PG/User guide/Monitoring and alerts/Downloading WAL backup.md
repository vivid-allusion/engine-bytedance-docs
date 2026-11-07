---
title: "Downloading WAL backup"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_WAL_backup"
---

RDS for PostgreSQL supports downloading WAL backup to the local. This topic describes the procedure to download backup files.

<span id="RKNo2Mvo"></span>
## Prerequisites


* An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).


<span id="rg7m0ter"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Under the **WAL management** tab, you can view the instance's backed\-up WAL list.

7. In the backup list, click **Download** in the **Actions** column of the target WAL backup file.

8. In the pop\-up **Download** window, you can get the private network address and public network address of the downloaded backup file.

   * Click **Copy** to the right of the download link to copy the download link.

   * Click **Download** to the right of the download link to download the backup file.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The backup file download link is valid for 7x24 hours and remains unchanged during that period. When the download link expires, click the <strong>Download</strong> button to retrieve a new link.</div>


* <div data-tips="true" data-tips-type="default">The backup file cannot be directly downloaded from the current page through the private network address. Download the backup using the private network address in a private network environment (such as on the ECS in the same VPC).</div>


* <div data-tips="true" data-tips-type="default">You can use pg_waldump to translate wal binary logs into readable content to view write actions, check wal integrity, analyze replication/recovery issues, and assess write performance.</div>



<span id="zrkNKeGN"></span>
## Related APIs


|**API** |**Note** |
|---|---|
|[DescribeWALLogBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeWALLogBackups?lang=zh) |Call DescribeWALLogBackups API to retrieve the WAL backup list of the specified instance. |
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink) |Call GetBackupDownloadLink interface to get the download address of the backup. |
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) |Call DownloadBackup API to download the backup. |
