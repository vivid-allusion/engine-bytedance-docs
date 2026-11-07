---
title: "Snapshot management overview"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/snapshot_management_overview"
---

To avoid data loss, you can back up your index data, i.e. create snapshots. When data gets lost or you wish to retrieve data from a certain period, you can quickly obtain data by restoring the index. On the snapshot management page, you can create snapshots and restore snapshots for all instances in the current account and region.

<span id="712a05c3"></span>
## **Snapshot method**

Snapshots are not real\-time and take a certain amount of time to complete, so a snapshot is a view at some point in time from the start time to the end time. You can continue to index documents or perform other operations while the creation of a snapshot is in progress, but new or updated documents may not be included in the snapshot.

Currently, we support two methods to create snapshots: **Automatic** and **Manual**. Choose the appropriate method according to your business needs. It is recommended not to perform manual and automatic snapshots on the same instance at the same time, as it affects the performance of the instance because data backups consume the read and write bandwidth of the node's hard disk.


|**Method** |**Description** |
|---|---|
|Automatic snapshots |According to predefined rules, snapshots are automatically created at a specified time.<br><br>Snapshots are incremental, automatically deleting duplicate data, and storing only the data that has changed since the last successful snapshot. The feature of snapshots effectively saves storage space and reduces network transmission costs, while decreasing the time needed to perform snapshots. |
|Manual snapshots |Snapshots can be manually created for current instance data or several indexes.<br><br>Creating snapshots manually backs up the full amount of data for the index each time. |


<span id="87dfd1a5"></span>
## Snapshot storage

When you create a snapshot for an instance for the first time, the system automatically creates a TOS Bucket for storing snapshots and searchable snapshots.

The default name format for system buckets is `es-shadow-prod-{region}-{accountId}`, such as `es-shadow-prod-cn-beijing-2100***`.

You can click on the snapshot name and view the storage bucket and storage path information on the snapshot **details** page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For existing instances, there may be two special cases:</div>



* <div data-tips="true" data-tips-type="tip">If the existing instance has been configured to automatically create snapshots, it continues to use the configured bucket for the current account; if it is newly configured to automatically create snapshots, it uses the system default bucket.</div>


* <div data-tips="true" data-tips-type="tip">If the mirror version of the existing instance is too old, the instance may only be able to use the current account's bucket.</div>



<span id="4a83e02d"></span>
## **Snapshot recovery**

Through the snapshot recovery feature, restore the index data in the snapshot to the instance. For the target instance with cold data nodes enabled, recovery to a searchable snapshot\-read\-only index is supported.

For details, refer to [Recovering data using a created snapshot](https://docs.byteplus.com/docs/cloudsearch/36400#5ff7f7d4).
