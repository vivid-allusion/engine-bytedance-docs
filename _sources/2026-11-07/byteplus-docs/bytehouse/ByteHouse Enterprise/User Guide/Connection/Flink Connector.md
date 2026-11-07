---
title: "Flink Connector"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/flink-connector"
---

Flink Connector for ByteHouse is specifically designed to load data into ByteHouse via Flink. This document introduces how to connect ByteHouse using the Flink Connector and provides examples of data writing into ByteHouse in typical scenarios.

<span id="2941018a"></span>
# Background information

Flink Connector can connect to ByteHouse and handle data through [Table API&SQL](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/table/overview/) and [DataStreamAPI](https://nightlies.apache.org/flink/flink-docs-stable/docs/dev/datastream/overview/) of Flink. Before connecting to ByteHouse, you need to download and install the corresponding version of the driver and add the required dependencies according to the guide below. Once the preparations are complete, you can use the Connector to connect to ByteHouse for data processing.

<span id="35200fee"></span>
# Preparation work

<span id="e9536e29"></span>
## Download the driver


|**Flink Version** |**Driver** |**Release Date** |
|---|---|---|
|1.18 |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39e2eec136c5437fa84d2044143ab2f6~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.18.jar">flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.18.jar</Attachment><br> |2025\-01\-13 |
|1.17 |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77720d5beff249bcad871a03e42bbf02~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.17.jar">flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.17.jar</Attachment><br> |2025\-01\-13 |
|1.16 |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66ea00a355cb448eb8bf36ebdf6dc63e~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.16.jar">flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.16.jar</Attachment><br> |2025\-01\-13 |
|1.15 |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eea5be5c23549c7bc24986beaca5e4e~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.15.jar">flink-sql-connector-bytehouse-ce_2.12-1.27.117-1.15.jar</Attachment><br> |2025\-01\-13 |
|1.13<br><br>(Scala version: 2.11 and above) |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/217690a0834f425389bc0ca50f5fd3fc~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce-1.27.43-1.13.jar">flink-sql-connector-bytehouse-ce-1.27.43-1.13.jar</Attachment><br> |2024\-03\-25 |
|1.11<br><br>(Scala version: 2.11 and above) |<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcc97ef208a7481ba8cd2176bbce4fb0~tplv-goo7wpa0wc-image.image" name="flink-sql-connector-bytehouse-ce_2.11-1.27.104-1.11.jar">flink-sql-connector-bytehouse-ce_2.11-1.27.104-1.11.jar</Attachment><br> |2024\-10\-23 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please use the driver that matches the Flink version to ensure proper functionality.</div>


<span id="dd21f040"></span>
## Local Installation

To install the downloaded `flink-sql-connector-bytehouse-ce-${flink-sql-connector-bytehouse-ce.version}.jar` file to the local Maven repository, please run the following command:

```Bash
mvn install:install-file \
    -Dfile=${your_path}/flink-sql-connector-bytehouse-ce-${flink-sql-connector-bytehouse-ce.version}.jar \
    -DgroupId=com.bytedance.bytehouse \
    -DartifactId=flink-sql-connector-bytehouse-ce \
    -Dversion=${flink-sql-connector-bytehouse-ce.version} \
    -Dpackaging=jar
```


<span id="7a1381d2"></span>
## Add Maven Dependency

For Maven projects that compile using the Flink connector, add the following dependencies to your project's `pom.xml` file. `scala.version` is either 2.11 or 2.12, corresponding to the associated Scala version of the Flink release. `${flink-sql-connector-bytehouse-ce.version}` can be set to the desired version of the Flink connector.

```XML
<dependency>
    <groupId>com.bytedance.bytehouse</groupId>
    <artifactId>flink-sql-connector-bytehouse-ce</artifactId>
    <version>${flink-sql-connector-bytehouse-ce.version}</version>
</dependency>
```


<span id="951c2b71"></span>
# Usage instructions

<span id="8e11514a"></span>
## DDL definition

```SQL
CREATE TABLE bh_ce_sink (
  f0 VARCHAR,
  f1 VARCHAR,
  f2 VARCHAR
) WITH (
  'connector' = 'bytehouse-ce',
  'clickhouse.cluster' = 'bytehouse_cluster_***',
  'clickhouse.shard-discovery.service.host' = '7249621***.bytehouse-ce.ibytepluses.com',
  'username' = 'user_a',
  'password' = 'pa***45',
  'database' = 'default',
  'table-name' = 'doc_test',
  'sink.buffer-flush.interval' = '10 second',
  'sink.buffer-flush.max-rows' = '5000',
  'clickhouse.shard-discovery.address-mapping' = '192.18.*.*|8123:192.168.*.*|8123'
);
```


<span id="642864b1"></span>
## Explanation of parameters with "With"


|**Options** |**Mandatory** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|`connector` |Yes |No |String |Specify the connector to be used. Configure as `bytehouse-ce` (ByteHouse Enterprise Edition) or `clickhouse`. |
|`database` |Yes |No |String |The name of the ByteHouse Enterprise Edition database to connect to. |
|`table-name` |Yes |No |String |The name of the ByteHouse Enterprise Edition table to connect to.<br><br>Please note that the "table" here refers to the local table of each shard. |
|`clickhouse.cluster` |Yes |None |String |ByteHouse cluster name. |
|`clickhouse.shard-discovery.kind` |No |`SYSTEM_CLUSTERS` |String |Type of ByteHouse shard discovery. Supported values are:<br><br><br>* `SYSTEM_CLUSTERS`: Retrieve shard IPs through system.cluster.<br><br>* `CE_GATEWAY`: Retrieve shard IP through ByteHouse Enterprise Edition Gateway. It's possible to track this way when connected via a public network, but it's not recommended in a production environment.<br><br>* `CE_API_CLUSTERS`: Retrieve shard IP through a specific OpenAPI of ByteHouse Enterprise Edition. Recommended for use in production. |
|`clickhouse.shard-discovery.service.host` |No |`127.0.0.1` |String |Hostname of the ByteHouse Shard Discovery Service. |
|`clickhouse.shard-discovery.service.port` |No |`8123` |Integer |Port number for ByteHouse shard discovery service. |
|`clickhouse.shard-discovery.address-mapping` |No |None |Map |Address mapping of discovered shards. |
|`bytehouse-ce.api.get-shard-info` |No |Internal |String |ByteHouse API used for retrieving shard information. |
|`bytehouse-ce.api.account-id` |No |None |String |Main account ID of BytePlus calling the ByteHouse API. |
|`bytehouse.ce.gateway.host` |No |None |String |Host of ByteHouse Enterprise Edition Gateway. |
|`bytehouse.ce.gateway.port` |No |`8123` |Integer |Port of ByteHouse Enterprise Edition Gateway. |
|`username` |No |None |String |JDBC connection username. |
|`password` |No |None |String |JDBC connection password. |
|`jdbc.query.timeout` |No |`1 minute` |Duration |Timeout setting for executing queries through JDBC. |
|`sink.group-by.key` |No |None |String |Key for pre\-sink grouping. Key can consist of multiple fields, separated by commas. |
|`sink.group-by.expression` |No |None |String |Expression for pre\-receiver grouping. If set, all relevant field names must also be listed in `sink.group-by.key`. |
|`sink.group-by.number-of-groups` |No |None |Integer |The number of group limits set by the pre\-receiver for logging. The value cannot be less than `sink.parallelism`.<br><br><br>* If not set, it will take the value of `sink.parallelism`.<br><br>* It is recommended to set this value to a multiple of the number of shards, where the multiple is a positive integer (e.g., 1, 2, 3) or a negative power of 2 (e.g., 1/2, 1/4, 1/8). |
|`sharding-strategy` |No |None |String |ByteHouse distributed sharding strategy. Supported values include:<br><br><br>* `NONE`: Do not perform write partitioning.<br><br>* `RANDOM`: Random writing.<br><br>* `ROUND_ROBIN`: Sequential writing (round\-robin).<br><br>* `HASH`: Write by hashing based on the shard_key. |
|`sharding-key` |No |None |String |Key for hash partitioning. The key can contain multiple fields, separated by commas. |
|`sharding-expression` |no |none |String |Expression for hash partitioning. If this option is set, all involved field names must also be listed in `sharding-key`. |
|`sink.buffer-flush.interval` |no |`1 second` |Duration |The maximum interval between two batch flushing. The minimum value is `200 ms`.<br><br>During use, flushing will be triggered when either the `sink.buffer-flush.interval` or `sink.buffer-flush.max-rows` condition is met. |
|`sink.buffer-flush.max-rows` |No |`20,000` |Integer |The maximum number of records buffered before flushing. The value must be at least `100`.<br><br>During use, flushing will be triggered when either the `sink.buffer-flush.interval` or `sink.buffer-flush.max-rows` condition is met. |
|`sink.buffer-flush.max-batches` |No |`6` |Integer |The threshold of pending batches triggered by asynchronous refresh to prevent overload. The minimum value is `1`. |
|`sink.max-retries` |No |`3` |Integer |The maximum number of retries when data refresh fails. Setting it to `-1` means unlimited retries. |
|`sink.parallelism` |No |None |Integer |Max degree of parallelism for refreshing data. By default, the degree of parallelism is determined by the framework using the same parallelism as the upstream chained operator. Generally, it is suggested to be the same as the number of shards. |
|`sink.proactive-validate` |No |`false` |Boolean |Specifies whether to enable proactive data verification (i.e., to verify each record before adding it to the batch). By default, passive data verification (i.e., data verification is triggered only when a data refresh attempt fails) is used to minimize runtime overhead. |
|`sink.mode` |No |`insert` |String |Select the data records to be received. Supported values include:<br><br><br>* `Insert`: Only accepts records with `INSERT` actions.<br><br>* `upsert`: Accepts records for `INSERT`, `UPDATE_AFTER`, and `DELETE`.<br><br>* `upsert-no-delete`: Accepts records for `INSERT` and `UPDATE_AFTER`.<br><br>* `upsert-all`: Accepts all types of records.<br><br>* `upsert-all-no-delete`: Accepts all records except those for `DELETE`.<br><br>* `delete-only`: Only accepts records for `DELETE`.<br><br><br>If set to any value other than `insert`, the ByteHouse table must contain a UNIQUE KEY clause. In addition, the PRIMARY KEY of the corresponding Flink table must include all column names that are part of the UNIQUE KEY in the ByteHouse table. |
|`metrics.update-interval` |No |`5 seconds` |Duration |Fixed intervals for refreshing metrics. The shortest interval is `5 seconds`. |
|`metrics.log-level` |No |`INFO` |String |Log level for log metrics. This corresponds to [the standard Log4J built-in log levels](https://logging.apache.org/log4j/2.x/manual/customloglevels.html). |
|`timestamp-offset` |No |None |Duration |Additional time offset for Timestamp data. |
|`lookup.async.scale-factor` |No |`1` |Integer |Scale factor for asynchronous lookup.<br><br><br>* If set to less than 2, the lookup runs in Sync Mode.<br><br>* If set to `n` (`n>=2`), it operates in an asynchronous (ASYNC) mode, and each lookup instance has a maximum concurrency of `n`. |
|`lookup.cache.max-rows` |No |`0` |Long |The maximum number of rows in the Table's lookup cache. If set to 0, caching is inactivated. |
|`lookup.cache.ttl` |No |None |Duration |TTL for the lookup cache of the ByteHouse table. If not specified, no TTL is set for the cached records. |
|`lookup.max-retries` |No |`3` |Integer |The maximum number of retries allowed when a lookup operation fails. |
|`jdbc.max-retry-backoff` |No |`32 seconds` |Duration |Maximum backoff time between continuous attempts to refresh data.<br><br>Please note that batch refresh retries use exponential backoff, starting with a 1 second latency. |
|`max-rows-per-second` |No |`0` |Long |The maximum number of rows that can be processed per second. If set to a non\-positive value, rate limiting is disabled.<br><br>Optional for lookup and sink, currently not applicable for source. |


<span id="dc8b0b99"></span>
## Data type mapping


|**Fink SQL Field Type** |**ByteHouse Field Type** |
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
|TIME [(p)] [WITHOUT TIMEZONE] |Not supported yet, use String Type instead |
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


<span id="c0638cd4"></span>
# Usage example

<span id="74c49916"></span>
## Flink SQL

<span id="30c95b1b"></span>
### Example of results

The following is an example of loading data from an AWS Kinesis Data Stream table (bh_ce_source) into a ByteHouse CE table (bh_ce_sink).

```SQL
CREATE TEMPORARY TABLE `bh_ce_source` (  -- source table
  `id` BIGINT NOT NULL,
  `time` TIMESTAMP(0),
  `content` ARRAY<DECIMAL(20, 0)>
) WITH (
  'connector' = 'kinesis',
  'stream' = 'demo_stream',
  'format' = 'json',
  'aws.region' = 'cn-north-1',
  'aws.credentials.provider' = 'BASIC',
  'aws.credentials.basic.accesskeyid' = '???',
  'aws.credentials.basic.secretkey' = '???',
  'scan.shard.getrecords.maxretries' = '7'
);

CREATE TEMPORARY TABLE `bh_ce_sink` (  -- sink table
  `id` STRING NOT NULL,
  `event_time` STRING,
  `content` ARRAY<DECIMAL(20, 0)>
) WITH (
  'connector' = 'bytehouse-ce',
  'clickhouse.shard-discovery.kind' = 'CE_API_CLUSTERS',
  'clickhouse.shard-discovery.service.host' = '7314499681491849526.bytehouse-ce.ibytepluses.com',
  'clickhouse.shard-discovery.service.port' = '80',
  'bytehouse-ce.api.get-shard-info' = '/openapi/v1/clusters/{cluster_name}/nodes',
  'bytehouse-ce.api.account-id' = '<< your BytePlus account ID >>',
  'username' = '<< your ByteHouse CE username >>',
  'password' = '<< your ByteHouse CE password >>',
  'sink.buffer-flush.interval' = '1 second',
  'sink.buffer-flush.max-rows' = '5000',
  'sink.parallelism' = '10',  -- Recommended to be no more than the number of shards
  'clickhouse.cluster' = '<< your cluster name of ByteHouse CE >>',
  'database' = 'my_db',
  'table-name' = 'my_table_local',  -- MUST BE LOCAL TABLE
  'sink.group-by.key' = 'event_time',
  'sink.group-by.expression' = 'cityHash64(event_time)',
  'sink.group-by.number-of-groups' = '16',  -- Need to be n (n > 0) times of the number of shards
  'sharding-strategy' = 'HASH',
  'sharding-key' = 'event_time',
  'sharding-expression' = 'cityHash64(event_time)'
);

INSERT INTO `bh_ce_sink` (  -- data loading
  `id`,
  `event_time`,
  `content`
)
SELECT
  IFNULL(CAST(`id` AS STRING), '43'),  -- type casting with default value
  CAST(`time` AS STRING),  -- type casting
  IFNULL(`content`, ARRAY[123,12345])  -- default value
FROM `bh_ce_source`
```


<span id="7b24641f"></span>
### Maintenance example

Below is an example of querying using ByteHouse CE tables through FlinkSQL.

```SQL
CREATE TABLE main_table (
  some_id BIGINT,
  proctime AS PROCTIME()
) WITH (
  'connector' = 'datagen',
  'fields.some_id.kind' = 'random',
  'fields.some_id.min' = '0',
  'fields.some_id.max' = '799999',
  'rows-per-second' = '1000',
  'number-of-rows' = '100000'
);

CREATE TABLE lookup_table (
  aiid VARCHAR,
  content VARCHAR,
  PRIMARY KEY (aiid) NOT ENFORCED
) WITH (
  'connector' = 'bytehouse-ce',
  ---- Connection settings ----
  'clickhouse.shard-discovery.kind' = 'CE_API_CLUSTERS',
  'clickhouse.shard-discovery.service.host' = '7314499681491849526.bytehouse-ce.ibytepluses.com',
  'clickhouse.shard-discovery.service.port' = '80',
  'bytehouse-ce.api.get-shard-info' = '/openapi/v1/clusters/{cluster_name}/nodes',
  'bytehouse-ce.api.account-id' = '<< your BytePlus account ID >>',
  'username' = '<< your ByteHouse CE username >>',
  'password' = '<< your ByteHouse CE password >>',
  ---- Lookup settings ----
  'lookup.async.scale-factor' = '8', -- set '1' to disable asynchronous lookup, i.e. SYNC mode
  'lookup.cache.max-rows' = '0', -- set '0' to disable caching
  'lookup.cache.ttl' = '1 minute',
  'clickhouse.query.enable-log' = 'false', -- set 'true' for debugging
  ---- Table settings ----
  'clickhouse.cluster' = '<< your cluster name of ByteHouse CE >>',
  'database' = 'my_db',
  'table-name' = 'my_lookup_all'  -- NEED TO BE DISTRIBUTED TABLE
  'sharding-strategy' = 'HASH',
  'sharding-key' = 'aiid',
  'sharding-expression' = 'cityHash64(aiid)' -- same as that set for the distributed table
);

CREATE TABLE print_sink (
  some_id BIGINT,
  content VARCHAR
) WITH (
  'connector' = 'print'
);

INSERT INTO print_sink
SELECT
  m.some_id,
  l.content
FROM
  main_table AS m
JOIN
  lookup_table FOR SYSTEM_TIME AS OF m.proctime AS l
ON
  CAST(m.some_id AS VARCHAR) = l.aiid;
```


<span id="0530ae62"></span>
## Flink DataStream API

<span id="1e4cd388"></span>
### Example of results

```SQL
package bytehouse.flink.connectoer.demo;
import com.bytedance.bytehouse.flink.connector.clickhouse.ClickHouseSinkFunction;
import com.bytedance.bytehouse.flink.connector.clickhouse.api.java.ClickHouseSinkFunctionBuilder;
import com.bytedance.bytehouse.flink.table.api.RowDataConstructor;
import org.apache.flink.api.common.functions.RuntimeContext;
import org.apache.flink.api.common.typeinfo.TypeInformation;
import org.apache.flink.runtime.state.FunctionInitializationContext;
import org.apache.flink.streaming.api.datastream.DataStream;
import org.apache.flink.streaming.api.environment.StreamExecutionEnvironment;
import org.apache.flink.streaming.api.functions.source.datagen.DataGenerator;
import org.apache.flink.streaming.api.functions.source.datagen.DataGeneratorSource;
import org.apache.flink.table.api.DataTypes;
import org.apache.flink.table.catalog.Column;
import org.apache.flink.table.data.RowData;
import org.apache.flink.table.types.DataType;

import java.time.Duration;
import java.time.LocalDateTime;
import java.util.Arrays;
import java.util.List;
import java.util.Random;
public class AcceptLogSinkDataStreamExample {
    public static void main(String[] args) throws Exception {
        final String gatewayHost = args[0];
        final String username = args[1];
        final String password = args[2];
        final String clusterName = args[3];
        final String dbName = args[4];
        final String tableName = args[5];
        final long rowsPerSecond = Long.parseLong(args[6]);
        final long numberOfRows = Long.parseLong(args[7]);
        // Creating the execution environment
        final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
        // Adding a source to the data stream
        DataStream<RowData> dataStream =
                env.addSource(
                                new DataGeneratorSource<>(new RowDataGenerator(), rowsPerSecond, numberOfRows))
                        .returns(TypeInformation.of(RowData.class));
        // List of columns representing the table schema
        List<Column> columns =
                Arrays.asList(
                        Column.physical("create_time", DataTypes.TIMESTAMP(0)),
                        Column.physical("completion_id", DataTypes.STRING()),
                        Column.physical("device_mid", DataTypes.STRING()));
        try (@SuppressWarnings("unchecked")
             ClickHouseSinkFunction<RowData> sink =
                     new ClickHouseSinkFunctionBuilder.Upsert(clusterName, dbName, tableName)
                             .withSchema(columns)
                             .withShardDiscoveryKind("CE_GATEWAY")
                             .withGateway(gatewayHost)
                             .withAccount(username, password)
                             .withPrimaryKey(Arrays.asList("completion_id"))
                             .withShardingKey("completion_id")
                             .withFlushInterval(Duration.ofSeconds(1))
                             .build()) {
            // Add the sink to the data stream
            dataStream.addSink(sink);
            // Trigger the execution
            env.execute();
        }
    }
    static class RowDataGenerator implements DataGenerator<RowData> {
        private final Random random = new Random();
        private final RowDataConstructor rowDataConstructor =
                RowDataConstructor.apply(
                        new DataType[] {DataTypes.TIMESTAMP(0), DataTypes.STRING(), DataTypes.STRING()});
        @Override
        public RowData next() {
            final Object[] rowDataFields = {
                    LocalDateTime.now(), "CID-" + random.nextInt(1000), "DMID-" + random.nextInt(1000)
            };
            return rowDataConstructor.constructInsert(rowDataFields);
        }
        @Override
        public void open(
                String name, FunctionInitializationContext context, RuntimeContext runtimeContext)
                throws Exception {
            // Initialization code here (if needed)
        }
        @Override
        public boolean hasNext() {
            return true; // Continuous generation
        }
    }
}
```
