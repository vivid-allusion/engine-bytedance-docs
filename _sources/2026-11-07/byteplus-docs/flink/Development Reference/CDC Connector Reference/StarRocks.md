---
title: "StarRocks"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/CDC_Connector_StarRocks"
---

StarRocks Pipeline connectors can be used as a Data Sink for Pipelines, writing data into [StarRocks](https://github.com/StarRocks/starrocks). This document describes how to set up StarRocks Pipeline connectors.

<span id="0c2810f1"></span>
## Usage Restrictions


* StarRocks Pipeline connectors are currently only supported in **Flink 1.16\-volcano** and higher engine versions.


<span id="cc2330c9"></span>
## **Connector Features**


* Automatic Table Creation

* Table Structure Change Synchronization

* Real\-Time Data Synchronization


<span id="b2cb3693"></span>
## **How to Create a Pipeline**

The pipeline for synchronizing data from MySQL to StarRocks can be defined as follows:

```YAML
source:
   type: mysql
   name: MySQL Source
   hostname: 127.0.0.1
   port: 3306
   username: admin
   password: pass
   tables: adb.\., bdb.user_table_[0-9]+, [app|web].order_\.
   server-id: 5401-5404

sink:
  type: starrocks
  name: StarRocks Sink
  jdbc-url: jdbc:mysql://127.0.0.1:9030
  load-url: 127.0.0.1:8030
  username: root
  password: pass

pipeline:
   name: MySQL to StarRocks Pipeline
   parallelism: 2
```


<span id="66bbb579"></span>
## **Connector Configuration Options**


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the connector to use, set it to 'StarRocks'. |
|name |optional |(none) |String |Name of the Sink. |
|jdbc\-url |required |(none) |String |Used to access the MySQL server on the FE node. Multiple addresses are separated by commas (,). Format: `jdbc:mysql://fe_host1:fe_query_port1,fe_host2:fe_query_port2`. |
|load\-url |required |(none) |String |Used to access the HTTP server on the FE node. Multiple addresses are separated by semicolons (;). Format: `fe_host1:fe_http_port1;fe_host2:fe_http_port2`. |
|username |required |(none) |String |Username for the StarRocks cluster. |
|password |required |(none) |String |User password for the StarRocks cluster. |
|sink.label\-prefix |optional |(none) |String |Specify the label prefix used by Stream Load. |
|sink.connect.timeout\-ms |optional |30000 |String |Timeout for establishing an HTTP connection with FE. Value range: [100, 60000]. |
|sink.wait\-for\-continue.timeout\-ms |optional |30000 |String |Timeout for waiting for an FE HTTP 100\-continue response. Valid range: [3000, 60000]. |
|sink.buffer\-flush.max\-bytes |optional |157286400 |Long |Size of the data buffered in memory, shared by all imported tables, one or more tables are chosen to write data to StarRocks when reaching the threshold. Valid range after reaching the threshold: [64MB, 10GB]. |
|sink.buffer\-flush.interval\-ms |optional |300000 |Long |The interval for sending buffered data for each table, used to control the data writing delay to StarRocks. The unit is milliseconds, with a range of values: [1000, 3600000]. |
|sink.scan\-frequency.ms |optional |50 |Long |The connector periodically checks whether each table has reached the sending interval. This configuration controls the frequency of checks, measured in milliseconds. |
|sink.io.thread\-count |optional |2 |Integer |The number of threads used to perform Stream Load, importing different tables can be executed concurrently. |
|sink.at\-least\-once.use\-transaction\-stream\-load |optional |TRUE |Boolean |Whether to use transaction stream load under at\-least\-once. |
|sink.properties.\* |optional |(none) |String |Parameters for Stream Load that control the behavior of Stream Load imports. For example, the parameter `sink.properties.timeout` controls the import timeout. All parameters and explanations please refer to [STREAM LOAD](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/STREAM_LOAD). |
|table.create.num\-buckets |optional |(none) |Integer |The number of buckets used when automatically creating a StarRocks table. For StarRocks versions 2.5 and later, the bucket number can be unset, and StarRocks will [automatically set the bucket number](https://docs.starrocks.io/zh/docs/table_design/Data_distribution/#%E7%A1%AE%E5%AE%9A%E5%88%86%E6%A1%B6%E6%95%B0%E9%87%8F); for versions prior to StarRocks 2.5, it must be set. |
|table.create.properties.\* |optional |(none) |String |Properties used when automatically creating a StarRocks table. For example: If using StarRocks version 3.2 and later, 'table.create.properties.fast_schema_evolution' = 'true' will enable the fast schema evolution feature. For more information, please refer to [the Primary Key model](https://docs.starrocks.io/docs/table_design/table_types/primary_key_table/). |
|table.schema\-change.timeout |optional |30min |Duration |The timeout for executing a schema change in StarRocks, which must be a multiple of seconds. If timed out, StarRocks will cancel the schema change, causing the job to fail. |


<span id="89fb0147"></span>
## **Usage Instructions**


* Only supports tables with a Primary Key, hence the source table must have a Primary Key

* Does not support exactly\-once; the connector achieves idempotent writes through at\-least\-once and tables with a Primary Key

* Regarding automatic table creation

   * The bucket key is the same as the Primary Key

   * No partition key

   * The number of buckets is controlled by `table.create.num-buckets`. If using StarRocks version 2.5 or later, setting the number of buckets is optional, as StarRocks can [automatically set the number of buckets](https://docs.starrocks.io/zh/docs/table_design/Data_distribution/#%E7%A1%AE%E5%AE%9A%E5%88%86%E6%A1%B6%E6%95%B0%E9%87%8F). For versions prior to StarRocks 2.5, settings must be configured, otherwise tables cannot be automatically created.

* Synchronization of table structure changes

   * Only supports adding or deleting columns

   * New columns can only be added as the last column

   * If using StarRocks 3.2 or later versions, and creating tables automatically via a connector, changes can be expedited by setting `table.create.properties.fast_schema_evolution` to `true`.

* For data synchronization, the pipeline connector uses the [StarRocks Sink connector](https://github.com/StarRocks/starrocks-connector-for-apache-flink) to write data into StarRocks, for more details refer to [Sink documentation](https://github.com/StarRocks/starrocks-connector-for-apache-flink/blob/main/docs/content/connector-sink.md).


<span id="f3589bc1"></span>
## **Data Type Mapping**


|**CDC type** |**StarRocks type** |**NOTE** |
|---|---|---|
|TINYINT |TINYINT | |
|SMALLINT |SMALLINT | |
|INT |INT | |
|BIGINT |BIGINT | |
|FLOAT |FLOAT | |
|DOUBLE |DOUBLE | |
|DECIMAL(p, s) |DECIMAL(p, s) | |
|BOOLEAN |BOOLEAN | |
|DATE |DATE | |
|TIMESTAMP |DATETIME | |
|TIMESTAMP_LTZ |DATETIME | |
|CHAR(n) where n <= 85 |CHAR(n \* 3) |In CDC, length represents the number of characters, while in StarRocks, it represents the number of bytes. According to UTF\-8 encoding, a Chinese character occupies three bytes, hence in CDC the length corresponds to n \* 3 in StarRocks. Since the maximum length of the CHAR type in StarRocks is 255, only when the length in CDC does not exceed 85 is the CDC CHAR mapped to StarRocks CHAR. |
|CHAR(n) where n \> 85 |VARCHAR(n \* 3) |In CDC, length represents the number of characters, while in StarRocks, it represents the number of bytes. According to UTF\-8 encoding, a Chinese character occupies three bytes, therefore in CDC the length corresponds to n \* 3 in StarRocks. Since the maximum length for the CHAR type in StarRocks is 255, CDC CHAR type is mapped to StarRocks VARCHAR only when the length exceeds 85. |
|VARCHAR(n) |VARCHAR(n \* 3) |The length in Change Data Capture represents the number of characters, while in StarRocks it represents the number of bytes. According to UTF\-8 encoding, a Chinese character occupies three bytes, hence the length in CDC corresponds to n \* 3 in StarRocks. |
