---
title: "StarRocks Spark Connector"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_Spark_Connector"
---

As a high\-performance analytical database, StarRocks supports reading and writing data through Spark. You can use the Spark Connector to connect Spark and StarRocks for data import and export. Currently, the Spark Connector version provided by EMR supports two different modes for reading and writing StarRocks data: native and bypass. The differences are shown in the following table:


|Modes |Data import |Data export |
|---|---|---|
|Native mode |Batch data in memory, then import it into StarRocks using StreamLoad. |Read data from StarRocks via RPC requests. |
|Bypass mode |Bypass the StarRocks service layer and directly write data files stored by StarRocks in the object storage system. |Bypass the StarRocks service layer and directly read data files stored by StarRocks in the object storage system. |


The bypass mode offers the following advantages over the native mode:


* It implements the Spark StarRocks Catalog, allowing direct access to StarRocks database and table metadata in Spark without the need to create external tables in advance.

* For StarRocks compute\-storage separated clusters, it supports reading and writing data files stored in object storage systems directly through Spark, avoiding the consumption of StarRocks cluster computing resources and preventing impact on online queries.


<span id="628c65be"></span>
## Bypass mode

The bypass mode is now available out of the box in products such as EMR on ECS, EMR on VKE, and Serverless Spark.

<span id="fe7f07cf"></span>
### Configuration parameters


|Parameters |Required |Default value |Note |
|---|---|---|---|
|spark.sql.extensions |Yes | |Set to `com.starrocks.connector.spark.StarRocksExtensions` to rewrite the Spark execution plan. |
|spark.sql.catalog.starrocks |Yes | |Set to `com.starrocks.connector.spark.catalog.StarRocksCatalog` to enable Spark to directly access StarRocks database and table metadata. |
|spark.sql.catalog.starrocks.writer.mode |Yes | |Set to BYPASS to directly write StarRocks data files. |
|spark.sql.catalog.starrocks.reader.mode |Yes | |Set to BYPASS to directly read StarRocks data files. |
|spark.sql.catalog.starrocks.fe.http.url |Yes | |The HTTP address of StarRocks FE. Multiple FE addresses are supported and separated by a comma `,`. The format is `http://<fe_host1>:<fe_http_port1>,<fe_host2>:<fe_http_port2>`. |
|spark.sql.catalog.starrocks.fe.jdbc.url |Yes | |The MySQL Server connection address of StarRocks FE. The format is `jdbc:mysql://<fe_host>:<fe_query_port>`. |
|spark.sql.catalog.starrocks.user |Yes | |The username of the StarRocks cluster account. |
|spark.sql.catalog.starrocks.password |Yes | |The password of the StarRocks cluster account. |
|spark.sql.catalog.starrocks.fs.s3a.endpoint |Yes | |The TOS object storage S3 access endpoint for the StarRocks storage\-compute separated cluster. |
|spark.sql.catalog.starrocks.fs.s3a.endpoint.region |Yes | |The TOS object storage S3 access region for the StarRocks storage\-compute separated cluster. |
|spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled |Yes | |Set to true |
|spark.sql.catalog.starrocks.fs.s3a.path.style.access |Yes | |Set to false |
|spark.sql.catalog.starrocks.fs.s3a.access.key |Yes | |The static AccessKey for accessing TOS object storage. |
|spark.sql.catalog.starrocks.fs.s3a.secret.key |Yes | |The static SecretKey for accessing TOS object storage. |
|spark.sql.catalog.starrocks.fs.s3a.retry.limit |No |5 |The number of retry attempts for failed access to TOS object storage. |
|spark.sql.catalog.starrocks.batch.size |No |4096 |The batch granularity for write operations. Increasing this parameter can optimize write performance. |


<span id="82b22c9e"></span>
### Note

<span id="7a7bd2c6"></span>
#### EMR on ECS

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using Bypass mode in EMR on ECS, you need to ensure the following:</div>



* <div data-tips="true" data-tips-type="tip">The StarRocks version must be 3.2.3 or above.</div>


* <div data-tips="true" data-tips-type="tip">The Hadoop cluster must be EMR\-3.11.0 or above.</div>


* <div data-tips="true" data-tips-type="tip">Ensure that the Hadoop cluster and the StarRocks cluster are in the same VPC.</div>



<span id="c7f741df"></span>
##### Spark SQL method

The following is an example of parameters that need to be set when starting the Spark SQL client:

```Bash
spark-sql \
    --conf spark.sql.extensions="com.starrocks.connector.spark.StarRocksExtensions" \
    --conf spark.sql.catalog.starrocks="com.starrocks.connector.spark.catalog.StarRocksCatalog" \
    --conf spark.sql.catalog.starrocks.batch.size=8092 \
    --conf spark.sql.catalog.starrocks.writer.mode="BYPASS" \
    --conf spark.sql.catalog.starrocks.reader.mode="BYPASS" \
    --conf spark.sql.catalog.starrocks.fe.http.url="http://192.168.6.7:8030" \
    --conf spark.sql.catalog.starrocks.fe.jdbc.url="jdbc:mysql://192.168.6.7:9030" \
    --conf spark.sql.catalog.starrocks.user="root" \
    --conf spark.sql.catalog.starrocks.password="******" \
    --conf spark.sql.catalog.starrocks.fs.s3a.endpoint="https://tos-s3-cn-beijing.ivolces.com" \
    --conf spark.sql.catalog.starrocks.fs.s3a.endpoint.region="cn-beijing" \
    --conf spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled=true \
    --conf spark.sql.catalog.starrocks.fs.s3a.path.style.access=false \
    --conf spark.sql.catalog.starrocks.fs.s3a.retry.limit=27 \
    --conf spark.sql.catalog.starrocks.fs.s3a.access.key="******" \
    --conf spark.sql.catalog.starrocks.fs.s3a.secret.key="******" \
    --jars /opt/emr/current/spark/starrocks-connector/starrocks-spark-connector-3.5_2.12-1.1.2-ve-bypass-2.jar
```


After entering the Spark SQL terminal, you can switch to the StarRocks Catalog and then execute query statements:

```SQL
USE starrocks.demo;
SELECT * FROM example_table;
```


<span id="dafd1cf3"></span>
##### pySpark method

Prepare the `demo.py` program example:

```Python

import sys
import time
from operator import add

from pyspark.sql import SparkSession
from pyspark.sql.functions import *

if __name__ == "__main__":
    spark = SparkSession\
        .builder\
        .appName("Bypass Read")\
        .config("spark.shuffle.service.enabled", "true")\
        .config("spark.sql.extensions", "com.starrocks.connector.spark.StarRocksExtensions")\
        .config("spark.sql.catalog.starrocks", "com.starrocks.connector.spark.catalog.StarRocksCatalog")\
        .config("spark.sql.catalog.starrocks.fe.http.url", "http://xxx:8030")\
        .config("spark.sql.catalog.starrocks.fe.jdbc.url", "jdbc:mysql://xxx:9030")\
        .config("spark.sql.catalog.starrocks.user", "root")\
        .config("spark.sql.catalog.starrocks.password", "******")\
        .config("spark.sql.catalog.starrocks.writer.mode","BYPASS") \
        .config("spark.sql.catalog.starrocks.reader.mode","BYPASS") \
        .config("spark.sql.catalog.starrocks.fs.s3a.endpoint", "https://tos-s3-cn-beijing.ivolces.com")\
        .config("spark.sql.catalog.starrocks.fs.s3a.endpoint.region", "cn-beijing")\
        .config("spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled", "true")\
        .config("spark.sql.catalog.starrocks.fs.s3a.path.style.access", "false")\
        .config("spark.sql.catalog.starrocks.fs.s3a.retry.limit", "27")\
        .config("spark.sql.catalog.starrocks.fs.s3a.access.key", "******")\
        .config("spark.sql.catalog.starrocks.fs.s3a.secret.key", "******")\
        .getOrCreate()
    spark.sql("use starrocks.demo").show()   
    spark.sql("show tables").show()
    spark.sql("select count(1) from tb_all_primitivetype_read_duplicate ").show()
    spark.sql("insert into tb_all_primitivetype_read_duplicate select * from tb_all_primitivetype_read_duplicate limit 10 ").show()
    spark.sql("select count(1) from tb_all_primitivetype_read_duplicate ").show()
    spark.stop()
```



* Submit and execute in client mode


```Bash
spark-submit \
    --conf spark.app.name="bypass-test" \
    --jars /opt/emr/current/spark/starrocks-connector/starrocks-spark-connector-3.5_2.12-1.1.2-ve-bypass-2.jar \
    --conf "spark.yarn.jars=hdfs://master-1-1.emr-58048cfb501d90d6411d.cn-beijing.emr-volces.com:8020/user/application/label-pipeline/spark-jars-v2/*,hdfs://master-1-1.emr-58048cfb501d90d6411d.cn-beijing.emr-volces.com:8020/user/application/label-pipeline/app-jars/*" \
    demo.py
```



* Submit and execute in cluster mode


```Bash
spark-submit \
    --deploy-mode cluster \
    --conf spark.app.name="bypass-test" \
    --conf "spark.yarn.jars=hdfs://master-1-1.emr-58048cfb501d90d6411d.cn-beijing.emr-volces.com:8020/user/application/label-pipeline/spark-jars-v2/*,hdfs://master-1-1.emr-58048cfb501d90d6411d.cn-beijing.emr-volces.com:8020/user/application/label-pipeline/app-jars/*" \
    demo.py
```


<span id="64a3095f"></span>
#### EMR on VKE

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using Bypass mode in EMR on VKE, you need to ensure the following:</div>



* <div data-tips="true" data-tips-type="tip">The StarRocks version must be 3.2.3 or above.</div>


* <div data-tips="true" data-tips-type="tip">The EMR on VKE cluster must be EMR\-1.6.0 or above and include the Spark component.</div>


* <div data-tips="true" data-tips-type="tip">Ensure that the EMR on VKE cluster and the StarRocks cluster are in the same VPC.</div>


* <div data-tips="true" data-tips-type="tip">Read "<a href="https://docs.byteplus.com/docs/undefined/69aa383ba2748d0549db5ea8">Manage jobs using kubectl</a>" to learn how to submit Spark jobs to the VKE cluster.</div>



After learning how to submit Spark jobs to an EMR on VKE cluster, you can modify the job yaml file and add the following configuration to enable reading and writing StarRocks data files through Spark:

```YAML
spec:
    deps:
      jars:
        # starrocks-spark-connector jar file, the VKE cluster image has it built in
        - local:///opt/spark/starrocks-connector/starrocks-spark-connector-3.5_2.12-1.1.2-ve-bypass-2.jar
    sparkConf:
      spark.sql.extensions: "com.starrocks.connector.spark.StarRocksExtensions"
      spark.sql.catalog.starrocks: "com.starrocks.connector.spark.catalog.StarRocksCatalog"
      # Enable direct read and write mode
      spark.sql.catalog.starrocks.writer.modeL: "BYPASS"
      spark.sql.catalog.starrocks.reader.mode: "BYPASS"
      # Connection configuration for the corresponding StarRocks cluster, that is, the internal IP addresses of each FE node
      spark.sql.catalog.starrocks.fe.http.url: "http://192.168.0.180:8030,192.168.0.181:8030,192.168.0.178:8030"
      spark.sql.catalog.starrocks.fe.jdbc.url: "jdbc:mysql://192.168.0.180:9030,192.168.0.181:9030,192.168.0.178:9030"
      # Authentication configuration for the corresponding StarRocks cluster
      spark.sql.catalog.starrocks.user: "root"
      spark.sql.catalog.starrocks.password: "******"
      # Configuration for StarRocks storage-compute separation cluster TOS connection and authentication
      spark.sql.catalog.starrocks.fs.s3a.endpoint: "https://tos-s3-cn-beijing.ivolces.com"
      spark.sql.catalog.starrocks.fs.s3a.endpoint.region: "cn-beijing"
      spark.sql.catalog.starrocks.fs.s3a.connection.ssl.enabled: "true"
      spark.sql.catalog.starrocks.fs.s3a.path.style.access: "false"
      spark.sql.catalog.starrocks.fs.s3a.access.key: "******"
      spark.sql.catalog.starrocks.fs.s3a.secret.key: "******"
      # [Recommended] Specify the path to load the so file. If not specified, self-extraction will be attempted, which incurs approximately 30 seconds of overhead.
      spark.driver.extraJavaOptions: "-Dcom.starrocks.format.jni.lib.path=/opt/starrocks/native"
      spark.executor.extraJavaOptions: "-Dcom.starrocks.format.jni.lib.path=/opt/starrocks/native"
      # [Optional] Used to set the batch granularity for writing.
      spark.sql.catalog.starrocks.batch.size: "8092"
```


<span id="289c5ae7"></span>
#### EMR Serverless Spark

Refer to the [Serverless Spark StarRocks read/write operation manual](https://www.volcengine.com/docs/6491/1302227).

<span id="9e3b7f51"></span>
## Native mode

<span id="587b76dc"></span>
### Configuration parameters


|Parameters |Required |Parameter value |Note |
|---|---|---|---|
|starrocks.fe.jdbc.url |Yes | |Configure the FE node MySQL server address. The format is `jdbc:mysql://<fe_host>:<fe_query_port>`. |
|starrocks.fe.http.url |Yes | |Configure the FE node HTTP server. The format is `<fe_host>:<fe_http_port>`. Multiple addresses are separated by an English comma `,`. |
|starrocks.table.identifier |Yes | |The StarRocks data table to be imported. The format is: `<database_name>.<table_name>`. |
|starrocks.user |Yes | |StarRocks user name for access. |
|starrocks.password |Yes | |Password for accessing StarRocks. |
|starrocks.write.label.prefix |No |* Default value: `spark-` |Used to configure the prefix for Stream Load import task labels. It is recommended to configure the label prefix based on the specific business scenario. |
|starrocks.write.enable.transaction\-stream\-load |No |* Default value: true |Used to configure whether the import operation uses the [Stream Load transaction interface](https://docs.starrocks.io/zh/docs/loading/Stream_Load_transaction_interface/). Compared to the standard interface, it offers better memory usage and performance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>starrocks.write.max.retries > 0</code> is configured, this parameter does not take effect.</div><br> |
|starrocks.write.buffer.size |No |* Default value: 104857600<br><br>* Unit: Defaults to bytes. Supports `kb`, `mb`, and `gb`. |Used to configure the amount of data cached in memory. When the cached data reaches this threshold, a Stream Load import is triggered. |
|starrocks.write.buffer.rows |No |Integer.MAX_VALUE |Used to configure the number of data rows cached in memory. When the cached data reaches this threshold, a Stream Load import is triggered. |
|starrocks.write.flush.interval.ms |No |* Default value: 300000<br><br>* Unit: milliseconds |Used to configure the interval for sending data. |
|starrocks.write.max.retries |No |* Default value: 3 |Used to configure the maximum number of retry attempts after failure.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the value of this parameter is greater than 0, the <code>starrocks.write.enable.transaction-stream-load</code> configuration will be ignored.</div><br> |
|starrocks.write.retry.interval.ms |No |* Default value: 10000<br><br>* Unit: milliseconds |Retry interval after failure. |
|starrocks.columns |No | |Used to configure which columns to write; multiple column names are separated by an English comma `,`. |
|starrocks.write.num.partitions |No | |Used to configure the number of partitions for parallel Spark writes. The default is determined by Spark. |
|starrocks.write.partition.columns |No | |Used to configure the columns for Spark partitioning. If not specified, all written columns are used for partitioning.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect after <code>starrocks.write.num.partitions</code> is configured.</div><br> |
|starrocks.timezone |No | |Used to configure the time zone. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In native mode, the Spark Connector uses Stream Load for data import at the underlying layer. In addition to the configuration parameters listed in this section, you can also directly set Stream Load import behavior using <code>starrocks.write.properties.{stream load parameter name}</code>. For example, you can set the data format for import using <code>starrocks.write.properties.format</code>, which corresponds to the Stream Load <code>format</code> parameter.</div>


<span id="640bdc5d"></span>
### Note

This section uses importing data into the StarRocks detail table `examples.tb_duplicate_key` as an example. The table creation statement is as follows:

```SQL
CREATE TABLE IF NOT EXISTS tb_duplicate_key
(
    event_time BIGINT       NOT NULL COMMENT 'timestamp of event',
    event_type INT          NOT NULL COMMENT 'type of event',
    user_id    INT          NOT NULL COMMENT 'id of user',
    device     VARCHAR(128) NULL     COMMENT 'device'
) ENGINE = OLAP DUPLICATE KEY(event_time, event_type)
DISTRIBUTED BY HASH(user_id)
PROPERTIES (
    'replication_num' = '3'
);
```


<span id="49da76a9"></span>
#### Spark SQL method

You can write data directly to the corresponding StarRocks data table using Spark SQL. The steps are as follows:


1. Enter the Spark SQL interactive terminal. Refer to the [Spark SQL Client usage method](https://docs.byteplus.com/docs/E-MapReduce/109471#_3-3-%E4%BD%BF%E7%94%A8-sql-%E4%BA%A4%E4%BA%92%E5%BC%8F%E7%BC%96%E7%A8%8B%E7%8E%AF%E5%A2%83) to enter the Spark SQL interactive terminal. The following additional parameters need to be added:


```Bash
--jars /opt/emr/current/spark/starrocks-connector/starrocks-spark-connector-3.5_2.12-1.1.2-ve-bypass-2.jar
```



2. Create an external table for the StarRocks `tb_duplicate_key` table using `CREATE TABLE`. The table name does not need to match:


```SQL
CREATE TABLE IF NOT EXISTS tb_duplicate_key 
USING starrocks 
OPTIONS
(
    "starrocks.fe.http.url"="192.168.10.2:8030",
    "starrocks.fe.jdbc.url"="jdbc:mysql://192.168.10.2:9030",
    "starrocks.table.identifier"="examples.tb_duplicate_key",
    "starrocks.user"="system_query_user",
    "starrocks.password"="******"
);
```



3. Insert data into the external table using `INSERT INTO`:


```SQL
INSERT INTO tb_duplicate_key
VALUES (1703128450, 1, 1001, 'PHONE'),
       (1703128451, 0, 1002, 'PAD'),
       (1703128452, 1, 1003, 'TV');
```


Under normal circumstances, you can query the data just written from the Spark side in StarRocks.

<span id="70e775e1"></span>
#### Spark DataFrame method

This section uses a batch job as an example to demonstrate importing data constructed in memory into the StarRocks `tb_duplicate_key` table using the Spark DataFrame method. The Scala sample code is as follows:

```Scala
val spark = SparkSession
  .builder()
  .appName("load_data_example")
  .getOrCreate()

import spark.implicits._

// Simulate data
val data = Seq(
  (1703128450, 1, 1001L, "PHONE"),
  (1703128451, 0, 1002L, "PAD"),
  (1703128452, 1, 1003L, "TV"),
)

// Write data to StarRocks
val df = data.toDF("event_time", "event_type", "user_id", "device")
df.write
  .format("starrocks")
  .option("starrocks.fe.http.url", "192.168.10.2:8030")
  .option("starrocks.fe.jdbc.url", "jdbc:mysql://192.168.10.2:9030")
  .option("starrocks.table.identifier", "examples.tb_duplicate_key")
  .option("starrocks.user", "system_query_user")
  .option("starrocks.password", "******")
  .mode("append")
  .save()
```


For information on how to submit Spark jobs, refer to the [Spark documentation](https://docs.byteplus.com/docs/E-MapReduce/109471#_4-%E7%A8%8B%E5%BA%8F%E6%8F%90%E4%BA%A4). The following additional parameters need to be added:

```Bash
--jars /opt/emr/current/spark/starrocks-connector/starrocks-spark-connector-3.5_2.12-1.1.2-ve-bypass-2.jar
```


<span id="125fcad0"></span>
## More information

You can visit the [StarRocks official documentation](https://docs.starrocks.io/zh/docs/loading/Spark-connector-starrocks/) to learn more about importing data into StarRocks using Spark Connector, as well as how to use [Spark Connector](https://docs.starrocks.io/zh/docs/unloading/Spark_connector/) to read data from StarRocks.
