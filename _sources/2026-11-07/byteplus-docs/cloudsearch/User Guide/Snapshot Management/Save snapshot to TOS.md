---
title: "Save snapshot to TOS"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Save_snapshot_to_TOS"
---

Cloud Search supports saving snapshots created automatically or manually to other TOS under the current account. This topic explains how to save snapshots to TOS.

> **tip**

> The save snapshot to TOS feature is not available to individual users. To use it, complete enterprise authentication. For detailed steps, see [Enterprise authentication](https://docs.byteplus.com/en/docs/6261/64937).

## Preparations

You need to obtain the bucket name, Access Key, and Secret Key of the target TOS in advance.

## Precautions

Saving snapshots to TOS automatically creates a migration task in the storage migration task console and incurs related fees. For related reference documentation, see [create migration task](https://docs.byteplus.com/en/docs/dms/Quick_start1) and [billing instruction](https://docs.byteplus.com/en/docs/dms/Product-Billing).

## Save snapshot to TOS

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Snapshot management**, filter snapshots by **Snapshot name**, **Instance name**, and **Instance ID**, then click **Save to TOS** behind the target snapshot.

   > **tip**

   * > Support saving to TOS for snapshots created automatically or manually. If the snapshot of an existing instance is already stored in this account's TOS, saving to TOS is not supported.

   * > Snapshots originally saved from TOS do not support saving to TOS again.

4. In the **Save to TOS** dialog, select the bucket, set the snapshot path, and enter AK and SK information, then click **OK**.

   |**Configuration** |**Description** |
   |---|---|
   | Select bucket |Select the target bucket to transfer the current snapshot to this bucket. |
   |Destination path |Customize the snapshot storage path to transfer the current snapshot to the bucket's path.<br><br>> **tip**<br><br><br><br>* > If the bucket does not contain a folder for the path, a new folder will be created after executing the transfer.<br><br><br>* > If the bucket already has a folder for the path, that folder must be empty; otherwise, an error will occur.<br> |
   |Access key |Use the Access key and Secret Key to access the target TOS. |
   |Secret Key ||

5. Click the snapshot name to view transfer progress under the **Transfer Records** tab.

   After transferring the snapshot to TOS, a migration task will be automatically created in the Storage Migration Task Console. Click the migration task ID to go to the [Storage Migration Service](https://console.byteplus.com/dms/) console and view the automatically generated migration task.
