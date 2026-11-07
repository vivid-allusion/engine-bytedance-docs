---
title: "Manually create searchable snapshots"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Manually_create_searchable_snapshots"
---

Cloud Search supports searchable snapshots by building read\-only searchable snapshot indices based on snapshots. This article explains the steps to manually create searchable snapshots.

<span id="16df863b"></span>
## Prerequisites


* Before using searchable snapshots, ensure that cold data nodes are enabled in the instance. Elasticsearch 6.7.1 and 6.8.23 instances do not support cold data nodes, so searchable snapshots are not available. Elasticsearch 7.10.2 and later versions, as well as OpenSearch 2.9.0 and later versions, support searchable snapshots.

* You can create a new instance and enable cold data nodes during creation. For detailed steps, see [Create instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2).

* If you already have an instance without enabled cold data nodes, you can enable them by upgrading the instance. For detailed steps, see [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading).


<span id="ef37b4ae"></span>
## Create searchable snapshots


1. Log in to the visualization tool to check index data distribution.

   1. Log in to the visualization tool. Log in to the visualization tool using the public access address. For details, see [Public network access Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool#3cbdb7b4).

   2. In the left navigation bar, select **Management \> Dev Tools**.

   3. Execute the `GET _cat/shards/&lt;index-name&gt;?v` command in the code area to query the index data distribution.

      Assuming the log index data has been created and written, you can use the wildcard `*` to represent multiple indexes. After executing the command, you can see from the returned results that the log index data is stored on the **data nodes**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60b20aa0da81437fa07e6c75028e9400~tplv-goo7wpa0wc-image.image) </span>

2. Create a snapshot repository.

   The following example shows how to create a snapshot repository named `doc-repo`. You can customize the repository name as needed.

   ```HTTP
   PUT _snapshot/doc-repo
   {
     "type" : "s3",
     "settings" : {
       "bucket" : "es-shadow-prod-cn-beijing-210094***",
       "path_style_access" : "false",
       "endpoint" : "tos-s3-cn-beijing.ivolces.com/",
       "protocol" : "https",
       "client" : "default",
       "base_path" : "_remote_index",
       "region" : "cn-beijing",
       "searchable" : true
     }
   }
   ```
   

   * `bucket`: use the system default bucket directly. The system default bucket is not visible on your TOS product page. You can view its name by hovering over the **bucket name** on the **Snapshot Management** page of Cloud Search service.

   * `endpoint`: the S3 Endpoint address of the TOS bucket. Use the private network address directly, matching the region of the Cloud Search service instance.

   * `base_path`: customize the snapshot storage path.

   * `region`: the region of the TOS bucket, which is the same as the region of the Cloud Search service instance.

   * `searchable`: when using the system\-built TOS bucket to create a snapshot repository, **this parameter must be set to true**. When using another TOS bucket, this parameter does not need to be configured.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7627598c54bf42bba188ba891ecf703d~tplv-goo7wpa0wc-image.image) </span>

3. Create a snapshot.

   The following example creates a snapshot named `doc-snapshot` in the specified repository `doc-repo`. In practice, you can customize the snapshot name.

   ```HTTP
   PUT _snapshot/doc-repo/doc-snapshot
   {
     "indices": "eventlogs-2024-07-*",
     "ignore_unavailable": true,
     "include_global_state": false
   }
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c8b14f3867848759a14f6ea00f1de85~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Description** |
   |---|---|
   |indices |List of indices to include in the snapshot.<br><br>Separate multiple indices with commas (,). Use a wildcard (\*) to replace part of the index name and match multiple indices. |
   |ignore_unavailable |Ignore missing indices in the `indices` list without causing snapshot failure.<br><br><br>* true: Ignore missing indices and continue the snapshot process.<br><br>* false: Default value, do not ignore, causing snapshot failure if an index is missing. |
   |include_global_state |Whether to include instance status in the snapshot.<br><br><br>* true: Default value, includes instance status.<br><br>* false: Does not include instance status. |
   

4. Query whether the snapshot was created successfully.

   You can only proceed to recover searchable snapshots after the snapshot is created successfully. When the query result returns `"state": "SUCCESS"`, it means the snapshot has been created successfully.

   In actual use, you need to replace the repository and snapshot names in the following commands.

   ```JSON
   GET _snapshot/doc-repo/doc-snapshot/_status
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7817d9f5f43a43e686833451620b9d8b~tplv-goo7wpa0wc-image.image) </span>

5. After the snapshot is created successfully, you can select indices from the snapshot to restore them as searchable snapshot indices.

   Note that the commands for restoring searchable snapshots differ between OpenSearch version 2.9.0 instances and ES version 7.10.2 instances.


<span id=".b3BlbnNlYXJjaC0yLTktMC3niYjmnKzlrp7kvos="></span>
### OpenSearch version 2.9.0 instance

```HTTP
   POST /_snapshot/doc-repo/doc-snapshot/_restore?pretty
   {
     "storage_type": "remote_snapshot",
     "indices": "eventlogs-2024-07-01,eventlogs-2024-07-02",
     "rename_pattern": "(.+)",
     "rename_replacement": "remote_$1",
     "include_global_state": false
   }
```



* `storage_type`: must be set to `remote_snapshot`, indicating that searchable snapshot indices can read data from a remote repository during retrieval.

* `indices`: select indices from the snapshot and restore them as searchable snapshot indices. Separate multiple indices with English commas `,`; use the wildcard `*` to represent multiple indices.

* `rename_pattern`: regular expression filter for index names to rename indices that match the filter.

* `rename_replacement`: rename rule applied to the matched indices. The example value `remote_$1` means adding the prefix `remote_` before the index name to be restored.

* `include_global_state`: whether to include the instance state; `false` means not included.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbf21278ac344ef18610d31dbd182c27~tplv-goo7wpa0wc-image.image) </span>

<span id=".ZXMtNy0xMC0yLeeJiOacrOWunuS-iw=="></span>
### ES 7.10.2 instance

```JSON
   POST _remoteindex/doc-repo/doc-snapshot-es/_restore
   {
   "indices": "eventlogs-2024-07-01,eventlogs-2024-07-02",
   "rename_pattern": "(.+)",
   "rename_replacement": "remote_$1",
   "include_global_state": false
   }
```



* indices: select indices from the snapshot to restore as searchable snapshot indices. Separate multiple indices with English commas `,`; use wildcards `*` to represent multiple indices.

* rename_pattern: regex filter for index names to rename matching indices.

* rename_replacement: renaming rule for matched indices. Example value `remote_$1` means adding the prefix `remote_` before the index name to be restored.

* include_global_state: whether to include the instance state; `false` means not included.

6. Review the data distribution of the logs index again.

   ```HTTP
   GET _cat/shards?v&s=index,shard
   ```
   

   The results show that all searchable snapshot indices are stored on cold data nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Searchable snapshot indexes restored in ES version 7.10.2 only have active shards.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc1c51bf19c04ee48c44da868ef769fa~tplv-goo7wpa0wc-image.image) </span>

7. Retrieve searchable snapshot indexes.

   ```HTTP
   GET /<index-name>/_search
   ```
   

   Replace with the correct index name when retrieving searchable snapshot indexes. This article allows querying `remote_eventlogs-2024-07-01` or `remote_eventlogs-2024-07-*`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53fb07bcc81845f58b10ded0ef2df4d8~tplv-goo7wpa0wc-image.image) </span>
