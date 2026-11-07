---
title: "Overview of snapshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots"
---

Creating a snapshot is a backup method. Each snapshot is a backup file of volume data at a specific point in time. When data is lost or a failure occurs, you can roll back changes in volume data through snapshots to restore the lost data.

<span id="use-scenarios"></span>
## Use scenarios

You can use the volume snapshot feature in the following scenarios:


* Daily backup: To back up your data daily, you can create snapshots for your volume in a scheduled manner. When an operation is performed by mistake, you can roll back data changes through snapshots. This prevents data errors or loss caused by multiple reasons, such as unintentional operations, hacker attacks, and viruses.

* Fault tolerance improvement: You can create a snapshot to improve fault tolerance before you perform important O&M operations, such as changing an operating system, migrating business data, and updating applications or software.


<span id="billing-guidance"></span>
## Billing guidance

Snapshots only support pay\-as\-you\-go billing, and charges are calculated based on storage capacity and usage duration. For more details, see[ Snapshot Billing](https://docs.byteplus.com/en/docs/ecs/Snapshot_billing).

<span id="limits"></span>
## Limits


|Category |Precautions |
|---|---|
|Billing |If your account is in arrears, the snapshot function cannot be used normally. If the account is overdue for more than 15 days, snapshots will be deleted. Recharge promptly to avoid affecting your business. |
|Volume specifications |Only ESSD volumes support snapshot creation. |
|Number of snapshots |Each volume can create up to 256 manual snapshots and 1024 automatic snapshots. Description as follows:<br><br><br>* Manual snapshot: If the maximum number is reached, an error will occur when creating a new manual snapshot.<br><br>* Automatic snapshot: Once the maximum number is reached, the system will automatically delete the oldest automatic snapshot. |


<span id="operation-overview"></span>
## Operation overview


* [Create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot)

* [View a snapshot](https://docs.byteplus.com/en/docs/ecs/View-a-snapshots)

* [View a snapshot chains](https://docs.byteplus.com/en/docs/ecs/View-a-snapshot-chain)

* [Delete a snapshot](https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot)

* [Rollback volume through snapshot](https://docs.byteplus.com/en/docs/ecs/Rollback-volume-through-snapshot)

* [Modify a snapshot property](https://docs.byteplus.com/en/docs/ecs/Modify-a-snapshot-property)

* [Create a volume through snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot)
