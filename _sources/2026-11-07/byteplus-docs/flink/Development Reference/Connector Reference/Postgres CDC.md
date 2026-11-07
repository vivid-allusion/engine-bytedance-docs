---
title: "Postgres CDC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Postgres_CDC"
---

Postgres CDC Connector is used to read full snapshot and incremental data from PostgreSQL databases, and it only supports being used as a source table.

<span id="ca0e6cd2"></span>
## Usage Restrictions


* Postgres CDC Connector is currently only supported on **Flink 1.16\-byted** engine version.

* When the incremental snapshot feature is disabled, Postgres CDC does not support performing Checkpoints during the full table scan phase.

   When `scan.incremental.snapshot.enabled=false` (default configuration), if a task triggers a Checkpoint during the full table scan phase, it may cause task Failover due to Checkpoint timeout. Therefore, it is recommended to configure the Checkpoint interval in Flink parameters and Task restart strategy to avoid task Failover due to Checkpoint timeout during the full synchronization phase.


<span id="81cd046c"></span>
## DDL Definitions

```SQL
CREATE TABLE pgsql_source (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp,
  PRIMARY KEY (`order_id`) NOT ENFORCED  -- If the database table has a primary key defined, it also needs to be defined here.
) WITH (
  'connector' = 'postgres-cdc',
  'hostname' = 'postgre***da.rds-pg.byteplus.com',
  'port' = '5432',
  'username' = 'doc_user',
  'password' = 'Pw**45!',
  'database-name' = 'doc_autotest',
  'schema-name' = 'public',
  'table-name' = 'orders',
  'slot.name' = 'order'
);
```


<span id="590e862f"></span>
## WITH Parameters


|**Parameters** |**Is it Mandatory?**  |**Default value** |**Data type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to be used, which is the postgres\-cdc connector here. |
|hostname |Yes |(none) |String |The IP address or hostname of the PostgreSQL database. |
|username |Is |(none) |String |The username for the PostgreSQL database. |
|password |Yes |(none) |String |The user password for the PostgreSQL database. |
|database\-name |Yes |(none) |String |The name of the PostgreSQL database. |
|schema\-name |Yes |(none) |String |PostgreSQL Schema name. Schema name supports regular expressions to read data from multiple schemas. |
|table\-name |is |(none) |String |PostgreSQL Table name. Table name supports regular expressions to read data from multiple tables. |
|port |No |5432 |Integer |The port number for the Postgres database service. The default value is 5432. |
|slot.name |No |flink |String |Name of the logical decoding slot.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">It is recommended to set the <code>slot.name</code> parameter for each table to avoid issues</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>PSQLException: ERROR: replication slot "flink" is active for PID 974</code> error.</div><br> |
|decoding.plugin.name |No |decoderbufs |String |Name of the Postgres Logical Decoding plugin. Depends on the plugins installed on the Postgres service. The list of supported plugins is as follows:<br><br><br>* decoderbufs (default)<br><br>* wal2json<br><br>* wal2json_rds<br><br>* wal2json_streaming<br><br>* wal2json_rds_streaming<br><br>* pgoutput |
|changelog\-mode |No |all |String |The changelog mode used supports the following two modes.<br><br><br>* All: Using the all mode, changes are encoded using a retraction stream that includes all RowKinds. This means that each change operation will be encoded as events of INSERT, UPDATE, and DELETE.<br><br>* Upsert: In upsert mode, changes are encoded as upsert streams that describe idempotent updates to the Primary Key. This means that each change operation will be encoded as idempotent updates to tables with Primary Keys. This mode is suitable for tables with Primary Keys that do not use the complete replica identity (replica identity FULL). When using upsert mode, the Primary Key must be set. |
|heartbeat.interval.ms |No |30s |Duration |The interval duration for sending heartbeat messages. |
|debezium.\* |No |(none) |String |Debezium properties.<br><br>More granular control of Debezium client behavior. For example `'debezium.snapshot.mode' = 'never'`, see details<br><br>[Configuration properties](https://debezium.io/documentation/reference/1.9/connectors/postgresql.html#postgresql-connector-properties). |
|debezium.snapshot.select.statement.overrides |No |(none) |String |If there is a large amount of data in the table but you do not need all the historical data, you can specify the data range for snapshot in the underlying configuration of Debezium. This parameter will only affect snapshots, not subsequent data read consumption.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In PostgreSQL, it is necessary to configure using Schema and Table names, such as <code>'debezium.snapshot.select.statement.overrides' = 'schema.table'</code>.</div><br><br><br><div data-tips="true" data-tips-type="tip">After setting this parameter, it is also necessary to set the <code>debezium.snapshot.select.statement.overrides.[schema].[table]</code> parameter.</div><br> |
|debezium.snapshot.select.statement.overrides.[schema].[table] |No |(none) |String |If you want to limit the scope of snapshot data, you can use the `debezium.snapshot.select.statement.overrides` configuration property to specify SQL statements.<br><br><br>* SQL statements must conform to the syntax of the data source and must include the schema and table names for the snapshot selection to be applied. For example, `'debezium.snapshot.select.statement.overrides.schema.table' = 'select * from schema.table where 1 != 1'`.<br><br>* For tasks submitted via the Flink SQL client, the use of functions enclosed in single quotes within the content is not supported. For instance, `'debezium.snapshot.select.statement.overrides.schema.table' = 'select * from schema.table where to_char(rq, 'yyyy-MM-dd')'`. |
|scan.incremental.snapshot.enabled |no |false |Boolean |Incremental snapshot use is not enabled by default.<br><br>Incremental snapshot reading has the following advantages over traditional snapshot mechanisms:<br><br><br>* By utilizing incremental snapshots for reading, the source can **read snapshots in parallel**, enhancing read performance and reducing read times.<br><br>* Incremental snapshot reading allows the source to perform **Checkpoint operations at the block level during snapshot reading**, providing better fault tolerance and recovery capabilities.<br><br>* For incremental snapshot reading, the source **does not need to acquire a global read lock** (FLUSH TABLES WITH READ LOCK) before reading the snapshot, offering improved concurrency and availability. |


<span id="c80ab5ec"></span>
### Incremental Snapshot Related Parameters

When `scan.incremental.snapshot.enabled=true`, the following incremental snapshot parameters are available.


|**Parameter** |**Mandatory** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|scan.incremental.snapshot.chunk.size |optional |8096 |Integer |Snapshot chunk size (rows), which refers to splitting the captured table into multiple smaller chunks or sections when reading a table snapshot. |
|scan.startup.mode |No |initial |String |Optional startup modes for the Postgres CDC Consumer, supporting `initial` and `latest-offset` modes.<br><br><br>* initial: Performs an initial snapshot of the database table at startup and continues to read the latest binlog.<br><br>* latest\-offset: At startup, does not perform a snapshot of the database table, and the connector only starts reading from the end of the binlog, meaning it can only read data changes after the connector has started. |
|chunk\-meta.group.size |No |1000 |Integer |Snapshot chunk metadata group size refers to the division of metadata into multiple groups if the size of the metadata exceeds the group size. |
|connect.timeout |No |30s |Duration |Maximum wait time after the connector connects to the PostgreSQL service. |
|connect.pool.size |No |30 |Integer |Connection pool size. |
|connect.max\-retries |No |3 |Integer |Maximum number of reconnection attempts with the PostgreSQL database server. |
|scan.snapshot.fetch.size |No |1024 |Integer |Maximum number of rows fetched per read when scanning a table snapshot. |
|scan.incremental.snapshot.chunk.key\-column |No |(none) |String |Chunk key for the table snapshot, which divides the captured table into multiple chunks based on a chunk key while reading the table snapshot. By default, the chunk key is the first column of the primary key. The column must be part of the primary key.<br><br>When reading the table snapshot, the system divides the table data into multiple smaller chunks through the chunk key. This enhances the efficiency of reading and processing and allows parallel processing of each chunk. The chunk key is usually a critical column of the table, used for distributing data reasonably into different chunks. |
|chunk\-key.even\-distribution.factor.lower\-bound |No |0.05d |Double |Lower limit of the chunk key's uniform distribution factor.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The chunk key distribution factor is used to determine if the table's distribution is uniform. When the data distribution is uniform, the table chunks will utilize uniform calculation optimizations; when the distribution is uneven, split queries will occur.</div><br><br><br><div data-tips="true" data-tips-type="tip">The distribution factor can be calculated using the formula <code>(MAX(id) - MIN(id) + 1) / rowCount</code>.</div><br> |
|chunk\-key.even\-distribution.factor.upper\-bound |No |1000.0d |Double |Upper limit of the chunk key's uniform distribution factor. |


<span id="327f022e"></span>
## Available Metadata

In the table definition, metadata in the following formats can be exposed as read\-only (VIRTUAL) columns.


|**Metadata name** |**Data type** |**Description** |
|---|---|---|
|table_name |STRING NOT NULL |Name of the table containing this row. |
|schema_name |STRING NOT NULL |Name of the schema containing this row. |
|database_name |STRING NOT NULL |Name of the database containing this row. |
|op_ts |TIMESTAMP_LTZ(3) NOT NULL |Row time when changes are made in the database. Full phase data, this field value is 0. |


Metadata Usage Example:

```SQL
CREATE TABLE products (
    db_name STRING METADATA FROM 'database_name' VIRTUAL,
    table_name STRING METADATA  FROM 'table_name' VIRTUAL,
    operation_ts TIMESTAMP_LTZ(3) METADATA FROM 'op_ts' VIRTUAL,
    shipment_id INT,
    order_id INT,
    origin STRING,
    destination STRING,
    is_arrived BOOLEAN
) WITH (
  'connector' = 'postgres-cdc',
  'hostname' = 'localhost',
  'port' = '5432',
  'username' = 'postgres',
  'password' = 'postgres',
  'database-name' = 'postgres',
  'schema-name' = 'public',
  'table-name' = 'shipments'
);
```


<span id="d46a3757"></span>
## Data Mapping

The relationship between Postgres CDC and Flink field types is as follows:


|**Postgres Change Data Capture field type** |**Flink field type** |
|---|---|
| |TINYINT |
|SMALLINT<br><br>INT2<br><br>SMALLSERIAL<br><br>SERIAL2 |SMALLINT |
|INTEGER<br><br>SERIAL |INT |
|BIGINT<br><br>BIGSERIAL |BIGINT |
| |DECIMAL(20, 0) |
|BIGINT |BIGINT |
|REAL<br><br>FLOAT4 |FLOAT |
|FLOAT8<br><br>DOUBLE PRECISION |DOUBLE |
|NUMERIC(p, s)<br><br>DECIMAL(p, s) |DECIMAL(p, s) |
|BOOLEAN |BOOLEAN |
|DATE |DATE |
|TIME [(p)] [WITHOUT TIMEZONE] |TIME [(p)] [WITHOUT TIMEZONE] |
|TIMESTAMP [(p)] [WITHOUT TIMEZONE] |TIMESTAMP [(p)] [WITHOUT TIMEZONE] |
|CHAR(n)<br><br>CHARACTER(n)<br><br>VARCHAR(n)<br><br>CHARACTER VARYING(n)<br><br>TEXT |STRING |
|BYTEA |BYTES |


<span id="58f7cabd"></span>
## Sample Code

```SQL
CREATE TABLE pgsql_source (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp,
  PRIMARY KEY (`order_id`) NOT ENFORCED  -- If the database table has a primary key defined, it also needs to be defined here.
) WITH (
  'connector' = 'postgres-cdc',
  'hostname' = 'postgre***da.rds-pg.byteplus.com',
  'port' = '5432',
  'username' = 'doc_autotest',
  'password' = 'Pw**45!',
  'database-name' = 'doc_autotest',
  'schema-name' = 'public',
  'table-name' = 'orders',
  'slot.name' = 'order'
);

CREATE TABLE print_table (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp
) WITH (
 'connector' = 'print'
);
INSERT INTO print_table 
SELECT * FROM pgsql_source;
```
