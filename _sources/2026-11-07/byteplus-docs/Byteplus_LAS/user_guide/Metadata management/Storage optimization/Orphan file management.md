---
title: "Orphan file management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Orphan_file_management"
---

AI Data Lake Service (LAS) offers multiple storage optimization features, helping users improve query performance and optimize storage resources through capabilities such as orphan file management. The following provides a detailed description and operation guide for the orphan file management feature within storage optimization.

<span id="f653945f"></span>
# Limitations

Currently, only Iceberg\-type tables can use the storage optimization \- orphan file management feature.

<span id="005c454a"></span>
# Configure orphan file management

<span id="a49d7b9e"></span>
## Enable and configure


1. Log in to the LAS console. In the upper left corner, select the region as needed. In the left navigation bar, select Lake managementMetadata, then choose the corresponding **database and data table** to enter the data table list page.

2. Select the target table, go to the **Table details** Storage optimizationpage, enable the Orphan file governancefeature, and configure the parameters for orphan file management.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44c6f892defa4460a5675816cbdffd4b~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration description |
   |---|---|
   |Resource allocation |Set the number of resource CUs allocated for the current orphan file management task.<br><br>Currently, public queue resources are supported for executing storage optimization tasks. After setting resource allocation, the corresponding quota of public queue resources will be occupied when executing storage optimization tasks. |
   |Scheduling |Select whether to enable the periodic scheduling switch.<br><br><br>* Disable periodic scheduling: After task configuration is completed, you will need to manually trigger task execution subsequently.<br><br>* Enable periodic scheduling: You also need to configure the scheduling strategy for periodic scheduling, including the interval granularity and interval period. After task configuration is completed, tasks will be automatically executed according to the configured scheduling cycle. |
   |Stop Pre Task |Set whether to forcibly terminate the previous optimization task. After enabling the switch, the previous optimization task will be forcibly terminated each time a scheduled task is executed. |
   |Custom configuration |Configure custom parameters involved in the operation of the orphan file management task as needed. For details, see [参考：自定义参数说明](https://docs.byteplus.com/docs/Byteplus_LAS/91352#ff8287fe) below. |
   


<span id="ff8287fe"></span>
## Reference: Custom parameter description

<span id="3072e65c"></span>
### Iceberg

The following Iceberg custom parameters are supported for configuration.


|Custom parameters |Parameter description |
|---|---|
|older_than |Only delete orphan files that are older than the specified timestamp (to prevent accidental deletion of temporary files that are being written) |
|location |Specify the table path to scan (typically used for partitioned tables or custom locations) |
|dry_run |Preview mode; only lists files to be deleted without actually deleting them |
|max_concurrent_deletes |Controls the maximum number of threads for concurrent file deletion |
|file_list_view |(Reserved field; in some implementations, used to provide the view name for the list of files to be deleted; usually can be ignored) |
|equal_schemes |Whether to require the URI scheme to be consistent when comparing file paths (for example, hdfs:// and s3a:// are considered different) |
|equal_authorities |Whether to require the URI authority to be consistent when comparing file paths (for example, namenode1:9000 and namenode2:9000 are considered different) |
|prefix_mismatch_mode |Handling strategy when a file path prefix does not match the table location; optional values include FAIL (error), DELETE (still delete), SKIP (skip) |
|prefix_listing |Whether to enable prefix\-based object storage listing optimization (applicable to S3, OSS, and more) to improve scanning efficiency |


<span id="45553fa8"></span>
# Execute optimization tasks and view optimization results

After enabling and configuring the orphan file management feature, you can manually trigger optimization tasks on the orphan file management page, and also view optimization records and results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc97a3c76c644c24b05e49a93b972351~tplv-goo7wpa0wc-image.image) </span>
