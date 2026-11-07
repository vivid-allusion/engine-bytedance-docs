---
title: "Setting up automatic snapshots"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/automatic-snapshots"
---

Snapshots can be automatically captured within a specified time window based on predefined rules. When you require automatic snapshots, enable this feature and define the snapshot policy. When automatic snapshots are no longer needed, disable the feature.

<span id="a6252a4a"></span>
## Precautions


* The initial snapshot of an instance is a complete copy of the entire instance data. The duration for taking this snapshot varies based on the volume of data. Subsequent snapshots, however, only capture incremental changes and differences from the initial snapshot.

* During the backup or restoration, do not perform the following operations: restart a cluster, delete a cluster, delete a snapshot that is being created or used for restoration, create another snapshot, or use another snapshot for restoration.

* We recommend that you do not enable manual and automatic methods simultaneously, as it impact instance performance. Because backup will occupy the node's disk read and write bandwidth.

   Please first check the usage of node disk read/write bandwidth in the Cloud Monitoring console. If the disk read/write bandwidth has approached saturation, it is recommended to stop the data backup operation first to avoid affecting the read/write performance. For more information, refer to [Viewing monitoring information](https://docs.byteplus.com/en/docs/cloudsearch/viewing-monitoring).


<span id="e97578f2"></span>
## Enabling automatic snapshots


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance to go to its details page.

4. In **Instance management \> Backup management**, click **Automatic backup**.

5. In the **Automatic backup** dialog box, toggle the **Automatic backup** switch to enable the feature, configure the parameters described in the following table, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Automatic backup |Toggle the switch to enable automatic backups, and configure the backup policy as needed.<br><br>Exercise caution during policy configuration, as the backup policy cannot be modified once set. If the backup policy is incorrectly configured, you must disable automatic backups. |
   |Select the bucket |Select a Tinder Object Storage (TOS) bucket in which the snapshot is saved.<br><br>If no TOS bucket is available, click **Create a bucket** to create a bucket in the TOS console. |
   |Backup cycle settings |Configure the backup interval as needed.<br><br><br>* **Every day**: Creates a snapshot at a specified point in time every day.<br><br>* **Per hour**: Creates a snapshot at a specified point in time every hour.<br><br>* **User\-defined**: Creates a snapshot at a specific hour on a date that you specify. |
   |Select time point |If you set the backup interval to **Every day**, select a specific point in time, such as 20:30. |
   |Select minutes |If you set the backup interval to **Per hour**, select a specific minute, such as the 30th minute of each hour. |
   |Settings user\-defined time |If you set the backup interval to **User\-defined**, specify the date and time, such as 20:00 on Monday.<br><br><br>* **Backup date**: Select the date when the snapshot is created, such as Monday.<br><br>* **Backup time**: Select the time (on the hour) when the snapshot is created, such as 20:00. |
   |Backup retention days |Specify how long you want to retain snapshots. The value ranges from 1 day to 365 days. The default value is 7 days. |
   |Remarks |Type custom remarks. |
   


<span id="13911dc4"></span>
## Disabling automatic snapshots

When automatic snapshots are no longer needed, you can disable this feature.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Region of the target instance.

3. On the **Instances** page, click the name of the instance to go to its details page.

4. In **Instance management \> Backup management**, click **Automatic backup**.

5. In the **Automatic backup** dialog box, toggle the **Automatic backup** switch to disable the feature, select a TOS backup policy, then click **OK**.

   * **Keep TOS backup after disabling**: Retains the backups stored in TOS after disabling automatic snapshots.

   * **Disable and delete TOS backups**: Deletes the backups stored in TOS after disabling automatic snapshots. Deleted data cannot be restored. Exercise caution when performing this operation.
