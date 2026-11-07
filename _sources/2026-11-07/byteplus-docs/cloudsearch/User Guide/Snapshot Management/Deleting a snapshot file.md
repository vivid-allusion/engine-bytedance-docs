---
title: "Deleting a snapshot file"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/deleting_a_snapshot_file"
---

The snapshot files created automatically are deleted automatically when they reach the snapshot retention period, so it is recommended that you do not delete them manually. The snapshot files created manually can be deleted manually when they are no longer needed.

Deleting a snapshot file is an irreversible operation and cannot be recovered after deletion, so be careful.

<span id="cbc4c19f"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.volcengine.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the left navigation bar, select **Snapshot management**, filter the snapshot by snapshot name, instance name or instance ID, and then click **Delete** behind the target snapshot.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Delete</strong> behind the target snapshot in the <strong>Instance management \> Snapshot management</strong> page of an instance details page.   </div>
   

4. In the pop\-up dialog box, confirm the target snapshot file to be deleted, and then click **OK**.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the snapshot file has been used to recover searchable snapshots, deleting the snapshot file also affects the indexes recovered through searchable snapshots, so do not delete the snapshot file if these indexes are still needed for use.</div>
