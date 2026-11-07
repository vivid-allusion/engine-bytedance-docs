---
title: "Starrocks major version upgrade"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Starrocks_major_version_upgrade"
---

<span id="_1-背景需求"></span>
## 1 Background and requirements

Currently, some of our users are using version 2.5.x. Although this version is an LTS version, it was released nearly a year and a half ago, and many features available in the new versions are not supported in this version.

**As a result, many customers wish to upgrade their Starrocks version from 2.5.x to 3.2.x.** 

However, due to metadata compatibility issues in the SR community, direct upgrade is not possible. Intermediate versions 3.0 and 3.1 are required as transition versions, but neither of these are LTS versions. Upgrading through these versions may introduce additional issues. Therefore, we recommend the **migration upgrade** approach.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b78216782430351bde88b34a4f99fb6.png) </span>

<span id="_2-升级方案"></span>
## 2 Upgrade solution

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_258d58acab26f7dbf58d11dbaa6f0d49.png) </span>


1. Create a new SR cluster of the latest version within the same VPC subnet as the old cluster.

2. Select a node within the subnet that can connect to both clusters to serve as the client node, and deploy the synchronization tool.

3. Configure the synchronization tool options and start the synchronization task.

   1. The tool can automatically obtain metadata from the old cluster.

   2. Submit the synchronization task to the new cluster.

   3. The synchronization task will automatically pull synchronization data from the old cluster.

4. After all data migration is complete, redirect real\-time writes to the new cluster, completing the replacement between the old and new clusters.


<span id="_3-迁移详细步骤"></span>
## 3 Detailed migration steps

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9351b953fd1b08d25f513515ace0c96.png) </span>

<span id="_3-1-准备工作"></span>
### 3.1 Preparation

The following preparation must be performed in the target cluster for data migration.

<span id="_3-1-1-关闭-compaction-目标集群为存算分离集群"></span>
#### 3.1.1 Disable Compaction (target cluster is a storage\-compute separated cluster)

If the target cluster for data migration is a storage\-compute separated cluster, you must manually disable Compaction before data migration, and re\-enable it after migration is complete.


1. You can use the following statement to check whether Compaction is enabled in the current cluster:


```sql
ADMIN SHOW FRONTEND CONFIG LIKE 'lake_compaction_max_tasks';
```


If the return value is `0`, Compaction is disabled.


2. Dynamically disable Compaction:


```sql
ADMIN SET FRONTEND CONFIG("lake_compaction_max_tasks"="0");
```



3. To prevent Compaction from automatically enabling after a cluster restart during data migration, you also need to add the following configuration item to the FE configuration file **fe.conf**:


```properties
lake_compaction_max_tasks = 0
```



4. After data migration is complete, you need to remove `lake_compaction_max_tasks = 0` from the configuration file and use the following statement to dynamically enable Compaction:


```sql
ADMIN SET FRONTEND CONFIG("lake_compaction_max_tasks"="-1");
```


<span id="_3-1-2-配置数据迁移（可选）"></span>
#### 3.1.2 Configure data migration (optional)

You can configure data migration operations using the following FE and BE parameters. In most cases, the default configuration is sufficient. To retain the default configuration, you can choose to skip this step.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Caution: Increasing the following configuration items can speed up migration, but will also increase the load on the source cluster.</div>


<span id="fe-参数"></span>
##### FE parameters

The following FE parameters are dynamic parameters. For modification instructions, refer to [配置 FE 动态参数](https://docs.byteplus.com/docs/E-MapReduce/109516#%E9%85%8D%E7%BD%AE-fe-%E5%8A%A8%E6%80%81%E5%8F%82%E6%95%B0).


|Parameter name |Default value |Unit |Description |
|---|---|---|---|
|replication_max_parallel_table_count |100 |*  |The number of data synchronization tasks allowed to run concurrently. StarRocks creates one synchronization task for each table. |
|replication_max_parallel_data_size_mb |10240 |MB |The amount of data allowed for concurrent synchronization. |
|replication_transaction_timeout_sec |3600 |Seconds |Timeout period for synchronization tasks. |


```sql
ADMIN SET FRONTEND CONFIG("replication_max_parallel_data_size_mb"="102400");
```


<span id="be-参数"></span>
##### BE parameters

The following BE parameters are dynamic parameters. For modification instructions, refer to [配置 BE 动态参数](https://docs.byteplus.com/docs/E-MapReduce/109516#%E9%85%8D%E7%BD%AE-be-%E5%8A%A8%E6%80%81%E5%8F%82%E6%95%B0).


|Parameter name |Default value |Unit |Description |
|---|---|---|---|
|replication_threads |0 |*  |The number of threads for executing synchronization tasks. 0 means the number of threads is set to the number of CPU cores on the machine where BE is located. |


<span id="_3-2-第一步：安装工具"></span>
### 3.2 Step 1: Install the tool

It is recommended to install the migration tool on the server where the target cluster for data migration is located.

Open the terminal and download the tool installation package.

```bash
wget https://releases.starrocks.io/starrocks/starrocks-cluster-sync.tar.gz
```


Extract the installation package.

```bash
tar -xvzf starrocks-cluster-sync.tar.gz
```


<span id="_3-3-第二步：配置工具"></span>
### 3.3 Step 2: Configure the tool

Go to the extracted folder and modify the configuration file **conf/sync.properties**.

```bash
cd starrocks-cluster-sync
vi conf/sync.properties
```


The file content is as follows:

```properties
If true, all tables will be synchronized only once, and the program will exit automatically after completion.
one_time_run_mode=false

source_fe_host=
source_fe_query_port=9030
source_cluster_user=root
source_cluster_password=
source_cluster_token=

target_fe_host=
target_fe_query_port=9030
target_cluster_user=root
target_cluster_password=

meta_job_interval_seconds=180
ddl_job_interval_seconds=15
ddl_job_batch_size=10
ddl_job_allow_drop_target_only=false
ddl_job_allow_drop_schema_change_table=true
ddl_job_allow_drop_inconsistent_partition=true
replication_job_interval_seconds=15
replication_job_batch_size=10

Comma-separated list of database names or table names like <db_name> or <db_name.table_name>
example: db1,db2.tbl2,db3
Effective order: 1. include 2. exclude
include_data_list=
exclude_data_list=
```


The parameter descriptions are as follows:


|Parameter name |Description |
|---|---|
|one_time_run_mode |Whether to enable one\-time synchronization mode. After enabling one\-time synchronization mode, the migration tool performs only full synchronization and does not perform incremental synchronization. |
|source_fe_host |IP address or FQDN of the source cluster FE. |
|source_fe_query_port |Query port (query_port) of the source cluster FE. |
|source_cluster_user |Username for logging in to the source cluster. This user must have SYSTEM\-level OPERATE permission. |
|source_cluster_password |Password for logging in to the source cluster. |
|source_cluster_token |Token of the source cluster. For instructions on how to obtain the cluster token, see the section below on obtaining the cluster token. |
|target_fe_host |IP address or FQDN of the target cluster FE. |
|target_fe_query_port |Query port (query_port) of the target cluster FE. |
|target_cluster_user |Username for logging in to the target cluster. This user must have SYSTEM\-level OPERATE permission. |
|target_cluster_password |Password for logging in to the target cluster. |
|meta_job_interval_seconds |The interval, in seconds, at which the migration tool retrieves metadata from the source and target clusters. You can use the default value for this item. |
|ddl_job_interval_seconds |The interval, in seconds, at which the migration tool executes DDL operations on the target cluster. You can use the default value for this item. |
|ddl_job_batch_size |The batch size used by the migration tool when executing DDL operations on the target cluster. You can use the default value for this item. |
|ddl_job_allow_drop_target_only |Whether the migration tool automatically deletes databases, tables, or partitions that exist only in the target cluster but not in the source cluster. The default is false, which means deletion is not enabled. You can use the default value for this item. |
|ddl_job_allow_drop_schema_change_table |Whether the migration tool automatically deletes tables with schema inconsistencies between the source and target clusters. The default is true, which means deletion is enabled. You can use the default value for this setting. The migration tool will automatically synchronize deleted tables during the synchronization process. |
|ddl_job_allow_drop_inconsistent_partition |Whether the migration tool automatically deletes partitions with inconsistent data distribution between the source and target clusters. The default is true, which means deletion is enabled. You can use the default value for this setting. The migration tool will automatically synchronize deleted partitions during the synchronization process. |
|replication_job_interval_seconds |The interval at which the migration tool triggers data synchronization tasks, in seconds. You can use the default value for this setting. |
|replication_job_batch_size |The batch size for data synchronization tasks triggered by the migration tool. You can use the default value for this setting. |
|include_data_list |For databases and tables that need to be migrated, separate multiple objects with commas (,). For example: db1,db2.tbl2,db3. This setting takes precedence over exclude_data_list. To migrate all databases and tables in the cluster, this setting does not need to be configured. |
|exclude_data_list |For databases and tables that do not need to be migrated, separate multiple objects with commas (,). For example: db1,db2.tbl2,db3. The include_data_list takes precedence over this setting. To migrate all databases and tables in the cluster, this setting does not need to be configured. |


<span id="_3-3-1-获取集群-token"></span>
#### 3.3.1 Obtain the cluster Token

You can obtain the cluster Token through the FE HTTP port or from the metadata of the FE node.


* **Obtain the cluster Token through the FE HTTP port**


Run the following command:

```bash
curl -v http://<fe_host>:8030/check
```



* `fe_host`: The IP address or FQDN of the cluster FE.

* `fe_http_port`: The HTTP port of the cluster FE.


The output is as follows:

```http
About to connect() to xxx.xx.xxx.xx port 8030 (#0)
Trying xxx.xx.xxx.xx...
Connected to xxx.xx.xxx.xx (xxx.xx.xxx.xx) port 8030 (#0)
GET /check HTTP/1.1
User-Agent: curl/7.29.0
Host: xxx.xx.xxx.xx:8030
Accept: /

< HTTP/1.1 200 OK
< content-length: 0
< cluster_id: yyyyyyyyyyy
< content-type: text/html
< token: wwwwwwww-xxxx-yyyy-zzzz-uuuuuuuuuu
< connection: keep-alive
< 
Connection #0 to host xxx.xx.xxx.xx left intact
```


The `token` field contains the Token for the current cluster.


* **Obtain the cluster Token from the metadata of the FE node**


Log in to the server where the FE node is located and run the following command:

```bash
cat fe/meta/image/VERSION | grep token
```


The output is as follows:

```properties
token=wwwwwwww-xxxx-yyyy-zzzz-uuuuuuuuuu
```


<span id="_3-4-第三步：启动迁移工具"></span>
### 3.4 Step 3: Start the migration tool

After completing the configuration, start the migration tool to begin data migration.

```bash
./bin/start.sh
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please make sure that the BE nodes of both the source and target clusters are connected via the network.</div>


* <div data-tips="true" data-tips-type="warning">During operation, the migration tool periodically checks whether the data in the target cluster is lagging behind the source cluster. If it is, a data migration task will be initiated.</div>


* <div data-tips="true" data-tips-type="warning">If new data continues to be imported into the source cluster, data synchronization will continue until the data in the target cluster is consistent with the source cluster.</div>


* <div data-tips="true" data-tips-type="warning">You can query tables in the target cluster that are in the process of migration, but please do not import new data (the current migration tool does not prohibit imports), as this will cause data inconsistency between the target and source clusters.</div>


* <div data-tips="true" data-tips-type="warning">Note: Data migration does not end automatically. You need to manually check and confirm that the migration is complete before stopping the migration tool.</div>



<span id="_3-5-第四步：迁移进度校验"></span>
### 3.5 Step 4: Verify migration progress

<span id="_3-5-1-查看迁移工具日志"></span>
#### 3.5.1 View migration tool logs

You can check the migration progress in the migration tool log **log/sync.INFO.log**.

Example:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ad61e06bcc11522c4160387c9948242.png) </span>

The main metrics are as follows:


* `Sync progress`: Data migration progress. Because the migration tool periodically checks whether the target cluster's data is lagging behind the source cluster, when the progress reaches 100%, it only indicates that data synchronization is complete for the current check cycle. If new data continues to be imported into the source cluster, the progress may decrease in the next check cycle.

* `total`: The total number of all types of Jobs for this migration operation.

* `ddlPending`: The number of DDL Jobs pending execution.

* `jobPending`: The number of data synchronization Jobs pending execution.

* `sent`: The number of data synchronization Jobs sent from the source cluster but not yet started. In theory, this value should not be too large. If you notice that this value continues to increase, please contact the development team.

* `running`: The number of data synchronization jobs currently in progress.

* `finished`: The number of data synchronization jobs completed successfully.

* `failed`: The number of data synchronization jobs that failed. Failed data synchronization jobs will be resent. Therefore, under normal circumstances, you can ignore this metric. If this value becomes large, please contact the development team.

* `unknown`: The number of jobs in an unknown state. In theory, this value should always be `0`. If this value is not `0`, please contact the development team.


<span id="_3-5-2-查看迁移事务状态"></span>
#### 3.5.2 View migration transaction status

The migration tool opens a transaction for each table. You can check the status of the transaction to understand the migration status of the table.

```sql
SHOW PROC "/transactions/<db_name>/running";
```


Here, `<db_name>` is the name of the database where the table resides.

<span id="_3-5-3-查看分区数据版本"></span>
#### 3.5.3 View partition data version

You can compare the data versions of corresponding partitions in the source and target clusters to determine the migration status of the partition.

```sql
SHOW PARTITIONS FROM <table_name>;
```


Here, `<table_name>` is the name of the table to which the partition belongs.

<span id="_3-5-4-查看数据量"></span>
#### 3.5.4 View data volume

You can compare the data volume between the source and target clusters to determine the migration status.

```sql
SHOW DATA;
```


<span id="_3-5-5-查看表行数"></span>
#### 3.5.5 View table row count

You can compare the row counts of tables in the source and target clusters to determine the migration status of each table.

```sql
SELECT 
  TABLE_NAME, 
  TABLE_ROWS 
FROM INFORMATION_SCHEMA.TABLES 
WHERE TABLE_TYPE = 'BASE TABLE' 
ORDER BY TABLE_NAME;
```


<span id="_3-5-6-实时任务"></span>
#### 3.5.6 Real\-time tasks

If this is a real\-time task, the data in the source cluster is continuously increasing, so the row counts and data volumes on both sides may not be exactly equal.

You can compare the row counts of partitions. If the data in historical partitions is consistent, it indicates that the data has been fully synchronized, and the data in the current day's partition does not need to be compared.

After switching real\-time write traffic, you can backtrack one day's data in the real\-time pipeline to ensure that no data is left behind in the real\-time partition for the current day.
