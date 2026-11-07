---
title: "Deleting snapshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot"
---

You can delete a snapshot when you no longer need its data or when the number of snapshots exceeds the limit. Snapshots can be deleted individually or in batches.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Only snapshots with an "Available" or "Fail" status can be deleted. Snapshots with the status "Creating" or "Rolling back" cannot be deleted.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Deleting a snapshot from a specific time point does not affect snapshots taken at other times.

* Deleting the source volume does not automatically remove manual snapshots.

* Deleted snapshots cannot be recovered.


<span id=".5LuO5LqR55uY5YiX6KGo5Yig6Zmk5b-r54Wn"></span>
## Deleting snapshots from the Volumes page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, click "... \> View snapshot chain" in the "Actions" column of the volume.

5. Under "Snapshot list", you can either delete snapshots individually or in batches.

   * To delete a single snapshot, click "... \> Delete snapshot" in the "Actions" column of the volume.

   * To delete multiple snapshots, select the snapshots you want to delete, and then click "Delete" at the bottom of the page.

6. In the box that appears, confirm the deletion by clicking "Delete snapshot".


<span id=".5LuO5b-r54Wn5YiX6KGo5Yig6Zmk5b-r54Wn"></span>
## Deleting snapshots from the Snapshots page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshot resides.

4. On the "Snapshots" page, you can either delete snapshots individually or in batches.

   * To delete a single snapshot, click "... \> Delete snapshot" in the "Actions" column of the volume.

   * To delete multiple snapshots, select the snapshots you want to delete, and then click "Delete" at the bottom of the page.

5. In the box that appears, confirm the deletion by clicking "Delete snapshot".
