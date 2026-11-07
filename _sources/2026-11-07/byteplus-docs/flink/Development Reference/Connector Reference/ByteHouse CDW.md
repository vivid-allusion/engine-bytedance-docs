---
title: "ByteHouse CDW"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/ByteHouse_CDW"
---

In the Flink console, the `bytehouse-cdw` connector supports result tables, allowing data to be written to ByteHouse target tables through Flink tasks.

<span id="9b43429c"></span>
## Background Information

ByteHouse is a cloud\-native data warehouse, and the CDW (Cloud Data Warehouse) version is a self\-service data analytics platform that supports real\-time and offline imports, capable of efficiently analyzing massive data.

For more information about ByteHouse CDW, please see [ByteHouse CDW Overview](https://docs.byteplus.com/en/docs/bytehouse/docs-bytehouse-overview).

<span id="6914bc9f"></span>
## Usage Restrictions


* The ByteHouse CDW connector is currently only supported in **Flink 1.16\-byted** and later engine versions.

* If using byteplus engine private network, it is recommended to have ByteHouse CDW and Flink in the same VPC; for specific setup methods, refer to ByteHouse CDW Network Settings Document.

* If you require a newer version of the ByteHouse Flink Connector, it can be downloaded from [ByteHouse CDW Driver](https://docs.byteplus.com/en/docs/bytehouse/Flink_Connector).


<span id="269093d6"></span>
## DDL Definitions

```SQL
CREATE TABLE `bh_de_sink` ( -- sink table
 `id` STRING NOT NULL,
 `event_time` STRING,
 `content` ARRAY<DECIMAL(20, 0)>,
 PRIMARY KEY (`id`) NOT ENFORCED -- The primary key field corresponds to the Unique Key of the BH unique key table, and will be deduplicated when BH is stored.
) WITH (
 'connector' = 'bytehouse-cdw',
 'jdbc.enable-gateway-connection' = 'true',
 'bytehouse.gateway.region' = 'XXXX_PRIVATE',
 'bytehouse.gateway.host' = 'tenant-xxxx-cn-beijing.bytehouse.byteplus.com',
 'bytehouse.gateway.port' = '19000',
 'bytehouse.gateway.api-token' = '<API_KEY>',
 'bytehouse.gateway.virtual-warehouse' = '<VIRTUAL_WAREHOUSE>',
 'database' = '<BYTEHOUSE_DB>',
 'table-name' = '<BYTEHOUSE_TABLE>'
);
```


<span id="edad9504"></span>
## WITH parameters


|**Parameters** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|`connector` |Is |(none) |String |Specify the driver to use, which should be `ByteHouse CDW`. |
|`database` |Is |(none) |String |Name of the ByteHouse CDW database you want to connect to. |
|`table-name` |Yes |(none) |String |Name of the ByteHouse CDW table you want to connect to. |
|`jdbc.query.timeout` |No |`10 minutes` |Duration |Timeout settings for executing queries via JDBC. |
|`jdbc.enable-gateway-connection` |No |`false` |Boolean |Specifies whether the JDBC connection needs to go through the ByteHouse gateway. |
|`bytehouse.gateway.region` |No |(none) |String |ByteHouse gateway region. Supported values include:<br><br><br>* `XXXX_PRIVATE`: Suitable for Byteplus Engine cloud services bound with private gateway hosts. |
|`bytehouse.gateway.host` |No |(none) |String |Private host of the ByteHouse gateway. Provided that bytehouse.gateway.region is set to `XXXX_PRIVATE`. |
|`bytehouse.gateway.port` |No |`19000` |Integer |Private port of the ByteHouse gateway. The precondition is to set bytehouse.gateway.region to `XXXX_PRIVATE`. |
|`bytehouse.gateway.virtual-warehouse` |No |(none) |String |Name or ID of the compute group handling queries through the ByteHouse Gateway. By default, the default compute group configured through the ByteHouse console is used. |
|`bytehouse.gateway.account` |No |(none) |String |ByteHouse gateway account ID. |
|`bytehouse.gateway.access-key-id` |No |(none) |String |ByteHouse Gateway access key ID. |
|`bytehouse.gateway.secret-key` |No |(none) |String |ByteHouse gateway key. |
|`bytehouse.gateway.api-token` |No |(none) |String |ByteHouse gateway API token. |
|`bytehouse.storage.dump-parallelism` |No |1 |Integer |Parallelism of the storage dump (that is, the number of threads executed per insert). |
|`sink.group-by.key` |No |(none) |String |Key for pre\-receiver grouping. The key can consist of multiple fields separated by commas. |
|`sink.group-by.expression` |No |(none) |String |Expression for pre\-receiver grouping. If set, all involved field names must also be listed in sink.group\-by.key. |
|`sink.group-by.number-of-groups` |No |(none) |Integer |Records the number of groups for pre\-receipt If not specified, it will default to sink.parallelism (if provided). The ByteHouse Gateway secret key. |
|`sink.buffer-flush.interval` |No |`1 second` |Duration |The maximum interval between two batch flushes. The minimum is 200 milliseconds (ms). |
|`sink.buffer-flush.max-rows` |No |`50,000` |Integer |Maximum size of buffered records before flushing. The minimum is 100. |
|`sink.buffer-flush.max-batches` |No |`6` |Integer |Threshold for pending batches that triggers asynchronous refresh to avoid overloading. Minimum is 1. |
|`sink.max-retries` |No |`3` |Integer |Maximum number of attempts when failing to refresh data. Setting it to \-1 means infinite retries. |
|`sink.parallelism` |No |(none) |Integer |The maximum parallelism for refreshing data. By default, parallelism is determined by the framework using the same parallelism as the upstream chained operators. |
|`sink.proactive-validate` |No |`false` |Boolean |Specifies whether to enable proactive data validation (i.e., every record to be validated before adding to the batch). By default, use passive data validation (i.e., data validation is triggered only when data refresh attempts fail) to reduce runtime overhead. |
|`sink.mode` |No |`insert` |String |Select the data records to receive. Supported values include:<br><br><br>* insert: Only accept INSERT records.<br><br>* upsert: (Applicable when the base table is a unique table) Accept INSERT, UPDATE_AFTER, and DELETE records.<br><br>* upsert\-no\-delete: (Applicable when the base table is a unique table) Accept INSERT and UPDATE_AFTER records.<br><br>* Upsert\-all: (Applicable when the base table is a unique table) Accepts all types of records.<br><br>* Upsert\-all\-no\-delete: (Applicable when the base table is a unique table) Accepts all types of records except DELETE.<br><br>* Delete\-only: Only accepts DELETE records. |
|`sink.checkpoint.wait-for-buffer-drained` |No |`false` |Boolean |Allows checkpoints to wait until all buffer batches are completely drained. If set to false, all buffer batches will be written to the checkpoint state during each checkpoint. If the data flush to the table is known to be fast, it is recommended to set it to true. |
|`metrics.update-interval` |No |`5 seconds` |Duration |Fixed interval for refreshing metrics. The minimum time is `5` seconds. |
|`metrics.log-level` |No |`INFO` |String |Log level for recording metrics. This corresponds to [the standard log levels built into Log4J](https://logging.apache.org/log4j/2.x/manual/customloglevels.html). |
|`timestamp-offset` |No |(none) |Duration |Additional time offset for timestamp data. |
|`lookup.async.scale-factor` |No |`1` |Integer |Asynchronous fetch factor. If set to less than 2, the fetch will operate in synchronous (SYNC) mode. If set to n (n \>= 2), the fetch will operate in asynchronous (ASYNC) mode, with a maximum concurrency of n per fetch instance. |
|`lookup.cache.max-rows` |No |`0` |Long |Maximum number of rows in the lookup cache for the data table. If set to 0, caching is disabled. |
|`lookup.cache.ttl` |No |(none) |Duration |Lookup cache TTL for ByteHouse tables. If not specified, no TTL is set for cache records. |
|`lookup.max-retries` |No |`3` |Integer |Maximum allowed retry attempts when a search operation fails. |


<span id="8ec4d1b4"></span>
## Data types

The following table shows the mapping between [Flink SQL data types](https://nightlies.apache.org/flink/flink-docs-release-1.19/docs/dev/table/types/) and [ByteHouse data types](https://docs.byteplus.com/en/docs/bytehouse/data-type). If you need to know.


|**Flink SQL** **field type** |**ByteHouse** **field type** |
|---|---|
|TINYINT |Int8 |
|SMALLINT |Int16 |
|||
|||
|||
|INT |Int32 |
|||
|||
|BIGINT |Int64 |
|||
|DECIMAL(20, 0) |UInt64 |
|FLOAT |Float32 |
|||
|DOUBLE |Float64 |
|||
|DECIMAL(p, s) |Decimal(P, S) |
|||
|||
|BOOLEAN |Int8 |
|||
|DATE |Date |
|TIME [(p)] [WITHOUT TIMEZONE] |TIME [(p)] |
|TIMESTAMP [(p)] [WITHOUT TIMEZONE] |DateTime |
|STRING |String |
|||
|||
|||
|||
|||
|BYTES ||
|||
|||
|ARRAY |ARRAY |


<span id="eaf0eebc"></span>
## Code example

<span id="c70a7526"></span>
### SQL code example

```SQL
CREATE TABLE `bh_de_source` ( -- source table
 `id` BIGINT NOT NULL,
 `time` TIMESTAMP(0),
 `content` ARRAY<DECIMAL(20, 0)>
) WITH (
 'connector' = 'datagen'
);

CREATE TABLE `bh_de_sink` ( -- sink table
 `id` STRING NOT NULL,
 `event_time` STRING,
 `content` ARRAY<DECIMAL(20, 0)>,
 PRIMARY KEY (`id`) NOT ENFORCED -- The primary key field corresponds to the Unique Key of the BH unique key table
) WITH (
 'connector' = 'bytehouse-cdw',
 'jdbc.enable-gateway-connection' = 'true',
 'bytehouse.gateway.region' = 'XXXX_PRIVATE',
 'bytehouse.gateway.host' = 'tenant-xxxx-cn-beijing.bytehouse.byteplus.com',
 'bytehouse.gateway.port' = '19000',
 'bytehouse.gateway.api-token' = '<API_KEY>',
 'bytehouse.gateway.virtual-warehouse' = '<VIRTUAL_WAREHOUSE>',
 'database' = '<BYTEHOUSE_DB>',
 'table-name' = '<BYTEHOUSE_TABLE>'
);

INSERT INTO `bh_de_sink` ( -- data loading
 `id`,
 `event_time`,
 `content`
)
SELECT
 CAST(`id` AS STRING), 
 CAST(`time` AS STRING), 
 `content` 
FROM `bh_de_source`
```


<span id="20190a87"></span>
### Java DataStream code example

The source data type of the Flink connector's DataStream API is `RowData`. The main process of using the DataStream API is to obtain a CnchSinkFunction instance through the CnchSinkFun`CnchSinkFunction instance through the CnchSinkFunctionBuilder`, below is an example demonstrating basic usage. For detailed parameter configuration, please refer to [the ByteHouse official documentation](https://docs.byteplus.com/en/docs/bytehouse/Flink_Connector).

```Java
StreamExecutionEnvironment env = ...;

// Adding a source to the data stream
DataStream<RowData> dataStream =
    env.addSource(...).returns(TypeInformation.of(RowData.class));

// List of columns representing the table schema
List<Column> columns =
    Arrays.asList(
        Column.physical("year", DataTypes.INT()),
        Column.physical("npc", DataTypes.STRING()),
        Column.physical("offence", DataTypes.STRING()),
        Column.physical("case_no", DataTypes.INT()));

try (@SuppressWarnings("unchecked")
    CnchSinkFunction<RowData, ?> cnchSink =
        new CnchSinkFunctionBuilder.Insert(database, tableName)
            .withSchema(columns)
            .withGatewayConnection("XXXX_PRIVATE", "your_host", "your_port")
            .withGatewayApiToken("<< your API token >>")
            .withGatewayVirtualWarehouse("default_vw")
            .withFlushInterval(Duration.ofSeconds(1))
            .build()) {

    // Add the sink to the data stream
    dataStream.addSink(cnchSink);

    // Trigger the execution
    env.execute();
}
```


<span id="841bc9e1"></span>
## Frequently Asked Questions

<span id="3f34da5a"></span>
### Writing to ByteHouse tasks fails due to network disconnection, unable to verify SQL and start tasks

**Problem Description**: Long delays in using SQL verification function, eventually leading to a timeout exception This prevents SQL verification from succeeding For online tasks, this might result in prolonged inability to start, eventually failing

**Reason for the Problem**: In the process of SQL verification and syntax parsing, it tries to access ByteHouse server for metadata retrieval During this time, if the network is inaccessible, it could lead to prolonged delays

**Solution**:


1. In the ByteHouse CDW product interface, under Tenant Management \- Basic Information \- Network Information, check whether the VPC and subnet for the Flink task's resource pool are the same as those for ByteHouse VPC and subnet:

   1. If they are in different VPCs, the networks are not connected by default. It is recommended to create a Flink resource pool matching the ByteHouse VPC (recommended). [Create Resource Pool](https://docs.byteplus.com/docs/flink/Create_Resource_Pool)Alternatively, set up the public access domain name using the [network information settings](https://docs.byteplus.com/en/docs/bytehouse/network-settings) approach, with Flink accessing through the public network (not recommended).

   2. If they are in the same VPC

      1. Please check if the security groups are the same; if different, ensure that the security group’s rules do not restrict access to ByteHouse. If there are port or IP restrictions, consider lifting them as needed.

      2. Please check if Flink and ByteHouse are in the same subnet; if not, verify in **Private Network \- Network ACL** whether there are network access restrictions between the subnets. If there are, disable these restrictions.


<span id="f8a19f31"></span>
### Future times appear after importing into ByteHouse

**Problem description**:


1. In the upstream Kafka data source, there are fields with timestamp string formats such as `{"t": "2024-10-17 10:00:00"}`.

2. The DDL statement in Flink defines the field `t` as TIMESTAMP type.

3. The downstream data types in ByteHouse are either DateTime or DateTime64.

4. Query results written into ByteHouse with timestamp `2024-10-17 18:00:00`.


**The root cause**: When the timestamp data from the source end (e.g., Kafka data source) is output in a non\-timezone format (like "2024\-10\-17 10:00:00"), it is parsed by default as an Epoch timestamp in UTC; if the business timezone of the source end is not UTC, then this method of outputting timestamp values inadvertently introduces a time difference between UTC and the business timezone of the source end.

**The solution**:


1. Recommended solution one: In Kafka data sources, it is advised to use UTC time, such as "2024\-10\-17T10:00:00Z", and define the field type as TIMESTAMP_LTZ in the Flink table creation statement.

2. Recommended solution two: Add `'timestamp-offset' = '-8h'` in the WITH OPTIONS of the Flink ByteHouse table statement, so that it takes effect in a single ByteHouse Sink.

3. Recommended solution three: Set variables uniformly in Flink tasks, similar in effect to the second solution but applies to all ByteHouse Sinks in Flink tasks `containerized.taskmanager.env.FLINK_WRITE_TO_BYTEHOUSE_TIMESTAMP_OFFSET: -8h`.
