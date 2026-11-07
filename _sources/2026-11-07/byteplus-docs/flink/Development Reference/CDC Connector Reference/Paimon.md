---
title: "Paimon"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/CDC_Connector_Paimon"
---

Paimon Pipeline connectors can be used as a Data Sink for the Pipeline, writing data into [Paimon](https://paimon.apache.org/). This document describes how to set up Paimon Pipeline connectors.

<span id="98f47c40"></span>
## Usage Restrictions


* Paimon Pipeline connectors are currently only supported on **Flink 1.16\-volcano** engine versions and higher.


<span id="bfed3bae"></span>
## **Connector Features**


* Automatic Table Creation

* Synchronous Table Structure Changes

* Real\-Time Data Synchronization


<span id="a74ba020"></span>
## **How to Create a Pipeline**

Data synchronization from MySQL to Paimon's Pipeline can be defined as follows:

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
  type: paimon
  name: Paimon Sink
  catalog.properties.metastore: filesystem
  catalog.properties.warehouse: /path/warehouse

pipeline:
  name: MySQL to Paimon Pipeline
  parallelism: 2
```


<span id="2559ff3a"></span>
## **Pipeline Connector Configuration Items**


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the connector to use, set it to 'Paimon'. |
|name |optional |(none) |String |Name of the Sink. |
|catalog.properties.metastore |optional |"filesystem" |String |Type used to build the Paimon Catalog. Optional values: filesystem or Hive. |
|catalog.properties.warehouse |optional |(none) |String |The root directory for Paimon to store data. |
|catalog.properties.uri |optional |(none) |String |The URI for the Hive metastore, needed when the metastore is set to Hive. |
|commit.user |optional |admin |String |Username when submitting data files. |
|partition.key |optional |(none) |String |Set the partition fields for each partitioned table, allowing multiple partition fields to be specified for multiple partitioned tables. Different tables are separated by ';', while different fields are separated by ','. For example, we can set different partition fields for two tables as follows: 'testdb.table1:id1,id2;testdb.table2:name'. |
|catalog.properties.\* |optional |(none) |String |Pass the parameters supported by Paimon catalog to the pipeline, refer to [Paimon catalog options](https://paimon.apache.org/docs/master/maintenance/configurations/#catalogoptions). |
|table.properties.\* |optional |(none) |String |Pass the parameters supported by Paimon table to the pipeline, refer to [Paimon table options](https://paimon.apache.org/docs/master/maintenance/configurations/#coreoptions). |


<span id="c6ab33f1"></span>
## **Usage Instructions**


* Only Primary Key tables are supported; hence the source table must have a primary key.

* Exactly\-once is currently not supported; connectors implement idempotent writes through at\-least\-once and Primary Key tables.


<span id="08a8fcf5"></span>
## **Data Type Mapping**


|**CDC type** |**Paimon type** |
|---|---|
|TINYINT |TINYINT |
|SMALLINT |SMALLINT |
|INT |INT |
|BIGINT |BIGINT |
|FLOAT |FLOAT |
|DOUBLE |DOUBLE |
|DECIMAL(p, s) |DECIMAL(p, s) |
|BOOLEAN |BOOLEAN |
|DATE |DATE |
|TIMESTAMP |DATETIME |
|TIMESTAMP_LTZ |TIMESTAMP_LTZ |
|CHAR(n) |CHAR(n) |
|VARCHAR(n) |VARCHAR(n) |
