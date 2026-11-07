---
title: "StarRocks FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_FAQs"
---

<span id="09a8f0ab"></span>
## How to add an access allowlist for a StarRocks cluster


* **Issue symptoms**


When connecting to a StarRocks instance, the connection times out:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/477630c10db847d2b1c7895149f5067b~tplv-goo7wpa0wc-image.image" width="1356px" /></div>



* **Cause analysis**


The host or client IP address connecting to the StarRocks instance has not been added to the network connection allowlist of the StarRocks instance.


* **Solution**


Open the StarRocks instance, then go to **Network connection** \> **Allowlist management** \> **Inbound allowlist** \> **Add allowlist group**. After adding, click **Confirm.** 


* Connecting instances within the same VPC, example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3abef0c45dd4d0ca1c567a3901cd15f~tplv-goo7wpa0wc-image.image) </span>

* Connecting instances in different VPCs, use the public address, example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/178bb17c41c24c21bd58685f299643a6~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is not recommended to set 0.0.0.0/0. Allowing access from all addresses will create security risks.</div>


<span id="51bd984c"></span>
## Failed to import data or query via public network in StarRocks cluster


* **Issue symptoms**


When connecting to a StarRocks instance from a host or client not in the same VPC as the StarRocks instance, the connection times out or the network is unreachable.


* **Cause analysis**


It is necessary to connect to the StarRocks instance via a public address and add the public address of the target host to the network connection allowlist of the StarRocks instance.


* **Solution**

   * Open the StarRocks instance details, then go to **Network connection** \> **Public connection** \> **Enable public IP** \> **Bind public IP**. After selecting an available public IP address, click **Confirm**. If there is no available public IP address, create a new one via [Create public IP](https://console.volcengine.com/eip/region:eip+cn-beijing/eips/create?projectName=default).

   * For instructions on how to add, refer to [How to add an access allowlist for a StarRocks cluster](https://docs.byteplus.com/docs/E-MapReduce/109555#09a8f0ab).


<span id="30a10b42"></span>
## Insufficient memory error when executing jobs in StarRocks


* **Issue symptoms**


When using StarRocks for data snapshot backup, the following error message is encountered:

```Shell
Memory limit exceeded: Memory of default_wg exceed limit. read and decompress page Backend: xxx.xxx.xxx.xxx, Used: **********, Limit: **********. Mem usage has exceed the limit of query...
```



* **Cause analysis**


The memory resources used during job execution exceed expectations.


* **Solution**

   * Refer to [SQL diagnostics instructions](https://docs.byteplus.com/docs/E-MapReduce/109126) query optimization to tune the job;

   * Scale out or upgrade the instance. For detailed operations, refer to:

      * OLAP instance scale\-out: [Scale out and upgrade instance nodes](https://docs.byteplus.com/docs/E-MapReduce/109101).

      * OLAP instance upgrade: [【Take down】Instance configuration upgrade](https://docs.byteplus.com/docs/E-MapReduce/109106).


<span id="be9078a4"></span>
## Tablet imbalance in StarRocks cluster

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This section applies only to StarRocks instances with separated storage and compute.</div>



* **Issue symptoms**


Use `show compute nodes;` to query the number of Tablets on CN nodes, and an imbalance is observed:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57670e3879f64f28901d6b4c48e3cbd6~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**


After operations such as scaling out, the re\-balance operation was not performed, resulting in data imbalance. The StarRocks automatic balancing parameter `lake_enable_balance_tablets_between_workers` has a default value of false.


* **Solution**

   * Enable automatic balancing using the following command.


```SQL
ADMIN SET FRONTEND CONFIG (lake_enable_balance_tablets_between_workers=true);
```



* **Important notes**

   * Enabling automatic balancing results in additional resource consumption. It is recommended to perform this operation during off\-peak business hours and disable the setting after completion.

   * In scenarios where storage and compute are separated, keeping Tablet balancing enabled for an extended period increases the number of cold queries and leads to higher query latency.


<span id="f1ed21fe"></span>
## StarRocks FE connection pool is full


* **Issue symptoms**


The following error occurs when establishing a new connection to StarRocks.

```SQL
com.starrocks.mysql.nio.AcceptListener$AfterConnectedException: Reach limit of connection
```



* **Cause analysis**


The number of new connections in the cluster is too high, reaching the connection limit of FE or the user.


* **Solution**


Check whether the number of FE connections has reached the limit. Open the StarRocks instance details, then go to **Monitoring & Alerts \> FE connection status** to view the monitoring information.


1. If the number of connections reaches the upper limit set by the FE configuration `qe_max_connection`, modify this parameter to a reasonable threshold and restart FE for the change to take effect.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/978a04b2a5c1497d890768df3f4900a6~tplv-goo7wpa0wc-image.image) </span>

2. If monitoring indicates that the number of connections has not reached the upper limit set by the FE configuration `qe_max_connection`, the user\-level connection limit has been reached.


```SQL
-- View the maximum number of connections for the user
show property for '用户名';

-- Modify the connection limit at the user level
set property for '用户名' 'max_user_connections' = 'xxx'; 
```


<span id="0e195917"></span>
## StarRocks BE JDBC connection pool has reached the configured maximum connection limit


* **Issue symptoms**


The following error occurs when writing data to the StarRocks instance, and it is determined that the BE connection count has reached the limit:

```SQL
Caused by: java.sql.SQLTransientConnectionException: seetong-siot-tsl - Connection is not available, request timed out after 30006ms.
```



* **Cause analysis**


Connecting to the StarRocks instance via JDBC and writing data using Insert Into causes the number of connections to increase rapidly.


* **Solution**

   * Temporary mitigation: The default value of `jdbc_connection_pool_size` is 8. Adjust the connection limit to 1024 and restart the BE node for the change to take effect.

   * Import data using methods such as Stream Load to avoid writing data with Insert Into.

* **Reference**

   * Import data using Stream Load: [Stream Load](https://docs.byteplus.com/docs/E-MapReduce/109122).

   * Import data using Broker Load: [Broker Load](https://docs.byteplus.com/docs/E-MapReduce/109121).


<span id="5eb08ad8"></span>
## StarRocks Compaction index loading is too slow


* **Issue symptoms**


The Compaction task is stuck at the Publish Version stage and does not finish. Investigation shows that the cause is slow index loading.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a41e25577fe46e2af1225b45836fcb0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/caa232b1c4e64e3ca06a7af2dc3a90de~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**

   * The local cache time for the primary key index is set too low. When the import interval exceeds the cache expiration, the primary key index is loaded repeatedly.

   * The local cache memory for the primary key index is set too low. When a large amount of data is imported, repeated loading occurs.

* **Solution**

   * Increase the cache expiration time.

   ```SQL
   UPDATE information_schema.be_configs SET VALUE = 3600 WHERE name = "lake_local_pk_index_unused_threshold_seconds";
   ```
   

   * Adjust the cache space based on the memory usage of BE/CN nodes.

   ```SQL
   -- Set the custom parameter lake_metadata_cache_limit to 2GB
   UPDATE information_schema.be_configs SET VALUE = 2147483648 WHERE name = "lake_metadata_cache_limit";
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61794a22154540abb388dff8f713a814~tplv-goo7wpa0wc-image.image) </span>


<span id="69b8f4a7"></span>
## StarRocks CN node disk storage usage is too high


* **Issue symptoms**


In customer scenarios where compute and storage are separated, the disk usage of CN nodes is excessively high.


* **Cause analysis**


A large amount of local disk space is occupied by data cache, resulting in insufficient disk space.


* **Solution**

   * Adjust the proportion of local data cache occupying disk space, or consider expanding the disk capacity of CN nodes.

   ```SQL
   -- In separated storage and compute mode, enable file data cache. If the current remaining disk space (percentage) is lower than the value specified in this configuration item, cache eviction will be triggered
   starlet_cache_evict_low_water=0.2
   -- In separated storage and compute mode, enable file data cache. If the current remaining disk space (percentage) is higher than the value specified in this configuration item, cache eviction will stop
   starlet_cache_evict_high_water=0.3 
   -- In separated storage and compute mode, the maximum percentage of disk capacity that data cache can use
   starlet_star_cache_disk_size_percent=70
   ```
   


<span id="e0cbea6d"></span>
## StarRocks FE node memory usage exceeds 90%


* **Issue symptoms**


The memory usage of FE nodes in the StarRocks cluster gradually increases, exceeding 90%, and the JVM Heap memory also remains high:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2e0ffd96bfe4ec69867c84949148cb7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/218c02b372454b1a92e6e7879fc2a93b~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**


The memory usage setting of the FE node is unreasonable, causing memory usage to remain high.


* **Solution**


Adjust the memory usage limit via Xmx to reduce the memory usage ratio. Please adjust according to the total memory of the node. Example:


* Before adjustment: \-Xms13107m \-Xmx49152m

* After adjustment: \-Xms13107m \-Xmx45875m


<span id="d0dd67a3"></span>
## StarRocks error `get database read lock timeout`


* **Issue symptoms**


Real\-time tasks fail to write data to the StarRocks instance, with the following error message:

```Plain
Caused by: com.bytedance.bitsail.common.BitSailException: LOAD_FAILED - StarRocks load status is not success, response content: {"existingJobStatus":null,"label":"_1761718530459_ed7721edca174dffa1f456359c4a4cf8","txnId":577316498,"status":"Fail","message":"get database read lock timeout... ...
```



* **Cause analysis**


Cross\-database operations are involved in asynchronous materialized view operations, resulting in a deadlock.


* **Solution**

   * It is not recommended to use materialized views in lower versions of StarRocks. For details, see [Limits](https://www.volcengine.com/docs/6491/1339363).

   * Avoid using asynchronous materialized views, especially when cross\-database operations are involved.


<span id="d8076624"></span>
## StarRocks large queries lead to resource exhaustion


* **Issue symptoms**


A single query or job causes CPU usage to reach 100% and lasts for more than 10 seconds, occupying a large amount of cluster resources, resulting in normal business queries failing or experiencing increased latency.


* **Troubleshooting ideas**

   * Refer to [Locating large queries](https://docs.byteplus.com/docs/E-MapReduce/109152) to locate large queries currently running.

* **Solution**


Based on the results of locating large queries, manually terminate them; then manage queries by reviewing business usage and the query audit log table.


* You can deploy mitigation strategies using [Large query defense](https://docs.byteplus.com/docs/E-MapReduce/109153) to reduce the business impact caused by unknown large queries.

* You can optimize queries using [SQL diagnostics instructions](https://docs.byteplus.com/docs/E-MapReduce/109126).


<span id="9b48432c"></span>
## StarRocks Compaction Score is too high


* **Issue symptoms**


The read and write performance of the StarRocks cluster degrades or errors occur. Monitoring shows that the Compaction Score on BE/CN nodes is too high.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b436e4eaedaa47fa8685761431a428cf~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**


Compaction score is too high, indicating that there are many small files in the current cluster. The root cause is a mismatch between the write frequency and the efficiency of merging small files.


* **Solution**

   * It is recommended to reduce the client write frequency and increase client\-side data batching to avoid generating a large number of small files.

   * When resources permit, refer to [存算分离集群 Compaction](https://docs.byteplus.com/docs/E-MapReduce/109555#%E6%9F%A5%E7%9C%8B-compaction-score) to increase the concurrency of Compaction.


<span id="e07f6e6a"></span>
## StarRocks BE tablet version limit exceeded

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This Note applies only to StarRocks instances with integrated storage and compute.</div>



* **Issue symptoms**


The number of tablet versions exceeds the limit, resulting in errors during write operations:

```Plain
ERROR 5025 (HY000): Failed to load data into tablet XXXX, because of too many versions, current/limit: 1005/1000. You can reduce the loading job concurrency, or increase loading data batch size. If you are loading data with Routine Load, you can increase FE configs routine_load_task_consume_second and max_routine_load_batch_size... ...
```



* **Cause analysis**


The above error occurs because the import frequency is too high, and the data cannot be merged (Compaction) in time, causing the number of versions to exceed the maximum number of unmerged versions supported. The default maximum number of unmerged versions supported is 1000.


* **Solution**

   * Dynamic adjustment method


```SQL
-- StarRocks engine (integrated storage and compute)
UPDATE information_schema.be_configs SET VALUE = 1500 WHERE name = "tablet_max_versions";
```


<span id="16986bac"></span>
## StarRocks transaction limit exceeded


* **Issue symptoms**


The number of write transactions exceeds the limit, resulting in errors during write operations:

```Plain
current running txns on db xxxx is xxxx, larger than limit xxxx
```



* **troubleshooting**

   * Check the transaction backlog status for each database.


```SQL
-- StarRocks
show proc '/transactions';
-- View the status of each db
show proc '/transactions/${db_id}';
-- View completed import transactions, locate failed transactions, and check the reason
show proc '/transactions/${db_id}/finished';
```



* **Solution**

1. Dynamically increase the transaction limit to allow transactions to enter, alleviating upstream write task latency.


```SQL
-- Adjust FE configuration (default 1000)
admin set frontend config ("max_running_txn_num_per_db" = "2000")
```



2. Assess the cluster resource utilization and consider upgrading or expanding capacity.


<span id="3346fa43"></span>
## StarRocks write error `too many filter rows`


* **Issue symptoms**


Data write to StarRocks fails, with an error message `too many filtered rows`. For example:

```JSON
{
  "Status": "Fail",
  "BeginTxnTimeMs": 101,
  "Message": "too many filtered rows",
  "NumberUnselectedRows": 0,
  "CommitAndPublishTimeMs": 0,
  "Label": "xxxxxxxxx",
  "LoadBytes": 245396,
  "StreamLoadPlanTimeMs": 102,
  "NumberTotalRows": 984,
  "WriteDataTimeMs": 265,
  "TxnId": 13787,
  "LoadTimeMs": 469,
  "ErrorURL": "http://xx.xx.xx.xx:8040/api/_load_error_log?file=error_log_5a4aad49f7900ad7_9dec92739f8027b7",
  "ReadDataTimeMs":0,
  "NumberLoadedRows":0,
  "NumberFilteredRows":984
}
```



* **troubleshooting**


To ensure data quality, StarRocks performs validity checks on write data by default. When data does not match the field types of the StarRocks table, it will be filtered out. When the **proportion of filtered rows to total rows** exceeds the threshold, the system will terminate the write operation to prevent a large amount of invalid data from consuming resources or compromising data consistency.

Users can view the specific error reason via the URL in the error message. Common causes include:


1. Issues with the data itself (dirty data).

2. Incorrect field partition configuration, such as column fields not aligning or inconsistent types.

* **Solution**

   * **Standardize data source validation**: Add data validation logic (such as type checks, format validation, and constraint checks) in upstream business systems to reduce dirty data at the source;

   * **Set an appropriate fault tolerance rate**: In production environments, it is recommended to set `max_filter_ratio` to `0.05~0.1` (5%\-10%), which allows a small amount of occasional dirty data while preventing a large volume of invalid data from being written.

   * For more operations, refer to [数据导入故障排查](https://docs.byteplus.com/docs/E-MapReduce/109555#properties).


<span id="fe72988d"></span>
## StarRocks single replica and data corruption issues


* **Issue symptoms**


An error occurs when querying the data table, with the message "No available data replica found." For example:

```SQL
Caused by: com.starrocks.common.UserException: Failed to get scan range, no queryable replica found in tablet=xxxxxxxxx replica=xxxxx:x/x/x/x:DECOMMISSION:ALIVE,xxxxxxxx:x/x/x/x:NORMAL:ALIVE, schema_hash=xxxxxxxxxx version=x
```



* **troubleshooting**


This issue is usually related to a low number of replicas configured, resulting in poor fault tolerance. If a StarRocks data table uses single replica storage, when a storage node fails or the service is abnormal, data will become inaccessible or even corrupted, posing a risk of data loss.

**Replica count verification operation**: Use SQL statements to check the replica configuration of the target table and confirm whether it is single replica:

```SQL
-- Information about the database and data table
SHOW CREATE TABLE XXXX.XXXX
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daada31311fb44709f47d5d985c90734~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The replica count parameter <code>replication_num</code> with a value of 1 indicates a single replica.</div>



* **Solution**


When creating a data table, **proactively set the replica count parameter** **`replication_num`** and ensure its value is ≥2 to improve data fault tolerance and avoid the risk of corruption caused by a single replica.

Example:

```SQL
CREATE TABLE IF NOT EXISTS test_two_duplicate_table (
  id INT NOT NULL COMMENT '唯一标识',
  name STRING COMMENT '姓名',
  age TINYINT COMMENT '年龄',
  create_time DATETIME COMMENT '创建时间',
  score DECIMAL(5,2) COMMENT '分数（精度 5 位，小数 2 位）'
) ENGINE=OLAP
DUPLICATE KEY(id)  -- Duplicate key table, sorted by id, allows duplicate data
DISTRIBUTED BY HASH(id) BUCKETS 4  -- Hash partitioned by id, 4 buckets (testing does not require too many buckets)
PROPERTIES (
  "replication_num" = "2"
);
```
