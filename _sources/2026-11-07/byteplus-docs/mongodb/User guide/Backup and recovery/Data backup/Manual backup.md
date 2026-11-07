---
title: "Manual backup"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/manual-backup"
---

Document Database for MongoDB supports manual backup creation, allowing you to back up data for your MongoDB instances at any time using the manual backup feature. This topic describes the procedures for manual backup.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Backups** tab.

6. Under the **Full Backup** sub\-tab, click **Manual backup**.

7. In the pop\-up dialog box, confirm the instance ID, name and other information, select the backup method, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Manual backup can be performed based on logical backups and physical backups. Among these, local disk instances support both physical and logical backups. FlexPL instances only support physical backup (volume snapshot) and do not currently support logical backup. For more information on backup methods, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/backup-overview#.5aSH5Lu95pa55byP">Backup methods</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the backup is completed, you can refresh the <strong>Backups</strong> to view the backup data.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/mongodb/createbackup) |Call the CreateBackup API to manually create backup for target MongoDB instance. |
|[DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) |Call the DescribeBackups API to query backup file list of target MongoDB instance. |
