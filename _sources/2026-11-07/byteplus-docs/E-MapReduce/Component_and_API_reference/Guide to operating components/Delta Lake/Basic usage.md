---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/delta_lake_basic_usage"
---

This article introduces the commonly used basic command operations for the Delta Lake service in Volcano Engine E\-MapReduce (EMR).

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. An EMR engine with the Delta Lake service has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).

2. Currently, the Delta Lake component is only available to allowlisted users. You can apply for access via [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109210).


<span id="_2-初始化客户端"></span>
## 2 Initialize the client


1. [Log in to the EMR console](https://console.volcengine.com/emr).

2. Click to go to the **Cluster List \> Cluster Details \> Service List \> Delta Lake** service page.

3. In **Deployment Topology**, expand the component name.

4. Click the ECS ID of the cluster node to navigate to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password or key specified during cluster creation, and access the remote terminal.


Alternatively, use SSH to log in to the primary node of the cluster. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).


5. Run the following statements to initialize the client.


<span id="_2-1-spark-sql"></span>
### 2.1 Spark SQL

```shell
spark-sql \
    --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" \
    --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```


<span id="_2-2-spark-shell"></span>
### 2.2 Spark Shell

```shell
spark-shell \
    --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" \
    --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```


<span id="_2-3-pyspark"></span>
### 2.3 PySpark

The default Python environment used by PySpark is defined by the environment variable `PYSPARK_PYTHON` in `spark-env.sh`. EMR has already installed the delta package for the corresponding system version in this Python environment, so you do not need to install it using pip.

```shell
pyspark \
    --conf "spark.sql.extensions=io.delta.sql.DeltaSparkSessionExtension" \
    --conf "spark.sql.catalog.spark_catalog=org.apache.spark.sql.delta.catalog.DeltaCatalog"
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">If you do not use SQL features (such as saveAsTable), the two \-\-conf options in spark\-shell and pyspark can be omitted.</div>


2. <div data-tips="true" data-tips-type="warning">For PySpark, some features are provided by Spark itself, such as <code>spark.read.format("delta")</code> and <code>df.write.format("delta")</code>, which are natively supported in PySpark.</div>


   <div data-tips="true" data-tips-type="warning">Some features are unique to Delta, such as instantiating a Delta table object with <code>DeltaTable.forPath</code>. You need to clarify the relationship between the two (see the examples below).   </div>
   


In the following sections, our sample code will be provided using both Spark SQL and PySpark. For details, see:

<span id="_2-4-tos-支持"></span>
### 2.4 TOS support

EMR includes TOS support by default and provides automated authentication, so you do not need to enter AK.

You can use TOS in the same way as HDFS. For example, directly replace `hdfs://tmp/delta` with `tos://tmp/delta`.

If TOS support is lost due to unexpected configuration changes, simply add the following configuration item to the HDFS core\-site configuration:

```Plain
fs.AbstractFileSystem.tos.impl: com.volcengine.cloudfs.fs.TOS
fs.tos.impl: com.volcengine.cloudfs.fs.TosFileSystem
fs.tos.endpoint: <your_tos_endpoint>
```


<span id="_3-建表"></span>
## 3 Create tables

<span id="jump"></span>
### 3.1 Table types

Delta Lake supports creating tables using an external metastore or using a directory. For the former, some table information (such as table name and table path) will be stored in the external metastore. Additionally, as you will see below, to query using Hive, you need to create a Hive table in the metastore.

Therefore, we define the tables as follows:


1. Delta table: Refers to a table that does not depend on a metastore, with the schema stored in the underlying storage. Spark can query it by table path.

2. Spark table: Refers to an **internal or external table** created by Spark in the metastore, corresponding to a Delta table, which can be queried by table name in Spark.

3. Hive table: Refers to the **external table** created by Hive in the metastore corresponding to the Delta table, which can be queried using Hive SQL.


<span id="_3-2-直接建表"></span>
### 3.2 Direct table creation

<span id="_3-2-1-spark-sql-方式"></span>
#### 3.2.1 Spark SQL method

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">In this method, you need to enable Spark to access the Hive metastore. If you use the PySpark configuration provided by EMR, this has already been set up and no further action is required.</div>


2. <div data-tips="true" data-tips-type="warning"><strong>Tables created via the metastore method cannot be queried as Hive tables</strong>. Additionally, <strong>only the table name and table path in the table information are correct</strong>; other information, including the schema, is for reference only and is not guaranteed to be consistent with the actual schema of the Delta table.</div>



```sql
-- Method one: Create a Delta table in the directory specified by LOCATION and simultaneously create a Spark table
CREATE TABLE IF NOT EXISTS default.people (
    id INT,
    name STRING,
    age INT
) USING DELTA
LOCATION `/tmp/delta/people`
-- Method two: Create a Delta table directly in the specified directory
CREATE OR REPLACE TABLE delta.`/tmp/delta/people` (
    id INT,
    name STRING,
    age INT
) USING DELTA
```


<span id="_3-2-2-spark-python-api-方式"></span>
#### 3.2.2 Spark Python API method

```python
# Write a new table and Save it to an external metastore (Spark table)
df.write.format("delta").saveAsTable("default.people")
# Write or overwrite a table with the table path "/tmp/delta/people"
df.write.format("delta").mode("overwrite").save("/tmp/delta/people")
```


<span id="_3-3-将-hive-表转为-delta-表"></span>
### 3.3 Convert Hive table to Delta table

To convert an existing Hive table to a Delta table, use the CONVERT command directly:

<span id="_3-3-1-spark-sql-方式"></span>
#### 3.3.1 Spark SQL method

```Plain
CONVERT TO DELTA parquet.`<path-to-table>` [PARTITIONED BY (part int, part2 int)]
```


<span id="_3-3-2-spark-python-api-方式"></span>
#### 3.3.2 Spark Python API method

```Plain
DeltaTable deltaTable = DeltaTable.convertToDelta(spark, "parquet.`<path-to-table>`", "part int, part2 int");
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once the CONVERT operation is performed on a Hive table to convert it to a Delta table, you must use the VACUUM command provided by Delta (with the version expiration time set to 0) to restore the Delta table to a Hive table. If you delete the Delta table metadata directly without performing this operation, the table will be damaged and cannot be recovered. Similarly, <strong>Delta does not allow any direct manipulation of metadata that bypasses Delta itself</strong>.</div>


<div data-tips="true" data-tips-type="warning">For more commands, see: <a href="https://docs.delta.io/latest/delta-utility.html">https://docs.delta.io/latest/delta\-utility.html</a></div>


<span id="_4-查询"></span>
## 4 Query

**Spark SQL method**

```sql
-- Query by specifying the table name
SELECT * FROM default.people
-- Query by table path
SELECT * FROM delta.`/tmp/delta/people`
```


**Spark Python API method**

```python
# Query by specifying the table name
spark.table("default.people")
# Query by table path
spark.read.format("delta").load("/tmp/delta/people")
```


<span id="_4-1-使用-hive-查询"></span>
### 4.1 Query using Hive

EMR (version 1.4.0 and above) supports Hive reading Delta tables through the [Delta-Connectors](https://github.com/delta-io/connectors) project. Caution: This project does not support Hive writing Delta tables.


1. Start the Hive client and execute the following statements to configure:


```sql
SET hive.input.format=io.delta.hive.HiveInputFormat;
SET hive.tez.input.format=io.delta.hive.HiveInputFormat;
```



2. Create a **mapping table** for the Delta table in the Hive metastore (ensure the Delta table is already created before creating the mapping table). This mapping table is an **external table**, for example:


```sql
CREATE EXTERNAL TABLE deltaTable(col1 INT, col2 STRING)
STORED BY 'io.delta.hive.DeltaStorageHandler'
LOCATION 'tos://your_bucket/delta/table/path'
```



3. Query using Hive SQL.


Note: Hive tables, Delta tables, and Spark tables created in the metastore, although they share the same physical entity, are considered **three tables** (see: [3.1 Table types](https://docs.byteplus.com/docs/E-MapReduce/109210#jump)). Therefore, the following limitations exist:


* Hive cannot read tables created by Spark in the metastore.

* Spark cannot read mapping tables created by Hive.


Therefore, when the schema of the Delta table changes, the tables created by Hive and Spark must synchronize their schema changes.


* For Hive, since it is an external table, you only need to DROP and then CREATE TABLE again.

* For Spark, if it is a Spark\-created Managed Table, you cannot DROP and CREATE as with Hive (this would delete the data), so it is best to perform all operations through the table (including schema changes). Otherwise, it is better to use external tables as with Hive.


<span id="_4-2-使用-presto-查询"></span>
### 4.2 Query using Presto

Presto (version 0.269 and above) natively supports **reading** Delta tables. For details, please refer to the [official page](https://prestodb.io/docs/current/connector/deltalake.html).

<span id="_4-3-使用-trino-查询"></span>
### 4.3 Query using Trino

Trino (version 373 and above) natively supports **reading and writing** Delta tables. For details, please refer to the [official page](https://trino.io/docs/current/connector/delta-lake.html).

<span id="_5-删除"></span>
## 5 Delete

**Spark SQL method**

```sql
-- Delete by table name
DELETE FROM people WHERE age < 20
-- Delete by table path
DELETE FROM delta.`/tmp/delta/people` WHERE age < 20
```


**Spark Python API method**

```python
from delta.tables import *
from pyspark.sql.functions import *
# Obtain a table by specifying the table path
deltaTable = DeltaTable.forPath(spark, '/tmp/delta/people-10m')
# Delete method one
deltaTable.delete("age < 20")
# Delete method two
deltaTable.delete(col('age') < '20')
```


<span id="_6-更新"></span>
## 6 Update

**Spark SQL method**

```sql
-- Update by table name
UPDATE people SET age = 20 WHERE name = 'zhangsan';
-- Update by table path
UPDATE delta.`/tmp/delta/people` SET age = 20 WHERE name = 'zhangsan';
```


**Spark Python API method**

```python
from delta.tables import *
from pyspark.sql.functions import *

# Obtain a table by specifying the table path
deltaTable = DeltaTable.forPath(spark, '/tmp/delta/people-10m')

# Update method one
deltaTable.update(
  condition = "name = 'zhangsan'",
  set = { "age": "20" }
)
# Update method two
deltaTable.update(
  condition = col('name') == 'zhangsan',
  set = { "age": "20" }
)
```


<span id="_7-合并"></span>
## 7 Merge

Compared to insert, update, and delete operations, merge provides a more efficient way to batch “merge” data from one table into another, rather than performing insert, update, or delete operations on each row individually in the second table.

Merging is useful in many scenarios, such as merging upstream\-generated data into the current table at a specified time granularity to ensure the current table remains up\-to\-date.

**Spark SQL method**

```sql
MERGE INTO people
USING peopleupdates
ON people.id = peopleupdates.id
WHEN MATCHED THEN
  UPDATE SET
    id = peopleupdates.id,
    name = peopleupdates.name,
    age = peopleupdates.age
WHEN NOT MATCHED
  THEN INSERT (
    id,
    name,
    age
  )
  VALUES (
    peopleupdates.id,
    peopleupdates.name,
    peopleupdates.age,
  )
```


**Spark Python API method**

```python
from delta.tables import *

# Obtain the table by specifying the table path
deltaTablePeople = DeltaTable.forPath(spark, '/tmp/delta/people')
deltaTablePeopleUpdates = DeltaTable.forPath(spark, '/tmp/delta/people-updates')

dfUpdates = deltaTablePeopleUpdates.toDF()

# Execute the merge operation
deltaTablePeople.alias('people') \
  .merge(
    dfUpdates.alias('updates'),
    'people.id = updates.id'
  ) \
  .whenMatchedUpdate(set =
    {
      "id": "updates.id",
      "name": "updates.name",
      "age": "updates.age"
    }
  ) \
  .whenNotMatchedInsert(values =
    {
      "id": "updates.id",
      "name": "updates.name",
      "age": "updates.age"
    }
  ) \
  .execute()
```


<span id="_8-流式读写-delta-表"></span>
## 8 Streaming read and write for Delta tables

<span id="_8-1-spark-streaming"></span>
### 8.1 Spark Streaming

<span id="_8-1-1-source"></span>
#### 8.1.1 Source

```scala
spark.readStream
  .format("delta")
  .option(<option_key>, <option_value>)
  .load("/tmp/delta_table")
```


Common option parameters:


|Parameters |Note |
|---|---|
|**maxFilesPerTrigger** |The maximum number of files processed in a single batch; the default value is 1000. |
|**maxBytesPerTrigger** |The maximum amount of data processed in a single batch. Caution that this maximum value may be slightly exceeded and is not a strict limit. In addition, if the Trigger policy is Trigger.Once, this option will be ignored. |
|**ignoreDeletes** |After this option is set to true, deletions of partitions will not be responded to. |
|**ignoreChanges** |After this option is set to true, data will be re\-consumed when changes occur (such as UPDATE, MERGE INTO, DELETE (within partitions), or OVERWRITE). This may cause data duplication, so you need to handle duplicate data yourself. |


<span id="_8-1-2-sink"></span>
#### 8.1.2 Sink

Append mode (default mode):

```scala
df.writeStream
  .format("delta")
  .outputMode("append")
  .option("checkpointLocation", "/tmp/delta_table/_checkpoints")
  .start("/tmp/delta_table")
  
 // toTable is a new syntax in Spark 3.1; for versions below 3.1, use the `table()` method
 df.writeStream
   .outputMode("append")
   .option("checkpointLocation", "/tmp/delta/events/_checkpoints/")
   .toTable("delta_table")
```


Complete mode:

```scala
spark.readStream
  .format("delta")
  .load("/tmp/delta_table")
  .select("name","sales")
  .groupBy("name")
  .agg(sum("sales"))
  .writeStream
  .format("delta")
  .outputMode("complete")
  .option("checkpointLocation", "/tmp/delta_table_output/_checkpoints")
  .start("/tmp/delta_table_output")
```


<span id="_8-2-flink"></span>
### 8.2 Flink

EMR (version 1.4.0 and above) supports Flink reading and writing Delta tables through the [Delta-Connectors](https://github.com/delta-io/connectors) project.

<span id="_8-2-1-source"></span>
#### 8.2.1 Source

```java
// For bounded streams (batch), use the forBoundedRowData API.
DataStream<RowData> createBoundedDeltaSourceWithTimeTravel(
        StreamExecutionEnvironment env,
        String deltaTablePath) {

    DeltaSource<RowData> deltaSource = DeltaSource
        .forBoundedRowData(
            new Path(deltaTablePath),
            new Configuration())
        // could also use `.versionAsOf(314159)`
        .timestampAsOf("2022-06-28 04:55:00")
        .build();

    return env.fromSource(deltaSource, WatermarkStrategy.noWatermarks(), "delta-source");
}

// For unbounded streams, use the forContinuousRowData API.
public DataStream<RowData> createContinuousDeltaSourceWithTimeTravel(
        StreamExecutionEnvironment env,
        String deltaTablePath) {

    DeltaSource<RowData> deltaSource = DeltaSource
        .forContinuousRowData(
            new Path(deltaTablePath),
            new Configuration())
        // could also use `.startingVersion(314159)`
        .startingTimestamp("2022-06-28 04:55:00")
        .build();

    return env.fromSource(deltaSource, WatermarkStrategy.noWatermarks(), "delta-source");
}
```


Common option parameters:


|Parameters |Note |
|---|---|
|Bounded mode ||
|versionAsOf |Specify the version of the Delta table to read. |
|timestampAsOf |Specify the timestamp of the Delta table to read. |
|columnNames |Specify which columns of the Delta table to read; if not specified, all columns will be read. |
|Unbounded mode ||
|columnNames |Specify which columns of the Delta table to read; if not specified, all columns will be read. |
|startingVersion |Stream read the Delta table starting from this version. |
|startingTimestamp |Read the Delta table starting from this timestamp. |
|updateCheckIntervalMillis |The interval for checking changes in the Delta table. |
|ignoreDeletes |When set to True, deletions of data will not be responded to. |
|ignoreChanges |When set to True, data will be re\-consumed when changes occur (such as UPDATE, MERGE INTO, DELETE (within partitions), or OVERWRITE). This may cause data duplication, so you need to handle duplicate data yourself. |


<span id="_8-2-2-sink"></span>
#### 8.2.2 Sink

```java
import io.delta.flink.sink.DeltaBucketAssigner;
import io.delta.flink.sink.DeltaSinkBuilder;

public DataStream<RowData> createDeltaSink(
        DataStream<RowData> stream,
        String deltaTablePath,
        RowType rowType) {
    String[] partitionCols = { "partCol" };
    DeltaSink<RowData> deltaSink = DeltaSink
        .forRowData(
            new Path(deltaTablePath),
            new Configuration(),
            rowType)
        .withPartitionColumns(partitionCols)
        .build();
    stream.sinkTo(deltaSink);
    return stream;
}
```


<span id="_9-使用-tos-作为存储底层"></span>
## 9 Using TOS as the storage backend

TOS provides a FileSystem implementation compatible with the HDFS FileSystem API, and relevant configurations have already been made in HDFS, so **TOS can be used as the underlying storage for Delta tables just like HDFS**. Here is an example:

Spark SQL

```sql
CREATE TABLE delta_test (
    id int,
    name string
) USING delta
LOCATION 'tos://tmp/delta_test';

INSERT INTO delta_test VALUES (1, 'zhangsan'),(2, 'lisi');

SELECT * FROM delta_test;

-- Result display:
1        zhangsan
2        lisi
Time taken: 0.921 seconds, Fetched 2 row(s)
```


PySpark

```python
from pyspark.sql.types import StructType,StructField, StringType, IntegerType

data = [(1, 'zhangsa'), (2, 'lisi')]
schema = StructType([ \
    StructField("id", IntegerType(), True), \
    StructField("name", StringType(), True), \
])

df = spark.createDataFrame(data=data,schema=schema)
# If you do not need to create a table, you can directly use save('/path/to/your/table')
df.write.format('delta').saveAsTable('delta_test', path='tos://tmp/delta_test')

df_read = spark.read.format('delta').load('tos://tmp/delta_test')
df_read.show()

# Result display
+---+-------+
| id|   name|
+---+-------+
|  1|zhangsa|
|  2|   lisi|
+---+-------+
```
