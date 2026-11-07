---
title: "Managing backup files"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/manage-backup-file"
---

MongoDB now supports downloading backup files generated from physical or logical backups to a local PC. This topic introduces how to obtain and download MongoDB backup files through the console.

<span id="4HQ10otI"></span>
## Obtaining backup files

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Data backup files generated from physical backups are saved as shards in <a href="https://docs.byteplus.com/en/docs/tos/docs-what-is-tos">TOS</a>. Therefore, you need to obtain the backup files as follows first and then download the backup files. For more information, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/backup-overview#.5aSH5Lu95pa55byP">Backup methods</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/backup-overview#.5aSH5Lu95a-56LGh">Backup objects</a>.</div>


* <div data-tips="true" data-tips-type="tip">FlexPL volume instances do not support obtaining backup files.</div>


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Backups** tab.

6. In the list of backup files under the **Full backup** sub\-tab, locate the backup file to be downloaded. In the **Actions** column, click **Obtain backup**.

7. In the dialog box displayed, verify the backup file information (such as the backup ID, backup file name, and backup file size), and click **OK**.

   When obtaining a backup file, click **View progress** in the **Actions** column of the backup file. The backup file acquisition progress is displayed in a dialog box. After the progress bar comes to 100%, you can download the backup file.


<span id="OQemzRNR"></span>
## Downloading backup files

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After obtaining a backup file, you can download the backup file to a local PC as follows.</div>


* <div data-tips="true" data-tips-type="tip">FlexPL volume instances do not support downloading backup files.</div>


1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Backups** tab.

6. In the list of backup files under the **Full backup** sub\-tab, locate the backup file to be downloaded. In the **Actions** column, click **Download backup file**.

7. In the pop\-up **Backup Download** dialog box, perform the following operations as needed for your business to complete the download.

   
   |Business scenario |Procedure |
   |---|---|
   |Download via public network address |1. Click the icon on the right side of **Public network address** <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6da1a6571a3b9cc35b99ef2d70cfb6c1.jpg) </span>icon.<br><br>2. Paste the public network address into the browser address bar and press Enter. The browser will automatically complete the download. |
   |Download via private network address<br><br> |1. Click the icon on the right side of **Private network address** <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_6da1a6571a3b9cc35b99ef2d70cfb6c1.jpg) </span>icon.<br><br>2. Perform the corresponding operations according to the operating system of the ECS (which must be in the same region as the current MongoDB instance) to complete the download:<br><br>   * Windows operating system: Paste it into the browser's address bar and press Enter; the browser will automatically complete the download.<br><br>   * Linux operating system: Execute the command in the following format to download.<br><br>      ```Bash```<br>```      wget -c '<Private network download link for backup files>' -O <customized backup file name>.<suffix>```<br>```      ```<br>      <br><br>      Example is as follows.<br><br>      ```Bash```<br>```      wget -c '<Private network download link for backup files>' -O backupdownloadtest.backup```<br>```      ```<br>      <br><br><br> |
   


<span id="v7PllaO9"></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeBackups](https://docs.byteplus.com/en/docs/mongodb/describebackups) |Call the DescribeBackups API to query backup file list of target MongoDB instance. |
|[ModifyDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/modifydbinstancebackupurl) |Call the ModifyDBInstanceBackupURL API to obtain the download address of the specified backup file in the target MongoDB instance. |
|[DescribeDBInstanceBackupURL](https://docs.byteplus.com/en/docs/mongodb/describedinstancesbackupurl) |Call the DescribeDBInstanceBackupURL API to query information such as the acquisition progress, download URL, and validity period of the download URL of a specified backup file in the target MongoDB instance. |
