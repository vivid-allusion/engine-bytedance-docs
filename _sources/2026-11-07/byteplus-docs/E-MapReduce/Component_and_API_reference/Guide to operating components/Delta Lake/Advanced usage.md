---
title: "Advanced usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/delta_lake_advanced_usage"
---

<span id="_1-查阅历史版本"></span>
## 1 View historical versions

<span id="_1-1-历史版本信息"></span>
### 1.1 Historical version information

**Spark SQL method**

```sql
-- Query directly by path
DESCRIBE HISTORY '/path/to/delta/' [LIMIT <n>]
-- Query by delta prefix
DESCRIBE HISTORY delta.`/path/to/delta/` [LIMIT <n>]
-- Query by table name
DESCRIBE HISTORY deltaTable [LIMIT <n>]
```


**Spark Python API method**

```python
from delta.tables import *


# Obtain the table by specifying the table path
deltaTable = DeltaTable.forPath(spark, pathToTable)
# Query historical versions. The parameter n is optional and specifies the number of records to retrieve. If n is not specified, all records will be retrieved.
lastOperationDF = deltaTable.history(<n>)
```


<span id="_1-2-历史版本查询"></span>
### 1.2 Historical version query

**Spark SQL method**

```sql
-- Query historical versions by timestamp
SELECT * FROM table_name TIMESTAMP AS OF timestamp_expression
-- Query historical versions by version number
SELECT * FROM table_name VERSION AS OF version
```


**Spark Python API method**

```python
# Query historical versions by timestamp
df1 = spark.read.format("delta").option("timestampAsOf", timestamp_string).load("/tmp/delta/people")
# Query historical versions by version number
df2 = spark.read.format("delta").option("versionAsOf", version).load("/tmp/delta/people")
```


Among them:


* The format of `timestamp_expression` is

   * `'2018-10-18T22:15:12.013Z'`, which can be converted to the standard timestamp format

   * `cast('2018-10-18 13:36:32 CEST' as timestamp)`

   * `'2018-10-18'`, date

   * `current_timestamp() - interval 12 hours` time expression

   * `date_sub(current_date(), 1)` time expression

   * Other time formats that can be converted to a timestamp

* `version` can be obtained using the `DESCRIBE HISTORY` command.


<span id="_2-查阅表的详情"></span>
## 2 View table details

**Spark SQL method**

```sql
-- Obtain table information by path
DESCRIBE DETAIL '/path/to/delta/'
-- Obtain table information by table name
DESCRIBE DETAIL deltaTable
```


**Spark Python API method**

```python
from delta.tables import *

# Obtain the table by specifying the table path
deltaTable = DeltaTable.forPath(spark, pathToTable)
# Query table property details
detailDF = deltaTable.detail()
```


<span id="_3-表管理"></span>
## 3 Table management

<span id="_3-1-清理过期数据"></span>
### 3.1 Clean up expired data

<span id="_3-1-1-delta-lake-的保存期机制"></span>
#### 3.1.1 Delta Lake retention mechanism

Delta Lake provides historical version rollback functionality and records all modifications to the table. Each table change generates a new log file and may also generate new data files. For log files and data files, Delta Lake introduces a retention mechanism:


* For log files, data within 30 days is retained by default. Expired data is automatically deleted, and you do not need to take any action.

* For data files, the default retention period is 7 days. Expired data must be deleted manually by executing the VACUUM command.


Users can configure `delta.logRetentionDuration = "interval <interval>"` and `delta.deletedFileRetentionDuration = "interval <interval>"` to set the retention period for log files and data files, respectively. See below for specific configuration methods:[4.2.1 Table configuration](https://docs.byteplus.com/docs/E-MapReduce/109209#jump).

<span id="_3-1-2-清理过期数据"></span>
#### 3.1.2 Clean up expired data

**Spark SQL method**

```sql
-- Perform cleanup actions by table name. RETAIN 100 HOURS means cleaning up data older than 100 hours.
VACUUM deltaTable [RETAIN 100 HOURS]  -- vacuum files not required by versions older than the default retention period
-- Perform cleanup actions by path string
VACUUM '/path/to/delta/' [RETAIN 100 HOURS]-- vacuum files in path-based table
-- Perform cleanup actions by delta prefix Perform cleanup actions using the prefix
VACUUM delta.`/path/to/delta/` [RETAIN 100 HOURS]
-- Only lists cleanup details without actually performing the cleanup.
VACUUM deltaTable DRY RUN
```


**Spark Python API method**

```python
from delta.tables import *

# Obtain the table by specifying the table path
deltaTable = DeltaTable.forPath(spark, pathToTable)
# Or obtain the table by specifying the table name
deltaTable = DeltaTable.forName(spark, tableName)
# Clean up historical data exceeding the retention period
deltaTable.vacuum()
# Clean up historical data exceeding 100 hours (relative to the table version)
deltaTable.vacuum(100)
```


<span id="_3-2-小文件合并（compaction，bin-packing）"></span>
### 3.2 Small file compaction (Compaction, bin\-packing)

Writing to Delta in streaming mode usually generates a large number of small files. The finer the time granularity, the smaller the files. In addition, if you execute a complex SQL statement that ultimately writes to Delta, the written data may also generate a large number of small files due to excessive partitioning.

The existence of small files can cause many issues, such as slower metadata processing, increased disk random reads during execution due to file fragmentation, excessive small tasks caused by overly high parallelism settings, and more. All of these can significantly reduce Spark query performance, so it is necessary to perform compaction. Delta performs this operation using the optimize command.

**Spark SQL method**

```sql
-- Optimize by specifying the path
OPTIMIZE '/path/to/delta/' [WHERE CLAUSE]
-- Optimize by table name
OPTIMIZE deltaTable [WHERE CLAUSE]
-- By delta. Optimize the prefix
OPTIMIZE delta.`/path/to/delta/` [WHERE CLAUSE]
```


**Spark Python API method**

```python
from delta.tables import *

# Obtain the table by specifying the table path
deltaTable = DeltaTable.forPath(spark, pathToTable)
# Or obtain the table by specifying the table name
deltaTable = DeltaTable.forName(spark, tableName)
# Perform optimization, where 'where' is optional
deltaTable.optimize().where("date='2021-11-18'").executeCompaction()
```


<span id="_3-2-data-skipping-与-z-order"></span>
### 3.2 Data skipping and Z\-Order

Data skipping is a method that uses statistical information to filter data, enabling a large amount of data to be filtered out during table scans based on filter conditions, thereby accelerating queries. Delta's statistics are column\-based, file\-level MIN and MAX statistics. If a column is relatively ordered across multiple files, multiple files can be filtered out based on the statistics of that column. Conversely, if column values are evenly distributed across multiple files, the filtering effect will be greatly reduced or even nonexistent. For a multi\-dimensional table, if sorted by multiple dimensions, the filtering effect of the earlier dimensions will be better, while the filtering effect of the later dimensions will be worse.

Z\-Order provides a method to balance the sorting effect across all dimensions. Z\-Order is an algorithm that enables each column involved in sorting to be **locally** relatively ordered, so filtering by any column involved in sorting can achieve a good filtering effect.

Delta Lake provides the `OPTIMIZE` statement with the `ZORDER BY` clause to perform Z\-Order sorting on tables.

**Spark SQL method**

```sql
OPTIMIZE events [WHERE CLAUSE] ZORDER BY (<columns>)
```


**Spark Python API method**

```python
from delta.tables import *

# Obtain the table by specifying the table path
deltaTable = DeltaTable.forPath(spark, pathToTable)
# Or obtain the table by specifying the table name
deltaTable = DeltaTable.forName(spark, tableName)
# Perform optimization, where 'where' is optional
deltaTable.optimize().where("date='2021-11-18'").executeZOrderBy(<columns>)
```


<span id="_3-4-审计功能"></span>
### 3.4 Audit features

Delta Lake's history feature provides detailed audit information for tables. When executing `DESCRIBE HISTORY` or calling the `history()` function in the API, the returned fields include but are not limited to


* userId

* userName

* operation

* job

* notebook

* clusterId

* ...


and other fields. These fields help administrators discover and manage the history of jobs submitted by regular users and optimize cluster management accordingly.

<span id="_4-delta-表配置"></span>
## 4 Delta table configuration

<span id="_4-1-配置说明"></span>
### 4.1 Configuration instructions

You can configure Delta tables in multiple ways:


* Configure by specifying `TBLPROPERTIES` when creating the table.

* Add default configurations through Spark's configuration file.

* Configure by modifying `TBLPROPERTIES` after table creation.

* Configure in the session when querying with the CLI.


Delta tables support three configuration formats:


1. `delta.<property>`: Used for configuration via `TBLPROPERTIES`.

2. `spark.databricks.delta.properties.defaults.<property>`: Used to set the **default** configuration for the table via Spark SQL. This will be filled into the table as the default value for the corresponding configuration item at table creation. If this configuration is not set, Delta's default configuration will be used. In other words, it is equivalent to "`delta.defaults.<property>`", but for certain reasons, `spark.databricks.delta.properties.defaults.` is used. This prefix.

3. `spark.databricks.delta.<property>`: **Runtime** configuration for Spark SQL when reading and writing Delta tables.


Both 1 and 2 are **table\-level configurations**; 3 is a Spark **engine configuration**.

The priority order for table configurations, from highest to lowest, is as follows:


1. Explicitly set table properties using `TBLPROPERTIES`.

2. The user sets the default table configuration in the session by using `set spark.databricks.delta.properties.defaults.<property> = xxx`.

3. The user sets `spark.databricks.delta.properties.defaults.<property>` in spark\-default\-conf.


If using other engines, it is recommended to configure the table by explicitly specifying `TBLPROPERTIES`.

For 3, it affects the execution behavior of Spark SQL.

<span id="_4-2-常用配置列表"></span>
### 4.2 Common configuration list

<span id="jump"></span>
#### 4.2.1 Table configuration

Note: In the following,refers to `delta` or `spark.databricks.delta.properties.defaults`.


|Configuration item |Note |
|---|---|
|.logRetentionDuration |The retention period for log files. The default is 30 days. |
|.deletedFileRetentionDuration |The retention period for data files. The default is 7 weeks. |
|.checkpointInterval |Set the checkpoint interval for log files. The default is 10. |
|.appendOnly |Set the table to appendOnly. In this case, you can delete and append data, but cannot update data. Delta optimizes appendOnly tables. If you do not need to update or delete data, it is recommended to set this value. |
|.enableChangeDataFeed |Whether to enable the ChangeDataFeed feature. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>It is strongly discouraged</strong> to set <code>deletedFileRetentionDuration</code> to a small value to achieve faster data cleanup. For example, in some cases where historical versions are not needed, this value is set to 1h or even 0 to allow rapid cleanup of historical versions. In such cases, jobs with longer execution times may fail!</div>


<span id="_4-2-2-spark-sql-引擎配置"></span>
#### 4.2.2 Spark SQL engine configuration

Note: In the following,refers to `spark.databricks.delta`.


|Configuration item |Note |
|---|---|
|.stats.collect |Whether to collect statistics. The default is true. |
|.stats.skipping |Whether to enable the data skipping feature. The default is true. |
|.maxCommitAttempts |The maximum number of retries when a commit fails. The default is 10000000. |
|.optimize.minFileSize |Files smaller than this size will be merged. The default value is 1024 \* 1024 \* 1024. |
|.optimize.maxFileSize |The target maximum size for merged files. The default is 1024 \* 1024 \* 1024. |
|.optimize.maxThreads |The number of threads enabled when performing the optimize operation. The default is 15. |
|.vacuum.parallelDelete.enabled |Whether to execute vacuum in parallel. The default is false. Parallel execution is recommended for large tables. |
|.vacuum.parallelDelete.parallelism |The number of threads used when running vacuum in parallel. |
