---
title: "Custom backup policy"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/custom-backup-policy"
---

This article describes the steps to customize a backup policy.

<span id="prerequisite"></span>
## **prerequisite**

The [instance was created](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) and is **in the running** state.

<span id="precautions"></span>
## **Precautions**


* It is recommended that the backup time window be set during peak business periods.

* After enabling cross\-regional backup, the frequency of cross\-regional backup remains the same as the basic backup frequency, that is, local backup will also be backed up once across regions.

* The log backup policy is consistent with the backup retention days for full physical backups.

* Cross\-regional backup is performed after the local backup is successful. If the local backup fails, the cross\-regional backup will not be synchronized.


<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **Instance list** page, click the target instance name.

4. At the top of the page, click the **Backup Recovery** tab.

5. On the Backup Recovery tab, click **Backup Settings**, and in the pop\-up dialog box, set the backup policy. The description of each setting item is shown in the following table.



|**Policy Type** |**parameter** |**explain** |
|---|---|---|
|**basic backup strategy** |**backup retention days** |How long the backup file will remain in the backup space. Optional range: 7 days (default) to 30 days. |
||**backup time window** |Select a time period with a granularity of 1 hour from the drop\-down list to perform data backup. By default, data backup is performed in any 1 hour between 22:00 and 06:00. It is recommended to set the backup time window during the off\-peak period of business.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The backup time window for instances created before August 29, 2023 is still based on a 6\-hour backup policy. We recommend that you change the backup time window to start with a 1\-hour granularity to facilitate adjustment of the backup execution time.</div><br> |
||**full backup cycle** |Frequency of performing full backups. By default, two days are selected for full backup. You can customize other times, but choose at least one day per week for full backup.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a full backup date is not selected, SQL Server automatically performs incremental backups.</div><br> |
||**log backup frequency** |Set the log backup frequency on demand, currently supports log backup in **5 minutes** and **30 minutes**. |
|**cross\-region backup strategy** |**Cross\-region backup copy** |Turn cross\-region backup on or off as needed. |
||**backup region** |Select the destination region for cross\-region backup.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After enabling cross\-region backup, the target region can be changed.</div><br> |
||**backup retention days** |How long the backup file will remain in the backup space. Optional range: 7 days (default) to 30 days. |
||**I have read and agree to compliance** |Check **I have read and agree to the compliance commitment**. |



7. Click **OK** when setup is complete.
