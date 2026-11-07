---
title: "Manually create backup"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Manually_create_a_snapshot"
---

Milvus for VectorDB supports manual backup creation for the entire instance data, a specified database, or a specified collection. This article explains how to manually create backups.

## Prerequisites

An instance is created. For more information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

* Only Dedicated and Serverless instances support manual backup creation.

* The process of backup and recovery does not support restarting instances, deleting instances, deleting backups being created or restored, or creating or restoring backups again.

* Avoid enabling manual backup and automatic backup simultaneously to prevent backup disk read and write bandwidth from affecting instance performance.

* After creating a backup, the system charges hourly based on the actual TOS storage usage of the backup. The backup feature itself is free. For details, see [backup billing rules](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_billing?TagIDs=#SCCogyeM).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the region for the backup in the top menu bar.

3. Select **Backup management** in the left navigation bar, then click **Create backup** at the top of the page.

4. In the **Create backup** dialog, configure the parameters below and click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Instance type |Select **Dedicated** or **Serverless**. |
   |Instance |Select the target instance for manual backup from the dropdown list. |
   |Authorize to use an instance |Enter the authorized Milvus for VectorDB instance **username** and **password**, then click **Authorize**.<br><br>> **tip**<br><br><br>> This parameter is only visible when the instance is not authorized.<br> |
   |Backup name |Set a custom backup name.<br><br><br>* Must start with a letter.<br><br>* Can only contain letters, numbers, and underscores (_).<br><br>* Length must be between 6 and 102 characters. |
   |Backup object |Select the data objects to back up for manual backup.<br><br><br>* Instance: Back up the full data of the current instance.<br><br>* Specify database: Back up part of the current instance's databases.<br><br>* Specify Collection: Back up part of the current instance's collections. |
   |Back up database |Select the database to back up from the drop\-down list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Backup object** selects **Specify database**.<br> |
   |Select Collections |Select the Collection to back up from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Backup object** selects **Specify Collection**.<br> |
   |Storage location |Select the storage location for the backup.<br><br><br>* Default bucket: the default storage bucket of Milvus for VectorDB.<br><br>* User\-defined bucket: choose the bucket you want to use. |
   |Backup bucket |Select the bucket for storing backups from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Storage location** selects **Custom bucket**.<br> |
   |Bucket authorization |Click **Authorize** to grant the instance access to the selected bucket.<br><br>> **tip**<br><br><br>> This parameter is only visible when the bucket is not authorized.<br> |
   |Remarks |Customize remarks for the manual backup. Maximum length is 65,535 characters. |

## Subsequent operations

After manually creating a backup, you can check the backup progress.

Return to the **Backup management** page to view the progress and status of manually created backups in the **Backup status** column.

> **tip**

* > When the backup status is **Waiting** or **Backing up**, you can select **Cancel** in the backup's **Actions** column to stop the backup creation.

* > **Backing up** changes to **Generated**, indicating the backup is complete and cannot be canceled.
