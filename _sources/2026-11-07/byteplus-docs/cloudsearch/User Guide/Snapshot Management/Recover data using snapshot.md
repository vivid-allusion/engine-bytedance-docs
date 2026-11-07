---
title: "Recover data using snapshot"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/recovering_data_using_a_snapshot"
---

After creating a snapshot, you can use the snapshot recovery feature to restore snapshot data to a specified instance. This article explains how to use snapshot recovery to restore data.

<span id="0724132f"></span>
## Prerequisites

Automatic or manual snapshots have been created, or snapshot data already exists in a user\-defined TOS bucket. For related documentation, see [automatic snapshot creation](https://docs.byteplus.com/docs/cloudsearch/creating_snapshots_automatically) and [manual snapshot creation](https://docs.byteplus.com/docs/cloudsearch/creating_a_snapshot_manually).

<span id="iNEuadRY"></span>
## Background

The Cloud Search snapshot recovery feature rolls back instance data to a specific point in time, commonly used for accidental data deletion, configuration failures, or system exceptions. Currently, two snapshot recovery methods are supported:


* Restore data using created snapshots: Snapshots created in the Cloud Search console are managed centrally by the system. The creation and recovery processes are simple, suitable for fast rollback and fault recovery in daily operations and maintenance scenarios. This method requires no additional external storage configuration, has a low operation threshold, and is suitable for most routine data protection needs.

* Restore data using snapshots in TOS: Snapshot recovery based on user\-owned TOS buckets allows long\-term storage of snapshot data in your own TOS. It offers higher flexibility and control, suitable for scenarios with strict data retention periods, cross\-environment recovery, or compliance requirements. This method is usually used for disaster recovery, cross\-instance migration, or data recovery after long\-term archiving.


Snapshots created automatically or manually can be restored to the original instance or to other instances. When restoring to another instance, confirm that the target instance and the snapshot’s instance are the same version.

<span id="RROihKhH"></span>
## Restore data using created snapshots


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. In the left navigation bar, select **Snapshot Management**. Filter snapshots by **Snapshot name**, **Instance name**, and **Instance ID**, then click **Restore Snapshot** behind the target snapshot.

4. In the **Snapshot Recovery** dialog, configure the following parameters, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Select instance to recover |Supports restoring snapshot data to the original instance or returning to other instances. Choose according to business needs.<br><br>The default display shows the source instance of the snapshot, that is, the original instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If restoring to other instances, ensure the target instance and the instance to which the snapshot belongs have the same version.</div><br> |
   |Restore index type |Select the type of index restoration based on your business scenario:<br><br><br>* Regular index: restore the index from the snapshot as a regular index with full read and write capabilities.<br><br>* Searchable snapshot: restore the index from the snapshot as a searchable snapshot, which is a read\-only index.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only target instances with cold data nodes enabled support restoration as searchable snapshot read\-only indexes. For how to enable cold data nodes, see <a href="https://docs.byteplus.com/docs/cloudsearch/upgrading">Upgrade instance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Elasticsearch versions 6.7.1 and 6.8.23 do not support cold data nodes, so searchable snapshots are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Snapshots previously created by Elasticsearch 7.10.2 instances cannot be restored as searchable snapshots in the Cloud Search console; however, OpenSearch instances support restoring as searchable snapshots as long as they have cold data nodes.</div><br> |
   |Recoverable index |The list of indexes available for restoration from the snapshot. Check the indexes you want to restore. |
   |Index Rename |When restoring data using snapshots, ensure the target instance does not have identically named indices to avoid restoration failure. You can rename indices to prevent restoration failure.<br><br><br>* Index name matching pattern: a regular expression filter for index names. Indices matching this filter will be renamed. Example value `index-test-(.+)` matches indices with the prefix `index-test-`.<br><br>* Index name replacement pattern: specify the renaming rule for matched indices. Example value `restore_index-test-$1` means adding the `restore_` prefix before the index name to be restored. |
   

5. Click the snapshot name to view the data recovery progress under the **Recovery Information** tab.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the restore state is <strong>Recovering</strong>, you can click <strong>Cancel</strong> in the <strong>actions</strong> column of the task to cancel the snapshot recovery.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Status changes from <strong>Recovering</strong> to <strong>Completed</strong>, indicating the snapshot recovery is complete and cannot be canceled.   </div>
   


<span id="f1302864"></span>
## Recover data using snapshot in TOS


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **Snapshot Management** in the left navigation, then click **Recover from TOS**.

4. In the **Recover from TOS** dialog, configure the following parameters, then click **Confirm Snapshot Information and Register**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Snapshot name |Customize the snapshot name. Naming rules are as follows:<br><br><br>* Must start with a letter.<br><br>* Can only contain lowercase letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length must be between 2 and 32 characters. |
   | Select bucket |Select the bucket where the snapshot is stored from the drop\-down list. |
   |Snapshot path |Select the snapshot path in the bucket from the dropdown list. |
   |Select restore instance |Select the target instance from the dropdown list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure the target instance and the snapshot's instance share the same main account and version; otherwise, restoring the snapshot will fail.</div><br> |
   |Select snapshot to restore |Select the target snapshot from the dropdown list. |
   |Restore index type |Choose the index restore type based on your business scenario:<br><br><br>* Normal index: restores the snapshot index as a normal index with full read\-write access.<br><br>* Searchable snapshot: restores the snapshot index as a searchable snapshot, which is read\-only.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only target instances with cold data nodes enabled support restoring to searchable snapshot read\-only indices. For instructions on enabling cold data nodes, see <a href="https://docs.byteplus.com/docs/cloudsearch/upgrading">Upgrade instance</a>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">ES version 6.7.1 instances do not support cold data nodes and therefore do not support searchable snapshots.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Snapshots created by existing ES 7.10.2 instances cannot be restored as searchable snapshots through a white\-screen recovery; however, OpenSearch instances support restoring to searchable snapshots as long as they have cold data nodes.</div><br> |
   |Recoverable indexes |A list of indexes available for recovery from the snapshot. Select the indexes to recover. |
   |Remarks |Enter remarks. Maximum length is 1000 characters. |
   

5. In the popup dialog, click **OK**.

6. Configure the following parameters in the snapshot recovery panel, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Select restore instance |Support restoring snapshot data to the source instance or to other instances; choose according to business needs.<br><br>The default display is the snapshot’s source instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To restore to another instance, ensure the target instance is the same version as the snapshot’s instance.</div><br> |
   |Restore index type |Select the restore index type based on your business scenario:<br><br><br>* Normal index: restore the index from the snapshot as a normal index that supports read and write operations.<br><br>* Searchable snapshot: restore the index from the snapshot as a searchable snapshot, which is read\-only.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only target instances with cold data nodes enabled support restoring as a searchable snapshot – a read\-only index. For instructions on enabling cold data nodes, see <a href="https://docs.byteplus.com/docs/cloudsearch/upgrading">Upgrade instance</a>.</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Elasticsearch versions 6.7.1 and 6.8.23 do not support cold data nodes and therefore do not support searchable snapshots.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Snapshots created by legacy Elasticsearch 7.10.2 instances cannot be restored as searchable snapshots in the console; OpenSearch instances support restoring as searchable snapshots as long as they have cold data nodes.</div><br> |
   |Recoverable Index |The index list available for recovery in the snapshot. Check the indexes you want to recover. |
   |Index rename |When recovering data using a snapshot, ensure no indexes with the same name exist in the target instance to avoid recovery failure. You can rename indexes to prevent recovery failure.<br><br><br>* Index name matching pattern: a regular expression filter for index names; indexes matching the filter are renamed. Example value `index-test-(.+)` matches indexes with the prefix `index-test-`.<br><br>* Index name replacement pattern: specify renaming rules for matched indexes. Example value `restore_index-test-$1` adds the prefix `restore_` before the index name to be restored. |
   |Maximum recovery speed (optional) |Customize the snapshot recovery speed. Default value: 40. Unit: MiB/s.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The snapshot recovery speed is determined by the snapshot recovery speed and the index recovery speed <code>IndicesRecoveryMaxBytesPerSec</code> (whichever is lower), and it consumes disk write bandwidth. Excessive speed may affect business read and write operations; configure this parameter cautiously.</div><br> |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the restore state is <strong>Recovering</strong>, you can click <strong>cancel</strong> in the task's <strong>actions</strong> column to cancel the snapshot recovery.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The status changes from <strong>Recovering</strong> to <strong>Completed</strong>, indicating the snapshot recovery is finished and cannot be canceled.   </div>
   


<span id="3164431b"></span>
## Verify results

After recovering index data through snapshot recovery, you can check cluster health status, index health status, index name, and index size in the target instance where the recovery was performed.


1. Log in to the visualization tool console of the target instance.

   For detailed operation, see [Log in to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool).

2. Click the menu button in the top left corner, then navigate to **Management \> Dev Tools**.

3. Run the `GET /_cluster/health?pretty=true` command to check the cluster health status.

   Status returned as **green** indicates cluster health, with all active primary shards and replica shards available in the cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2676cee2f0f64e9eba67441d7e69c0ed~tplv-goo7wpa0wc-image.image) </span>

4. Run the `GET /_cat/indices?v` command to view index details.

   You can check the index health status, index name, index size, and other information from the returned data to determine whether the index in the backup file has been restored and whether the index name has been modified according to the renaming rules.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e297d8b8bb9f47818097b55804f7d20d~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Run the `GET _cat/shards?v&s=index,shard` command to check whether the index is a Snapshots can be searched read\-only index.

   The returned results show that Snapshots can be searched read\-only indexes are fully stored on Cold data nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The Snapshots can be searched indexes restored from Elasticsearch version 7.10.2 instances contain only primary shards.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae11cc7a6d348828f6c8a4826a6354a~tplv-goo7wpa0wc-image.image) </span>
