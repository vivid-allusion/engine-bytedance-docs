---
title: "Bytehouse CDW"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Bytehouse_CDW"
---

ByteHouse CDW Pipeline connectors can be used as a Data Sink for the Pipeline, transferring data to [ByteHouse CDW](https://docs.byteplus.com/en/docs/DataWind/ByteHouse_CDW). This document describes how to set up ByteHouse CDW Pipeline connectors.

<span id="690730e0"></span>
## Usage Restrictions


* ByteHouse CDW Pipeline connectors are currently only supported in **Flink 1.16\-volcano** and higher engine versions.


<span id="192ce7a3"></span>
## Connector Capabilities


* Real\-time data synchronization (includes entire database synchronization, and sharded database/table synchronization)


<span id="fceefd3b"></span>
## **How to Create a Pipeline**

A Pipeline for synchronizing data from MySQL to ByteHouse CDW can be defined as follows:

```YAML
################################################################################
# Description: Sync MySQL all tables to BH CDW
################################################################################
source:
   type: mysql
   name: MySQL Source
   hostname: vedbm-xxx.pri.mysql.vedb.ivolces.com
   port: 3306
   username: your-username
   password: your-password
   tables: app_db.\.*
   server-id: 5401-5420

sink:
  type: bytehouse-cdw
  name: Bytehouse CDW Sink
  region: VOLCANO_PRIVATE
  host: tenant-xxxx-cn-beijing.bytehouse.ivolces.com
  port: 19000
  virtual-warehouse: test
  api-token: xxx:xxx
  sink.buffer-flush.interval: 5s
  sink.buffer-flush.max-rows: 10000
  timestamp-offset: -8h

pipeline:
  name: MySQL to Bytehouse CDW Pipeline
  parallelism: 16
```


<span id="43fa0292"></span>
## Connector Configuration Items


|**Parameters** |**Mandatory Selection** |**Default Values** |**Data Types** |**Description** |
|---|---|---|---|---|
|type |required |(none) |String |Specify the connector to use, which needs to be set to `bytehouse-cdw`. |
|name |optional |(none) |String |Name of the Sink. |
|region |optional |`VOLCANO_PRIVATE` |String |Specify the region of the ByteHouse Gateway.<br><br><br>* `VOLCANO_PRIVATE`: Volcanic engine private network, which requires ByteHouse CDW and Flink to be in the same VPC. And fill in the private domain address and port. |
|host |required |(none) |String |ByteHouse's private host. The prerequisite is to set the region to `VOLCANO_PRIVATE`. |
|port |optional |19000 |String |ByteHouse's private port. The prerequisite is to set the region to `VOLCANO_PRIVATE`. |
|virtual\-warehouse |required |(none) |String |Used to specify the name of the compute group. |
|api\-token |required |(none) |String |API Token for the connector account. |
|sink.mode |optional |upsert |String |Select the data records to receive. Supported values include:<br><br><br>* insert: Only accept INSERT records.<br><br>* upsert: Accept INSERT, UPDATE_AFTER, and DELETE records.<br><br>* upsert\-no\-delete: Accept INSERT and UPDATE_AFTER records.<br><br>* upsert\-all: Accept all types of records.<br><br>* upsert\-all\-no\-delete: Accept all types of records except DELETE.<br><br>* upsert\-with\-delete\-to\-null: Accept INSERT and UPDATE_AFTER records. For DELETE, it sets all fields except the UPSERT keys (including partition keys and unique keys) to NULL.<br><br>* delete\-only: Only accepts DELETE records. |
|sink.buffer\-flush.interval |optional |1s |Duration |Flush interval, with a minimum of 200 ms. |
|sink.buffer\-flush.max\-rows |optional |50000 |Integer |Buffer record size, minimum value is 100. |
|sink.max\-retries |optional |15 |Integer |Maximum number of write retries, setting to \-1 means infinite retries. |
|jdbc.max\-retry\-backoff |optional |32s |Duration |Maximum exponential backoff retry interval, starting at 1s and increasing exponentially. Default is 32s, indicating an increase from 1s, 2s, 4s, etc., up to 32s, after which it remains unchanged. |
|timestamp\-offset |optional |(none) |Duration |Additional time offset for TIMESTAMP type.<br><br>Note: For Flink fields of type TIMESTAMP and TIMESTAMP WITH LOCAL TIME ZONE, the current practice is to convert them to local timestamps before entering the ByteHouse CDW Sink. As ByteHouse CDW Sink parses these timestamps using UTC, a \-8h offset is needed to correct the data. |


<span id="00f7aaca"></span>
## Usage Instructions


* Currently, automatic table creation is not supported because ByteHouse CDW requires multiple parameters for table creation, rendering the automatically created tables unusable. Therefore, it is recommended to manually create tables and optimize the table creation parameters before starting the Flink CDC 3.0 task to import data.

* For fields in Flink of type TIMESTAMP and TIMESTAMP WITH LOCAL TIME ZONE, their data will be converted to local timestamps before entering the ByteHouse CDW Sink. Since ByteHouse CDW Sink interprets these timestamps based on UTC, a \-8h offset is needed to correct the data.


<span id="fad0c9a4"></span>
## Data Type Mapping


|CDC type |Bytehouse CDW type |NOTE |
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
|TIME |TIME |Bytehouse CDW Connector currently does not support writing of TIME type; it is expected to be supported in the next version. |
|TIMESTAMP |DATETIME | |
|TIMESTAMP_LTZ |DATETIME | |
|CHAR(n) |STRING | |
|VARCHAR(n) |STRING | |
|STRING |STRING | |
