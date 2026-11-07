---
title: "Use TOS for cross-region data migration"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Use-TOS-for-cross-region-data-migration"
---

Cloud Search ES instances support data backup and recovery. Combined with TOS's cross\-region replication feature, you can achieve cross\-region offline data migration in the BytePlus Cloud Search service. This topic introduces the process of using ES backup and recovery to implement cross\-region data migration.

<span id="EDufo7im"></span>
## Solution overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99299ecaefeb4c039355d2ce52b1c96e~tplv-goo7wpa0wc-image.image) </span>

The source ES instance in South China needs to migrate data to the target ES instance in North China.


1. The source ES instance performs data backup and stores the generated snapshot files in the TOS bucket in South China.

2. The TOS bucket in South China copies the snapshot files to the TOS bucket in North China through cross\-region replication.

3. The target ES instance recovers the target index data by reading the snapshot files from TOS storage through backup restore.


<span id="ZDNqkLrY"></span>
## Preparations


1. Create the source ES instance and TOS bucket, both must be in the same region (for example, South China). For related documentation, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) and [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

2. Create the target ES instance and TOS bucket; both must be in the same region (such as North China). For related documentation, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) and [Create a bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="BzEqnwif"></span>
## Step 1: Back up data from the source ES instance

The source ES instance generates a snapshot by backing up data and stores the snapshot file in a TOS bucket within the same region.


1. Log on to the [Cloud Search console](https://console.byteplus.com/es) and switch regions in the top navigation bar.

2. On the **Instances** page, click the target instance name to enter the Instance details page.

3. Create a snapshot.

   The ES instance supports both automatic and manual snapshot creation. Choose the suitable method to create a snapshot. For detailed steps, see [Snapshot management](https://docs.byteplus.com/en/docs/cloudsearch/Backup).


<span id="OpWdRuZo"></span>
## Step 2 (optional): Transfer snapshot to TOS via DMS service


1. Confirm whether the bucket type in the snapshot details is the system default bucket.

   1. If it is a system default bucket, transfer the snapshot to TOS under the current account.

   2. If it is a bucket under the current account, skip step two and proceed to the next step.


<span id="dvYufP8o"></span>
## Step 3: Execute cross\-region replication for the source TOS bucket

The source TOS bucket uses cross\-region replication to copy snapshot files to the TOS bucket in the target region.


1. Log on to the [TOS console](https://console.byteplus.com/tos).

2. Select **Buckets** in the left navigation bar, then filter and click the target bucket name of the source region on the **Buckets** page.

3. Select **Fault tolerance and disaster recovery \> CRR** in the left navigation bar, then click **Create rule**.

4. In the **Create CRR rule** dialog box, select the target TOS bucket, configure the cross\-region replication rule, and click **OK**.

   This section briefly introduces the parameter configuration of the TOS cross\-region replication rule. For detailed information, refer to [Cross-region replication](https://docs.byteplus.com/en/docs/tos/Cross-regional-replication-within-the-same-account).

   
   |**Configuration** |**Description** |
   |---|---|
   |Source bucket location |Region of the source bucket. |
   |Source bucket |Source bucket name. |
   |Location of the destination storage bucket |Select the region where the target storage bucket for file copying is located. |
   |Destination bucket |Select the destination bucket for copying files. |
   |Destination storage type |Select the storage type of files after cross\-region replication. This example uses **Inherit target bucket**. |
   |sync range |Select the source data scope for cross\-region replication; this article uses **the entire bucket** as an example.<br><br><br>* **The entire bucket**: copy all files in the bucket to the destination bucket.<br><br>* **Specify prefix**: set a file prefix to copy files matching the prefix to the destination bucket. |
   |Synchronize historical objects |Choose whether to sync historical files to the target storage bucket. This topic uses **sync** of historical data as an example.<br><br><br>* **Sync**: synchronize historical files to the bucket.<br><br>* **No sync**: do not synchronize historical files; only sync newly added or updated files after the rule creation. |
   

5. Check synchronization progress.

   Once the cross\-region replication rule is created, the rule activates automatically. Cross\-region replication uses an asynchronous replication mechanism. Depending on your file size, the process takes from several minutes to several hours. When the **Synchronization 100%**  prompt appears, the synchronization is complete.

   After synchronization completes, you can visit the target TOS bucket to verify whether the files have been synchronized.


<span id="onnCHGwp"></span>
## Step 4: Restore data on the target ES

The target ES instance restores data by reading from TOS storage via backup and recovers the target index data.


1. Log on to the Kibana console of the target ES instance.

   1. Log on to the [Cloud Search console](https://console.byteplus.com/es) and switch regions in the top navigation bar.

   2. On the **Instances** page, select the target instance name, then click **Kibana** behind the instance to access the Kibana console via the public address.

      To access the Kibana console via the public network, enable public network access in advance. See [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool).

   3. Enter the username and password on the Kibana login page, then click **Log in** to sign in to Kibana.

      The username is "admin," and the password is the one you set when creating the instance. If you forget your login password, you can reset it on the **Instance details** page. For related documentation, see [Reset password](https://docs.byteplus.com/en/docs/cloudsearch/resetting-password).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/826ab6d2df5f4888a0e6b5a2db4f04e0~tplv-goo7wpa0wc-image.image) </span>

   4. Select **Management \> Dev Tools** in the Kibana menu bar.

2. Create a snapshot repository based on the target TOS bucket.

   Run the following command on the **Dev Tools** page to create the snapshot repository.

   ```HTTP
   PUT _snapshot/<repository-name>/
   {
       "type": "s3",
       "settings": {
         "bucket" : "tosbucket-name", 
         "path_style_access" : "false",
         "endpoint" : "tos-s3-cn-beijing.ivolces.com",  
         "protocol" : "https",
         "client" : "default",
         "base_path" : "manual-snapshot-o-00****hn7-doc-shnapshot-source",  
         "region" : "cn-beijing",
         "access_key": "AK****NTQyYjY5YTY",  
         "secret_key": "Tm1Oa*****VE0TVdZeVkyWQ=="
       }
   }
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |`<repository-name>` |Set a custom name for the snapshot repository, such as doc_restore_1. |
   |type |Specify the repository type and set it to `s3`. |
   |bucket |The name of the target TOS bucket from which existing snapshot files can be read. |
   |path_style_access |Whether to use path\-style access for the repository; usually, keep the default false. |
   |endpoint |Access address of the target TOS bucket. |
   |protocol |Communication protocol, default is HTTPS. |
   |client |Specify the client used for communication with the repository, usually keep the default. |
   |base_path |Path of the target TOS bucket storing snapshot files. |
   |region |Region of the target TOS bucket. |
   |access_key |Access Key of the account accessing the TOS bucket. |
   |secret_key |Account Secret Access Key for accessing the TOS Bucket. |
   

3. Recover target index data.

   Run the following command on the **Dev Tools** page to recover target index data.

   ```HTTP
   POST /_snapshot/<repository-name>/<snapshot-name>/_restore
   {
      "indices": "custom*"
   }
   ```
   

   * `<repository-name>`: the snapshot repository, the name of the repository you created.

   * `<snapshot-name>`: the snapshot name created in the source ES, which you can also obtain from the TOS storage path.

   * `indices`: the target index to recover. Separate multiple indices with commas (,); use a hyphen (\-) to indicate deleted indices; use a wildcard (\*) to match indices that fit the expression.

      The returned information below indicates recovery success.

   ```HTTP
   {
       "accepted" : true
   }
   ```
   


<span id="uytriEfj"></span>
## Verify results

After cross\-region recovery, you can check cluster health status, index health status, index names, storage size, and other details on the target instance.


1. Run `GET /_cluster/health?pretty=true` in **Dev Tools** to check cluster health status.

   Status returned as **green** indicates cluster health, with all active primary shards and replica shards available in the cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2676cee2f0f64e9eba67441d7e69c0ed~tplv-goo7wpa0wc-image.image) </span>

2. Run the `GET /_cat/indices?v` command in **Dev Tools** to view index details.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acda4e2caaf64c5abd633a305605d8b8~tplv-goo7wpa0wc-image.image) </span>

   You can check the index health status, index name, storage size, and other information from the returned data.

   As shown above: it recovered an index named `customer` with health status `green`, where the primary and replica shards occupy a total cluster storage space of 22.7KB.
