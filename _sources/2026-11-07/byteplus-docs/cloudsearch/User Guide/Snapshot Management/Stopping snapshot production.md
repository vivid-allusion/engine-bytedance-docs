---
title: "Stopping snapshot production"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/stopping_snapshot_production"
---

It is not recommended for instances to enable both manual snapshots and automatic snapshots at the same time, which will affect the performance of the instance because performing data backups will consume the read and write bandwidth of the node's disks.

This topic describes how to stop snapshot production.

<span id="2429dd4a"></span>
## Function description

Stopping snapshot production on Kibana/Dashboards is not recognized by the front console. After stopping snapshot production, the backend stops making the snapshot directly, and the front console will change its status from **Generating** to **Failed**.

<span id="1f8e58b0"></span>
## Procedure


1. Log on to the visualization tool console. For details, refer to [Logging on to the visualization tool](https://docs.byteplus.com/docs/cloudsearch/logging-tool).

2. On the left navigation bar, click **Management \> Dev Tools**.

3. View the snapshot repository for the instance.

   ```Shell
   GET _snapshot?pretty
   ```
   

   Returns information similar to the following. You can obtain the name of the snapshot repository, TOS bucket name, endpoint, storage path, etc. from the returned information.

   * Manual snapshot creation: Repository name format is `s3_manual_repo_manual_snapshot_name`.

   * Automatic snapshot creation: Repository name format is `s3_repo_instance_id`.

   ```JSON
   {
     "s3_manual_repo_doctest" : {
       "type" : "s3",
       "settings" : {
         "bucket" : "es-shadow-qa-cn-beijing-210094**",
         "path_style_access" : "false",
         "endpoint" : "tos-s3-cn-beijing.ivolces.com",
         "protocol" : "https",
         "client" : "default",
         "base_path" : "manual-snapshot-o-test-00g04n2**-doctest",
         "region" : "cn-beijing",
         "searchable" : "true"
       }
     },
     "s3_repo_o-test-00g04n2**" : {
       "type" : "s3",
       "settings" : {
         "bucket" : "es-shadow-qa-cn-beijing-210094**",
         "path_style_access" : "false",
         "endpoint" : "tos-s3-cn-beijing.ivolces.com",
         "protocol" : "https",
         "client" : "default",
         "base_path" : "snapshot-o-test-00g04n2**",
         "region" : "cn-beijing",
         "searchable" : "true"
       }
     }
   }
   ```
   

4. View the snapshot information in the target repository.

   ```HTTP
   GET _snapshot/{repository_name}/_all?pretty
   ```
   

   Returns information similar to the following. You can obtain the snapshot name, snapshot status, cluster status, indexes contained in the snapshot, snapshot start time, snapshot end time, etc. from the returned information.

   * The name format for automatic snapshot creation is `escloud-autosnap-creation_time`.

   * The `state` field indicates the creation status of the snapshot, `IN_PROGRESS` indicates that the snapshot is in progress, and `SUCCESS` indicates that the snapshot is complete.

   ```JSON
   {
     "snapshots" : [
       {
         "snapshot" : "escloud-autosnap-2024-11-04_17:34:40",
         "uuid" : "dXKPzZqFQ1-KbBa6dU**",
         "version_id" : 7100299,
         "version" : "7.10.2",
         "indices" : [
           ".opendistro_security",
           "restore_restore_ind1_restore_ind_restore_test_1",
           ".kibana_1"
         ],
         "data_streams" : [ ],
         "include_global_state" : true,
         "state" : "IN_PROGRESS",
         "start_time" : "2024-11-04T09:35:20.630Z",
         "start_time_in_millis" : 1730712920630,
         "end_time" : "1970-01-01T00:00:00.000Z",
         "end_time_in_millis" : 0,
         "duration_in_millis" : 0,
         "failures" : [ ],
         "shards" : {
           "total" : 0,
           "failed" : 0,
           "successful" : 0
         }
       }
     ]
   }
   ```
   

5. Stop the snapshot in production (`"state": "IN_PROGRESS"`).

   ```HTTP
   DELETE _snapshot/{repository_name}/{snapshot_name}
   ```
   

   Returns the following information.

   ```HTTP
   {
     "acknowledged" : true
   }
   ```
