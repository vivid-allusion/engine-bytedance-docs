---
title: "Downloading the data backup file"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Downloading_a_data_backup"
---

RDS for PostgreSQL supports downloading backups to the local. This article describes the steps to download backup files.

<span id="YiHbmmlR"></span>
## Precautions

Only downloading logical data backups is supported.

<span id="VY9wuifH"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* A logical backup has been created and the status of the backup is **Succeeded**. For more information, see [Creating a backup](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_manual_backup).


<span id="N2JbRqfK"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name to enter the instance details page.

5. At the top of the page, click the **Backups** tab.

6. Under the **Data backup** tab, you can view a list of data backups for your instance.

7. In the Backup list, click  **...**  \> **Retrieve** in Actions column of the target logical backup.

8. In the **Retrieve** window that pops up, click **Retrieve**.

   * After clicking **Retrieve**, the **Retrieve backup window** will automatically close, and the backend will automatically complete the pre\-work required to obtain the backup file. After completion, you can choose the way to obtain the backup file on demand.

   * After obtaining the backup file is completed,  **...**  \> **Retrieve** in the **Action** column of the backup list will switch to **Download**. You can confirm the acquisition progress in this way, and you can also view the acquisition progress of the backup in the [Historical event](https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_historical_events).

9. In the Backup list, click  **... ** \> **Download** in Actions column of the target logical backup.

10. In the pop\-up **Download** window, you can get the private network address and public network address of the downloaded backup file.

   * Click **Copy** to the right of the download link to copy the download link.

   * Click **Download** to the right of the download link to download the backup file.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The download link for backup files is valid for 7x24 hours. Backup files can be downloaded from this link at any time within the valid period. After the download link expires, you can re\-obtain it by clicking the <strong>Download</strong> button, but the download address obtained each time is different.</div>


* <div data-tips="true" data-tips-type="default">The same set of full and incremental backups has the same name prefix. It is recommended to download the same set of full and incremental backups to obtain the full backup data.</div>


* <div data-tips="true" data-tips-type="default">The backup file cannot be directly downloaded from the current page through the private network address. Download the backup using the private network address in a private network environment (such as on the ECS in the same VPC).</div>



<span id="pdwIUN32"></span>
## Related APIs


|API |Note |
|---|---|
|[GetBackupDownloadLink](https://docs.byteplus.com/en/docs/RDS_for_PG/GetBackupDownloadLink) |Call GetBackupDownloadLink interface to get the download address of the backup. |
|[DownloadBackup](https://docs.byteplus.com/en/docs/RDS_for_PG/DownloadBackup) |Call DownloadBackup API to download the backup. |
