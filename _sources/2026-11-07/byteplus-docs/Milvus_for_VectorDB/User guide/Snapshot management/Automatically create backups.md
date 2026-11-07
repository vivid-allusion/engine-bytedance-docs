---
title: "Automatically create backups"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Automatically_create_a_snapshot"
---

Automatic backup means automatically creating backups for specified targets at specified times according to the set rules. This section introduces how to automatically create backups.

## Precautions

* Only Dedicated and Serverless instances support automatic backup creation.

* The process of backup and recovery does not support restarting instances, deleting instances, deleting backups being created or restored, or creating or restoring backups again.

* It is recommended not to enable manual backup and automatic backup simultaneously, as backing up data consumes node disk read and write bandwidth and may affect instance performance.

* After creating a backup, the system charges hourly based on the actual TOS storage usage of the backup. The backup feature itself is free. For details, see [Backup billing rules](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_billing?TagIDs=#SCCogyeM).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the region for the backup in the top menu bar.

3. In the left navigation bar, select **Backup management**, then click **Automatic backup rule** at the top of the page.

4. In the **Automatic backup rule** panel, click **Create a rule**.

5. In the **Create automatic backup rule** dialog, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Instance type |Select **Dedicated** or **Serverless**. |
   |Instance |Select the target instance for manual backup from the dropdown list. |
   |Authorize to use an instance |Enter the authorized Milvus for VectorDB instance **username** and **password**, then click **Authorize**.<br><br>> **tip**<br><br><br>> This parameter is only visible when the instance is not authorized.<br> |
   |Backup object |Select the data objects to back up for automatic backups.<br><br><br>* Instance: Back up the full data of the current instance.<br><br>* Specify database: Back up part of the current instance's databases.<br><br>* Specify Collection: Back up part of the current instance's collections. |
   |Back up database |Select the database to back up from the drop\-down list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Backup object** selects **Specify database**.<br> |
   |Select Collections |Select the Collection to back up from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Backup object** selects **Specify Collection**.<br> |
   |Storage location |Select the storage location for the backup.<br><br><br>* Default bucket: the default storage bucket of Milvus for VectorDB.<br><br>* User\-defined bucket: choose the bucket you want to use. |
   |Backup bucket |Select the bucket for storing backups from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Storage location** selects **Custom bucket**.<br> |
   |Bucket authorization |Click **Authorize** to grant the instance access to the selected bucket.<br><br>> **tip**<br><br><br>> This parameter is only visible when the bucket is not authorized.<br> |
   |Backup schedule |Set the automatic backup cycle as needed.<br><br><br>* Daily: create a backup once daily at the specified time.<br><br>* Hourly: create a backup once every hour at the specified minute.<br><br>* Custom: create a backup once at a specified hour on the backup date. |
   |Select time point |When the **Backup schedule** is set to **Daily**, you need to select a specific time, for example, 20:30 every day. |
   |Select minutes |When **Backup schedule** is set to **Hourly**, select a specific minute, for example, 30 minutes past the hour. |
   |Set user\-defined time |When the **Backup schedule** is set to **Custom**, you need to specify the date and time, for example, 20:00 on Monday.<br><br><br>* Select day: the date to create the backup, such as Monday.<br><br>* Select time: the time to create the backup (on the hour), such as 20:00. |
   |Expiration duration |Select **Limited\-time valid** or **Permanently valid**. When **Limited\-time valid** is selected, set the expiration duration for automatic backups, supporting up to 365 days. |
   |Remarks |Customize remarks for manual backups, supporting up to 65,535 characters. |

## Subsequent operations

When an instance no longer needs to automatically create backups, you can choose to turn off automatic backup creation.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

3. In the left navigation bar, select **Backup management**, then click **Automatic backup rule** at the top of the page.

4. In the **Automatic backup rule** panel, click to filter the automatic backup rules of the target instance by **Instance name/ID**, then click **delete** behind the backup rule.

5. In the pop\-up dialog box, click **OK**.

> **tip**

> After turning off the automatic backup rule, the already created backup data will be retained.
