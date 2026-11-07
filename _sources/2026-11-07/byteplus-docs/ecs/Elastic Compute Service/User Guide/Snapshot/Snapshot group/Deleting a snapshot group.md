---
title: "Deleting a snapshot group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot-consistency-group"
---

You can delete a snapshot group when you no longer need it to reduce the number of snapshots.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

All snapshots in the snapshot group must have an "Available" or "Fail" status. The group cannot be deleted if any snapshots have a status of "Creating" or "Rolling back".

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Deleting a snapshot group created at a specific time point does not affect snapshots taken at other times.

* Deleting a source volume or instance does not change the status of the snapshot group.

* Deleted snapshots cannot be recovered.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshot group resides.

4. On the "Snapshots" page, click the "Snapshot Groups" tab.

5. On the "Snapshot Groups" tab, click "Delete" in the "Actions" column of the snapshot group you want to remove.

6. In the box that appears, click "Delete".
