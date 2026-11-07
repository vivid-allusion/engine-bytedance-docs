---
title: "Instant access snapshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instant-access"
---

With instant access, you can create a new volume using a snapshot without waiting for the snapshot to finish being created. This makes the process faster and more convenient.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Instant access snapshots are supported by ESSD PL0 and ESSD FlexPL volumes at no additional charge.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You cannot create images from instant access snapshots.

* Instant access only works for manual snapshots that are currently being created.

* You cannot create a volume from an instant access snapshot in a different availability zone than the one where the snapshot is stored.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the availability zones of instant access snapshots, navigate to the <strong>Availability zone</strong> column on the <strong>Snapshots</strong> page.   </div>
   

<span id=".5L2_55So5b-r54Wn5p6B6YCf5Y-v55So"></span>
## Using instant access snapshots

Instance access is an attribute of a snapshot. After creating a snapshot with instance access **Enabled**, you can use it to create a new volume directly from the snapshots list. You can also select this snapshot while creating a volume on the **Volumes** page, even if its status is **Creating**. Follow these steps to create a volume from a snapshot on the **Snapshots** page:

On the **Snapshots** page, click **Create new volume** in the **Actions** column of the desired snapshot. Then, configure the parameters to create a new volume from the snapshot.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the snapshot status is <strong>Creating</strong> and instance access is <strong>Not enabled</strong>, you can only modify the snapshot's attributes, extend its retention period, or view the snapshot chain. You cannot use the snapshot to create a new volume.</div>


&nbsp;

&nbsp;

<span id="FAQ"></span>
## FAQ

**How can I tell if a snapshot has instant access enabled?** 

Check the **InstantAccess** column on the Snapshots page to see if the feature is enabled for a particular snapshot.

&nbsp;
