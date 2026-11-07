---
title: "FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/starrocks_faqs"
---

<span id="_1-使用建议"></span>
## Usage recommendations

The [Optimize performance](https://docs.starrocks.io/zh-cn/latest/administration/Profiling) section on the StarRocks official website provides several ways to optimize performance. The following sections introduce several methods for optimizing StarRocks performance.

<span id="_1-1-如何分桶"></span>
### How to bucket data

The number of buckets affects import and query performance. Recommendations:


* Use high\-cardinality columns for bucketing to avoid data skew.

* After data compression, it is recommended that the bucket size be between 100 MB and 1 GB. Therefore, you can configure the bucket size based on the size of the table:

   * For small data volumes, use a single bucket of 128 MB.

   * For data larger than 4 GB, it is recommended to use one bucket for every 1–10 GB.

   * It is not recommended to exceed 32 buckets.

* When there are fewer machines, consider using `BE数量 * cpu core / 2` to set the number of buckets, so that machine resources can be fully utilized.

* It is not recommended to use random bucketing. When creating a table, specify the hash column for bucketing explicitly.


<span id="_1-2-如何选择数据模型"></span>
### **How to choose a data model**

The [Data model](https://docs.starrocks.io/zh-cn/latest/table_design/table_types/table_types) section on the StarRocks official website describes four modes in detail. You can choose the appropriate one based on your needs.

General recommendations are as follows:


|Data models |Use cases |
|---|---|
|Duplicate key model (DUPLICATE KEY) |* Data updates are infrequent, such as importing log data or time\-series data. The main characteristic is that old data is not updated, only new data is appended.<br><br>* Query methods are flexible and not limited to pre\-aggregated analysis.<br><br>* Retain the original data. |
|Aggregate model (AGGREGATE KEY) |* Suitable for analyzing statistical and summary data.<br><br>* No need to query the original data.<br><br>* Old data is updated infrequently; only new data is appended. |
|Update model (UNIQUE KEY) |* Suitable for scenarios with updates and real\-time analysis. For example: analyzing e\-commerce orders. |
|Primary key model (PRIMARY KEY) |* Suitable for scenarios with updates and real\-time analysis. For example: real\-time integration of transactional data into StarRocks, synchronizing insert, delete, and update data to the primary key model in real time. |


<span id="_1-3-建表注意事项"></span>
### Important notes for table creation


1. Regarding order by, it is not recommended to use it in StarRocks version 2.5 and earlier.


<span id="_1-4-删除表注意事项"></span>
### Important notes for table deletion

StarRocks provides a table deletion function. Refer to the following statement:

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name [FORCE]
```



* When deleting a table, if the `FORCE` keyword is not used, the table will be placed in the recycle bin (retained for 1 day by default). The data is not deleted at this time and can be restored using the [RECOVER](https://docs.starrocks.io/zh-cn/latest/sql-reference/sql-statements/data-definition/RECOVER) statement.

* When executing `DROP TABLE FORCE`, the system will not check whether there are unfinished transactions for the table. The table will be deleted directly and cannot be recovered.


<span id="_2-故障排除"></span>
## Troubleshooting

<span id="_2-1-数据导入过程中报-tablet-too-many-version"></span>
### Error 'tablet too many version' during data import


* **Issue description:** 

   The following error message occurs during data import:

   ```json
   {
     "label": "_1693125063307_fe1fc397da6644dd856c2b05211aec1b",
     "existingJobStatus": null,
     "txnId": 351688,
     "status": "Fail",
     "message": "Too many versions. tablet_id: 177006, version_count: 1002, limit: 1000, replica_state: 0: be:xx.xx.xx.xx",        
   }
   ```
   

* **Cause analysis:** 

   The above error occurs because the import frequency is too high, and the data cannot be merged (compacted) in time, resulting in the number of versions exceeding the maximum supported unmerged versions. The default maximum supported unmerged versions is 1000.

* **Handling steps**:

   Generally, increasing the amount of data per import and reducing the import frequency can resolve the issue. Check the import frequency according to the following steps:

   1. Log in to the ECS node of the BE instance in the StarRocks cluster and analyze the BE logs. The directory where the logs are located is: `/var/log/emr/starrocks/be`. For details on login methods, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

   2. Run the following command to check the frequency of data imports:

      ```json
      cd /var/log/emr/starrocks/be/sys
      cat be.INFO  |grep 'new income streaming load ' | grep '${表名}' |grep '${时间点}'
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For BE log configuration and archiving strategies, you need to locate the log file path corresponding to be.INFO based on the time the error occurred.      </div>
      

      2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The parameter ${表名} is the name of the table into which data is imported.      </div>
      

      3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The parameter ${时间点} is the time when the error occurred. For example, "0906 15:54" means September 6 at 15:54.      </div>
      

      4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Traverse all BE instances to check whether there is a high\-frequency data import phenomenon, such as importing twice per second.      </div>
      

      For example, as shown in the figure below, during a continuous period, there are basically 5 writes per second, which is a relatively high frequency:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ad7f6205eb7a163e59f7c6f3db35bb6.png) </span>

   3. If the issue of excessively high import frequency has been confirmed, increase the amount of data imported in each batch. It is recommended to import once every 5 seconds.

   4. If it is confirmed that the import frequency is not too high, you can speed up merging by adjusting the merge strategy. Log in to the EMR StarRocks cluster console, add the following parameters to the **be.conf** file under **Cluster Details \> Service List \> StarRocks Service Parameters**, and restart StarRocks.

      1. For non\-primary key models, the parameters are as follows:

         ```json
         cumulative_compaction_num_threads_per_disk = 4
         base_compaction_num_threads_per_disk = 2
         cumulative_compaction_check_interval_seconds = 2
         ```
         

      2. For primary key models, the parameters are as follows:

         ```sql
         update_compaction_check_interval_seconds = 2
         update_compaction_num_threads_per_disk = 2
         ```
         


<span id="_2-2-数据导入过程中报-the-size-of-this-batch-exceed-the-max-size"></span>
### The error "The size of this batch exceed the max size" occurs during data import.


* **Issue description:** 

   ```json
   {
     "txnId": -1,
     "existingJobStatus": null,
     "label": "_1693983827223_815bd46ac1f24c49a984a30281fd3c8e",
     "status": "Fail",
     "message": "The size of this batch exceed the max size [104857600]  of json type data  data [ 300569714 ]. Set ignore_json_size to skip the check, although it may lead huge memory consuming.",
     "TxnId": -1,
     "Label": "_1693983827223_815bd46ac1f24c49a984a30281fd3c8e",
     "Status": "Fail",
     "ExistingJobStatus": null,
     "Message": "The size of this batch exceed the max size [104857600]  of json type data  data [ 300569714 ]. Set ignore_json_size to skip the check, although it may lead huge memory consuming.",
     "NumberTotalRows": 0,
     "NumberLoadedRows": 0,
     "NumberFilteredRows": 0,
     "NumberUnselectedRows": 0,
     "LoadBytes": 0,
     "LoadTimeMs": 0,
     "BeginTxnTimeMs": 0,
     "StreamLoadPutTimeMs": 0,
     "ReadDataTimeMs": 0,
     "WriteDataTimeMs": 0,
     "CommitAndPublishTimeMs": 0,
     "ErrorURL": null
   }
   ```
   

* **Cause analysis:** 

   This error occurs when the JSON Body size is too large during Stream Load. Refer to the official documentation [Streaming Data Source Import Parameter Configuration](https://docs.starrocks.io/zh-cn/latest/loading/StreamLoad#%E5%8F%82%E6%95%B0%E9%85%8D%E7%BD%AE).

* **Resolution steps:** 

   * Solution 1: Add the `"ignore_json_size:true"` setting in the HTTP request header to ignore the check on JSON Body size.

   * Solution 2: On the ECS node of the cluster, execute the following command for each BE instance to dynamically modify BE parameters, that is, increase the JSON Body size without restarting StarRocks:

      ```shell
      curl -XPOST http://${BE地址}:8040/api/update_config?streaming_load_max_batch_size_mb=${size}
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The parameter ${size} configures the size of the JSON body according to actual requirements.      </div>
      

      2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This parameter takes effect dynamically. This parameter takes effect after StarRocks restarts.      </div>
      

   * Solution 3: Log in to the EMR StarRocks cluster console, add the parameter `streaming_load_max_batch_size_mb` (default value is 100) to the **be.conf** file under **Cluster Details \> Service List \> StarRocks Service Parameters**, and restart StarRocks.


<span id="_2-3-数据导入时报-mem-usage-has-exceed-the-limit-of-be"></span>
### The error "Mem usage has exceed the limit of BE" occurs during data import.


* **Issue description:** 

   ```shell
   Caused by: java.io.IOException: stream load error: Memory of process exceed limit. try consume:2097152 Used: 27644351240, Limit: 27051754291. Mem usage has exceed the limit of BE
   ```
   

* **Cause analysis:** 

   This is generally caused by unreasonable bucket settings for the table, or by writing data that is too small and at a high frequency, resulting in too many small files.

* **Resolution steps:** 

   1. Estimate the size of the table and analyze whether the number of buckets is reasonable. Generally, the size of a bucket is 100 MB to 1 GB (after data compression).

   2. Log in to the ECS node of the BE instance and check the growth rate of Segment files in the data storage directory (default is `/data01/ju/output/be/storage/data`):

      ```shell
      find /data01/starrocks/be/storage/data -name *.dat |wc -l
      ```
      

      Example: After data import begins, the number of imported files reaches 200,000 after two hours. If the import frequency is high, you can increase the size of each data import.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8984da6ccc7844564b4743f9aada5f6.png) </span>

   3. Analyze BE memory consumption during task execution. Refer to the official documentation [Manage memory][Manage memory](https://docs.starrocks.io/zh-cn/latest/administration/Memory_management#%E5%86%85%E5%AD%98%E5%88%86%E7%B1%BB).


<span id="_2-4-数据导入时报-primary-key-index-exceeds-the-limit"></span>
### When importing data, the error 'Primary\-key index exceeds the limit' occurs.


* **Issue description:** 

   ```plain
   stream load error: Primary-key index exceeds the limit. tablet_id: 347620, consumption: 66234184315, limit: 65516516056. Memory stats of top five tablets: 347628(2038M)347640(2038M)347620(2038M)347624(2038M)347644(2038M): be:XX.XX.XX.XX
   ```
   

* **Cause analysis:** 

   The primary key index occupies excessive memory and can be persisted.

* **Resolution steps:** 

   Execute the following SQL statement to persist the primary key index:

   ```sql
   ALTER TABLE ${表名} SET ("enable_persistent_index"="true")
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The parameter ${size} configures the size of the JSON body according to actual requirements.   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This parameter takes effect dynamically. This parameter takes effect after StarRocks restarts.   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the open\-source StarRocks 3.x version, the default value of the enable_persistent_index parameter is true.   </div>
   


<span id="_2-5-如何查看日志？"></span>
### **How to view logs?** 

The log directory is usually located at the following paths:


* FE

   * /var/log/emr/starrocks/fe/log

   * /var/log/emr/starrocks/fe/sys

* BE

   * /var/log/emr/starrocks/be/log

   * /var/log/emr/starrocks/be/sys
