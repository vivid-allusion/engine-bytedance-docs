---
title: "ByteHouse CE"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/ByteHouse_CE"
---

In the Flink console, the ByteHouse CE connector supports result tables, and data can be written to the ByteHouse target table through Flink tasks.

<span id="194abd9a"></span>
## Background Information

ByteHouse is a cloud\-native data warehouse, a version deeply optimized and modified by Byteplus Engine based on the open\-source ClickHouse, offering stronger query services and data writing performance for massive data.

ByteHouse CE is deeply customized based on the rich scenarios within Byteplus as well as pain points in the open\-source version of ClickHouse, including multi\-scenario table engines, extended data types, and multi\-level storage. For more information about ByteHouse CE, please refer to [ByteHouse CE Overview](https://docs.byteplus.com/en/docs/bytehouse/intro).

<span id="a52e4a07"></span>
## Usage Limitations

The ByteHouse CE connector is currently only supported in the **Flink 1.16\-byted** engine version.

<span id="54e96f65"></span>
## DDL Definition

```SQL
CREATE TABLE bh_ce_sink (
  f0 VARCHAR,
  f1 VARCHAR,
  f2 VARCHAR
) WITH (
  'connector' = 'bytehouse-ce',
  'clickhouse.cluster' = 'bytehouse_cluster_***',
  'clickhouse.shard-discovery.service.host' = '7249621***.bytehouse-ce.byteplus.com',
  'username' = 'user_a',
  'password' = 'pa***45',
  'database' = 'default',
  'table-name' = 'doc_test',
  'sink.buffer-flush.interval' = '10 second',
  'sink.buffer-flush.max-rows' = '5000',
  'clickhouse.shard-discovery.address-mapping' = '192.18.*.*|8123:192.168.*.*|8123'
);
```


<span id="bfacb72d"></span>
## Data Type Mapping

The following table maps the [Flink SQL data types](https://nightlies.apache.org/flink/flink-docs-release-1.19/docs/dev/table/types/) to the [ByteHouse data types](https://docs.byteplus.com/en/docs/bytehouse/data-type). If you need to learn


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
|||
|||
|BOOLEAN |Int8 |
|||
|DATE |Date |
|TIME [(p)] [WITHOUT TIMEZONE] |Not supported, please use String type as a substitute |
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


<span id="f6f66406"></span>
## WITH parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to use, here it is `ByteHouse CE` or `ClickHouse` connector. |
|database |Yes |(none) |String |Database name. You need to create the database in advance in the ByteHouse CE console, see [create database and tables](https://docs.byteplus.com/en/docs/bytehouse/docs-databases-tables-and-views). |
|table\-name |Yes |(none) |String |Table name. You need to create the table in advance in the ByteHouse CE console, see [create database and tables](https://docs.byteplus.com/en/docs/bytehouse/docs-databases-tables-and-views). |
|clickhouse.cluster |Yes |(none) |String |ByteHouse CE cluster name. You must create the cluster in advance via the ByteHouse CE console, see [create a cluster](https://docs.byteplus.com/en/docs/bytehouse/getting-started). |
|clickhouse.shard\-discovery.kind |No |SYSTEM_CLUSTERS |String |Shard discovery type.<br><br><br>* `SYSTEM_CLUSTERS`: By querying the `system.clusters` table to obtain the shard's IP.<br><br>* `CONSUL`: By using the Consul service to obtain the shard's IP.<br><br>* `API_CLUSTERS`: By using specific OpenAPI of ByteHouse CE to obtain the shard's IP.<br><br>* `CE_GATEWAY`: By using ByteHouse CE Gateway to obtain the shard's IP. |
|clickhouse.shard\-discovery.service.host |No |127.0.0.1 |String |The host address of the shard discovery service. |
|clickhouse.shard\-discovery.service.port |No |8123 |Integer |Port number for shard discovery service. |
|clickhouse.shard\-discovery.address\-mapping |No |(none) |Map |Shard discovery address mapping that maps the actual shard addresses to accessible addresses.<br><br>Example: `192.18.*.*\|8123:192.168.*.*\|8123` *.*  |
|bytehouse\-ce.api.get\-consul\-info |No |(built\-in) |String |ByteHouse CE API for retrieving Consul service information |
|bytehouse\-ce.api.get\-shard\-info |No |(built\-in) |String |ByteHouse CE API for retrieving shard information |
|bytehouse\-ce.auth.api |No |(built\-in) |String |ByteHouse CE API used for authentication. |
|username |No |(none) |String |JDBC username.<br><br>To set up a username, a password must also be configured. |
|password |No |(none) |String |JDBC user password. |
|sharding\-strategy |No |NONE |String |Partitioning Strategy.<br><br><br>* `NONE`: No partitioning.<br><br>* `RANDOM`: Random partitioning.<br><br>* `ROUND_ROBIN`: Partitioning based on the sequence of data arrivals.<br><br>* `HASH`: Partitioning based on the content of data. |
|sharding\-key |No |(none) |String |Hash partitioning key, used to determine the distribution of data across different shards. It can consist of one or more fields, separated by commas between multiple fields. |
|sharding\-expression |No |(none) |String |Hash partitioning expression, used to determine the distribution of data across different shards. If a hash partitioning expression is set, the names of all relevant fields must also be listed in the partition key. |
|sink.buffer\-flush.interval |No |1 second |Duration |Refresh interval, minimum of `200 ms`. |
|sink.buffer\-flush.max\-rows |No |50,000 |Integer |Buffer record size, minimum of `100`. |
|sink.buffer\-flush.max\-batches |No |6 |Integer |The maximum number of batches for data writing into the Sink buffer, with the minimum value being `1`. |
|sink.max\-retries |No |\-1 |Integer |The maximum number of attempts when data refresh fails. Set to `-1`, which means unlimited retries. |
|sink.parallelism |No |(none) |Integer |Parallelism for refreshing data. By default, it maintains the same parallelism as the upstream operators. |
|sink.proactive\-validate |No |false |Boolean |Whether to proactively validate data.<br><br><br>* true: Proactively validate data. Verify each record before batch processing.<br><br>* False: Default value, passive data validation. Trigger data validation when data refresh attempt fails. |
|sink.enable\-upsert |No |false |Boolean |Whether to enable Upsert operations (insert or update) to the Sink.<br><br>When `sink.enable-upsert` is set to `true`, upsert operations are allowed, which means if data already exists it will be updated, otherwise inserted.<br><br>Since not all Sinks support upsert operations, please ensure your Sink supports this operation before enabling `sink.enable-upsert`. Otherwise, it may lead to errors or unpredictable behavior. |
|metrics.update\-interval |No |5 seconds |Duration |The interval for refreshing metrics, with a minimum setting of 5 seconds. |
|metrics.log\-level |No |INFO |String |Log level.<br><br>For more information, please refer to [Log4j built-in log levels](https://logging.apache.org/log4j/2.x/manual/customloglevels.html). |


<span id="06006a3b"></span>
## Example code

```SQL
CREATE TABLE random_source (
   f0 VARCHAR,
   f1 VARCHAR,
   f2 VARCHAR
 ) WITH (
   'connector' = 'datagen',
   'rows-per-second' = '1'
 );

CREATE TABLE bh_ce_sink (
  f0 VARCHAR,
  f1 VARCHAR,
  f2 VARCHAR
) WITH (
  'connector' = 'bytehouse-ce',
  'clickhouse.cluster' = 'bytehouse_cluster_***',
  'clickhouse.shard-discovery.service.host' = '7249621***.bytehouse-ce.byteplus.com',
  'username' = 'user_a',
  'password' = 'pa***45',
  'database' = 'default',
  'table-name' = 'doc_test',
  'sink.buffer-flush.interval' = '10 second',
  'sink.buffer-flush.max-rows' = '5000',
  'clickhouse.shard-discovery.address-mapping' = '192.18.*.*|8123:192.168.*.*|8123'
);

INSERT INTO bh_ce_sink 
SELECT f0, f1, f2 FROM random_source;
```


<span id="4fc6fac9"></span>
## Common questions

<span id="a5f5968a"></span>
### Future timestamps appear after importing into ByteHouse

**Problem description**:


1. In the upstream Kafka data source, fields are formatted as string timestamps, for example `{"t": "2024-10-17 10:00:00"}`

2. The Flink DDL statement defines the `t` field as TIMESTAMP type.

3. The downstream data type in ByteHouse is either DateTime or DateTime64.

4. The result of querying the timestamp in ByteHouse is `2024-10-17 18:00:00`


**The cause of the issue**: When the timestamp data from the source (such as Kafka data source) is output in a format without timezone (like “2024\-10\-17 10:00:00”), it is parsed by default as Epoch timestamp in UTC; if the timezone of the source business is not UTC, this method of outputting timestamps will indirectly introduce an hour offset between UTC and the source business's timezone.

**Solution**:


1. Recommended approach one: It is advised to use UTC time in the Kafka data source, such as "2024\-10\-17T10:00:00Z", and to define the field type as TIMESTAMP_LTZ in the Flink table creation statement.

2. Recommended approach two: Add `'timestamp-offset' = '-8h'` in the WITH OPTIONS of the ByteHouse table creation statement in Flink, effective in a single ByteHouse Sink.

3. Recommended approach three: Set the variable uniformly in the Flink job, similar in effect to approach two, but effective for all ByteHouse Sinks in the Flink job`containerized.taskmanager.env.FLINK_WRITE_TO_BYTEHOUSE_TIMESTAMP_OFFSET: -8h`
