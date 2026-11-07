---
title: "Data export"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Data_export"
---

<span id="_1-导出概述"></span>
## Overview of data export

StarRocks supports four methods for exporting data:


|Export method |Description |Supported data formats |Supported storage systems |
|---|---|---|---|
|INSERT INTO FILES export |Export the StarRocks table or query results using the INSERT statement. |parquet |TOS/HDFS |
|Export export |Export data using the StarRocks EXPORT statement. |CSV |TOS/HDFS |
|Spark Connector export |Export data by querying StarRocks table data with Spark. |Any format supported by Spark |Any address supported by Spark, including TOS, HDFS, JDBC, and other destinations |
|Flink Connector export |Export data by querying StarRocks table data with Flink. |Any format supported by Flink |Any address supported by Flink, including TOS, HDFS, JDBC, and other destinations |


<span id="_2-使用insert-into-files导出"></span>
## INSERT INTO FILES export

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method only supports StarRocks version 3.2.x and above.</div>


<div data-tips="true" data-tips-type="warning">Export of LargeInt type is not supported.</div>


INSERT INTO FILES allows writing query results to external storage systems, so StarRocks tables can be exported using this method. The supported external storage systems are HDFS or TOS.

<span id="_2-1-语法"></span>
### Syntax

```sql
INSERT INTO 
FILES(
    "path" = "s3://bucketName/sr_export/",
    "format" = "parquet",
    "aws.s3.region" = "cn-beijing",
    "aws.s3.endpoint" = "https://tos-s3-cn-beijing.ivolces.com",
    "aws.s3.use_aws_sdk_default_behavior" = "false",
    "aws.s3.use_instance_profile" = "false",
    "aws.s3.access_key" = "xxx",
    "aws.s3.secret_key" = "yyy==",
    "compression" = "zstd",
    "single" = "true"
)
SELECT * FROM tb_demo;
```


<span id="_2-2-参数说明"></span>
### Parameter note


|Parameters |Required |Note |
|---|---|---|
|path |Yes |The export data path. When exporting to TOS, the path is |
|format |Yes |The output data format. Currently, only parquet format is supported. |
|compression |Yes |The compression format used,<br><br><br>* `uncompressed`: No compression algorithm is used.<br><br>* `gzip`: The gzip compression algorithm is used.<br><br>* `brotli`: The Brotli compression algorithm is used.<br><br>* `zstd`: The Zstd compression algorithm is used.<br><br>* `lz4`: The LZ4 compression algorithm is used. |
|max_file_size |No |The maximum size of a single file when exporting as multiple files. Supports configuring the default value of 1GB. |
|single |No |Whether to export to a single data file. The default is false. |
|partition_by |No |This property can be set when it is necessary to partition exported data files by a specific column. After setting, the output directory will be divided into different subdirectories based on the values of the column specified by partition_by. |
|aws.s3.access_key |No |The ak for accessing TOS. |
|aws.s3.secret_key |No |The sk for accessing TOS. |
|aws.s3.region |No |The region where the TOS bucket is located. |
|aws.s3.endpoint |No |The S3\-compatible endpoint of the TOS service. |
|aws.s3.enable_ssl |No |Whether to use SSL when accessing TOS. |
|aws.s3.use_instance_profile |No |To access TOS using instance_profile mode, this must be set to true. When using instance_profile mode, ak and sk do not need to be specified. |
|aws.s3.enable_path_style_access |No |Whether to use path style access mode. |


<span id="_2-3-示例"></span>
### Example

```sql
INSERT INTO 
FILES(
  "path" = "s3://bucketName/sr_export/",
    "format" = "parquet",
    "aws.s3.region" = "cn-beijing",
    "aws.s3.endpoint" = "https://tos-s3-cn-beijing.ivolces.com",
    "aws.s3.use_aws_sdk_default_behavior" = "false",
    "aws.s3.use_instance_profile" = "false",
    "aws.s3.access_key" = "xxx",
    "aws.s3.secret_key" = "yyy==",
    "compression" = "zstd",
    "single" = "true"
)
SELECT * FROM tb_demo;
```


<span id="_3-export导出"></span>
## Export export

<span id="_3-1-参数配置"></span>
### Parameter configuration

FE can configure export\-related parameters to control export task timeout and more.


* `export_checker_interval_second`: The scheduling interval of the export job scheduler. The default is 5 seconds.

* `export_running_job_num_limit`: The limit on the number of export jobs running concurrently. If this limit is exceeded, jobs enter a waiting state after completing `snapshot`. The default is 5. This parameter value can be adjusted while export jobs are running.

* `export_task_default_timeout_second`: The timeout duration for export jobs. The default is 2 hours. This parameter value can be adjusted while export jobs are running.

* `export_max_bytes_per_be_per_task`: The maximum amount of data exported by each export subtask on each BE, used to split export jobs for parallel processing. Calculated based on compressed data volume, the default is 256 MB.

* `export_task_pool_size`: The size of the export subtask thread pool, that is, the maximum number of subtasks allowed to run in parallel in the thread pool. The default is 5.


<span id="_3-2-操作步骤"></span>
### procedure

<span id="_3-2-1-提交导出作业"></span>
#### Submit export job

Syntax:

```sql
EXPORT TABLE <table_name>
[PARTITION (<partition_name>[, ...])]
[(<column_name>[, ...])]
TO <export_path>
[opt_properties]
WITH BROKER
[broker_properties]
```


Example:

```sql
EXPORT TABLE demo.tb_demo 
(c1, c2, c3, c4, c5, c6)
TO "s3a://bucketName/sr_export/" 
PROPERTIES
(
    "column_separator"=",",
    "load_mem_limit"="2147483648"
)
WITH BROKER
(
    "aws.s3.region" = "cn-beijing",
    "aws.s3.endpoint" = "https://tos-s3-cn-beijing.ivolces.com",
    "aws.s3.use_aws_sdk_default_behavior" = "false",
    "aws.s3.use_instance_profile" = "false",
    "aws.s3.access_key" = "xxx",
    "aws.s3.secret_key" = "yyy=="
);
```


<span id="_3-2-2-查看导出作业"></span>
#### View export jobs

SHOW EXPORT can be used to view submitted export jobs and their status.

Syntax:

```sql
SHOW EXPORT
[ FROM <db_name> ]
[
WHERE
    [ QUERYID = <query_id> ]
    [ STATE = { "PENDING" | "EXPORTING" | "FINISHED" | "CANCELLED" } ]
]
[ ORDER BY <field_name> [ ASC | DESC ] [, ... ] ]
[ LIMIT <count> ]
```


Example:

```sql
MySQL [demo]> SHOW EXPORT FROM demo;
+-------+--------------------------------------+-----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+---------------------+---------------------+------------+---------+----------+
| JobId | QueryId                              | State     | Progress | TaskInfo                                                                                                                                                                                               | Path                        | CreateTime          | StartTime           | FinishTime | Timeout | ErrorMsg |
+-------+--------------------------------------+-----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+---------------------+---------------------+------------+---------+----------+
| 10329 | 3f0fe574-e100-11ee-821b-00163e5b1b2a | FINISHED  | 100%     | {"partitions":["*"],"column separator":",","columns":["c1","c2","c3","c4","c5","c6"],"tablet num":6,"broker":"","coord num":1,"db":"demo","tbl":"tb_demo","row delimiter":"\n","mem limit":2147483648} | s3a://bucketName/sr_export/ | 2024-03-13 14:09:26 | 2024-03-13 14:09:28 | NULL       | 7200    | NULL     |
+-------+--------------------------------------+-----------+----------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+---------------------+---------------------+------------+---------+----------+
```


<span id="_3-2-3-查看导出作业的状态"></span>
#### View the status of export jobs

SHOW EXPORT can specify a WHERE clause to view the execution status of export jobs for a specific QueryId or a specific status.

```sql
SHOW EXPORT WHERE queryid = "b560e5fa-e100-11ee-821b-00163e5b1b2a";
```


<span id="_3-2-4-取消导出作业"></span>
#### Cancel export job

To cancel an export job, use the CANCEL EXPORT statement to cancel an export job that is currently running.

Syntax:

```sql
CANCEL EXPORT
[FROM db_name]
WHERE QUERYID = "query_id"
```


Example:

```sql
CANCEL EXPORT WHERE queryid = "b560e5fa-e100-11ee-821b-00163e5b1b2a";
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">Only export jobs that are currently running can be canceled.</div>


2. <div data-tips="true" data-tips-type="warning">EXPORT permission for the corresponding table is required to cancel.</div>



<span id="_4-spark-connector导出"></span>
## Spark Connector export

Spark can be used to query data stored in StarRocks, enabling data export from StarRocks.

<span id="_4-1-基本原理"></span>
### Basic principle

The Spark Driver obtains table\-related meta information from StarRocks FE, including the list of tablets to query, the BE addresses where the tablets are located, and more. Then the Spark Executor sends an RPC request to the corresponding BE to obtain tablet data.

<span id="_4-2-前置条件"></span>
### prerequisites


* The StarRocks table already exists.

* The Spark cluster and StarRocks cluster are network\-connected.


<span id="_4-3-使用示例"></span>
### Example usage

<span id="_4-3-1-spark-sql"></span>
#### Spark SQL


1. Create a StarRocks view in Spark SQL.


```sql
spark-sql> CREATE TEMPORARY VIEW tb_starrocks
           USING starrocks
           OPTIONS
           (
               "starrocks.table.identifier" = "demo.tb_demo",
               "starrocks.fe.http.url" = "<fe_host>:<fe_http_port>",
               "starrocks.fe.jdbc.url" = "jdbc:mysql://<fe_host>:<fe_query_port>",
               "starrocks.user" = "test",
               "starrocks.password" = "xxx"
           );
```



2. Run an INSERT statement to export StarRocks table data.

   dest_table can be any table supported by Spark. Depending on the storage path, the storage system can be HDFS or TOS.


```sql
spark-sql> INSRT INTO dest_table SELECT * FROM tb_starrocks;
```


<span id="_4-3-2-spark-dataframe"></span>
#### Spark DataFrame


1. Run spark shell and execute the following statements.


```sql
scala> val df = spark.read.format("starrocks")
           .option("starrocks.table.identifier", s"demo.tb_demo")
           .option("starrocks.fe.http.url", s"<fe_host>:<fe_http_port>")
           .option("starrocks.fe.jdbc.url", s"jdbc:mysql://<fe_host>:<fe_query_port>")
           .option("starrocks.user", s"test")
           .option("starrocks.password", s"xxx")
           .load()
```



2. Execute the following statements to query data from the StarRocks table.

   Select csv, json, parquet, or orc according to the required data format. The path can be set to an HDFS address or a TOS address.


```sql
scala> df.write.format("csv").save(filepath)
```



3. To export only part of the StarRocks data, specify starrocks.filter.query when creating the dataFrame.


```sql
scala> val df = spark.read.format("starrocks")
       .option("starrocks.table.identifier", s"demo.tb_demo")
       .option("starrocks.fenodes", s"<fe_host>:<fe_http_port>")
       .option("user", "test")
       .option("password", "xxx")
       .option("starrocks.filter.query", "k=7 and dt='2022-01-02 08:00:00'")
       .load()
```


<span id="_5-flink-connector导出"></span>
## Flink Connector export

StarRocks provides a self\-developed Apache Flink® Connector (StarRocks Connector for Apache Flink®), which supports batch reading of data from a StarRocks cluster via Flink.

<span id="_5-1-基本原理"></span>
### Basic principle

When StarRocks Flink Connector queries StarRocks data, JobManager obtains the query plan from FE, and then TaskManager sends an RPC request to the corresponding BE to retrieve tablet data.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d8486231ff00a7d8a95cddeb7a19730.png" width="737px" /></div>


<span id="_5-2-前置条件"></span>
### prerequisites


* The StarRocks table already exists.

* The Spark cluster and StarRocks cluster are network\-connected.


<span id="_5-3-使用样例"></span>
### Usage example

<span id="_5-3-1-使用-flink-sql-读取数据"></span>
#### Read data using Flink SQL


1. Create a StarRocks table in Flink SQL.


```sql
CREATE TABLE tb_sr_table
(
    `id` INT,
    `name` STRING
)
WITH
(
    'connector'='starrocks',
    'scan-url'='192.168.xxx.xxx:8030',
    'jdbc-url'='jdbc:mysql://192.168.xxx.xxx:9030',
    'username'='xxxxxx',
    'password'='xxxxxx',
    'database-name'='test',
    'table-name'='tb_demo'
);
```



2. Query StarRocks table data in Flink.


```sql
SELECT * FROM tb_sr_table;
```



3. Export the StarRocks table to another table using the INSERT statement.

   dest_table can be any table supported by Flink. Depending on the storage path, the storage system can be HDFS or TOS.


```sql
INSERT INTO dest_table SELECT * FROM tb_sr_table;
```


<span id="_5-3-2-使用-flink-datastream-读取数据"></span>
#### Read data using Flink DataStream

Use Flink Connector to create StarRocksSource to query data.

```sql
import com.starrocks.connector.flink.StarRocksSource;
import com.starrocks.connector.flink.table.source.StarRocksSourceOptions;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.table.api.DataTypes;
import org.apache.flink.table.api.TableSchema;
   
public class StarRocksSourceApp {
        public static void main(String[] args) throws Exception {
            StarRocksSourceOptions options = StarRocksSourceOptions.builder()
                   .withProperty("scan-url", "192.168.xxx.xxx:8030")
                   .withProperty("jdbc-url", "jdbc:mysql://192.168.xxx.xxx:9030")
                   .withProperty("username", "root")
                   .withProperty("password", "")
                   .withProperty("table-name", "tb_demo")
                   .withProperty("database-name", "demo")
                   .build();
            TableSchema tableSchema = TableSchema.builder()
                   .field("id", DataTypes.INT())
                   .field("name", DataTypes.STRING())
                   .build();
            StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
            env.addSource(StarRocksSource.source(tableSchema, options)).setParallelism(5).print();
            env.execute("StarRocks flink source");
        }

    }
```
