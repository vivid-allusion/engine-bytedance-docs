---
title: "Use backup to restore data"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Recover_data_using_a_snapshot"
---

After creating a backup, you can use the backup restore feature to restore backup data to a specified instance, including the original or another instance. This document explains how to use backup to restore data.

## Prerequisites

Backups have been completed automatically or manually, or imported from TOS. Related documents: see [Manually create a backup](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Manually_create_a_snapshot), [Automatically create a backup](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Automatically_create_a_snapshot), and [Import a backup from TOS](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Import_a_snapshot_from_TOS).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the region to restore data using the backup from the top menu bar.

3. Select **Backup management** from the left navigation bar, filter backups by **Backup name**, **Instance name**, and **Instance ID**, then click **Recover** in the **Actions** column for the target backup.

4. In the **Recover from backup** panel, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Target instance type |Fixed to **Dedicated instance**, **Serverless instance** is not supported. |
   |Target instance |Select the instance to be recovered from the dropdown list. |
   |Authorize to use an instance |Enter the authorized Milvus for VectorDB instance **username** and **password**, then click **Authorize**.<br><br>> **tip**<br><br><br>> This parameter is only visible when the instance is not authorized.<br> |
   |Recoverable collections ||

5. Check backup restore progress under the **Recovery list** tab.

   When the **Recovery status** changes from **Recovering** to **Normal**, the instance has completed recovery.
