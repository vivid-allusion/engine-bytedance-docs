---
title: "Supported data sources"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/supported_data_sources"
---

Data integration supports multiple synchronization modes, including offline synchronization, streaming synchronization, and full and incremental data synchronization solutions. This article introduces the types of data sources supported by each synchronization mode. In each mode, the supported read and write data sources can be freely combined to form channels.

Data sources used for data integration must first be configured in **Project Console \> Data Source Management**, and their network connectivity must be tested for [Exclusive Integrated Resource Group Management](https://docs.byteplus.com/docs/dataleap/exclusive_integrated_resource_group). Once the data source is successfully registered, it can be used in data integration tasks.

For more information about registering a data source, see [Configure Datasource](https://docs.byteplus.com/docs/dataleap/configure_datasource).

<span id="c3a703ee"></span>
## Asia Pacific(Johor)

<span id="466b9320"></span>
### **The data source capabilities supported by offline and real\-time synchronization modes**

✅ Supports visual mode (also supports script mode)

✔️: Only supports script mode

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Some data sources support table types and field types that use incomplete schemas. Please refer to the detailed documentation of the data source for more information. See <a href="https://docs.byteplus.com/docs/dataleap/configure_datasource">Configure Datasource</a> for details.</div>



|Data source type |Data sources |Offline synchronization |||Real\-time synchronization ||Note |
|---|---|---|---|---|---|---|---|
|||Single table read |Incremental read (where clause filtering) |Write to a single table |Incremental read of a single table |Incremental write to a single table | |
|Relational databases |[MySQL](https://docs.byteplus.com/docs/dataleap/69127) |✅ |✅ |✅ | |✅ | |
|Relational database |[Oracle](https://docs.byteplus.com/docs/dataleap/69140) |✅ |✅ |✅ | |✅ | |
|Relational databases |[SQLServer](https://docs.byteplus.com/docs/dataleap/69125) |✅ |✅ |✅ | |✅ | |
|Relational databases |[PostgreSQL](https://docs.byteplus.com/docs/dataleap/69141) |✅ |✅ |✅ | |✅ | |
|Relational databases |[VeDB](https://www.volcengine.com/docs/6260/126105) |✅ |✅ |✅ | |✅ | |
|Relational database |[GaussDB](https://docs.byteplus.com/docs/dataleap/gaussdb_datasource) |✅ |✅ |✔️ | | | |
|Relational databases |[GBase8s](https://docs.byteplus.com/docs/dataleap/69120) |✅ |✅ | | | | |
|Relational database |[GreenPlum](https://docs.byteplus.com/docs/dataleap/69136) |✅ |✅ |✅ | | | |
|Relational databases |[OceanBase](https://docs.byteplus.com/docs/dataleap/69147) |✅ |✅ | | | | |
|Relational databases |TiDB | | |✅ | | | |
|Big data storage |[LAS](https://docs.byteplus.com/docs/undefined/659f9f19331e7c053f130cde)（Whitelist） |✅ | |✅ | |✅ | |
|Big data storage |[HBase](https://docs.byteplus.com/docs/dataleap/69130) |✅ | |✅ | |✅ | |
|Big data storage |[HDFS](https://docs.byteplus.com/docs/dataleap/69109) |✅ | | | |✅ | |
|Big data storage |[Hive(on HDFS)](https://docs.byteplus.com/docs/dataleap/69123) |✅ | |✅ | |✅ | |
|Big data storage |[Hive(on TOS)](https://docs.byteplus.com/docs/dataleap/69123) |✅ |✅ |✅ | |✅ | |
|Big data storage |[MaxCompute](https://docs.byteplus.com/docs/dataleap/69146) |✅ | |✅ | | | |
|Big data storage |[Kudu](https://docs.byteplus.com/docs/dataleap/69133) |✅ |✅ |✔️ | | | |
|In\-memory databases |[SAP Hana](https://www.volcengine.com/docs/6260/1159225) |✅ |✅ |✅ | | | |
|MPP database |[ClickHouse](https://docs.byteplus.com/docs/dataleap/69105) |✅ |✅ |✅ | | | |
|MPP database |[ByteHouse CE](https://docs.byteplus.com/docs/dataleap/69129) |✅ |✅ |✅ | |✅ | |
|MPP database |[ByteHouse CDW](https://www.volcengine.com/docs/6260/153003) |✅ |✅ |✅ | |✅ | |
|Time series database |[TDengine](https://docs.byteplus.com/docs/dataleap/69115) |✅ |✅ | |✅ | | |
|Semi\-structured |[RestApi](https://docs.byteplus.com/docs/dataleap/69137) |✅ | | | | | |
|Semi\-structured |[TOS](https://docs.byteplus.com/docs/dataleap/69126) |✅ | |✅ | |✅ | |
|Semi\-structured |[OSS](https://www.volcengine.com/docs/6260/1220830) |✅ | | | | | |
|Semi\-structured |[FTP/SFTP](https://docs.byteplus.com/docs/dataleap/69138) |✅ | | | | | |
|Semi\-structured |S3 |✔️ | | | | | |
|Semi\-structured |[LarkSheet](https://docs.byteplus.com/docs/dataleap/69119) |✅ | |✅ | | | |
|NoSQL |[MongoDB](https://docs.byteplus.com/docs/dataleap/69107) |✅ |✅ |✅ | |✔️ | |
|NoSQL |[ElasticSearch](https://docs.byteplus.com/docs/dataleap/69111) |✅ |✅ |✅ | |✅ | |
|NoSQL |[Redis](https://docs.byteplus.com/docs/dataleap/69124) |✅ | |✅ | |✔️ | |
|Message queues |[Kafka](https://docs.byteplus.com/docs/dataleap/69134) |✅ | |✅ |✅ | | |
|Message queue |[RocketMQ](https://docs.byteplus.com/docs/dataleap/69149) | | | |✅ | | |
|Log service |[TLS](https://docs.byteplus.com/docs/dataleap/69131) |✅ | | |✅ | |When reading the TLS data source:<br><br><br>* Offline support for Hive, ByteHouse_CDW, LAS, Hudi, and MaxCompute targets |


<span id="e7c2c702"></span>
### Channels and enterprise\-level capabilities supported by the CDC solution

One\-click configuration solution that supports automatic table creation, performing full synchronization first, followed by incremental synchronization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Some data sources support table types and field types that do not fully conform to a strict schema; please refer to the detailed documentation of the data source. For details, see <a href="https://docs.byteplus.com/docs/dataleap/configure_datasource">Configure Datasource</a>.</div>



|Target side |Supported sources |Automatic table creation during synchronization |DDL is automatically synchronized during the synchronization process |
|---|---|---|---|
|ByteHouse Cloud Data Warehouse Edition |MySQL |✅ |✅ |
||VeDB |✅ |✅ |
||Mongo |✅ |❌ |
||PostgreSQL |✅ |❌ |
||SQLServer |✅ |❌ |
||Oracle (it is recommended to access CDC data through the Kafka caching mode) |✅ |❌ |
||GaussDB (CDC data must be collected into Kafka first) |✅ |❌ |
||TiDB (CDC data must first be sent to Kafka) |✅ |❌ |
|ByteHouse Enterprise Edition |MySQL |✅ |❌ |
||VeDB |✅ |❌ |
||PostgreSQL |✅ |❌ |
||TiDB (CDC data must first be sent to Kafka) |✅ |❌ |
||Mongo |✅ |❌ |
|Elasticsearch |MySQL |✅ |❌ |
||VeDB |✅ |❌ |
||PostgreSQL |✅ |❌ |
||SqlServer |✅ |❌ |
||Oracle (it is recommended to access CDC data through the Kafka caching mode) |✅ |❌ |


&nbsp;
