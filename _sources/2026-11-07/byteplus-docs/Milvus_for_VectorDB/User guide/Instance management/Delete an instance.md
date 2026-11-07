---
title: "Delete an instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Delete_an_instance"
---

You can delete an instance to release related resources when it is no longer in use. This topic describes how to delete a Milvus for VectorDB instance.

## Prerequisites

* Created instances must be in **Running** or **Creation failed** status. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* The delete protection feature is **disabled** for the instance. For more information, see [Configure delete protection for an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Configure_delete_protection_for_an_instance).

## Precautions

* After deleting an instance, the system automatically creates a backup and retains it for 7 days. Within 7 days, you can use the backup to restore the instance. For detailed operations, see [Use a backup to restore data](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Recover_data_using_a_snapshot). After 7 days, all nodes and data of the instance will be permanently cleared and unrecoverable; proceed with caution.

* After an instance is deleted, the IP resources it occupied will be released.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the instances list, select the **Dedicated**, **Serverless**, or **On\-Demand** tab as needed, then choose  **... \> Delete** (Dedicated instance) in the **Actions** column of the target instance., or click **Delete** (Serverless or On\-Demand instance) in the **Actions** column of the target instance.

   > **tip**

   > You can also go to the instance details page and click **Delete** in the top right corner.

5. In the pop\-up dialog, click **Delete**.
