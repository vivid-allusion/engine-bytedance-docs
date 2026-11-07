---
title: "Deleting an auto snapshot policy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Deleting-an-auto-snapshot-policy"
---

If you no longer need to use the automatic snapshot policy, you can delete the corresponding policy. This topic describes the steps to delete an automatic snapshot policy in the Byteplus console.

<span id="前提条件"></span>
## Prerequisite

Before deleting the automatic snapshot policy, please ensure that the policy is not associated with any file system, otherwise it will result in deletion failure.

<span id="注意事项"></span>
## Precautions


* Once the automatic snapshot policy is deleted, it cannot be recovered. Please be cautious when deleting.

* If the instance is in the process of creating an automatic snapshot when the automatic snapshot policy is deleted, the server will continue to create that snapshot. However, subsequent automatic snapshots will no longer be created.


<span id="操作步骤"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** page, click **Auto Snapshot Policy** tab.

5. Click **Delete** corresponding to the target automatic snapshot policy **Actions** column.

6. Click **Delete** in the pop\-up dialog box.
