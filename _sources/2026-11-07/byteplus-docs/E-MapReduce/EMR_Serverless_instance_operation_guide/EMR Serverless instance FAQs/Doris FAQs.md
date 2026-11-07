---
title: "Doris FAQs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Doris_FAQs"
---

<span id="e1ad0567"></span>
## How to add an access allowlist for a Doris cluster


* **Problem description**


When connecting to a Doris instance, the connection times out:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c507713b14c241af8b6c0bec96590ec1~tplv-goo7wpa0wc-image.image" width="1356px" /></div>



* **Cause analysis**


The host or client IP address connecting to the Doris instance has not been added to the Doris instance's network connection allowlist.


* **Solution**

   * Open the Doris instance, then go to **Network connection** \> **Allowlist management** \> **Inbound allowlist** \> **Add allowlist group**. After adding, click **Confirm**. Example:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74327d4d623d426ba98bdfa0c2e50468~tplv-goo7wpa0wc-image.image) </span>

   * For instances not under the same VPC, use the public address. Example:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f5c4671a6064385a990f1fd27e73e1e~tplv-goo7wpa0wc-image.image) </span>

* **important notes**

   * It is not recommended to set 0.0.0.0/0, which allows access from all addresses and poses a security risk.


<span id="cf6e1859"></span>
## Importing data or querying via the public network in the Doris cluster fails.


* **Problem description**


When connecting to a Doris instance from a host or client not in the same VPC as the Doris instance, the connection times out or the network is unreachable.


* **Cause analysis**


It is necessary to connect to the Doris instance via the public address and add the public address of the target host to the Doris instance's network connection allowlist.


* **Solution**

   * Open the Doris instance details, then go to **Network connection** \-\> **Public connection** \-\> **Enable public IP** \-\> **Bind public IP**. After selecting an available public IP address, click **Confirm**. If there is no available public IP address, create a new one via [Create public IP](https://console.volcengine.com/eip/region:eip+cn-beijing/eips/create?projectName=default).

   * Add the public address of the target host to the allowlist group of the current instance. Refer to “**How to add an access allowlist for a Doris cluster**” for instructions.


<span id="da59dbbb"></span>
## Resource isolation between different business lines in the Doris cluster


* **Problem description**


Different business lines use the same Doris cluster, causing jobs to affect each other.


* **Cause analysis**


No resource isolation is implemented, resulting in jobs interfering with each other.


* **Solution**


Refer to the official Doris documentation for resource allocation:

[Recommended] Resource Group method: [Multi-tenancy and resource allocation](https://doris.apache.org/zh-CN/docs/3.x/admin-manual/workload-management/workload-management-summary?_highlight=%E8%B5%84%E6%BA%90&_highlight=%E5%88%92%E5%88%86#%E8%B5%84%E6%BA%90%E5%88%92%E5%88%86%E6%96%B9%E5%BC%8F)

Workload Group method: [Workload Group](https://doris.apache.org/zh-CN/docs/3.x/admin-manual/workload-management/workload-group?_highlight=workload&_highlight=group)

<span id="41e71480"></span>
## Tablet imbalance in Doris cluster


* **Problem description**


When running show backends; to query the number of Tablets on BE nodes, an imbalance is observed:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d5d7db75194b518fb20e11fe6fef91~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**


After expansion or similar operations, the re\-balance operation was not performed, resulting in data imbalance. Additionally, the Doris automatic balancing parameter lake_enable_balance_tablets_between_workers defaults to false.


* **Solution**

   * Enable auto balancing with the following command


```SQL
ADMIN SET FRONTEND CONFIG (lake_enable_balance_tablets_between_workers=true);
```



* **important notes**

   * Enabling auto balancing will result in additional resource consumption. It is recommended to perform this operation during off\-peak business hours, and to disable this setting after completion.

   * In scenarios with storage\-compute separation, keeping Tablet balancing enabled for extended periods will increase the number of cold queries and lead to higher query latency.


<span id="bc75d4a2"></span>
## Doris FE connection pool is full


* **Problem description**


The following error occurs when establishing a new connection to Doris

```SQL
Reach limit of connection
```



* **Cause analysis**


The number of new connections in the cluster is too high, reaching the connection limit of FE or the user.


* **Solution**

   * First, confirm whether the FE connection limit has been reached. Open the Doris instance details, then sequentially open **Monitoring & Alerts \> FE connection status** to check the monitoring status. If the number of connections reaches the upper limit set by the FE configuration parameter qe_max_connection, you can increase the qe_max_connection parameter in the FE configuration file to a reasonable threshold. After modification, restart FE to apply the changes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24c36101f60e4bfd8d42946219e38183~tplv-goo7wpa0wc-image.image) </span>


* If monitoring indicates that the upper limit set by the FE configuration parameter qe_max_connection has not been reached, then the user\-level connection limit has been reached.


```SQL
-- View the connection limit for user
show property for '用户名';

-- Modify the connection limit at the user level
set property for '用户名' 'max_user_connections' = 'xxx'; 
```


<span id="3c5af0d9"></span>
## Doris BE node performing compaction operations causes sustained high CPU usage


* **Problem description**


BE node CPU remains fully utilized, and the number of compaction tasks matches the number of cores on the BE node.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15a56fa163c8445592b79ab263562a23~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41c1193c45dc44fbbe3960092dcbe5de~tplv-goo7wpa0wc-image.image) </span>


* **Cause analysis**


The BE node specification is 4 vCPUs. When merging small files via Base Compaction, the concurrency limit is 4, which leads to full utilization of CPU resources.


* **Solution**

   * Reduce the number of threads executing compaction tasks simultaneously:


```SQL
-- Number of threads for base compaction, default is 4
max_base_compaction_threads
-- Number of threads for cumulative compaction, default is 10
max_cumu_compaction_threads
```



* Upgrade the BE node to increase cluster configuration: [【Take down】Instance configuration upgrade](https://docs.byteplus.com/docs/E-MapReduce/109106)


<span id="1696acdf"></span>
## Doris large queries cause resource saturation


* **Problem description**


A single query or job drives CPU usage to 100% for more than 10 seconds, occupying a large amount of cluster resources and causing normal queries to fail or experience increased latency.


* **Troubleshooting approach**

   * Refer to [Locating large queries](https://docs.byteplus.com/docs/E-MapReduce/109164) to locate running large queries

* **Solution**

   * Based on the results of large query identification, manually terminate the large query. Additionally, perform query optimization using business usage and the query audit log table.

   * You can choose to deploy defense strategies based on [Large query defense](https://docs.byteplus.com/docs/E-MapReduce/109163) to reduce the impact of unknown large queries on business operations.


<span id="c64511c2"></span>
## Doris BE compaction score is too high


* **Problem description**


Doris cluster read/write performance degradation or errors. Monitoring reveals that the Compaction Score on BE nodes is excessively high.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9f36900200e4cccbedf4a8f6e1f535b~tplv-goo7wpa0wc-image.image" width="2324px" /></div>



* **Cause analysis**

   * An excessively high Compaction Score indicates that there are many small files in the current cluster. The root cause is a mismatch between the write frequency and the efficiency of merging small files.

* **Solution**

   * It is recommended to reduce the client write frequency and increase the client data batch size to avoid generating a large number of small files.

   * If resources permit, refer to [Compaction optimization](https://doris.apache.org/zh-CN/docs/3.x/admin-manual/trouble-shooting/compaction?_highlight=compact) to increase Compaction concurrency.


<span id="fe911955"></span>
## Doris BE tablet version limit exceeded

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This note applies only to integrated compute\-storage Doris instances</div>



* **Problem description**


The number of tablet versions exceeds the limit, resulting in errors when performing operations such as Insert Into:

```Plain
ERROR 5025 (HY000): Failed to load data into tablet XXXX, because of too many versions, current/limit: 6/5. You can reduce the loading job concurrency, or increase loading data batch size. If you are loading data with Routine Load, you can increase FE configs routine_load_task_consume_second and max_routine_load_batch_size... ...
```



* **Cause analysis**


The above error occurs because the import frequency is too high, and the data cannot be merged (Compaction) in time, causing the number of versions to exceed the maximum supported number of unmerged versions. The default maximum number of supported unmerged versions is 1000.


* **Solution**

   * Increase the parameter limit and restart the cluster to take effect, allowing write transactions to be committed first.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f97dc3a8cd0413c8e95d6a849ddbc33~tplv-goo7wpa0wc-image.image" width="2320px" /></div>


<span id="9fa92649"></span>
## Doris transaction limit exceeded


* **Problem description**


The number of write transactions exceeds the limit, resulting in errors during write operations:

```Plain
current running txns on db xxxx is xxxx, larger than limit xxxx
```



* **Troubleshooting**

   * Check the transaction backlog for each databases:


```SQL
-- Doris
show proc '/transactions';
-- View the status of each db
show proc '/transactions/${db_id}';
-- View completed import transactions, locate failed transactions, and check the reason
show proc '/transactions/${db_id}/finished';
```



* **Solution**

1. Dynamically increase the transaction limit to allow transactions to enter first, alleviating upstream write task latency:


```SQL
-- Doris engine
-- Adjust FE configuration; a restart is required for changes to take effect
-- Default 1000
admin set frontend config ("max_running_txn_num_per_db" = "xxx")
```



2. Assess the cluster resource utilization and consider upgrading or expanding capacity.


<span id="7b8b3082"></span>
## Doris write error `too many filtered rows`


* **Problem description**


Data write to Doris fails, with the error message `too many filtered rows`. Example:

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



* **Troubleshooting**


To ensure data quality, Doris performs validity checks on write data by default. If the data does not match the field types of the Doris table, it will be filtered out. When the **proportion of filtered rows to total rows** exceeds the threshold, the system will terminate the write operation to prevent a large amount of invalid data from occupying resources or compromising data consistency.

Users can check the specific error cause via the URL in the error message. Common causes include:


1. Problems with the data itself (dirty data).

2. Field partition configuration errors, such as misaligned column fields or inconsistent types.

* **Solution**

   * **Standardize data source validation**: Add data validation logic (such as type checking, format validation, and constraint validation) in upstream business systems to reduce dirty data at the source.

   * **Set a reasonable fault tolerance rate**: In production environments, it is recommended to set `max_filter_ratio` to `0.05~0.1` (5%\-10%), which allows a small amount of occasional dirty data while preventing a large volume of invalid data from being written.

   * For more operations, refer to [data import troubleshooting](https://doris.apache.org/zh-CN/docs/3.x/faq/load-faq).


<span id="50897cd9"></span>
## Doris single replica and data corruption issues


* **Problem description**


An error occurs when querying the data table, with the message "No available data replica found." Example:

```SQL
Failed to get scan range, no queryable replica found in tablet=xxxxxxxxx replica=xxxxx:x/x/x/x:DECOMMISSION:ALIVE,xxxxxxxx:x/x/x/x:NORMAL:ALIVE, schema_hash=xxxxxxxxxx version=x
```



* **Troubleshooting**


This issue is usually related to a low number of data replicas and poor fault tolerance. If a Doris data table uses single\-replica storage, when a storage node fails or a service exception occurs, it will directly result in data being inaccessible or even corrupted, posing a risk of data loss.

**Replica count verification operation**: Use SQL statements to check the replica configuration of the target table and confirm whether it is a single replica:

```SQL
-- Information about database.data table
SHOW CREATE TABLE XXXX.XXXX
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daada31311fb44709f47d5d985c90734~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The value of the replica count parameter <code>replication_num</code> is 1, indicating a single replica.</div>



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
DISTRIBUTED BY HASH(id) BUCKETS 4  -- Hash partitioned by id, 4 buckets (no need for too many in testing)
PROPERTIES (
  "replication_num" = "2"
); 
```
