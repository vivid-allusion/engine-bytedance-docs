---
title: "Creating a new file system using a snapshot"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating-a-new-file-system-using-a-snapshot"
---

After creating a snapshot, if you need to restore the data of the file system, you can use the snapshot to create a new file system.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

When using snapshots to create a file system, please ensure that the status of the snapshot is created successfully.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Currently, only creating a file system using snapshots is supported, and rolling back to other file systems using snapshots is not supported.

* Only creating Extreme NAS file systems is supported through snapshots.

* During the process of creating a file system using snapshots, it is not possible to create snapshots for that file system.

* After creating a file system using snapshots, the snapshot will still be retained and not deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** List page, click **Create File System** in the corresponding **Actions** column of the target snapshot.

5. On the **Create File System** page, configure the file system parameters, and then click **Confirm order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Parameter Description for Creating File System, please refer to <a href="https://docs.byteplus.com/docs/nas/Creating-a-file-system">Creating a file system</a>.   </div>
   

6. On the details page, read and check **The Terms Of storage products and services**, then click **Buy now**.

7. After confirming the information is correct, click **Next step**.
