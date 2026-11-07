---
title: "MongoDB CDC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/MongoDB_CDC"
---

MongoDB CDC Connector enables reading both full and incremental data from MongoDB databases, exclusively as a data source table.

<span id="ba438b3e"></span>
## Usage Restrictions


* MongoDB CDC Connector is currently only supported on the **Flink 1.16\-byted** engine version.

* MongoDB CDC only supports being used as a data source table and supports versions 3.6, 4.X, 5.0, 6.0.


<span id="83933d1c"></span>
## DDL Definitions

```SQL
CREATE TABLE products (
    _id bigint,
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time varchar,
    PRIMARY KEY (_id) NOT ENFORCED  -- Primary key must be defined.
) WITH (
  'connector' = 'mongodb-cdc',
  'hosts' = 'localhost:27017,localhost:27018,localhost:27019',
  'username' = 'flinkuser',
  'password' = 'flinkpw',
  'database' = 'inventory',
  'collection' = 'products'
);
```


<span id="0b6b39ab"></span>
## WITH parameters


|**Parameters** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Is |(none) |String |The specified connector here is the mongodb\-cdc connector. |
|scheme |No |mongodb |String |Specifies the protocol for connecting to MongoDB, example values `mongodb` or `mongodb+srv`. |
|hosts |is |(none) |String |MongoDB server address format: `ip:port`.<br><br>If multiple addresses are present, separate them with a comma (,). |
|username |No |(none) |String |Username for the MongoDB database service.<br><br>Username is required only when MongoDB is set to require authentication. |
|password |No |(none) |String |Password for the MongoDB database service.<br><br>Password is required only when MongoDB is set to require authentication. |
|database |No |(none) |String |MongoDB database name.<br><br>Supports using regular expressions to match databases; if not set, it means all databases. |
|collection |No |(none) |String |MongoDB Collection name.<br><br>Supports using regular expressions to match Collections; if not set, it means all Collections. |
|connection.options |No |(none) |String |MongoDB connection options require using & to connect when there are multiple configurations. Example value `replicaSet=test&connectTimeoutMS=300000`.<br><br>For more information about connection options, please see [Connection String Options](https://www.mongodb.com/docs/manual/reference/connection-string/#std-label-connections-connection-options). |
|scan.startup.mode |No |initial |String |MongoDB CDC Consumer's optional startup modes include `initial`, `latest-offset`, and `timestamp`.<br><br>For information on startup modes, see [Startup Reading Position](https://ververica.github.io/flink-cdc-connectors/release-2.4/content/connectors/mongodb-cdc.html#startup-reading-position). |
|scan.startup.timestamp\-millis |No |(none) |Long |Set the starting timestamp when the launch mode is set to `timestamp`. |
|copy.existing.queue.size |No |10240 |Integer |The maximum size of the queue to be used when copying data. |
|batch.size |No |1024 |Integer |The cursor batch size refers to the number of documents MongoDB returns for each query execution. |
|poll.max.batch.size |No |1024 |Integer |Maximum number of data fetches each time.<br><br>Default value 1024, which means up to 1024 data can be fetched during the default interval (1000 ms). |
|poll.await.time.ms |No |1000 |Integer |Data fetching interval. |
|heartbeat.interval.ms |No |0 |Integer |The interval duration for sending heartbeat messages.<br><br>The default is 0ms, which means heartbeat messages are disabled, indicating that heartbeat messages won't be sent to maintain the active status of the connection, potentially causing connection interruptions or failures to go undetected for a period.<br><br>Heartbeat message intervals should not be too short to avoid frequent transmission that could lead to network overhead; nor should they be too long, to ensure timely detection of connection interruptions or failures. |
|scan.incremental.snapshot.enabled |No |false |Boolean |Whether to use incremental snapshots, which are disabled by default.<br><br>Incremental snapshots are supported only in MongoDB version 4.0 and later. |
|scan.incremental.snapshot.chunk.size.mb |No |64 |Integer |The chunk size for incremental snapshots, measured in MB. |
|scan.incremental.close\-idle\-reader.enabled |No |false |Boolean |Close idle readers after the snapshot is completed. |


<span id="ac720d7c"></span>
## Type Mapping

The mapping of MongoDB CDC and Flink field types is as follows:


|**MongoDB field type** |**Flink SQL field type** |
|---|---|
|\- |TINYINT |
|\- |SMALLINT |
|Int |INT |
|Long |BIGINT |
|\- |FLOAT |
|Double |DOUBLE |
|Decimal128 |DECIMAL(p, s) |
|Boolean |BOOLEAN |
|DateTimestamp |DATE |
|DateTimestamp |TIME |
|Date |TIMESTAMP(3)<br><br>TIMESTAMP_LTZ(3) |
|Timestamp |TIMESTAMP(0)<br><br>TIMESTAMP_LTZ(0) |
|String<br><br>ObjectId<br><br>UUID<br><br>Symbol<br><br>MD5<br><br>JavaScript<br><br>Regex |STRING |
|BinData |BYTES |
|Object |ROW |
|Array |ARRAY |
|DBPointer |ROW<$ref STRING, $id STRING\> |
|[GeoJSON](https://www.mongodb.com/docs/manual/reference/geojson/) |Point : ROW<type STRING, coordinates ARRAY\><br><br>Line : ROW<type STRING, coordinates ARRAY<ARRAY< DOUBLE\>\>\><br><br>... |


<span id="cc37b4ce"></span>
## Sample Code

```SQL
CREATE TABLE mongo_cdc_source (
    _id bigint,
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time varchar,
    PRIMARY KEY (_id) NOT ENFORCED
) WITH (
  'connector' = 'mongodb-cdc',
  'hosts' = 'localhost1:3717,localhost2:3717',
  'username' = 'flinkuser',
  'password' = 'flinkpw',
  'database' = 'doc-db',
  'collection' = 'products'
);
CREATE TABLE print_table (
    _id bigint,
    order_id bigint,
    order_product_id bigint,
    order_customer_id bigint,
    order_status varchar,
    order_update_time varchar
) WITH (
 'connector' = 'print'
);
insert into print_table 
select * from mongo_cdc_source;
```


<span id="b4516234"></span>
## FAQ

If the topology of the job has been modified, such as adding or removing fields from the Source, it cannot be restored from the historical state. In this case, the state can be discarded, and restart from scratch using the timestamp mode:

Parameters as follows:

> 'scan.startup.mode' = 'timestamp',

> 'scan.startup.timestamp\-millis' = 'xxxx' \-\- millisecond timestamp, which can be obtained from https://tool.chinaz.com/tools/unixtime.aspx
