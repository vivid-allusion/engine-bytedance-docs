---
title: "Viewing snapshots"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Viewing-snapshots"
---

This topic introduces the operation steps for viewing all snapshot lists and snapshot chains.

<span id=".5b-r54Wn54q25oCB6K-05piO"></span>
## Snapshot status


|**Status** |**Description** |**API value** |
|---|---|---|
|Creating |Snapshot is being created. |Progressing |
|Creation successfully |Snapshot creation successful, in an available state. You can use this snapshot to create a new file system. |Accomplished |
|Creation failed |Snapshot creation failed, unable to use. |Failed |


<span id=".5p-l55yL5b-r54Wn5YiX6KGo"></span>
## View snapshot list


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** page, click the name of the target snapshot.

5. On the snapshot details page, you can view the basic information of the snapshot, including **Snapshot name**, **Snapshot ID**, **File System Name**, and other information.


<span id=".5p-l55yL5b-r54Wn6ZO-"></span>
## View snapshot chain

The snapshot chain is a relationship chain composed of all the snapshots in a single file system, with one snapshot chain corresponding to one file system.

<span id=".5Zyo5a6e5L6L5YiX6KGo5p-l55yL"></span>
### View snapshot chain in file system List


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System** \> **File System List**.

4. On the **File System List** page, click the target file system name.

5. On the **Overview** page, click the number after **the number of Snapshots** to access the snapshot chain list.

6. In the **Snapshot chain** list, view all snapshot information associated with the current file system.


<span id=".5Zyo5b-r54Wn5YiX6KGo5p-l55yL"></span>
### View snapshot chain in snapshot list.


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** List page, click  **...**  button in the **Actions** column of the target snapshot name, and then select View Snapshot Chain.

5. In the **Snapshot chain** list, view all snapshot information associated with the current file system.
