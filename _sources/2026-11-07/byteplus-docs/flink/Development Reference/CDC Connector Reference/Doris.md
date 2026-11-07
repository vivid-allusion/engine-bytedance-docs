---
title: "Doris"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/CDC_Connector_Doris"
---

The Doris Pipeline connector can be used as a Data Sink for Doris, writing data into [Doris](https://doris.apache.org/). This document describes how to set up the Doris Pipeline connector.

<span id="925aff5b"></span>
## Usage Restrictions


* The Doris Pipeline connector is currently only supported in **Flink 1.16\-volcano** and higher engine versions.


<span id="29ec75d2"></span>
## **Connector Features**


* Automatic Table Creation

* Table Structure Change Synchronization

* Real\-Time Data Synchronization


<span id="e918258f"></span>
## **How to Create a Pipeline**

```YAML
source:
  type: mysql
  name: MySQL Source
  hostname: 127.0.0.1
  port: 3306
  username: admin
  password: pass
  tables: adb.\.*, bdb.user_table_[0-9]+, [app|web].order_\.*
  server-id: 5401-5404

sink:
   type: doris
   name: Doris Sink
   fenodes: 127.0.0.1:8030
   username: root
   password: ""
   table.create.properties.replication_num: 1

pipeline:
   parallelism: 1
```


<span id="356f43d4"></span>
## **Connector Configuration Options**


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the Sink to use, here it is 'Doris'. |
|name |optional |(none) |String |Name of the Pipeline |
|fenodes |required |(none) |String |Http address of the Doris FE cluster, such as 127.0.0.1:8030 |
|benodes |optional |(none) |String |Http address of the Doris BE cluster, such as 127.0.0.1:8040 |
|jdbc\-url |optional |(none) |String |JDBC address for the Doris cluster, such as: jdbc:mysql://127.0.0.1:9030/db |
|username |required |(none) |String |Username for the Doris cluster |
|password |optional |(none) |String |Doris cluster password |
|auto\-redirect |optional |FALSE |String |Whether to redirect writes via FE or directly write to BE |
|sink.enable.batch\-mode |optional |TRUE |Boolean |Whether to use batch accumulation method for writing into Doris |
|sink.flush.queue\-size |optional |2 |Integer |Queue size for batch accumulation writes |
|sink.buffer\-flush.max\-rows |optional |50000 |Integer |Maximum number of records flushed in a single batch |
|sink.buffer\-flush.max\-bytes |optional |10485760(10MB) |Integer |Maximum number of bytes flushed in a single batch |
|sink.buffer\-flush.interval |optional |10s |String |The interval duration for Flush. If this time is exceeded, the data will be flushed asynchronously. |
|sink.properties. |optional |(none) |String |Parameters for StreamLoad. For example: sink.properties.strict_mode: true. Learn more about [StreamLoad's Properties](https://doris.apache.org/zh-CN/docs/dev/sql-manual/sql-statements/Data-Manipulation-Statements/Load/STREAM-LOAD/) attributes. |
|table.create.properties.\* |optional |(none) |String |Configuration of properties for creating tables. For example: table.create.properties.replication_num: 1. See more about [Doris Table properties](https://doris.apache.org/zh-CN/docs/dev/sql-manual/sql-statements/Data-Definition-Statements/Create/CREATE-TABLE/) |


<span id="7f323e1e"></span>
## **Data Type Mapping**


|**CDC type** |**Doris type** |**NOTE** |
|---|---|---|
|TINYINT |TINYINT | |
|SMALLINT |SMALLINT | |
|INT |INT | |
|BIGINT |BIGINT | |
|DECIMAL |DECIMAL | |
|FLOAT |FLOAT | |
|DOUBLE |DOUBLE | |
|BOOLEAN |BOOLEAN | |
|DATE |DATE | |
|TIMESTAMP [(p)] |DATETIME [(p)] | |
|TIMESTAMP_LTZ [(p)] |DATETIME [(p)] | |
|CHAR(n) |CHAR(n\*3) |In Doris, strings are stored using UTF\-8 encoding. Thus, English characters occupy 1 byte, and Chinese characters occupy 3 bytes. Here, the length is uniformly multiplied by 3. The maximum length of CHAR is 255. If exceeded, it will automatically convert to VARCHAR type. |
|VARCHAR(n) |VARCHAR(n\*3) |As above, the length is uniformly multiplied by 3. The maximum length of VARCHAR is 65533. If exceeded, it will automatically convert to STRING type. |
|BINARY(n) |STRING | |
|VARBINARY(N) |STRING | |
|STRING |STRING | |
