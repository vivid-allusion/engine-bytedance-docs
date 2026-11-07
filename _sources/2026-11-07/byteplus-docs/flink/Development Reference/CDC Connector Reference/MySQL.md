---
title: "MySQL"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/MySQL"
---

The MySQL CDC Pipeline connector allows reading snapshot and incremental data from the MySQL database and provides end\-to\-end whole database synchronization capabilities. This article describes how to set up the MySQL CDC Pipeline connector.

<span id="5393217c"></span>
## Usage Restrictions


* The MySQL CDC connector is currently only supported on **Flink 1.16\-volcano** and higher engine versions.

* Based on compliance requirements, if MySQL CDC functionalities are needed, users must upload the MySQL Driver themselves. Please go to [the official MySQL website](https://downloads.mysql.com/archives/c-j/) to download version 8.0.27 and upload it to the job development dependencies. For detailed operations, please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources).


<span id="f666c2a0"></span>
## **How to Create a Pipeline**

A Pipeline that reads data from MySQL and syncs to Doris can be defined as follows:

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
  type: doris
  name: Doris Sink
  fenodes: 127.0.0.1:8030
  username: root
  password: pass

pipeline:
   name: MySQL to Doris Pipeline
   parallelism: 4
```


<span id="95d079bb"></span>
## Connector Configuration Options


|**Option** |**Required** |**Default** |**Type** |**Description** |
|---|---|---|---|---|
|hostname |required |(none) |String |IP address or hostname of the MySQL database server. |
|port |optional |3306 |Integer |Integer port number of the MySQL database server. |
|username |required |(none) |String |Name of the MySQL user to be used when connecting to the MySQL database server. |
|password |required |(none) |String |Password to be used when connecting to the MySQL database server. |
|tables |required |(none) |String |The name of the MySQL database table that needs to be monitored. Table names support regular expressions to monitor multiple tables that satisfy the regular expression.<br><br>It's important to note that the period (.) is considered as a delimiter between database names and table names. If using a dot (.) in regular expressions to match any character, you must escape the dot with a backslash.<br><br>For example, db0..\*, db1.user_table_[0\-9]+, db[1\-2].[app |
|tables.exclude |optional |(none) |String |Table names of the MySQL databases to be excluded; the parameter takes effect after the tables parameter. Table names support regular expressions to exclude multiple tables that match the regular expression.<br><br>Usage is the same as the tables parameter. |
|schema\-change.enabled |optional |TRUE |Boolean |Whether to send schema change events, downstream sinks can respond to schema changes to implement table structure synchronization; defaults to true. |
|server\-id |optional |(none) |String |The server id used for reading data can be a single integer or a range of integers, such as '5400' or '5400\-5408'. It is recommended to configure it as a range of integers when the 'scan.incremental.snapshot.enabled' parameter is enabled. Because in the current MySQL cluster, all slave nodes running must have a unique id to identify each slave node. So when the connector joins the MySQL cluster as another slave node (with a unique id), it can read the binlog. By default, the connector generates a random number between 5400 and 6400, but we recommend users to explicitly specify the Server id. |
|scan.incremental.snapshot.chunk.size |optional |8096 |Integer |The block size (number of rows) of the table snapshot; when reading the snapshot of the table, the captured table is split into multiple blocks. |
|scan.snapshot.fetch.size |optional |1024 |Integer |Maximum number of rows read per fetch when reading a table snapshot. |
|scan.startup.mode |optional |initial |String |Optional startup modes for MySQL Change Data Capture consumers are "initial", "earliest\-offset", "latest\-offset", "specific\-offset", "timestamp", and "snapshot". |
|scan.startup.specific\-offset.file |optional |(none) |String |In the "specific\-offset" startup mode, the binlog file name of the startup position. |
|scan.startup.specific\-offset.pos |optional |(none) |Long |In "specific\-offset" startup mode, the binlog file position of the startup checkpoint. |
|scan.startup.specific\-offset.gtid\-set |optional |(none) |String |In "specific\-offset" startup mode, the GTID set of the startup checkpoint. |
|scan.startup.timestamp\-millis |optional |(none) |Long |In "timestamp" mode, the millisecond timestamp of the startup position. |
|scan.startup.specific\-offset.skip\-events |optional |(none) |Long |The number of events to skip after the specified startup position. |
|scan.startup.specific\-offset.skip\-rows |optional |(none) |Long |Number of data rows to skip after the specified startup position. |
|connect.timeout |optional |30s |Duration |The maximum time the connector should wait before timing out after attempting to connect to the MySQL database server. The duration must be no less than 250 milliseconds. |
|connect.max\-retries |optional |3 |Integer |The connector should retry the maximum number of times to establish a connection with the MySQL database server. |
|connection.pool.size |optional |20 |Integer |Connection pool size. |
|jdbc.properties.\* |optional |20 |String |Option to pass custom JDBC URL properties. The user can pass custom attributes, such as 'jdbc.properties.useSSL' = 'false'. |
|heartbeat.interval |optional |30s |Duration |The interval for sending heartbeat events to track the latest available binlog offset. |
|debezium.\* |optional |(none) |String |Pass Debezium properties to the Debezium Embedded Engine, which is used to capture data changes from a MySQL server. For example: 'debezium.snapshot.mode' = 'never'. Learn more about [Debezium's MySQL connector properties](https://debezium.io/documentation/reference/1.9/connectors/mysql.html#mysql-connector-properties). |
|scan.incremental.close\-idle\-reader.enabled |optional |FALSE |Boolean |Whether to close idle Readers after the snapshot ends. This feature requires Flink version 1.14 or higher and 'execution.checkpointing.checkpoints\-after\-tasks\-finish.enabled' must be set to true.<br><br>If the Flink version is 1.15 or higher, the default value for 'execution.checkpointing.checkpoints\-after\-tasks\-finish.enabled' changes to true, and explicit configuration of 'execution.checkpointing.checkpoints\-after\-tasks\-finish.enabled' = true is not necessary. |
|scan.newly\-added\-table.enabled |optional |FALSE |Boolean |Enable dynamic table addition feature, default is off. This configuration only takes effect when the job starts from a savepoint/checkpoint. |


<span id="c8309c53"></span>
## Startup Mode

The configuration option `scan.startup.mode` specifies the startup mode for the MySQL CDC consumer. Valid enumerations include:


* `initial` (default): Performs an initial snapshot of the monitored database tables at startup and continues to read the latest binlog.

* `earliest-offset`: Skips the snapshot phase and starts reading from the earliest readable binlog position.

* `latest-offset`: At first startup, does not perform a snapshot of the monitored database tables, and the connector only reads from the end of the binlog, meaning it can only read data changes that occur after the connector has started.

* `specific-offset`: Skips the snapshot phase and begins reading from a specified binlog position. Positions can be specified by binlog file name and location, or by GTID sets when GTID is enabled on the cluster.

* `timestamp`: Skips the snapshot phase and begins reading binlog events from a specified timestamp.

* `Snapshot`: Only performs the snapshot phase, skips the incremental phase, and exits after finishing reading during the snapshot phase.


For example, you can specify the launch mode in the YAML configuration file like this:

```YAML
source:
  type: mysql
  scan.startup.mode: earliest-offset                    # Start from earliest offset
  scan.startup.mode: latest-offset                      # Start from latest offset
  scan.startup.mode: specific-offset                    # Start from specific offset
  scan.startup.mode: timestamp                          # Start from timestamp
  scan.startup.mode: snapshot                          # Read snapshot only
  scan.startup.specific-offset.file: 'mysql-bin.000003' # Binlog filename under specific offset startup mode
  scan.startup.specific-offset.pos: 4                   # Binlog position under specific offset mode
  scan.startup.specific-offset.gtid-set: 24DA167-...    # GTID set under specific offset startup mode
  scan.startup.timestamp-millis: 1667232000000          # Timestamp under timestamp startup mode
  # ...
```


<span id="f741d7c8"></span>
## Data Type Mapping


|**MySQL type** |**CDC type** |**NOTE** |
|---|---|---|
|TINYINT(n) |TINYINT | |
|SMALLINT<br><br>TINYINT UNSIGNED<br><br>TINYINT UNSIGNED ZEROFILL |SMALLINT | |
|INT<br><br>YEAR<br><br>MEDIUMINT<br><br>MEDIUMINT UNSIGNED<br><br>MEDIUMINT UNSIGNED ZEROFILL<br><br>SMALLINT UNSIGNED<br><br>SMALLINT UNSIGNED ZEROFILL |INT | |
|BIGINT<br><br>INT UNSIGNED<br><br>INT UNSIGNED ZEROFILL |BIGINT | |
|BIGINT UNSIGNED<br><br>BIGINT UNSIGNED ZEROFILL<br><br>SERIAL |DECIMAL(20, 0) | |
|FLOAT<br><br>FLOAT UNSIGNED<br><br>FLOAT UNSIGNED ZEROFILL |FLOAT | |
|REAL<br><br>REAL UNSIGNED<br><br>REAL UNSIGNED ZEROFILL<br><br>DOUBLE<br><br>DOUBLE UNSIGNED<br><br>DOUBLE UNSIGNED ZEROFILL<br><br>DOUBLE PRECISION<br><br>DOUBLE PRECISION UNSIGNED<br><br>DOUBLE PRECISION UNSIGNED ZEROFILL |DOUBLE | |
|NUMERIC(p, s)<br><br>NUMERIC(p, s) UNSIGNED<br><br>NUMERIC(p, s) UNSIGNED ZEROFILL<br><br>DECIMAL(p, s)<br><br>DECIMAL(p, s) UNSIGNED<br><br>DECIMAL(p, s) UNSIGNED ZEROFILL<br><br>FIXED(p, s)<br><br>FIXED(p, s) UNSIGNED<br><br>FIXED(p, s) UNSIGNED ZEROFILL<br><br>where p <= 38 |DECIMAL(p, s) | |
|NUMERIC(p, s)<br><br>NUMERIC(p, s) UNSIGNED<br><br>NUMERIC(p, s) UNSIGNED ZEROFILL<br><br>DECIMAL(p, s)<br><br>DECIMAL(p, s) UNSIGNED<br><br>DECIMAL(p, s) UNSIGNED ZEROFILL<br><br>FIXED(p, s)<br><br>FIXED(p, s) UNSIGNED<br><br>FIXED(p, s) UNSIGNED ZEROFILL<br><br>where 38 < p <= 65 |STRING |In MySQL, decimal data types have a precision of up to 65, but in Flink, the precision of decimal data types is limited to 38. Therefore, if a decimal column is defined with precision greater than 38, it should be mapped to a string to avoid precision loss. |
|BOOLEAN<br><br>TINYINT(1)<br><br>BIT(1) |BOOLEAN | |
|DATE |DATE | |
|TIME [(p)] |TIME [(p)] | |
|TIMESTAMP [(p)] |TIMESTAMP_LTZ [(p)] | |
|DATETIME [(p)] |TIMESTAMP [(p)] | |
|CHAR(n) |CHAR(n) | |
|VARCHAR(n) |VARCHAR(n) | |
|BIT(n) |BINARY(⌈(n + 7) / 8⌉) | |
|BINARY(n) |BINARY(n) | |
|VARBINARY(N) |VARBINARY(N) | |
|TINYTEXT<br><br>TEXT<br><br>MEDIUMTEXT<br><br>LONGTEXT |STRING | |
|TINYBLOB<br><br>BLOB<br><br>MEDIUMBLOB<br><br>LONGBLOB |BYTES |Currently, for the BLOB data types in MySQL, only blobs with a length not exceeding 2,147,483,647 (2\*\*31\-1) are supported. |
|ENUM |STRING | |
|JSON |STRING |The JSON data type will be converted to a JSON\-formatted string in Flink. |
|SET |*  |Not supported currently |
|GEOMETRY<br><br>POINT<br><br>LINESTRING<br><br>POLYGON<br><br>MULTIPOINT<br><br>MULTILINESTRING<br><br>MULTIPOLYGON<br><br>GEOMETRYCOLLECTION |STRING |Spatial data types in MySQL will be converted into strings with a fixed Json format. Please refer to the [MySQL spatial data type mapping](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.2/zh/docs/connectors/pipeline-connectors/mysql/#a-name-id-003-a) section for more detailed information. |


<span id="35ac77aa"></span>
### Spatial Data Type Mapping

In MySQL, all spatial data types except `GEOMETRYCOLLECTION` are converted to JSON strings with a fixed format, such as:

```JSON
{"srid": 0 , "type": "xxx", "coordinates": [0, 0]}
```


The field `srid` identifies the SRS that defines the geometry; if SRID is not specified, SRID 0 is the default value for new geometry values. Since MySQL 8+ only supports specific SRIDs when defining spatial data types, in older versions of MySQL, the field `srid` will always be 0.

The field `type` identifies the spatial data type, such as `POINT`/`LINESTRING`/`POLYGON`.

The field `coordinates` represents the `coordinates` of the spatial data.

For `GEOMETRYCOLLECTION`, it will be converted to a JSON string with a fixed format, such as:

```JSON
{"srid": 0 , "type": "GeometryCollection", "geometries": [{"type":"Point","coordinates":[10,10]}]}
```


The `Geometrics` field is an array containing all spatial data.

Examples of mapping different spatial data types are as follows:


|**Spatial data in MySQL** |**Json String converted in Flink** |
|---|---|
|POINT(1 1) | |
|LINESTRING(3 0, 3 3, 3 5) | |
|POLYGON((1 1, 2 1, 2 2, 1 2, 1 1)) | |
|MULTIPOINT((1 1),(2 2)) | |
|MultiLineString((1 1,2 2,3 3),(4 4,5 5)) | |
|MULTIPOLYGON(((0 0, 10 0, 10 10, 0 10, 0 0)), ((5 5, 7 5, 7 7, 5 7, 5 5))) | |
|GEOMETRYCOLLECTION(POINT(10 10), POINT(30 30), LINESTRING(15 15, 20 20)) |{"geometries":[{"type":"Point","coordinates":[10,10]},{"type":"Point","coordinates":[30,30]},{"type":"LineString","coordinates":[[15,15],[20,20]]}],"type":"GeometryCollection","srid":0} |
