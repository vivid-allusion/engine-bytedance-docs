---
title: "Viewing snapshot information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View-a-snapshots"
---

After you create a snapshot for a volume, you can find the snapshot and view its details from either the Volumes or Snapshots page.

<span id=".5b-r54Wn54q25oCB6K-05piO"></span>
## Snapshot status


|Status |Description |
|---|---|
|Creating |The snapshot is being created. |
|Available |The snapshot is available. You can use it to roll back a volume. |
|Rolling back |The snapshot is being used to roll back a volume. |
|Deleting |The snapshot is being deleted. |
|Fail |The snapshot is unavailable due to an error. |


<span id=".5p-l55yL5b-r54Wn6K-m57uG5L-h5oGv"></span>
## Viewing snapshot details

<span id=".5Zyo5LqR55uY5YiX6KGo5p-l55yL"></span>
### From the Volumes page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Volumes".

3. In the top menu bar, select the project and region where the volume resides.

4. On the "Volumes" page, click "... \> View snapshot chain" in the "Actions" column of the volume.

5. Under "Snapshot list", click the name of the snapshot you want to check. This will open its details page.


<span id=".5Zyo5b-r54Wn5YiX6KGo5p-l55yL"></span>
### From the Snapshots page


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the snapshot resides.

4. On the "Snapshots" page, click the name of the snapshot you want to check. This will open its details page.


<span id=".5p-l55yL5b-r54Wn5a656YeP5ZKM5pWw6YeP"></span>
## Viewing the size and quantity of snapshots

**Viewing the size of snapshots in a specific region**


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region you want to check.

3. In the left navigation pane, select "Storage \> Snapshots". On the "Snapshots" page, view the size of snapshots in the selected region at the top.


**Viewing the total number of snapshots in a specific project and region**


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the project and region you want to check.

3. In the left navigation pane, select "Storage \> Snapshots". On the "Snapshots" page, view the total number of snapshots in the selected project and region at the top.
