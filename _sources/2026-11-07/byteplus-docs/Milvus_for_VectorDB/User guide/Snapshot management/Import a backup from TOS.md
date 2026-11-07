---
title: "Import a backup from TOS"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Import_a_snapshot_from_TOS"
---

Milvus for VectorDB supports importing created backups from TOS. This document explains how to import backups.

## Prerequisites

Obtain the TOS bucket name and backup storage path where the backup is stored.

## Precautions

Importing backups only supports Dedicated instances and does not support Serverless or On\-Demand editions.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the region for importing the backup from the top menu bar.

3. Select **Backup management** in the left navigation bar, then click **Import backup** at the top of the page.

4. In the **Import backup** dialog, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Instance type |Fixed to **Dedicated**. |
   |Instance |Select the target instance to import the backup from the dropdown list. |
   |Authorize to use an instance |Enter the authorized Milvus for VectorDB instance **username** and **password**, then click **Authorize**.<br><br>> **tip**<br><br><br>> This parameter is only visible when the instance is not authorized.<br> |
   |Backup name |Set a custom backup name.<br><br><br>* Must start with a letter.<br><br>* Can only contain letters, numbers, and underscores (_).<br><br>* Length must be between 6 and 102 characters. |
   |||
   |Bucket name |Select the bucket where the backup to import is stored from the dropdown list. |
   |Bucket authorization |Click **Authorize** to grant the instance access to the selected bucket.<br><br>> **tip**<br><br><br>> This parameter is only visible when the bucket is not authorized.<br> |
   |Backup root path |Select the storage path of the backup to import in the bucket from the dropdown list. |

5. Check the progress of the backup import.

   On the **Backup management** page, check the progress of the backup import. Status changes from **Backup** to **Generated**, indicating the backup import is complete.
