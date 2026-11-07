---
title: "Deleting a snapshot"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Deleting-a-snapshot"
---

When you no longer need to retain certain snapshot data or the number of snapshots created exceeds the limit, you can delete the snapshots.

<span id="前提条件"></span>
## Prerequisite

Only snapshots with a status of creation successfully or creation failed can be deleted. Snapshots that are in the process of being created or rolled back cannot be deleted.

<span id="注意事项"></span>
## Precautions


* Delete snapshots of a file system at a specific point in time without affecting other snapshots at different points in time.

* Deleting the source file system does not automatically delete manual snapshots. Manual snapshots can only be deleted manually.

* Deleted snapshots cannot be recovered, so please proceed with caution.


<span id="操作步骤"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** List page, click  **...**  in the **Actions** column of the target snapshot name, and then select **Delete Snapshot**.

5. Click **Delete** in the pop\-up dialog box.
