---
title: "Recover data using snapshot"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/snapshots-restore-data"
---

After creating a snapshot, you can use the snapshot recovery feature to restore snapshot data to a specified instance. This topic describes how to recover data using a snapshot.

<span id="bdlEZ1W4"></span>
## Prerequisites


* Automatic or manual snapshot creation has been completed. For related documentation, see [Automatic snapshot creation](https://docs.byteplus.com/docs/cloudsearch/automatic-snapshots) or [Setting up manual snapshots](https://docs.byteplus.com/docs/cloudsearch/manual-snapshots).

* If you need to restore to another instance, first create the instance and obtain its ID. Ensure that the instance and the snapshot belong to the same version. For information about how to create an instance, see [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2).


<span id="a3f5db2d"></span>
## Recover data

You can restore snapshot data to the original instance or to another instance based on your business needs.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. Select **Instance management \> Snapshot management** in the left navigation bar.

5. In the snapshot list, click **Recover snapshot** behind the target snapshot file.

6. In the **Recover snapshot** dialog box, select the target instance, indexes to recover, recovery index type, enter the index rename rule, then click **OK**.

   
   |**Configuration** |**Description** |
   |---|---|
   |Select the instance to restore |You can restore snapshot data to the original instance or to other instances, depending on your business needs.<br><br>The default display shows the source instance of the snapshot, that is, the original instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If restoring to another instance, ensure the target instance and the snapshot’s original instance use the same version.</div><br> |
   |Restore index type |Choose the restore index type according to your business scenario:<br><br><br>* normal index: restores the index in the snapshot to a normal index, allowing regular read and write operations.<br><br>* searchable snapshot: restores the index in the snapshot to a searchable snapshot, which is a read\-only index.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">only target instances with cold data nodes enabled support restoring to searchable snapshot—read\-only index. for instructions on enabling cold data nodes, see <a href="https://docs.byteplus.com/docs/cloudsearch/upgrading">Upgrade instance</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Elasticsearch 6.7.1 and 6.8.23 instances do not support cold data nodes, so searchable snapshots are not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">snapshots created by previous Elasticsearch 7.10.2 instances cannot be restored as searchable snapshots in the Cloud Search console; however, OpenSearch instances support restoring as searchable snapshots as long as they have cold data nodes.</div><br> |
   |Recoverable Index |List of indexes available for recovery in the snapshot. Select the indexes to recover. |
   |**Index Rename**: When restoring data using snapshots, ensure the target instance has no indexes with the same name to avoid recovery failure.<br><br>You can rename the index to prevent recovery failure. ||
   |Index Name Matching Pattern |use regular expression filters on index names to rename indexes that match the filter conditions.<br><br>example value `index-test-(.+)` matches indexes with the prefix `index-test-`. |
   |Index name replacement mode |enter the renaming rule for the matched indexes.<br><br>example value `restore_index-test-$1` adds the prefix `restore_` before the index names to be restored. |
   

7. Click the snapshot name and view the data recovery progress under the **Recovery information** tab.

   When the status changes from **Recovering** to **Completed**, the target index recovery is finished. You can also check the target instance where recovery was made and the list of recovered indexes.


<span id="5afa1391"></span>
## Verify results

After restoring index data from the snapshot, you can check the cluster health status, index health status, index name, index size, and other details in the target instance where the data was restored.


1. Log in to the visualization tool console of the target instance.

   For detailed steps, see [log in to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool).

2. Click the menu button in the top left corner, then navigate to **Management \> Dev Tools**.

3. Run the command `GET /_cluster/health?pretty=true` to check the cluster health status.

   Status returned as **green** indicates cluster health, with all active primary shards and replica shards available in the cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2676cee2f0f64e9eba67441d7e69c0ed~tplv-goo7wpa0wc-image.image) </span>

4. Run the command `GET /_cat/indices?v` to view index details.

   You can check the index health status, index name, and index size from the returned information to determine if the indexes in the backup file have been restored and whether their names have been modified according to the index rename rules.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e297d8b8bb9f47818097b55804f7d20d~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Run the command `GET _cat/shards?v&s=index,shard` to check if the index is a searchable snapshot read\-only index.

   The results show that searchable snapshot read\-only indexes are all stored on cold data nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Searchable snapshot indexes restored in ES 7.10.2 version instances contain only primary shards.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ae11cc7a6d348828f6c8a4826a6354a~tplv-goo7wpa0wc-image.image) </span>
