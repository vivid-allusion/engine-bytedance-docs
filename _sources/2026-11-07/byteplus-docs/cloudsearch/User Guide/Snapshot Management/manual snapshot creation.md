---
title: "manual snapshot creation"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/creating_a_snapshot_manually"
---

Cloud Search supports creating snapshots manually for the entire instance data or specific indexes. On the snapshot management page, you can manually create snapshots for all instances under the current account and region. This article explains how to create snapshots manually.

<span id="20c3c59e"></span>
## Precautions


* During snapshot and recovery processes, operations such as restarting or deleting the cluster, deleting snapshots being created or recovered, or creating or recovering snapshots again are not supported.

* It is recommended not to enable manual and automatic snapshots simultaneously, as data backup consumes node disk read/write bandwidth and may affect instance performance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Check the usage of the node disk read/write bandwidth first. If the disk read/write bandwidth is nearly saturated, it is recommended to stop the snapshot to avoid affecting read/write performance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">How to view node disk read/write bandwidth, see <a href="https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring">View monitoring data</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">How to stop snapshots, see <a href="https://docs.byteplus.com/docs/cloudsearch/stopping_snapshot_production">Stop snapshot creation</a>. Stop snapshots in progress via Kibana or Dashboards. The backend stops snapshot creation directly, and the frontend page status changes from <strong>Generating</strong> to <strong>Failed</strong>.   </div>
   


<span id="3f1a53ab"></span>
## Procedure


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Snapshot management** in the left navigation bar, then click **Create snapshot** at the top of the page.

4. In the **Create snapshot** panel, configure the following parameters, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance name |Select the target instance for manual snapshot creation from the dropdown list. |
   |Snapshot name |Set a custom snapshot name.<br><br><br>* Must start with a letter.<br><br>* Can only contain lowercase letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length must be between 2 and 32 characters. |
   |Snapshot object |Select the data objects to back up for manual snapshots.<br><br><br>* Instance: Back up the full data of the current instance.<br><br>* Index: Back up some indexes of the current instance.<br><br>* User\-defined: query specified indexes through the Index Name Matching Pattern and back them up. |
   |Storage location |Select the location to store snapshots.<br><br><br>* Default bucket: the default storage bucket of Cloud Search.<br><br>* User\-defined bucket: select the bucket you want to use. |
   |Select bucket |Select the bucket for storing snapshots from the dropdown list. This parameter is only visible when **Storage location** is set to **User\-defined bucket**. |
   |Remarks |Customize remarks for manual snapshots. Maximum length is 1000 characters. |
   |Snapshot creation speed (optional) |Customize the snapshot creation speed. Default value: 40. Unit: MiB/s.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Snapshot creation consumes disk read bandwidth; setting the speed too high may affect business read and write operations. Configure this parameter carefully.</div><br> |
   

5. In the pop\-up dialog, specify the estimated snapshot duration and click **OK**.


<span id="IcgEoz8n"></span>
## Subsequent operations

After manually creating a snapshot, you can check its progress.

Return to the **Snapshot management** page, and check the progress and status of the manually created snapshot in the **Snapshot Status** column.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When the snapshot status is <strong>Generating</strong>, you can select <strong>... \> Cancel</strong> in the snapshot's actions column to cancel snapshot creation.</div>


* <div data-tips="true" data-tips-type="default">The status changes from <strong>Generating</strong> to <strong>Generated</strong>, indicating the snapshot is complete and cannot be canceled.</div>
