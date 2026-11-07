---
title: "Creating an auto snapshot policy"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Creating-an-auto-snapshot-policy"
---

If you want to regularly create snapshot backups for the file system, you can use automatic snapshot policies. This topic describes the steps to create automatic snapshot policies in the Byteplus console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


|**Classification** |**Note** |
|---|---|
|Specifications |Only the extreme file system supports automatic snapshot strategy. |
|Quantity |Currently, the snapshot function is in the free stage, and each file system can create up to 5 automatic snapshots. When the number of automatic snapshots exceeds the limit, the system will automatically delete the earliest created automatic snapshot. |
|Creation time |* There may be a certain time difference between the creation time point in the automatic snapshot strategy and the actual time when the server creates the snapshot. Please refer to the actual creation time.<br><br>* If the time taken to create a snapshot exceeds the time interval between two automatic snapshot executions, the system will automatically skip the second time point and not create a snapshot. For example, if you set 1:00, 2:00, and 3:00 as automatic snapshot time points, and the snapshot created at 1:00 takes longer and lasts until 2:30 to complete, then the snapshot will not be created at 2:00, and the next snapshot creation time point will be 3:00.<br><br>* The file system cannot create automatic snapshots and manual snapshots at the same time. At the automatic snapshot creation time point, if the file system is executing a snapshot creation task (manual or automatic), the system will not create an automatic snapshot at that time point.<br><br>* If the file system reaches its expiration release time exactly when creating a snapshot, the file system will be released and the snapshots being created will also be deleted, but the previously created automatic snapshots will not be deleted. |
|Automatic Snapshot Naming |The naming rule for automatic snapshots is `auto-yyyyMMdd-HH-x (number)`. Among them, yyyyMMdd represents the date of the day, and HH represents the hour. For example: auto\-20220227\-11\-2. |
|File system |* When creating an automatic snapshot, the file system must be in a **running** state.<br><br>* When creating an automatic snapshot, mounting the file system is allowed, but resizing operations are not allowed. |


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [FileNAS console](https://console.byteplus.com/filenas).

2. In the top menu bar, select the region where you want to create the file system.

3. On the left navigation bar, select **File System \> Snapshot**.

4. On the **Snapshot** page, click **Auto Snapshot Policy** tab.

5. On the **Auto Snapshot Policy** tab, click on **Create policy** and set the strategy parameters in the pop\-up dialog box.

   
   |**Parameters** |**Description** |
   |---|---|
   |Policy name |Set the name of the automatic snapshot strategy, with the following value description:<br><br><br>* It cannot start with a number, hyphen (\-), or "auto".<br><br>* It can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).<br><br>* The length should be between 1 and 128 characters. |
   |Creation time point |Choose the time point(s) for automatic snapshot creation, supporting the selection of one or multiple time points.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Creating snapshots will reduce storage performance. It is recommended to create snapshots during periods of low business activity.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the time taken to create an automatic snapshot exceeds the interval between two time points, the next time point will be skipped automatically. For example, if you have set 1:00, 2:00, and 3:00 as automatic snapshot time points, and the snapshot created at 1:00 takes a long time and is not completed until 2:30, then the snapshot will not be created at 2:00, and the next snapshot creation time point will be 3:00.</div><br> |
   |Creation time point |Choose the repeating dates when creating a snapshot, and support selecting one or multiple dates. |
   |Retention time<br><br> |The default retention time for automatic snapshots is 30 days.<br><br><br>* Custom retention time: The retention time can be set from 1 to 65536 days.<br><br>* Permanent retention will be automatically deleted until the number of automatic snapshots reaches the upper limit：After the number of automatic snapshots reaches the limit, the system will automatically delete the earliest created automatic snapshot.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, the snapshot function is in the free stage, and each file system can create up to 5 automatic snapshots. When the number of automatic snapshots for a single disk reaches the limit, the system will delete the earliest created automatic snapshot.</div><br> |
   

6. After completing the parameter settings, click **create**.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

After creating an automatic snapshot policy, you need to associate it with the file system for the policy to take effect. For specific steps, please refer to [Associating an automatic snapshot policy with a file system](https://docs.byteplus.com/docs/nas/Associating-an-auto-snapshot-policy-with-a-file-system).
