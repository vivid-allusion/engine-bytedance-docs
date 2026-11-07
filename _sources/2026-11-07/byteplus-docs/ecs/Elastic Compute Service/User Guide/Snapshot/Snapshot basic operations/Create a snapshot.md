---
title: "Create a snapshot"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot"
---

You can manually create a snapshot of your volume as a file to back up volume data at a specific point in time. This topic describes the precautions and the procedure for creating a volume snapshot.

<span id="before-you-begin"></span>
## Before you begin


* Make sure you create snapshots for an Enhance SSD volume.

* Make sure your volume is in the **Available** or **Attached** status before you create a snapshot.

* If your volume is in the **Attached** status, make sure the instance on which the volume is mounted is in the **Running** status or the **Stopped** status.

* The number of snapshots for the volume has not exceeded the snapshot limit for a single volume. Each volume can create up to 256 manual snapshots. When the number of manual snapshots reaches the limit, creating a new snapshot will result in an error.


<span id="precautions"></span>
## Precautions


* We recommend that you create snapshots during off\-peak hours because the system requires a period of time to complete this operation. During creation, do not expand or roll back your volume.

* By default, snapshots created for volume are stored in the same region and availability zone as the source disk.

* You cannot create 2 snapshots of each volume at the same time.

* Details about backup data in snapshots:

   * A snapshot includes the data that is already written to the volume.

   * A snapshot includes the data that is written from the memory to the volume.

   * A snapshot does not include the volume data generated when the snapshot is created.

      To ensure the integrity of snapshot data, we recommend that you do the following before you create a snapshot: 1. Close your instance or make sure all data is written to your volume and read and write operations on the volume are suspended. 2. Perform the operations described in the following table.

      
      |Business |Operation |
      |---|---|
      |Database |Before you create a snapshot, run the `FLUSH TABLES WITH READ LOCK` command to close all open tables and lock all tables for all databases with a global read lock. After the snapshot is created, run the `UNLOCK TABLES` command to unlock the tables. |
      |File system |Before you create a snapshot, run the `sync` command to write data in the memory of file systems to your volume and do not write other data. |
      


<span id="billing-description"></span>
## Billing description

Snapshots only support pay\-as\-you\-go billing, with charges based on capacity and duration. For details, see [Snapshot Billing](https://docs.byteplus.com/en/docs/ecs/Snapshot_billing).

<span id="creating-snapshots-on-the-volume-list"></span>
## Creating snapshots on the volume list


1. Log on to the [ECS console](https://console.byteplus.com/ecs).

2. Activate snapshot service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you see a snapshot list on the snapshot page, it means that the snapshot service has been activated, and there is no need to perform the activation process again.   </div>
   

   1. In the left\-side navigation pane, click **Storage** \> **Snapshots**.

   2. In the top menu bar, choose the project and the Region of the target snapshot.

   3. On the **Snapshots** page,click **Activate snapshot service**,

   4. In the popped\-up dialog box, carefully read and agree to the terms **Elastic Computes Service Terms of Service**, then click **OK**.

3. In the left\-side navigation pane, click **Volumes**.

4. Find the target volume. In the **Actions** column, click **Create snapshot**.

5. In the **Create snapshot** dialog box, configure the parameters described in the following table.

   
   |Parameter |Description |
   |---|---|
   |Snapshot name |(Required) Set the name of your snapshot. Requirements for a valid value:<br><br><br>* The name is 1 through 128 characters in length.<br><br>* The name cannot start with auto or an empty space. |
   |Retention time |You can set the retention time for snapshots. You can choose to retain snapshots permanently or define a custom retention time. The allowable range for custom retention time is from 1 to 65536 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The retention time for snapshots is calculated from the moment the snapshot is created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The retention time for snapshots can only be extended and cannot be shortened. The specific steps are as follows:</div><br><br><br>   <div data-tips="true" data-tips-type="tip">In the snapshot list, click <strong>...</strong> in the <strong>Actions</strong> column of the target snapshot, then choose <strong>Extend snapshot retention time</strong> Set the <strong>Retention Time</strong> and click <strong>OK</strong> to confirm.   </div><br>    |
   |Description |(Optional) Set the description of your snapshot. The description is 0 through 255 characters in length. |
   |Project |(Optional) Choose the project of your snapshot.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Projects are virtual, containing a group of resources, users, and roles. You can view and manage a group of resources in a unified manner based on a project. In addition, you can control the permissions of users and roles on the resources based on a project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If no appropriate projects exist, click <strong>create new project</strong> on the right side to create a project .</div><br> |
   |Tag |A tag consists of a key\-value pair and is used to identify a cloud resource. Tags can help you group cloud resources with the same characteristics in different dimensions, such as purposes, owners, and environments. This helps you search and aggregate cloud resources for easier cloud resource management.<br><br>Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon to add a tag to your snapshot by specifying a tag key and a tag value. For more information, refer to [Tag overview](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |
   

6. Click **Create snapshot**.

   Wait until the snapshot is created. After the snapshot is created, you can view the snapshot in the snapshot list or the snapshot chain of your volume.


<span id="creating-snapshots-on-the-snapshot-list"></span>
## Creating snapshots on the snapshot list


1. Log on to the [ECS console](https://console.byteplus.com/ecs).

2. In the left\-side navigation pane, click **Storage** \> **Snapshots**.

3. In the top menu bar, choose the project and the Region of the target snapshot.

4. Activate snapshot service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you see a snapshot list on the snapshot page, it means that the snapshot service has been activated, and there is no need to perform the activation process again.   </div>
   

   1. On the **Snapshots** page,click **Activate snapshot service**,

   2. In the popped\-up dialog box, carefully read and agree to the terms **Elastic Computes Service Terms of Service**, then click **OK**.

5. On the **Snapshots** tab, click **Create snapshot**.

6. In the **Create snapshot** dialog box, configure the parameters described in the following table.

   
   |**Parameter** |**Description** |
   |---|---|
   |Select volume |Choose a volume for which you want to create a snapshot. |
   |Snapshot name |(Required) Set the name of your snapshot. Requirements:<br><br><br>* The name is 1 through 128 characters in length.<br><br>* The name cannot start with auto or an empty space. |
   |Retention time |You can set the retention time for snapshots. You can choose to retain snapshots permanently or define a custom retention time. The allowable range for custom retention time is from 1 to 65536 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The retention time for snapshots is calculated from the moment the snapshot is created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The retention time for snapshots can only be extended and cannot be shortened. The specific steps are as follows:</div><br><br><br>   <div data-tips="true" data-tips-type="tip">In the snapshot list, click <strong>...</strong> in the <strong>Actions</strong> column of the target snapshot, then choose <strong>Extend snapshot retention time</strong> Set the <strong>Retention Time</strong> and click <strong>OK</strong> to confirm.   </div><br>    |
   |Description |(Optional) Set the description of your snapshot. The description is 0 through 255 characters in length. |
   |Project |(Optional) Choose the project of your snapshot.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Projects are virtual, containing a group of resources, users, and roles. You can view and manage a group of resources in a unified manner based on a project. In addition, you can control the permissions of users and roles on the resources based on a project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If no appropriate projects exist, click <strong>create new project</strong> on the right side to create a project .</div><br> |
   |Tag |A tag consists of a key\-value pair and is used to identify a cloud resource. Tags can help you group cloud resources with the same characteristics in different dimensions, such as purposes, owners, and environments. This helps you search and aggregate cloud resources for easier cloud resource management.<br><br>Click the <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_71b5756a3b692a50b81c3a89f42aa051.png) </span> icon to add a tag to your snapshot by specifying a tag key and a tag value. For more information, refer to [Tag overview](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |
   

7. Click **Create snapshot**.

   Wait until the snapshot is created. After the snapshot is created, you can view the snapshot in the snapshot list or the snapshot chain of your volume.


<span id="what-to-do-next"></span>
## What to do next


* [View a snapshot](https://docs.byteplus.com/en/docs/ecs/View-a-snapshots)

* [View a snapshot chain](https://docs.byteplus.com/en/docs/ecs/View-a-snapshot-chain)

* [Delete a snapshot](https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot)

* [Rollback volume through snapshot](https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot)

* [Modify a snapshot property](https://docs.byteplus.com/en/docs/ecs/Modify-a-snapshot-property)
