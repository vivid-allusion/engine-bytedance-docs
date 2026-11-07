---
title: "StarRocks Flink Connector"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_Flink_Connector"
---

StarRocks supports reading or writing data through Flink. You can use the Flink Connector to connect Flink and StarRocks for data import. The principle is to batch data in memory and use Stream Load to import the data into StarRocks in batches. The Flink Connector supports the DataStream API, Table API & SQL, as well as the Python API, and offers better performance and stability compared to the official Flink [JDBC Connector](https://nightlies.apache.org/flink/flink-docs-master/docs/connectors/table/jdbc/).

<span id="_1-获取-flink-connector"></span>
## Obtain the Flink Connector

You can download the latest `flink-connector-starrocks.jar` file that matches your Flink version from [StarRocks Flink Connector](https://docs.byteplus.com/docs/E-MapReduce/109509), or use the Flink Connector version provided by the EMR team.

The Flink Connector Jar file provided by the EMR team is included with the Flink installation package. You can find the corresponding jar file in the EMR cluster that supports deploying Flink components at `/usr/lib/emr/current/flink/connectors`.

Compared to the open\-source version of the Flink Connector, we recommend using the version provided by the EMR team, which has the following advantages:


1. Better integration with EMR clusters and their surrounding ecosystem.

2. Additional competitive features custom\-developed by the EMR team.

3. More timely fixes for known bugs.


However, maintaining compatibility with open source is a fundamental principle of EMR as an open\-source big data platform, so you can still choose to use the open\-source Flink Connector version.

<span id="_2-使用方式"></span>
## Usage

This section uses importing data into the StarRocks detail table `examples.tb_duplicate_key` as an example. The table creation statement is as follows:

```SQL
CREATE TABLE IF NOT EXISTS tb_duplicate_key
(
    event_time BIGINT       NOT NULL COMMENT 'timestamp of event',
    event_type INT          NOT NULL COMMENT 'type of event',
    user_id    INT          NOT NULL COMMENT 'id of user',
    device     VARCHAR(128) NULL     COMMENT 'device'
) ENGINE = OLAP DUPLICATE KEY(event_time, event_type)
DISTRIBUTED BY HASH(user_id)
PROPERTIES (
    'replication_num' = '3'
);
```


<span id="_2-1-flink-sql-方式"></span>
### Flink SQL method

You can write data directly into the corresponding StarRocks table using Flink SQL. The steps are as follows:


1. Enter the Flink SQL interactive terminal. Refer to [Flink SQL Client usage reference](https://docs.byteplus.com/docs/E-MapReduce/109229) to enter the Flink SQL interactive terminal. Here, YARN Session mode is used as an example.

2. Create a mapping table for the StarRocks `tb_duplicate_key` table using `CREATE TABLE`. The table name does not need to be the same:


```SQL
CREATE TABLE IF NOT EXISTS tb_duplicate_key
(
    event_time BIGINT       NOT NULL COMMENT 'timestamp of event',
    event_type INT          NOT NULL COMMENT 'type of event',
    user_id    INT          NOT NULL COMMENT 'id of user',
    device     VARCHAR(128) NULL COMMENT 'device'
)
WITH (
    'connector' = 'starrocks',
    'jdbc-url' = 'jdbc:mysql://{fe_ip}:9030',
    'load-url' = '{fe_ip}:8030',
    'database-name' = 'examples',
    'table-name' = 'tb_duplicate_key',
    'username' = 'system_query_user',
    'password' = '***'
);
```



3. Insert data into the mapping table using the `INSERT INTO` operation:


```SQL
INSERT INTO tb_duplicate_key
VALUES (1703128450, 1, 1001, 'PHONE'),
       (1703128451, 0, 1002, 'PAD'),
       (1703128452, 1, 1003, 'TV');
```


Normally, you can query the data just written from the Flink side in StarRocks.

<span id="_2-2-flink-datastream-方式"></span>
### Flink DataStream method

You can also write a corresponding Flink DataStream job according to the input data type to sink data into the specified StarRocks table. Supported data formats include CSV, JSON, and custom Java objects.

<span id="_2-2-1-csv-格式数据示例"></span>
#### CSV format data example

This section demonstrates how to import CSV data constructed in memory into the StarRocks `tb_duplicate_key` table using the Flink DataStream method. The sample code is as follows:

```Java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

// Simulate CSV format data
String[] records = new String[]{
        "1703128450, 1, 1001, PHONE",
        "1703128451, 0, 1002, PAD",
        "1703128452, 1, 1003, TV"
};

DataStream<String> source = env.fromElements(records);

// Configure Sink options
StarRocksSinkOptions options = StarRocksSinkOptions.builder()
        .withProperty("jdbc-url", "jdbc:mysql://{fe_ip}:9030")
        .withProperty("load-url", "{fe_ip}:8030")
        .withProperty("database-name", "examples")
        .withProperty("table-name", "tb_duplicate_key")
        .withProperty("username", "system_query_user")
        .withProperty("password", "******")
        .withProperty("sink.properties.format", "csv")
        .withProperty("sink.properties.column_separator", ",")
        .build();
// Create and register Sink
source.addSink(StarRocksSink.sink(options));

env.execute("load_data_example");
```


For information on how to submit a Flink job, refer to [Basic Flink usage](https://docs.byteplus.com/docs/E-MapReduce/109226).

<span id="_2-2-2-json-格式数据示例"></span>
#### JSON format data example

This section demonstrates how to import JSON data constructed in memory into the StarRocks `tb_duplicate_key` table using the Flink DataStream approach. The sample code is as follows:

```Java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

// Simulate JSON format data
String[] records = new String[]{
        "{\"event_time\":1703128450,\"event_type\":1,\"user_id\":1001,\"device\":\"PHONE\"}",
        "{\"event_time\":1703128451,\"event_type\":0,\"user_id\":1002,\"device\":\"PAD\"}",
        "{\"event_time\":1703128452,\"event_type\":1,\"user_id\":1003,\"device\":\"TV\"}"
};

DataStream<String> source = env.fromElements(records);

// Configure Sink options
StarRocksSinkOptions options = StarRocksSinkOptions.builder()
        .withProperty("jdbc-url", "jdbc:mysql://{fe_ip}:9030")
        .withProperty("load-url", "{fe_ip}:8030")
        .withProperty("database-name", "examples")
        .withProperty("table-name", "tb_duplicate_key")
        .withProperty("username", "system_query_user")
        .withProperty("password", "******")
        .withProperty("sink.properties.format", "json")
        .build();
// Create and register Sink
source.addSink(StarRocksSink.sink(options));

env.execute("load_data_example");
```


For information on how to submit a Flink job, refer to [Basic Flink usage](https://docs.byteplus.com/docs/E-MapReduce/109226).

<span id="_2-2-3-自定义-java-对象格式数据示例"></span>
#### Sample data for custom Java object format

This section demonstrates how to import Java data objects constructed in memory into the StarRocks `tb_duplicate_key` table using the Flink DataStream approach. Assume the data structure Record for a single row in this table is defined as follows:

```Java
public static final class Record {

        private final Long eventTime;
        private final Integer eventType;
        private final Integer userId;
        private final String device;

        public Record(Long eventTime, Integer eventType, Integer userId, String device) {
            this.eventTime = eventTime;
            this.eventType = eventType;
            this.userId = userId;
            this.device = device;
        }

        // ... getter
    }
```


You need to implement the StarRocksSinkRowBuilder interface to define the conversion method from the Record object to a row array:

```Java
private static class RecordTransformer implements StarRocksSinkRowBuilder<Record> {

        @Override
        public void accept(Object[] row, Record record) {
            row[0] = record.getEventTime();
            row[1] = record.getEventType();
            row[2] = record.getUserId();
            row[3] = record.getDevice();

            // For primary key tables, you also need to specify the last element to indicate whether the current operation is UPSERT or DELETE
            // row[row.length - 1] = StarRocksSinkOP.UPSERT.ordinal();
        }

    }
```


Finally, simulate constructing Java data objects in memory and perform the import. The sample code is as follows:

```Java
StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

// Simulate JSON format data
Record[] records = new Record[]{
        new Record(1703128450L, 1, 1001, "PHONE"),
        new Record(1703128451L, 0, 1002, "PAD"),
        new Record(1703128452L, 1, 1003, "TV")
};

DataStream<Record> source = env.fromElements(records);

// Define table Schema
TableSchema schema = TableSchema.builder()
        .field("event_time", DataTypes.BIGINT().notNull())
        .field("event_type", DataTypes.INT().notNull())
        .field("user_id", DataTypes.INT().notNull())
        .field("device", DataTypes.VARCHAR(128))
        .build();

// Configure Sink options
StarRocksSinkOptions options = StarRocksSinkOptions.builder()
        .withProperty("jdbc-url", "jdbc:mysql://{fe_ip}:9030")
        .withProperty("load-url", "{fe_ip}:8030")
        .withProperty("database-name", "examples")
        .withProperty("table-name", "tb_duplicate_key")
        .withProperty("username", "system_query_user")
        .withProperty("password", "******")
        .build();
// Create and register Sink
source.addSink(StarRocksSink.sink(schema, options, new RecordTransformer()));

env.execute("load_data_example");
```


For information on how to submit a Flink job, refer to [Basic Flink usage](https://docs.byteplus.com/docs/E-MapReduce/109226).

<span id="_3-配置参数"></span>
## Configuration parameters


|Parameter |Required |Parameter value |Note |
|---|---|---|---|
|connector |Yes | |Must be starrocks. |
|jdbc\-url |Yes | |Configure the MySQL server address of the FE node. The format is `jdbc:mysql://<fe_host>:<fe_query_port>`, and multiple addresses are separated by an English comma `,`. |
|load\-url |Yes | |Configure the HTTP server of the FE node. The format is `<fe_host>:<fe_http_port>`, and multiple addresses are separated by an English comma `,`. |
|database\-name |Yes | |Name of the StarRocks database to import into. |
|table\-name |Yes | |Name of the StarRocks table to import into. |
|username |Yes | |StarRocks access username. |
|password |Yes | |StarRocks access password. |
|sink.semantic |No |* Default value: at\-least\-once |Sink consistency semantics. Supports at\-least\-once and exactly\-once. |
|sink.version |No |* Default value: AUTO |The Flink Connector is implemented based on Stream Load. This parameter allows users to configure the Stream Load interface version to use. Supported options:<br><br><br>* **V1**: Uses the standard Stream Load interface.<br><br>* **V2**: Uses the [Stream Load transaction interface](https://docs.starrocks.io/zh/docs/loading/Stream_Load_transaction_interface/), which offers better performance in terms of memory usage and exactly\-once semantics compared to V1.<br><br>* **AUTO**: Automatically selects based on the StarRocks version. It is recommended to set this to AUTO. |
|sink.label\-prefix |No | |Used to configure the prefix for the Stream Load import task label. It is recommended to set the label prefix according to the specific business scenario of the job. |
|sink.buffer\-flush.max\-bytes |No |* Default value: 90M<br><br>* Unit: bytes<br><br>* Value range: [64MB, 10GB] |Used to configure the amount of data cached in memory. When the cached data reaches this threshold, a Stream Load import is triggered.<br><br>This parameter takes effect only when `sink.semantic=at-least-once`. |
|sink.buffer\-flush.max\-rows |No |* Default value: 500000<br><br>* Value range: [64000, 5000000] |Used to configure the number of data rows cached in memory. When the cached data reaches this threshold, a Stream Load import is triggered.<br><br>This parameter takes effect only when `sink.version=V1 && sink.semantic=at-least-once`. |
|sink.buffer\-flush.interval\-ms |No |* Default value: 300000<br><br>* Unit: milliseconds<br><br>* Value range: [1000, 3600000] |Used to configure the interval for sending data.<br><br>This parameter takes effect only when `sink.semantic=at-least-once`. |
|sink.max\-retries |No |* Default value: 3<br><br>* Value range: [0, 10] |Used to configure the maximum number of retry attempts.<br><br>This parameter takes effect only when `sink.version=V1`. |
|sink.connect.timeout\-ms |No |* Default value: 30000<br><br>* Unit: milliseconds<br><br>* Value range: [100, 60000] |Used to configure the timeout for establishing a connection.<br><br>The default value of this parameter has been adjusted to 30000 milliseconds since version v1.2.9; previously, it was 1000 milliseconds. |
|sink.socket.timeout\-ms |No |* Default value: \-1<br><br>* Unit: milliseconds<br><br>* Value range: |Used to configure the socket connection timeout. It is recommended that this parameter value be greater than the Stream Load `timeout` configuration value. |
|sink.wait\-for\-continue.timeout\-ms |No |* Default value: 10000<br><br>* Unit: milliseconds<br><br>* Value range: [3000, 60000] |Used to configure the timeout for waiting for the FE HTTP 100\-continue response. |
|sink.ignore.update\-before |No |* Default value: true |Used to configure whether to ignore UPDATE_BEFORE records from Flink when importing data into a primary key table. If set to false, these are treated as DELETE operations in the primary key table. |
|sink.parallelism |No | |Used to configure the write parallelism. By default, this is determined by the Flink Planner.<br><br><br>* This parameter applies only to Flink SQL.<br><br>* In scenarios with multiple parallel instances, users need to ensure that data is written in the correct order. |


<span id="_4-更多信息"></span>
## More information

You can visit the [StarRocks official documentation](https://docs.starrocks.io/zh/docs/loading/Flink-connector-starrocks/) for more details on using Flink Connector to import data into StarRocks, as well as how to use [Flink Connector](https://docs.starrocks.io/zh/docs/unloading/Flink_connector/) to read data from StarRocks.
