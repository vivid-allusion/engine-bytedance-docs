---
title: "manual snapshot creation"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/manual-snapshots"
---

Cloud Search supports manually creating snapshots for the entire instance data or selected indexes. This article explains how to manually create a snapshot.

<span id="d9e2e9cd"></span>
## Precautions


* During snapshot and recovery processes, operations such as restarting or deleting the cluster, deleting snapshots being created or recovered, or creating or recovering snapshots again are not supported.

* It is recommended not to enable manual and automatic snapshots simultaneously, as data backup consumes node disk read/write bandwidth and may affect instance performance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Check the usage of the node disk read/write bandwidth first. If the disk read/write bandwidth is nearly saturated, it is recommended to stop the snapshot to avoid affecting read/write performance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">How to view node disk read/write bandwidth, refer to <a href="https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring">View monitoring data</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">How to stop snapshots, refer to <a href="https://docs.byteplus.com/docs/cloudsearch/Viewing-snapshot-bucket">Stop snapshot creation</a>. Stop snapshots in progress through Kibana or Dashboards. The backend will directly stop snapshot creation, and the frontend page status will change from <strong>Generating</strong> to <strong>Failed</strong>.   </div>
   


<span id="73216e66"></span>
## Procedure


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. Select **Instance management \> Snapshot management** in the left navigation bar, then click **Create snapshot** at the top of the page.

5. In the **Create snapshot** panel, set the snapshot name, snapshot target, and remarks, then click **OK**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Snapshot name |Customize the snapshot name.<br><br><br>* Must start with a letter.<br><br>* Can only contain lowercase letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length must be between 2 and 32 characters. |
   |Snapshot object |Select the data objects to back up for manual snapshots.<br><br><br>* Instance: Back up the full data of the current instance.<br><br>* Index: Back up some indexes of the current instance.<br><br>* User\-defined: Query and back up specified indexes via the index name matching pattern.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the instance enables cold data nodes, a note will indicate that backup filters searchable read\-only snapshots.</div><br> |
   |Storage location |Select the snapshot storage location.<br><br><br>* Default bucket: the default storage bucket of Cloud Search.<br><br>* User\-defined bucket: choose the bucket you want to use. |
   |Select bucket |Select the bucket for storing the snapshot from the dropdown list. This parameter is visible only when **Storage location** is set to **User\-defined bucket**. |
   |Remarks |Customize the remarks for the manual snapshot. The maximum length is 1000 characters. |
   |Snapshot creation speed (optional) |Customize the snapshot creation speed. Default value: 40. Unit: MiB/s.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Snapshot creation consumes disk read bandwidth. Excessive speed may affect business read/write performance. Configure this parameter carefully.</div><br> |
   

6. In the pop\-up dialog, specify the expected duration of the snapshot, then click **OK**.

7. View manual snapshot progress.

   Check progress on the snapshot list page. The status changes from **Generating** to **Generated**, indicating the snapshot creation is complete.
