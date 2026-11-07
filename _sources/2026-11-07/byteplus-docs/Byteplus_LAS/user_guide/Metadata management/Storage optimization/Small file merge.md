---
title: "Small file merge"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Small_file_merge"
---

The AI Data Lake Service (LAS) provides multiple storage optimization features, helping users improve query performance and optimize storage resources through capabilities such as small file merge. The following is a detailed description and operation guide for the small file merge feature within storage optimization.

<span id="2c67cdef"></span>
# What is small file merge

In data lake management, small file merge is an important method for optimizing query efficiency and performance. Frequent incremental writes or small batch writes may generate a large number of small data file blocks. Continuous small file merge can improve storage utilization, achieve better query performance, and enable efficient data management.

LAS offers a storage optimization feature for small file merge. After enabling the feature, you can configure optimization tasks for small file merge. Once configuration is complete, small file merge optimization will be performed.

<span id="e8200785"></span>
# Limitations

Currently, only Lance and Iceberg table types support the storage optimization—small file merge feature.

<span id="627bdb94"></span>
# Configure small file merge

<span id="e33a41b8"></span>
## Enable and configure


1. Log in to the LAS Console, select the region at the top left as needed, and in the left navigation bar, choose Lake management \> Metadata, select the corresponding **Database \> Data Table**, and enter the data table list page.

2. Select the target table, navigate to the **Table Details \>**  Storage optimizationpage, and enable the Merge small filesfeature.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a009297a6504c7faa3406907360a03f~tplv-goo7wpa0wc-image.image) </span>

3. Configure the parameters for small file merge.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e3fbb8e2ba34c6d8e5a514dfd1f53ec~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration description |
   |---|---|
   |Resource allocation |Set the number of resource CUs allocated to the current small file merge task.<br><br>Currently, public queue resources are supported for executing storage optimization tasks. After resource allocation is set, the corresponding quota of public queue resources will be occupied when executing storage optimization tasks. |
   |Target file size |Set the size of small files to be merged. |
   |Scheduling |Select whether to enable periodic scheduling.<br><br><br>* Disable periodic scheduling: After the task configuration is completed, you will need to manually trigger task execution later.<br><br>* Enable periodic scheduling: You also need to configure the scheduling policy for periodic scheduling. After the task configuration is completed, the task will be automatically executed according to the configured scheduling cycle. |
   |Stop Pre Task |Set whether to forcibly terminate preceding optimization tasks. After enabling this option, the preceding optimization task will be forcibly terminated each time the scheduled task is executed. |
   |Custom configuration |Configure custom parameters involved in the operation of the small file merging task as needed. For details, see the following [参考：自定义参数说明](https://docs.byteplus.com/docs/Byteplus_LAS/91357#c2c52ba9). |
   


<span id="c2c52ba9"></span>
## Reference: Custom parameter description

<span id="ef930421"></span>
### Iceberg

During storage optimization configuration, the supported Iceberg custom parameters include the [options parameter](https://iceberg.apache.org/docs/nightly/spark-procedures/#options) from the official Iceberg documentation, as well as the strategy and sort_order parameters.

<span id="0facf87b"></span>
### Lance

During storage optimization configuration, the supported Lance custom parameters are as follows.


|Custom parameters |Parameter description |
|---|---|
|target_rows_per_fragment |Target number of rows per fragment after merging |
|max_rows_per_group |Maximum number of rows per row group during writing |
|materialize_deletions |Materialize logical deletions |
|materialize_deletions_threshold |When the deletion ratio of an input file exceeds this threshold, actual deletion is performed |
|batch_size |Micro\-batch size (number of rows) during merge rewrite |
|defer_index_remap |Used for "deferred index remapping/maintenance". When optimization or merging generates new data files, row groups, or changes the mapping of row IDs, index references are not updated immediately in the current operation. Instead, index maintenance is deferred to subsequent independent steps for unified processing. |


<span id="91577443"></span>
# Execute optimization tasks and view optimization results

After enabling and configuring the small file merge feature, you can manually trigger optimization tasks on the small file merge page, or view optimization records and results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c88152b5e7d9422299ad94967c9df876~tplv-goo7wpa0wc-image.image) </span>
