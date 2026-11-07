---
title: "SQLServer CDC"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/SQLServer_CDC"
---

SQLServer Change Data Capture Connector is used for reading full and incremental data from SQLServer databases, and is only supported as the source table.

<span id="2e7654d7"></span>
## Usage Restrictions


* The SQLServer Change Data Capture connector is currently only supported in the **Flink 1.16\-byted** engine version.

* SQLServer Change Data Capture is only supported as data sources, with supported SQLServer database versions being 2012, 2014, 2016, 2017, and 2019.


<span id="fec40216"></span>
## DDL Definition

```SQL
CREATE TABLE sqlserver_source (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp
 ) WITH (
    'connector' = 'sqlserver-cdc',
    'hostname' = 'mssql****85.rds-mssql.byteplus.com',
    'port' = '1433',
    'username' = 'doc_user',
    'password' = 'Pwd***5!',
    'database-name' = 'doc_autotest',
    'table-name' = 'dbo.orders'
 );
```


<span id="777b76ce"></span>
## WITH Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specify the connector to use, which is the sqlserver\-cdc connector here. |
|hostname |Yes |(none) |String |IP address or hostname of the SQLServer database. |
|username |Yes |(none) |String |The user name of the SQLServer SQLServer database. |
|password |Yes |(none) |String |SQLServer database user password. |
|database\-name |Yes |(none) |String |SQLServer database name. |
|table\-name |Yes |(none) |String |SQLServer Table name. Table names support regular expressions for reading data from multiple tables. |
|port |No |1433 |Integer |The default port number for SQLServer database service is 1433. |
|server\-time\-zone |No |UTC |String |SQLServer database session time zone setting, such as 'Asia/Shanghai'. |
|scan.incremental.snapshot.enabled |No |true |Boolean |**Whether to enable incremental snapshots, enabled by default**. |
|chunk\-meta.group.size |No |1000 |Integer |The group size of snapshot chunk metadata refers to dividing the metadata into multiple groups if its size exceeds the group size. |
|chunk\-key.even\-distribution.factor.lower\-bound |No |0.05d |Double |Lower limit of the uniform distribution factor for chunk keys.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The shard key distribution factor determines the uniformity of the table's distribution. When the data distribution is uniform, the table shards use uniform computation optimization; when the data distribution is uneven, split queries will occur.</div><br><br><br><div data-tips="true" data-tips-type="tip">The distribution factor can be calculated using the formula <code>(MAX(id) - MIN(id) + 1) / rowCount</code>.</div><br> |
|chunk\-key.even\-distribution.factor.upper\-bound |No |1000.0d |Double |Upper limit of the uniform distribution factor for chunk keys. |
|debezium.\* |No |(none) |String |Debezium property parameters allow for finer control over the behavior of the Debezium client. For example, `'debezium.snapshot.mode' = 'initial_only'`, see [configuration properties](https://debezium.io/documentation/reference/1.9/connectors/sqlserver.html#sqlserver-required-connector-configuration-properties) for details. |
|scan.incremental.close\-idle\-reader.enabled |No |false |Boolean |Should idle readers be closed after the snapshot ends? |


<span id="e7923bfb"></span>
## Available Metadata

In the table definition, metadata in the following format can be exposed as read\-only (VIRTUAL) columns.


|**Metadata name** |**Data type** |**Description** |
|---|---|---|
|table_name |STRING NOT NULL |The name of the table containing this Row. |
|schema_name |STRING NOT NULL |The name of the schema containing this Row. |
|database_name |STRING NOT NULL |The name of the database that contains this row. |
|op_ts |TIMESTAMP_LTZ(3) NOT NULL |The time the row was modified in the database. During the full load phase, the value of this field is 0. |


Metadata Usage Example:

```SQL
CREATE TABLE products (
    table_name STRING METADATA  FROM 'table_name' VIRTUAL,
    schema_name STRING METADATA  FROM 'schema_name' VIRTUAL,
    db_name STRING METADATA FROM 'database_name' VIRTUAL,
    operation_ts TIMESTAMP_LTZ(3) METADATA FROM 'op_ts' VIRTUAL,
    id INT NOT NULL,
    name STRING,
    description STRING,
    weight DECIMAL(10,3)
) WITH (
    'connector' = 'sqlserver-cdc',
    'hostname' = 'localhost',
    'port' = '1433',
    'username' = 'sa',
    'password' = 'Password!',
    'database-name' = 'inventory',
    'schema-name' = 'dbo',
    'table-name' = 'products'
```


<span id="48a22665"></span>
## Data Mapping

The relationship between SQLServer CDC and Flink field types is as follows:


|**SQLServer CDC Field Type** |**Flink Field Type** |
|---|---|
|char(n) |CHAR(n) |
|varchar(n)<br><br>nvarchar(n)<br><br>nchar(n) |VARCHAR(n) |
|text<br><br>ntext<br><br>xml |STRING |
|decimal(p, s)<br><br>money<br><br>smallmoney |DECIMAL(p, s) |
|numeric |NUMERIC |
|float<br><br>real |DOUBLE |
|bit |BOOLEAN |
|int |INT |
|tinyint |SMALLINT |
|smallint |SMALLINT |
|bigint |BIGINT |
|date |DATE |
|time(n) |TIME(n) |
|datetime2<br><br>datetime<br><br>smalldatetime |TIMESTAMP(n) |
|datetimeoffset |TIMESTAMP_LTZ(3) |


<span id="11a72e3a"></span>
## Sample Code

```SQL
CREATE TABLE sqlserver_source (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp
 ) WITH (
    'connector' = 'sqlserver-cdc',
    'hostname' = 'mssql****85.rds-mssql.byteplus.com',
    'port' = '1433',
    'username' = 'doc_user',
    'password' = 'Pwd***5!',
    'database-name' = 'doc_autotest',
    'table-name' = 'dbo.orders'
 );

CREATE TABLE print_sink (
  order_id bigint,
  order_customer_id bigint,
  order_product_id bigint,
  order_status varchar,
  order_update_time timestamp
) WITH (
  'connector' = 'print'
);

INSERT INTO print_sink 
SELECT * FROM sqlserver_source;
```
