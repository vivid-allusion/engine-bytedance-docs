---
title: "Creating a snapshot"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating-a-snapshot"
---

This topic introduces the prerequisites and steps for creating a snapshot.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* Already created extreme file system, and the file system status is running. For specific steps, please refer to [Creating a file system](https://docs.byteplus.com/docs/nas/Creating-a-file-system).

* The number of snapshots in the file system has not reached the limit. During the public beta period, a high\-speed NAS file system can create up to 5 manual snapshots.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only extreme file systems support creating snapshots.

* The current snapshot is in the public testing phase and is temporarily free of charge. During the testing period, a high\-speed NAS file system can create up to 5 manual snapshots.

* Creating a snapshot takes some time and there will be a period of time when the data cannot be written in minutes. It is recommended to perform the operation during the low peak period of your business. During the creation period, you can mount the file system, but you cannot delete or resize the file system.

* A single file system cannot create multiple snapshots at the same time.

* Batch creation of snapshots for multiple file systems is not supported.

* Manually created snapshots will be permanently retained and cannot be automatically deleted. If you need to delete a snapshot, please refer to [Deleting a snapshot](https://docs.byteplus.com/docs/nas/Deleting-a-snapshot).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**

<span id=".5Zyo5a6e5L6L5YiX6KGo5Yib5bu6"></span>
### Creating snapshots in the file system list


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System** \> **File System List**.

4. On the instance list page, click  **...**  button in the **Actions** column of the target file system, and then click **Create Snapshot**.

5. Set snapshot parameters in the pop\-up dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |File System ID |Instance ID, filled in by default. |
   |File System Name |Instance name, filled in by default. |
   |Snapshot name |Set snapshot name, required. Naming conventions are as follows:<br><br><br>* It cannnot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* It cannnot start with auto. |
   |Description |Optional, length of 0 to 120 characters. |
   |Setting File System to Read Only During Snapshot |Choose whether to turn on **Setting File System to Read Only During Snapshot**，It is recommended to select this configuration to obtain a snapshot with complete data. If this configuration is not selected, data written during the creation of the snapshot may not be saved to the snapshot created at that point in time. |
   

6. After completing the parameter settings, click **OK**.


<span id=".5Zyo5b-r54Wn5YiX6KGo5Yib5bu6"></span>
### Create a snapshot in the snapshot list


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** list page, click **Manually create snapshot**.

5. Set snapshot parameters in the pop\-up dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |File System |Select the file system for which you want to create a snapshot from the dropdown menu. |
   |Snapshot name |Set snapshot name, required. Naming conventions are as follows:<br><br><br>* It cannnot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length should be between 1 and 128 characters.<br><br>* It cannnot start with auto. |
   |Description |Optional, length of 0 to 120 characters. |
   |Setting File System to Read Only During Snapshot |Choosing whether to turn on **Setting File System to Read Only During Snapshot** is recommended to select this configuration to obtain a snapshot with complete data. If this configuration is not selected, data written during the creation of the snapshot may not be saved to the snapshot created at that point in time. |
   

6. After completing the parameter settings, click **Create**.


<span id=".55u45YWz5pON5L2c"></span>
## Related operations


* [Viewing snapshots](https://docs.byteplus.com/docs/nas/Viewing-snapshots)

* [Deleting a snapshot](https://docs.byteplus.com/docs/nas/Deleting-a-snapshot)

* [Creating a new file system using a snapshot](https://docs.byteplus.com/docs/nas/Creating-a-new-file-system-using-a-snapshot)

* [Modifying snapshot properties](https://docs.byteplus.com/docs/nas/Modifying-snapshot-properties)
