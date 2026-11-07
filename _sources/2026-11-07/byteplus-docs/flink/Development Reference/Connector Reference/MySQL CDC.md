---
title: "MySQL CDC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/MySQL_CDC"
---

MySQL CDC connector provides the capability to read both full and incremental data from MySQL databases, solely for use as a source table.

<span id="d811f4fb"></span>
## Usage Restrictions


* MySQL CDC connector currently only supports use in **Flink 1.16\-byted** and higher engine versions.

* Supports MySQL versions 5.6, 5.7, 8.x.

* If you need to use the MySQL CDC connector to connect to the cloud database veDB MySQL edition, please configure your connection terminal according to the following requirements, otherwise, task failures may occur due to custom connection terminal restrictions.

   For detailed understanding of the meanings of each parameter, please see [Edit Connection Terminal](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints).

   * Read and write mode: configure as **read\-write**.

   * Consistency level: configure as **eventual consistency**.

   * Master node accepts read: **disable** this option.

   * Task Splitting: **Enable** this option.

* In compliance with regulations, if the use of MySQL Change Data Capture functionality is needed, users must upload the MySQL Driver themselves. Please visit the [MySQL official website](https://downloads.mysql.com/archives/c-j/) to download version 8.0.27, and upload it to the job development dependency files. For specific operations, please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) .


<span id="01a6b922"></span>
## Prerequisites


* Add a whitelist to the MySQL instance for the Flink subnet, as follows:

* Authorize MySQL CDC User


The required permissions include read access to database tables (SELECT permission), and binlog read access (REPLICATION SLAVE, REPLICATION CLIENT permissions), with authorization commands as follows:

```SQL
GRANT SELECT, REPLICATION SLAVE, REPLICATION CLIENT ON test_db.test_table TO 'test'@'localhost';
FLUSH PRIVILEGES;
```


<span id="8aba5d79"></span>
## DDL Definition

```SQL
CREATE TABLE orders (
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time timestamp,
    PRIMARY KEY (order_id) NOT ENFORCED  -- If the database table to be synchronized has a primary key defined, you also need to define the primary key here.
     ) WITH (
     'connector' = 'mysql-cdc',
     'hostname' = 'localhost',
     'port' = '3306',
     'username' = 'flinkuser',
     'password' = 'flinkpw',
     'database-name' = 'mydb',
     'table-name' = 'orders'
     );
```


<span id="fe26c037"></span>
## WITH Parameters


|**Parameter** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to use, here it is the MySQL\-Change Data Capture connector. |
|hostname |Yes |(none) |String |The IP address or hostname of the MySQL database server.<br><br>**It is recommended to use the primary repository address**. |
|port |No |3306 |Integer |The port number for the MySQL database server. |
|username |Yes |(none) |String |User name for the MySQL database server. |
|password |Yes |(none) |String |User password for the MySQL database server. |
|database\-name |Yes |(none) |String |Database name.<br><br>Database names support regular expressions to match multiple databases. |
|table\-name |Yes |(none) |String |Table name.<br><br>Table names support regular expressions to match multiple tables. |
|server\-id |No |(none) |Integer |Server ID used for data retrieval can be either a single integer or a range of integers, e.g., 5400 or 5400~5408.<br><br>By default, the connector generates a random number between 5400 and 6400, but it is recommended that users explicitly specify the Server ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the <code>scan.incremental.snapshot.enabled</code> parameter is set to true, it is recommended that the server id be configured within an integer range.</div><br> |
|scan.incremental.snapshot.enabled |No |true |Boolean |Incremental snapshot reading mechanism.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is necessary to ensure the concurrent operation of the Source, a unique server id must be maintained, hence it is recommended to configure the server id within an integer range.</div><br> |
|scan.incremental.snapshot.chunk.size |No |8096 |Integer |When reading the snapshot of a table, the captured table is divided into several chunks. |
|scan.snapshot.fetch.size |No |1024 |Integer |When reading table snapshots, the maximum number of entries to read at a time. |
|scan.startup.mode |No |initial |String |Optional startup modes for the MySQL CDC consumer.<br><br><br>* initial: Performs an initial snapshot of the database table upon first startup and then continues reading the latest binlog.<br><br>* earliest\-offset: Skips the snapshot phase and starts reading from the first readable binlog position.<br><br>* latest\-offset: At first startup, does not perform a snapshot of the database table, the connector only starts reading from the end of the binlog, meaning it can only read data changes that occur after the connector has started.<br><br>* specific\-offset: Skips the snapshot phase and starts reading from a specified binlog position. Positions can be specified by binlog filename and location, or by GTID sets.<br><br>* timestamp: Skip the snapshot phase and start reading binlog events from the specified timestamp. |
|scan.startup.timestamp\-millis |No |(none) |Long |Set the starting timestamp when the startup mode is `timestamp`.<br><br>**Note: It is not recommended to use this, as the current version will consume from the oldest binlog file and then filter the necessary data based on the timestamp, which can lead to poor performance due to reading a large number of binlogs.**  |
|scan.startup.specific\-offset.file |No |(none) |String |In `specific-offset` mode, specify the binlog file name for the starting point. |
|scan.startup.specific\-offset.pos |No |(none) |Long |In the `specific-offset` launch mode, it specifies the binlog file location for the start point.<br><br>Note: If you want to start reading from the beginning of the binlog file, set the position to 4, as the first four bytes are the header of the binlog file. |
|scan.startup.specific\-offset.gtid\-set |No |(none) |String |In `specific-offset` mode, the GTID set of the start position. |
|scan.startup.specific\-offset.skip\-events |No |(none) |Long |In `specific-offset` mode, the number of events to skip after the specified start position. |
|scan.startup.specific\-offset.skip\-rows |No |(none) |Long |In `specific-offset` startup mode, the number of data rows to skip after the specified startup point. |
|server\-time\-zone |No |(none) |String |The session time zone used by the database, such as Asia/Shanghai. This parameter controls how the TIMESTAMP type in MySQL is converted to STRING type. |
|debezium.min.row. count.to.stream.result |No |1000 |Integer |During the snapshot operation, the connector queries each included table to generate read events for all the rows in that table. This parameter is used to specify the minimum number of rows a table must contain when delivering events downstream, with a default value of 1000.<br><br>If this parameter is set to 0, it indicates that there is no need to wait for a certain amount of data to accumulate; transmission will occur immediately as soon as there is a row. |
|connect.timeout |No |30s |Duration |The maximum waiting time to connect to the MySQL database server. |
|connect.max\-retries |No |3 |Integer |The maximum number of retries to reconnect to the MySQL database server. |
|connection.pool.size |No |20 |Integer |Connection pool size. |
|jdbc.properties.\* |No |20 |String |Custom JDBC URL parameters, such as: `'jdbc.properties.useSSL' = 'false'`. |
|heartbeat.interval |No |30s |Duration |The interval for sending heartbeat events to track the latest available binlog offset, typically used to address slow table issues (where data tables are slow to update). |
|debezium.\* |No |(none) |String | |
|debezium.skipped.operations |No |(none) |String |Select the operation types to filter, where 'c' stands for insert, 'u' for update, 'd' for delete.<br><br>Example: If configured as 'd', it means filtering delete messages, only syncing insert and update messages. |
|scan.incremental.close\-idle\-reader.enabled |No |false |Boolean |Should idle readers be closed after the snapshot ends? |
|scan.read\-changelog\-as\-append\-only.enabled |No |false |Boolean |Should the changelog data stream be converted to an append\-only data stream?<br><br>The parameter values are as follows:<br><br><br>* true: All types of messages (including INSERT, DELETE, UPDATE_BEFORE, UPDATE_AFTER) will be converted to INSERT type messages. Enabled only under special circumstances where upstream table deletion messages need to be retained.<br><br>* false (default): All types of messages remain unchanged. |


<span id="56a4e4f2"></span>
## Supported Metadata

The metadata in the table below can be declared as read\-only (virtual) meta columns in DDL.


|Key |DataType |Description |
|---|---|---|
|table_name |STRING NOT NULL |The name of the table to which the current record belongs. |
|database_name |STRING NOT NULL |The name of the database to which the current record belongs. |
|op_ts |TIMESTAMP_LTZ(3) NOT NULL |The current record table's update time in the database.<br><br>If records are read from a snapshot of the table rather than a binlog, this value will always be 0. |


The following example of creation demonstrates the use of metadata columns:

```SQL
CREATE TABLE products (
    db_name STRING METADATA FROM 'database_name' VIRTUAL,
    table_name STRING METADATA  FROM 'table_name' VIRTUAL,
    operation_ts TIMESTAMP_LTZ(3) METADATA FROM 'op_ts' VIRTUAL,
    order_id INT,
    order_date TIMESTAMP(0),
    customer_name STRING,
    price DECIMAL(10, 5),
    product_id INT,
    order_status BOOLEAN,
    PRIMARY KEY(order_id) NOT ENFORCED
) WITH (
    'connector' = 'mysql-cdc',
    'hostname' = 'localhost',
    'port' = '3306',
    'username' = 'root',
    'password' = '123456',
    'database-name' = 'mydb',
    'table-name' = 'orders'
);
```


<span id="77b58961"></span>
## Best Practices

<span id="a0903a4a"></span>
### Sharding and Synchronization

In multi\-database sharding scenarios, merging multiple sharded tables into one table is achieved by using regular expressions to match multiple database tables, as shown in the following example:

```SQL
CREATE TABLE products (
  db_name STRING METADATA FROM 'database_name' VIRTUAL,
  table_name STRING METADATA  FROM 'table_name' VIRTUAL,
  operation_ts TIMESTAMP_LTZ(3) METADATA FROM 'op_ts' VIRTUAL,
  order_id INT,
  order_date TIMESTAMP(0),
  customer_name STRING,
  price DECIMAL(10, 5),
  product_id INT,
  order_status BOOLEAN,
  PRIMARY KEY(order_id) NOT ENFORCED
) WITH (
  'connector' = 'mysql-cdc',
  'hostname' = 'localhost',
  'port' = '3306',
  'username' = 'root',
  'password' = '123456',
  'database-name' = '(^(test).*|^(tpc).*|txc|.*[p$]|t{2})', -- Regular expression matching multiple libraries。.
  'table-name' = '(t[5-8]|tt)' -- Regular expression matching multiple tables.
);
```



|Matching Example |Expression |Description |
|---|---|---|
|Prefix Matching |^(test).\* |Matches database or table names that begin with the prefix 'test', such as test1, test2, etc. |
|Suffix Matching |.\*[p$] |Match database or table names ending with the suffix 'p', such as cdcp, edcp, etc. |
|Specific Match |txc |Match specific database or table names. |


When matching database tables, the regular expression `database-name\\\\.table-name` is used to match against the fully qualified name of MySQL tables, hence this example uses `(^(test).*|^(tpc).*|txc|.*[p$]|t{2})\\\\.(t[5-8]|tt)`, which can match tables such as txc.tt and test2.test5.

<span id="94ca56aa"></span>
### Full Pull Specified by Sharding Key

In the full read stage, for large database tables, there can be pressure on the database. Post 2.0 version of MySQL CDC, based on the [DBLog Paper](https://arxiv.org/pdf/2010.12597v1.pdf), the MySQL CDC Connector implements a new method of full data fetching which allows parallel retrieval of full data without a global read lock (FLUSH TABLES WITH READ LOCK). This algorithm divides the full data of MySQL into different small chunks, which can be read concurrently (for a detailed principle, refer to [the documentation](https://nightlies.apache.org/flink/flink-cdc-docs-release-3.1/docs/connectors/flink-sources/mysql-cdc/)). Users can configure keys and chunk sizes to control the partition of chunks and the size of each chunk. The optimal conditions for chunk keys are as follows:


* Numerical type: It facilitates the quick calculation of the start and end values for each chunk based on their sizes.

* Uniform distribution: Ensures that the data within each chunk is evenly distributed; otherwise, it could lead to most of the data being concentrated in a few chunks, causing data skew during the data retrieval phase.


<span id="8af85fbe"></span>
## FAQ

<span id="1f11c977"></span>
### Filter delete messages

In the course of business usage, upstream MySQL sources often delete historical data regularly to save storage space, retaining only data from the last seven days. However, the business requires the OLAP system at the Sink to retain all historical data, hence, it is necessary to ignore the delete messages regularly sent by the Source.

Solution: Add the parameter 'debezium.skipped.operations' = 'd', which indicates that delete messages are filtered.

<span id="d1943a10"></span>
### State loss and restart

If you modify the topology of a job, such as adding or removing fields of a Source, you cannot restore from the historical state. In this case, you may discard the state and start anew from a specific\-offset mode. Steps are as follows:


1. Retrieve the current location information by opening the TM log. Each checkpoint logs the location information for each table, including the binlog file and binlog position.


```Plain
2024-09-27 18:16:10,488 INFO  com.ververica.cdc.connectors.mysql.source.reader.MySqlSourceReader [] - Binlog offset for tables [test_db.test] on checkpoint 4: {transaction_id=null, ts_sec=0, file=mysql-binlog.000666, pos=147223270, kind=SPECIFIC, gtids=e6e6e8e3-6351-11ef-8340-52540bd1ce99:81433397-81559559, row=0, event=20, server_id=1}
```



2. Modify the startup mode of the MySQL CDC Source in the SQL to recover from the aforementioned location.


```SQL
create table
  mysql_cdc_source (
    `id` INT NOT NULL,
    `a` DECIMAL(10, 2) NOT NULL,
    `b` DOUBLE,
    `c` DATE,
    `d` VARCHAR,
    PRIMARY KEY (`id`) NOT ENFORCED
  )
WITH
  (
    'connector' = 'mysql-cdc',
    'hostname' = 'vedbm-xxx.pri.mysql.vedb.byteplus.com',
    'port' = '3306',
    'username' = 'xroot',
    'password' = 'xxxx',
    'database-name' = 'test_db',
    'table-name' = 'test',
    'scan.startup.mode' = 'specific-offset', -- Start reading from the specified binlog location. The location can be specified by the binlog file name and position.
    'scan.startup.specific-offset.file' = 'binlog.000666',
    'scan.startup.specific-offset.pos' = '147223270'
  );
```



3. Restart the job to start from a completely new state.
