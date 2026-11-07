---
title: "Data disaster recovery and backup"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration"
---

Cloud environments often host large volumes of critical business data. To ensure the security and stability of cloud data, ECS instances provide disaster recovery solutions by using features such as snapshots and custom images.

<span id=".5pWw5o2u5aSH5Lu9"></span>
## Data backup

<span id=".5b-r54Wn"></span>
### Snapshot


* **Snapshot backup**

   A snapshot is a type of backup that captures the data on a volume at a specific point in time. You can specify an auto\-snapshot policy to create volume snapshots regularly, enabling daily data backup. For more information, see [Setting auto-snapshot policy to regularly back up important data](https://docs.byteplus.com/en/docs/ecs/Manage-auto-snapshot-policies).

   To reduce snapshot storage space and costs, volume snapshots use incremental mode. When you create snapshots, the first snapshot is a full snapshot, while all subsequent snapshots are incremental snapshots containing only data that has changed since the previous snapshot.

* **Snapshot rollback**

   In the event of an operational error, you can use snapshots to roll back data, preventing data errors or loss caused by human mistakes, hacker attacks, virus infections, and other issues. When you perform a rollback using a snapshot, EBS automatically merges that snapshot with previous snapshots. For identical data blocks, the data from the latest snapshot is retained. During rollback, EBS writes the merged data into the volume.

   For more information, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) and [Using snapshots to roll back data](https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot).


<span id=".6Ieq5a6a5LmJ6ZWc5YOP"></span>
### Custom image


* **Image backup**

   You can back up the system volume by creating a custom image and the data volumes by using snapshots. Custom image backups are full backups and must be triggered manually. For more information, see [Creating custom images](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-1).

* **Image recovery**

   After you create a custom image, you can restore data by creating an instance from it. For more information, see [Creating instances by using custom images](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images).


<span id=".6auY5Y-v55So6YOo572y"></span>
## High availability deployment

BytePlus offers the deployment set feature that manages the distributed deployment of instances across underlying hardware, enabling physical\-level security isolation. By creating deployment sets, you can distribute instances across different physical servers. This ensures underlying disaster recovery capabilities and high availability. For more information, see [Deployment sets](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview).
