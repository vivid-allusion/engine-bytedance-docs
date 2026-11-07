---
title: "Rollback volume through snapshot"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot"
---

If your volume becomes corrupted or loses data, you can roll back to a previous state using a snapshot.

<span id="before-you-begin"></span>
## Before you begin


* Make sure you do not delete the source volume. Currently, snapshot data can only be rolled back to the source volume.

* Make sure the source volume is in one of the following status:

   * **Available**: indicates the volume is not mounted on an instance. You can directly roll back data to your volume.

   * **Attached**: indicates the volume is mounted on an instance. You can roll back data to the volume when the instance is in the **Stopped** status.

* Make sure no snapshots are being created for the source volume.

* Make sure your snapshot is in the **Available** status.

* Avoid using a snapshot created with a different operating system than the current volume. Otherwise, the rollback will fail.


<span id="precautions"></span>
## Precautions


* We recommend that you create a snapshot to back up the current data before your rollback.

* After a volume is expanded, you can still use a snapshot created prior to the expansion for your rollback.

* When you roll back a mounted volume, do not start it.

* Assume that you expand a volume after a snapshot is created for it. After you use the snapshot to roll back the volume, expand the volume again. For more information on the related steps, refer to [Expanding volumes](https://docs.byteplus.com/en/docs/ecs/Overview-of-extending-volume).


<span id="rolling-back-on-the-volume-list"></span>
## Rolling back on the volume list


1. Log on to the [ECS console](https://console.byteplus.com/ecs).

2. In the left\-side navigation pane, click **Storage** \> **Volumes**.

3. In the top menu bar, choose the project and the Region of the target volume.

4. Find the target volume. Then, in the **Actions** column, click the **ellipsis** icon \> **Check snapshot chain**.

5. On the snapshot chain list, find the target snapshot. Then, in the **Actions** column, click the **ellipsis** icon \> **Rollback snapshot**.

6. In the dialog box that appears, click **Rollback snapshot**.


<span id="rolling-back-on-the-snapshot-list"></span>
## Rolling back on the snapshot list


1. Log on to the [ECS console](https://console.byteplus.com/ecs).

2. In the left\-side navigation pane, click **Storage** \> **Snapshots**.

3. In the top menu bar, choose the project and the Region of the target snapshot.

4. Find the target snapshot. Then, in the **Actions** column, click the **ellipsis** icon \> **Rollback snapshot**.

5. In the dialog box that appears, click **Rollback snapshot**.
