---
title: "Viewing the snapshot bucket"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Viewing-snapshot-bucket"
---

When a snapshot is automatically or manually created, the system automatically generates a bucket to store the snapshot.

<span id="dd51b4ba"></span>
## Before you begin


* Enable automatic snapshots. Make sure that snapshots have been created based on the specified backup policy. For more information, refer to [Setting up automatic snapshots](https://docs.byteplus.com/en/docs/cloudsearch/automatic-snapshots).

* Enable manual snapshots. Make sure that snapshots have been created. For more information, refer to [Setting up manual snapshots](https://docs.byteplus.com/en/docs/cloudsearch/manual-snapshots).


<span id="8e546110"></span>
## Viewing the snapshot bucket


1. Log on to the visualization tool. For more information, refer to [Logging on to the visualization tool](https://docs.byteplus.com/sem06tfc/1kg96qzi).

2. In the left\-side navigation pane, choose **Management \> Dev Tools**.

3. View the buckets that store snapshots of the instance.

   On the **Dev Tools** page, use the ES API to view all the buckets that store snapshots of the instance.

   ```JSON
   GET _snapshot?pretty
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/063253339f5041eba0451e6bab3c44f9~tplv-goo7wpa0wc-image.image) </span>

   The following information is returned: including the snapshot bucket name, TOS bucket name, endpoint, and storage path.

   ```JSON
   {
     "s3_repo_o-**3s1" : {
       "type" : "s3",
       "settings" : {
         "bucket" : "doc-828",
         "path_style_access" : "false",
         "endpoint" : "tos-s3-xxx.ibytepluses.com",
         "protocol" : "https",
         "client" : "default",
         "base_path" : "snapshot-o-**3s1",
         "region" : "xxx"
       }
     },
     "s3_manual_repo_**h-snap" : {
       "type" : "s3",
       "settings" : {
         "bucket" : "doc-828",
         "path_style_access" : "false",
         "endpoint" : "tos-s3-xxx.ibytepluses.com",
         "protocol" : "https",
         "client" : "default",
         "base_path" : "manual-snapshot-o-**3s1-**h-snap",
         "region" : "xxx"
       }
     } 
   }
   ```
   


<span id="c3052992"></span>
## Viewing snapshot information in a bucket


1. Obtain the name of the bucket that you want to view.

2. View snapshot information in the bucket.

   ```JSON
   GET _snapshot/s3_repo_iuz4gx4vfvyc****/_all?pretty
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6304b5a1a09d49378cc13c1a61b06ca7~tplv-goo7wpa0wc-image.image) </span>

   The following information is returned: The following information is returned, including the snapshot name, snapshot status, cluster status, included indices, snapshot start time, and end time.

   ```JSON
   {
     "snapshots" : [
       {
         "snapshot" : "**h-snap",
         "uuid" : "***FrW30h7aA",
         "version_id" : 7100299,
         "version" : "7.10.2",
         "indices" : [
           ".kibana_1",
           ".opendistro_security"
         ],
         "data_streams" : [ ],
         "include_global_state" : true,
         "state" : "SUCCESS",
         "start_time" : "2023-08-29T09:59:27.183Z",
         "start_time_in_millis" : 1693303167183,
         "end_time" : "2023-08-29T09:59:27.583Z",
         "end_time_in_millis" : 1693303167583,
         "duration_in_millis" : 400,
         "failures" : [ ],
         "shards" : {
           "total" : 2,
           "failed" : 0,
           "successful" : 2
         }
       }
     ]
   }
   ```
