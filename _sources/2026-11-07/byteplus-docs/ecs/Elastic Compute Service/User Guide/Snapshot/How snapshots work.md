---
title: "How snapshots work"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How_snapshots_work"
---

A snapshot is the data backup of a volume at a specific point in time. This topic describes how snapshots are implemented, including how incremental snapshots, snapshot\-based rollback, and snapshot deletion are implemented.

<span id="incremental-snapshots"></span>
## Incremental snapshots

When you use volume snapshots, incremental snapshots are created. Only the first snapshot is a full snapshot, while all subsequent snapshots only contain the changed data. This helps save on storage capacity and fees.

As shown in the following figure, the volume contains 3 snapshots: snapshot 1, snapshot 2, and snapshot 3.


* Snapshot 1: It is the first snapshot of the volume and backs up all data blocks in the volume.

* Snapshot 2: It is the second snapshot of the volume and backs up the changed data blocks: A' and D'. The data of data blocks B and C in snapshot 1 is referenced.

* Snapshot 3: It is the third snapshot of the volume and backs up the changed data block B''. The data of data blocks A' and D' in snapshot 2 is referenced, and that of the data block C in snapshot 1 is referenced.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d90481f1751117d2f82c2896dd0a88a6.png) </span>

<span id="snapshot-based-rollbacks"></span>
## Snapshot\-based rollbacks

When you use a specific snapshot to roll back data, Elastic Block Storage (EBS) automatically merges this snapshot and the previous snapshots. If identical data blocks exist, the data in the latest snapshot is retained. During the rollback, EBS writes the merged data to your volume.

As shown in the following figure, the volume contains 3 snapshots: snapshot 1, snapshot 2, and snapshot 3. If you use snapshot 3 to roll back data, the system rolls back data in data blocks A', B'', C, and D' to the volume.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fd4a8904222c694d628252fa4e0d0db9.png) </span>

<span id="deleting-snapshots"></span>
## Deleting snapshots

If you do not want to retain a specific snapshot or the number of snapshots exceeds the upper limit, delete snapshots to free up space.

As shown in the following figure, the volume contains 3 snapshots: snapshot 1, snapshot 2, and snapshot 3. If you delete snapshot 1, the system deletes data blocks A and D that are changed but does not delete data blocks B and C that are referenced.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d0dfce19f9c3698e44029a5494abfe3c.png) </span>
