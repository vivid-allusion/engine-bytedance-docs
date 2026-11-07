---
title: "Snapshot cleanup"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Snapshot_cleanup"
---

The AI Data Lake Service (LAS) provides multiple storage optimization features, helping users improve query performance and optimize storage resources through capabilities such as snapshot cleanup. The following is a detailed description and operation guide for the snapshot cleanup feature within storage optimization.

<span id="6622b93b"></span>
# Limitations

Currently, only tables of the Lance and Iceberg types support the storage optimization \- snapshot cleanup feature.

<span id="9c6894d1"></span>
# Configure snapshot cleanup

<span id="999ecd56"></span>
## Enable and configure


1. Log in to the LAS console, select the region in the upper left corner as needed, and in the left navigation bar, select Lake management \> Metadata, choose the corresponding **database \> data table**, and enter the data table list page.

2. Select the target table, go to **Table details \>**  Storage optimizationinterface, enable the Snapshot cleanup feature, and configure the parameters for snapshot cleanup.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7f09866d7ec41b384d48b7efd790e70~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration description |
   |---|---|
   |Resource allocation |Set the number of resource CUs allocated to the current snapshot cleanup task.<br><br>Currently, public queue resources are supported for executing storage optimization tasks. After setting resource allocation, the corresponding quota of public queue resources will be occupied when executing storage optimization tasks. |
   |Snapshot Retention Policy |Set the retention time range for snapshots. Snapshots that exceed the retention time will be cleaned up during the execution of optimization tasks. |
   |Scheduling |Select whether to enable the periodic scheduling switch.<br><br><br>* Disable periodic scheduling: After the task configuration is completed, you will need to manually trigger task execution.<br><br>* Enable periodic scheduling: You also need to configure the periodic scheduling strategy. After the task configuration is completed, tasks will be automatically executed according to the configured scheduling cycle. |
   |Stop Pre Task |Set whether to forcibly terminate preceding optimization tasks. After enabling the switch, forcibly terminate the previous optimization task each time a scheduled task is executed. |
   |Custom configuration |Configure custom parameters involved in the snapshot cleanup task as needed during its execution. For details, see [参考：自定义参数说明](https://docs.byteplus.com/docs/Byteplus_LAS/91354#898637d2) below. |
   


<span id="898637d2"></span>
## Reference: Custom parameter description

<span id="0062e21f"></span>
### Iceberg

The following Iceberg custom parameters are supported for configuration.


|Custom parameters |Parameter description |
|---|---|
|older_than |Specifies that snapshots earlier than this timestamp can be cleaned up. |
|retention_days |The number of days to retain snapshots. |
|max_concurrent_deletes |The maximum number of concurrent deletions allowed when deleting files. |
|stream_results |Whether to return the list of files to be deleted in a streaming manner to reduce memory usage. |
|snapshot_ids |Explicitly specify the list of snapshot IDs to be cleaned up. |


<span id="5de78493"></span>
### Lance

The following Lance custom parameters are supported for configuration.


|Custom parameters |Parameter description |
|---|---|
|error_if_tagged_old_versions |Whether to report an error and interrupt when tagged old versions exist within the cleanup scope, to avoid accidentally deleting versions marked for retention. |


<span id="8570d35f"></span>
# Execute optimization tasks and view optimization results

After enabling and configuring the snapshot cleanup feature, you can manually trigger the execution of optimization tasks on the snapshot cleanup page, and also view optimization records and results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/157bec85aad0496fbf5ff5dd5c9bfaa5~tplv-goo7wpa0wc-image.image) </span>
