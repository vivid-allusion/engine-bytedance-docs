---
title: "Overview"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Connector_Overview"
---

This article introduces the connectors and formats supported by BytePlus Flink.

<span id="de770c51"></span>
## Supported Connectors

The table below lists the connectors currently available in BytePlus Flink, along with the supported table types for each connector.


|**Connector** |**Description** |**Source Table** |**Result Table** |**Dimension Table** |**Engine Version** |
|---|---|---|---|---|---|
|kafka |Provides the ability to consume and write data from Kafka / BMQ / TLS Topic. |✅ |✅ |❌ |Flink 1.11, 1.16+ |
|upsert\-kafka |Provides the ability to read data in upsert\-mode from Kafka Topic and write it back into Kafka Topic. |✅ |✅ |❌ |Flink 1.16+ |
|jdbc |Provides read and write capabilities for common relational databases like MySQL and PostgreSQL, and supports dimension tables. |✅ |✅ |✅ |Flink 1.11, 1.16+ |
|mysql\-cdc |Provides the ability to read snapshot and incremental data from MySQL. |✅ |❌ |❌ |Flink 1.16+ |
|mongodb\-cdc |Provides the ability to read snapshot and incremental data from MongoDB. |✅ |❌ |❌ |Flink 1.16+ |
|postgres\-cdc |Used for reading full snapshot data and incremental data from PostgreSQL databases. |✅ |❌ |❌ |Flink 1.16+ |
|sqlserver\-cdc |Used for reading both full and incremental data from SQLServer databases. |✅ |❌ |❌ |Flink 1.16+ |
|redis |Provides writing capabilities to the caching database Redis, supports use as result tables and dimension tables. |❌ |✅ |✅ |Flink 1.11, 1.16+ |
|hbase\-1.4 |Provides the ability to read and write data from HBase tables, supports use as source tables, result tables, and dimension tables. |✅ |✅ |✅ |Flink 1.11, 1.16+ |
|hbase\-2.2 ||✅ |✅ |✅ |Flink 1.16 |
|elasticsearch\-6 |Provides write capability for different versions of the Elasticsearch search engine. |❌ |✅ |❌ |Flink 1.11, 1.16+ |
|elasticsearch\-7 ||❌ |✅ |❌ |Flink 1.11, 1.16+ |
|starrocks |Provides data reading and writing from the StarRocks database, supporting as source table, result table, and dimension table. |✅ |✅ |✅ |Flink 1.16+ |
|Pulsar |Provides the capability to consume and write data in the distributed messaging system Pulsar Topic. |✅ |✅ |❌ |Flink 1.11 |
|iceberg |Provides reading and writing data from Iceberg tables, as well as enhanced capabilities with Iceberg+upsert. |✅ |✅ |❌ |Flink 1.11, 1.16+ |
|filesystem |Provides read and write capabilities for common filesystems. |✅ |✅ |❌ |Flink 1.11, 1.16+ |
|doris |Provides the capability to read and write data for Doris database, supporting its use as a source table, result table, and dimension table. |✅ |✅ |✅ |Flink 1.11, 1.16+ |
|datagen |Debug\-specific connector (source table) that supports periodic generation of random data with customizable data types. |✅ |❌ |❌ |Flink 1.11, 1.16+ |
|print |Debug\-specific connector (result table), results will be printed. |❌ |✅ |❌ |Flink 1.11, 1.16+ |
|blackhole |Debug\-only connector (result table), results will not be printed. |❌ |✅ |❌ |Flink 1.11, 1.16+ |
|faker |Data generator for simulation, will generate test data using Java Faker expressions provided for each field in the table. |✅ |✅ |❌ |Flink 1.11 |


<span id="7b8b6a41"></span>
## Supported Formats


|**Format** |**Flink 1.11** |**Flink 1.16** |**Flink 1.17** |
|---|---|---|---|
|avro |✅ |✅ |✅ |
|avro\-confluent |❌ |✅ |✅ |
|byte\-pb |✅ |❌ |❌ |
|canal\-json |✅ |✅ |✅ |
|csv |✅ |✅ |✅ |
|debezium\-json |✅ |✅ |✅ |
|json |✅ |✅ |✅ |
|maxwell\-json |❌ |✅ |✅ |
|ogg\-json |❌ |✅ |✅ |
|orc |✅ |✅ |✅ |
|parquet |✅ |✅ |✅ |
|protobuf |❌ |✅ |✅ |
