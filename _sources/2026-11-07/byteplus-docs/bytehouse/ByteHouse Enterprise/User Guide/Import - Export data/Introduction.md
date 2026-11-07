---
title: "Introduction"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/import-data-concept"
---

ByteHouse Enterprise supports multiple methods for data import and export, including small file import, batch import, streaming import, DataSail, offline export, and more, providing you with convenient data transfer functionality. This article introduces ByteHouse's data import/export capabilities.

<span id="984d0629"></span>
# Function overview

ByteHouse Enterprise offers comprehensive data import and export capabilities. After you activate the ByteHouse Enterprise service, you can quickly connect your business data and experience the platform.

For data import, ByteHouse Enterprise provides a variety of built\-in data import capabilities to support fast and convenient loading of data from different sources into the data warehouse, so you can quickly get started and explore ByteHouse's core features:


* **Real\-time streaming import**:

   * Kafka engine real\-time import: The ByteHouse Enterprise console supports connecting to Kafka and continuously transferring data to the target table. Unlike batch import, a Kafka import task will continue running once started. Kafka import tasks in ByteHouse can provide at\-least\-once semantics. You can stop or resume consumption tasks. ByteHouse will record offset information to ensure that no data is lost. It is suitable for scenarios with high real\-time requirements, moderate data volume, and few field\-level ELT operations, such as real\-time business data collection, log data import, and similar scenarios. Direct aggregation of real\-time data is not supported.

   * Import based on Flink: Suitable for scenarios with high real\-time requirements, large data volumes, and complex ELT processes, such as large\-scale business data import. You can directly aggregate real\-time data by leveraging the capabilities of Flink SQL.

* **Batch import**:

   * Also known as offline import, this method is suitable for scenarios where you want to load pre\-prepared data into ByteHouse in a single operation. You can batch import data from object storage (S3 protocol), ClickHouse, and Hive into ByteHouse tables through the ByteHouse Enterprise Edition console.

* **Small file import**:

   * Supports importing small files as data from local files, object storage, ClickHouse, Hive, HDFS, and other data sources using the INSERT statement.

* At the export level, the ByteHouse Enterprise console provides a data export feature that supports exporting data to BytePlus Torch Object Storage Service (TOS), meeting your data export needs and helping you better manage and utilize your data assets.


<span id="558b7a51"></span>
# Data import

<span id="a97e647f"></span>
## Supported data sources


|**Do not** |**Data sources** |**Import methods** |**Document link** |
|---|---|---|---|
|Database |ClickHouse |Batch import |[Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import) |
||MaterializedMySQL |Create a MaterializedMySQL database |[Import data via MaterializedMySQL](https://docs.byteplus.com/docs/bytehouse/import-via-materializedmysql) |
|Storage |Object storage |Small file import |[Import from object storage](https://docs.byteplus.com/docs/bytehouse/import-from-small-files#9a29a197) |
|||Batch import |[Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import) |
||HDFS |Import small files |[Import from HDFS](https://docs.byteplus.com/docs/bytehouse/import-from-small-files#1a4a30cf) |
|Data warehouse |Hive |Batch import |[Batch import](https://docs.byteplus.com/docs/bytehouse/batch-import) |
|Message queue |Kafka |Recommended Flink |[Flink Connector](https://docs.byteplus.com/docs/bytehouse/flink-connector) |
|||Kafka engine |[Streaming import](https://docs.byteplus.com/docs/bytehouse/streaming-import) |


<span id="34add886"></span>
## Supported data formats for import


|Import methods |File formats |
|---|---|
|Batch import |Supported file types include: CSV, JSON, Parquet, and more. |
|Streamed import |The commonly used format is JSONEachRow. |
|Import small files |For currently supported formats, see [Input and output data formats](https://clickhouse.com/docs/interfaces/formats#formats-overview). |


<span id="17ec8ff8"></span>
# Data export

ByteHouse supports creating data export tasks, allowing you to export data to TOS either once or on a regular basis, making it easier for you to perform data analysis. For detailed instructions, see [Export data](https://docs.byteplus.com/docs/bytehouse/export-data-ce).

<span id="6c19c251"></span>
# Connector

ByteHouse supports Spark Connector and Flink Connector, allowing you to load data into ByteHouse, making it easier for you to process data.


* [Spark Connector](https://docs.byteplus.com/docs/bytehouse/spark-connector)

* [Flink Connector](https://docs.byteplus.com/docs/bytehouse/flink-connector)
