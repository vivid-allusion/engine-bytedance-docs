---
title: "Rolling back a volume using a snapshot group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Rollback-volumes-through-snapshot-consistency-group"
---

If an exception occurs, you can use a snapshot group to roll back a volume and restore your data.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a snapshot group and have not changed the ECS instance operating system since then.

* The instance for which the snapshot group was created is "Stopped". For steps to stop an instance, see [Stopping instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).

* None of the volumes for which the snapshot group was created have been deleted and all remain in "Attached" status.

* All snapshots in the snapshot group are "Available".


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Currently, you can only use a snapshot to roll back the volume from which it was taken. Rolling back other volumes is not supported. To use a snapshot group to create a new volume, create a new instance and select the snapshot group. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* Rolling back a volume restores its data to the state at the time the snapshot was created. Any data generated after that time point will be deleted and cannot be recovered. Proceed with caution.


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshot group resides.

4. On the "Snapshots" page, click the "Snapshot Groups" tab.

5. On the "Snapshot Groups" tab, click "Rollback" in the "Actions" column of the snapshot group you want to use.

6. In the box that appears, select the snapshot you want to use and click "Rollback snapshot group".
