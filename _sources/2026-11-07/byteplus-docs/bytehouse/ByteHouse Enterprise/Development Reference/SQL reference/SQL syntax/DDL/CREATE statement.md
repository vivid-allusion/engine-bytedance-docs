---
title: "CREATE statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-create-statement"
---

`CREATE` statements can be used to create databases, tables, views, dictionaries, and other data resources.

<span id="1ecaa591"></span>
# Create a database (CREATE DATABASE)

<span id="2d07927a"></span>
## Grammar

```SQL
CREATE DATABASE [IF NOT EXISTS] db_name 
[ON CLUSTER cluster] 
[ENGINE = engine(...)] 
[COMMENT 'Comment']
```


<span id="57175c70"></span>
## Parameter description


|Parameters |Required field |Note |
|---|---|---|
|IF NOT EXISTS |No |Check whether the newly created table already exists: if the `db_name` database already exists, ByteHouse will not create a new database and:<br><br><br>* If a clause is specified, no exception is raised.<br><br>* If no clause is specified, an exception is thrown. |
|db_name |Yes |Customize the database name. |
|ON CLUSTER |No |Specify the cluster name, and create a database on the specified cluster.<br><br>To avoid database loss or deficiency, please use ON CLUSTER to specify the cluster when creating a database. If you execute SQL statements in the ByteHouse console, you can select **all nodes**. |
|ENGINE |No |Specify the database engine If not specified, ByteHouse uses its self\-developed Atomic database engine by default. |
|COMMENT |No |Add annotations and explanatory information to the database |


<span id="01fe6c15"></span>
## Example


* Create the sample_db database using the default database engine.

   ```SQL
   CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;
   ```
   

* Create the database sample_db using a selectable database engine; currently, only Atomic is supported.

   ```SQL
   CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster ENGINE=Atomic;
   ```
   


<span id="40f51f73"></span>
# Create a table (CREATE TABLE)

<span id="27a6308a"></span>
## Grammar

```SQL
CREATE TABLE [IF NOT EXISTS] [db.]table_name (
  name1 [type1] [NULL|NOT NULL] [DEFAULT|ALIAS expr1 | MATERIALIZED expr1] [COMMENT 'string'][compression_codec][TTL expr1],
  name2 [type2] [NULL|NOT NULL] [DEFAULT|ALIAS expr2 | MATERIALIZED expr1] [COMMENT 'string'] [compression_codec] [TTL expr2],
  ...
) 
ENGINE = engine(...)
ORDER BY expr
[PARTITION BY expr]
[PRIMARY KEY expr]
[UNIQUE KEY expr]
[SAMPLE BY expr]
[TTL expr]
[SETTINGS name=value, ...]
[COMMENT='COMMENT']
```


<span id="8430c93d"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3: Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster (
  id UInt32,
  name String DEFAULT '',
  CONSTRAINT constraint1 CHECK id > 10
)
ENGINE = MergeTree
ORDER BY id;
```


<span id="f88c3341"></span>
## Parameter description

<span id="f5112b85"></span>
### table_name, name, type


|Parameters |Required field |Note |
|---|---|---|
|db. |No |Database name. If omitted, the current default database will be used. |
|table_name |Yes |Custom table names |
|name1 |Yes |Custom column names. |
|type1 |No |Define the data type of the column. For the data types currently supported by ByteHouse, please refer to [Data Types](https://docs.byteplus.com/en/docs/bytehouse/data-types). |


<span id="3bac5a95"></span>
### Null or not null modifiers

In a column definition, the NULL and NOT NULL modifiers following the data type specify whether the column is allowed to be [Can be null: Nullable](https://docs.byteplus.com/docs/bytehouse/nullable).

If the data type does not allow null values and NULL is specified, the column will be treated as nullable; if NOT NULL is specified, it will not be.

For example, INT NULL is the same as Nullable(INT). If the data type is nullable and a NULL or NOT NULL modifier is specified, an exception is thrown.

<span id="90b2e213"></span>
### Default values (**DEFAULT VALUES**)

A column description can specify a default value expression in the form of `DEFAULT expr`, `MATERIALIZED expr`, or `ALIAS expr`. Example: `URLDomain String DEFAULT domain(URL)`.

The expression expr is optional. If the expression is omitted, you must explicitly specify the column type, and


* The default value for numeric columns is 0;

* The default value of a string column is `' '` (empty string).

* The default value of the array column is `[ ]` (empty array).

* The default value of the date column is 1970\-01\-01;

* The default value of a nullable column is NULL.


If the column type declaration for a default value column is omitted, the system will infer the type from the type of `expr`. For example, the type of the column `EventDate DEFAULT toDate(EventTime)` will be inferred as `date`.

If both a data type and a default value expression are specified, the system will implicitly insert a type conversion function to convert the result of the expression to the specified type. For example: `Hits UInt32 DEFAULT 0` is represented internally as `Hits UInt32 DEFAULT toUInt32(0)`.

The default value expression `expr` can reference any table column and constant. ByteHouse does not introduce cycles in expression evaluation when checking for changes to table structure. For the `INSERT` operation, the system will check whether the expression can be resolved—that is, all columns required for the calculation have been provided.

<span id="c174b922"></span>
#### **DEFAULT**

Standard default value. If a value for such a column is not specified in the INSERT query, its value will be calculated based on `expr`.

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete the existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster (
  id UInt64,
  updated_at DateTime DEFAULT now(),
  updated_at_date Date DEFAULT toDate(updated_at)
)
ENGINE = MergeTree
ORDER BY id;

-- 4. Insert data
INSERT INTO sample_db.sample_table (id) Values (1);

-- 5: Query data
SELECT * FROM sample_db.sample_table;
┌─id─┬──────updated_at─┬─updated_at_date─┐
│1     │ 2023-02-24 17:06:46 │2023-02-24 │
└────┴──────────┴─────────────────┘
```


<span id="c665f05d"></span>
#### ALIAS

Calculated column (synonym). Values for this type of column are not stored in the table, and you cannot insert values into it.

When a SELECT query explicitly references such columns, their values are computed from `expr` at query time. By default, `SELECT *` does not include ALIAS columns. You can disable this behavior by setting `asterisk_include_alias_columns`.

When new columns are added using an ALTER query, these columns will not have data for existing rows. When reading old data that does not contain new column values, expressions are evaluated immediately by default. If evaluating these expressions requires accessing different columns that are not specified in the query, those columns will also be read, but only for the relevant data blocks.

If you add a new column to a table and then modify its default expression, the values of existing data will also change. This applies to data that has not been stored on disk. Caution: When running a background merge, segments that are missing data for certain columns will have data for those columns written into them during the merge.

Elements in nested data structures cannot be assigned default values.

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE OR REPLACE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
    id UInt64,
    size_bytes Int64,
    size String ALIAS formatReadableSize(size_bytes)
)
ENGINE = MergeTree
ORDER BY id;

-- 4: Insert test data
INSERT INTO sample_db.sample_table VALUES (1, 4678899);

-- 5. Verify data insertion
SELECT id, size_bytes, size FROM sample_db.sample_table;
┌─id─┬─size_bytes─┬─size─────┐
│  1  │    4678899   │ 4.46 MiB    │
└───┴────────┴────────┘

-- 6. Wildcard query demonstration
SELECT * FROM sample_db.sample_table SETTINGS asterisk_include_alias_columns=1;
┌─id─┬─size_bytes─┬─size───┐
│  1  │    4678899   │ 4.46 MiB │
└───┴────────┴──────┘
```


<span id="ce646fb1"></span>
#### MATERIALIZED

Materialized expressions. The values of columns of this type are automatically calculated based on the specified materialized expression when a row is inserted. During the `INSERT` operation, you cannot explicitly specify the values of these columns.

In addition, this type of default value column is not included in the results of `SELECT *`. This is to maintain the invariant that the results of `SELECT *` can always be inserted back into the table using `INSERT`. This behavior can be disabled by setting `asterisk_include_materialized_columns`.

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create with a materialized list
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
    id UInt64,
    updated_at DateTime MATERIALIZED now(),
    updated_at_date Date MATERIALIZED toDate(updated_at)
)
ENGINE = MergeTree
ORDER BY id;

-- 4: Insert data
INSERT INTO sample_db.sample_table Values (1);

-- 5. Basic query validation
SELECT * FROM sample_db.sample_table;
┌─id─┐
│1    │
└───┘

-- 6. Display the materialized columns of the query
SELECT id, updated_at, updated_at_date FROM sample_db.sample_table;
┌─id─┬──────────updated_at─┬─updated_at_date─┐
│1    │ 2023-02-24 17:08:08         │2023-02-24        │
└───┴─────────────────┴───────────┘

-- 7. Wildcard query demonstration
SELECT * FROM sample_db.sample_table SETTINGS asterisk_include_materialized_columns=1;
┌─id─┬──────────updated_at─┬─updated_at_date─┐
│1    │ 2023-02-24 17:08:08         │2023-02-24        │
└───┴─────────────────┴───────────┘
```


<span id="2b327f6d"></span>
### COMMENT

Add comments to columns or tables.

<span id="9a0999ba"></span>
### Compression

The `compression_codec` field can be used to configure the codec. This configuration is optional, and the default value is `LZ4`.

ByteHouse supports both general\-purpose and specific encodings. General\-purpose codecs are more like the default codecs (LZ4, ZTSD) and their modified versions. Specific codecs are designed to make compression more effective by utilizing specific characteristics of the data.

<span id="f436499f"></span>
#### **General encoding**


* NONE: No compression.

* LZ4: Default value, lossless ultra\-fast compression algorithm.

* LZ4HC[(level)]: A high compression ratio LZ4HC algorithm with configurable levels. The default value for level is 9. Supported values are from 1 to 12, and values from 4 to 9 are recommended.

* ZSTD[(level)]: ZSTD compression algorithm with a configurable level. The default value of level is 1, and values from 1 to 22 are supported.


<span id="368a7f2a"></span>
#### **Specific coding algorithms**


* Delta (delta_bytes): Delta encoding, an algorithm that retains the first value and stores the difference between each subsequent value and its previous value. The default value is sizeof(type). Valid options are 1, 2, 4, or 8, and if any other value is set, it will be treated as 1.


<span id="4e867a6c"></span>
#### **Multi\-codec**


* Use the multiple codecs mentioned above. Compression is performed in the order declared by the codec, while decompression is performed in the reverse order.


Example:

```SQL
-- 1: Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table with the compression attribute
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
  date Date CODEC(Delta, ZSTD),
  ts DateTime CODEC(LZ4HC),
  float_value Float32 CODEC(NONE),
  double_value Float64 CODEC(LZ4HC(9))
)
ENGINE = MergeTree
PARTITION BY tuple()
ORDER BY date
```


<span id="ce633637"></span>
### ENGINE

Specify the table engine. For configuration details and examples, see [Create a new database/table: Based on the DDL template](https://docs.byteplus.com/docs/bytehouse/create-a-database-table-based-on-ddl-template).

<span id="e127dcd0"></span>
### Design sort keys (ORDER BY)

It can be a tuple of columns or any expression. For example: `ORDER BY (OrderID, Date)`.

If sorting is not required, you can use `ORDER BY tuple()`, and DataPart will store data in the order in which it was inserted.

**Grammar**

```SQL
[columnExpr] [ASCENDING|ASC|DESCENDING|DESC] [NULLS [FIRST|LAST] [COLLATE STRING_LITERAL]
```



* `[ASCENDING|ASC|DESCENDING|DESC]`: Specify the sorting direction. If no direction is specified, the default is `ASC`.

* `[NULLS [FIRST|LAST]`: Determine the sorting order of `NaN` and `NULL`.

   * By default, or when the `NULLS LAST` modifier is used, values come first, followed by `NaN`, and finally `NULL`.

   * When using the `NULLS FIRST` modifier: `NULL` comes first, then `NaN`, and finally other values.

* `[COLLATE STRING_LITERAL]`: You can specify collation rules for sorting by string values.

   * Sorting rules support LowCardinality, Nullable, Array, and Tuple.

   * When using `COLLATE`, sorting is always case\-insensitive.

   * It is recommended to use `COLLATE` only when performing a final sort on a small number of rows, because sorting with `COLLATE` is less efficient than normal byte\-wise sorting.


<span id="badf559f"></span>
#### **Example 1: Sort by multiple orderExpr**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster;

-- 3. Create a table with a sort key
CREATE TABLE IF NOT EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster (
  id UInt32,
  val UInt32
)
ENGINE = MergeTree()
ORDER BY id;

-- 4. Insert data
INSERT INTO sample_db.sample_orderByTable VALUES (1, 5), (1, 15), (2, 5), (2, 15);

-- 5. Query data and sort by multiple orderExpr
SELECT * FROM sample_db.sample_orderByTable ORDER BY id ASC, val DESC;
```


<span id="c924f85d"></span>
#### **Example 2: Sort by NULL FIRST**

```SQL
-- 1: Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster;

-- 3. Create a table with a sort key
CREATE TABLE IF NOT EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster (
  id UInt32,
  val Nullable(UInt32)
)
ENGINE = MergeTree()
ORDER BY id;

-- 4: Insert data
INSERT INTO sample_db.sample_orderByTable VALUES (1, 2), (2, NULL), (3, 2), (3, 3), (3, NULL);

-- 5. Query data, and sort by NULL FIRST
SELECT * FROM sample_db.sample_orderByTable ORDER BY val DESC NULLS FIRST;
```


<span id="9663251a"></span>
#### **Example 3: Sort by COLLATE**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete the existing table
DROP TABLE IF EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster;

-- 3. Create a table with a sort key
CREATE TABLE IF NOT EXISTS sample_db.sample_orderByTable ON CLUSTER sample_cluster (
  x UInt32,
  s Nullable(String)
)
ENGINE = MergeTree
ORDER BY x;

-- 4. Insert data
INSERT INTO sample_db.sample_orderByTable VALUES 
  (1, 'bca'), (2, NULL), (3, 'ABC'), 
  (4, '123a'), (5, 'abc'), (6, NULL), (7, 'BCA');

-- 5. Query data, and sort using COLLATE
SELECT * FROM sample_db.sample_orderByTable ORDER BY s ASC COLLATE 'ru';
```


<span id="17211937"></span>
### Design partition key (PARTITION BY)

The partition key defines partitions. A partition is a logical data set within a table, created by dividing the table according to specified rules. Partitioning can be performed according to any criteria, for example, by date. To reduce the amount of data that needs to be processed, each partition is stored separately. When querying, ByteHouse tries to use the smallest possible subset of these partitions. The `PARTITION BY expr` clause is specified when creating a table. A partition key can be any expression involving the columns in the table. For example, to specify partitioning by month, use the expression `toYYYYMM(date)`; or to partition by an expression tuple, such as `(toMonday(date), EventType)`, and more.

Caution: The value range calculated by the partition expression in the table should not be too large (it is recommended that the range does not exceed ten thousand). Having too many partitions will consume significant memory and result in increased input/output (IO) and computational overhead.

Designing partition keys appropriately can significantly reduce the amount of data that needs to be scanned during queries. In general, columns that are most frequently used as query conditions and have a value range of no more than ten thousand, such as dates, should be designed as partition keys.

<span id="8b4d29ab"></span>
#### **Example 1: Partition key defined by columnExpr**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_partitionByTable ON CLUSTER sample_cluster;

-- 3. Create a partition key table defined by columnExpr
CREATE TABLE sample_db.sample_partitionByTable ON CLUSTER sample_cluster (
  VisitDate Date,
  Hour UInt8,
  ClientID UUID
)
ENGINE = MergeTree
PARTITION BY VisitDate
ORDER BY Hour;
```


<span id="39810274"></span>
#### **Example 2: Define partition keys in a tuple of columnExpr**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_partitionByTable ON CLUSTER sample_cluster;

-- 3. Create a table with a partition key
CREATE TABLE sample_db.sample_partitionByTable ON CLUSTER sample_cluster (
  VisitDate Date,
  Hour UInt8,
  ClientID UUID
)
ENGINE = MergeTree
PARTITION BY (VisitDate, Hour)
ORDER BY Hour;
```


<span id="e9861949"></span>
### Design a primary key (PRIMARY KEY)

By default, you do not need to explicitly specify the primary key. ByteHouse will use the sorting key as the primary key. When the primary key and sort key differ in special scenarios, the primary key must be the leftmost prefix of the sort key. If the sort key is `(OrderID, Date)`, the primary key must be `OrderID` and cannot be `Date`.

ByteHouse creates a sparse index on the primary key, using Granule as the unit. In contrast, a so\-called dense index creates index information for every row.

If the query condition can match the leftmost prefix of the primary key index, the primary key index can be used to quickly filter out the data granules that may need to be read, which is usually much more efficient than scanning the entire DataPart.

Caution: PRIMARY KEY does not guarantee uniqueness, so it is possible to insert rows with duplicate primary keys.

PARTITION BY and PRIMARY KEY are two distinct methods for accelerating data queries. When defining them, you should, if possible, use different columns for each to cover a wider range of query scenarios. For example, do not duplicate the first column of ORDER BY in PARTITION BY. Here are some considerations for selecting a primary key:


* Whether it is a column commonly used in query conditions;

* Not the first column among the non\-partition key columns;

* Columns with low selectivity, such as gender or yes/no, are not recommended for inclusion in the primary key.

* If the current primary key is (a, b), and in most cases the data range corresponding to (a, b) is large (including multiple Granules), you may consider adding a new commonly queried column to the primary key so that more data can be filtered.

* Excessively long primary keys can have a negative impact on insert performance and memory consumption, but do not affect query performance.


<span id="639432b1"></span>
#### **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster (
  id UInt32
) 
ENGINE=MergeTree 
ORDER BY id
PRIMARY KEY id;
```


<span id="c68635f4"></span>
### The unique key index (UNIQUE KEY)

A primary key does not guarantee deduplication. If deduplication based on uniqueness is required, you need to set a unique index when creating the table. After setting a unique key, ByteHouse provides upsert write semantics, allowing efficient updates to data rows based on the unique key. Alternatively, during upsert, you can set the virtual column `*delete_flag*=1`, which can be used to delete the specified key. The query automatically returns the latest value for each unique key. For more information, refer to the upsert functionality of the [HaUniqueMergeTree](https://docs.byteplus.com/docs/bytehouse/hauniquemergetree) table.

A unique key can be a tuple of columns or any expression, such as `UNIQUE KEY (product_id, sipHash64(city))`.

When querying by unique key, the unique key index is used to filter data and accelerate the query. Therefore, the primary key can be set to columns different from the unique key, allowing more query conditions to be covered. However, to use the partial column update feature, the unique key must be the leftmost prefix of the sort key.

<span id="1a7b09e2"></span>
#### **Example 1: Single\-field unique key**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete an existing table
DROP TABLE IF EXISTS sample_db.sample_uniqueKeyTable ON CLUSTER sample_cluster;

-- 3. Create a unique key table
CREATE TABLE sample_db.sample_uniqueKeyTable ON CLUSTER sample_cluster (
  `event_date` Date,
  `order_id` UInt64,
  `state` UInt32,
  `amount` UInt64
)
ENGINE = HaUniqueMergeTree
PARTITION BY event_date
ORDER BY state
UNIQUE KEY order_id;

-- 4. Insert data (including duplicate keys), rows with the same key will replace the previous row
INSERT INTO sample_db.sample_table VALUES
('2021-03-01', 1001, 1, 100),
('2021-03-01', 1002, 1, 200),
('2021-03-01', 1001, 2, 100),
('2021-03-02', 1001, 1, 400);

-- 5. Query data validation: records with the same order_id are merged, retaining the last inserted value
SELECT * FROM sample_db.sample_table ORDER BY event_date, order_id;
┌─event_date─┬─order_id─┬─state─┬─amount─┐
│ 2021-03-01 │ 1001 │ 2 │100 │
│ 2021-03-01 │ 1002 │ 1 │200 │
│ 2021-03-02 │ 1001 │ 1 │400 │
└────────────┴──────────┴───────┴────────┘

-- 6. Insert more test data to continue verification
INSERT INTO sample_db.sample_table VALUES
('2021-03-01', 1002, 2, 200),
('2021-03-02', 1001, 2, 400),
('2021-03-02', 1002, 1, 300);

-- 7. Final result verification. All records with duplicate order_id values have been merged into the latest version.
SELECT * FROM sample_db.sample_table ORDER BY event_date, order_id;
┌─event_date─┬─order_id─┬─state─┬─amount─┐
│ 2021-03-01 │ 1001 │ 2 │100 │
│ 2021-03-01 │ 1002 │ 2 │200 │
│ 2021-03-02 │ 1001 │ 2 │400 │
│ 2021-03-02 │ 1002 │ 1 │300 │
└────────────┴──────────┴───────┴────────┘
```


<span id="cd1b985b"></span>
#### **Example 2: Multi\-field Unique Key**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_uniqueKeyTable ON CLUSTER sample_cluster;

-- 3. Create a table with a multi-column unique key
CREATE TABLE sample_db.sample_uniqueKeyTable ON CLUSTER sample_cluster (
  `event_date` Date,
  `region` UInt64,
  `state` String,
  `amount` UInt64
)
ENGINE = HaUniqueMergeTree
PARTITION BY event_date
ORDER BY state
UNIQUE KEY (region, state);
```


<span id="6070b2c7"></span>
### Sampling (SAMPLE BY)

Expression used for sampling; this configuration is optional.

If you use a sampling expression, the primary key must include this expression. For example: `SAMPLE BY intHash32(UserID) ORDER BY (CounterID, EventDate, intHash32(UserID))`.

<span id="109b9843"></span>
### Column and table TTL

A list of rules that specify the retention duration for row storage and define the logic for moving data segments on disks and volumes (optional). An expression must contain at least one column of the `Date` or `DateTime` type, for example: `TTL date + INTERVAL 1 DAY`.

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_ttlTable ON CLUSTER sample_cluster;

-- 3. Create a table with TTL
CREATE TABLE sample_db.sample_ttlTable ON CLUSTER sample_cluster (
  VisitDate Date,
  Hour UInt8,
  ClientID UUID
)
ENGINE = MergeTree
ORDER BY Hour
PARTITION BY VisitDate
TTL VisitDate + INTERVAL 1 DAY;
```


<span id="5007c48c"></span>
### SETTINGS

To configure MergeTree settings, refer to the community documentation: [MergeTree table configuration](https://clickhouse.com/docs/operations/settings/merge-tree-settings).

<span id="e2ea1cc8"></span>
### MySQL compatibility

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL\-compatible syntax is recommended for use with relevant dialects.</div>


ByteHouse is compatible with most MySQL DDL statements, and you can directly execute MySQL CREATE TABLE statements in ByteHouse. Please refer to the following example:

<span id="46db1f49"></span>
#### MySQL

```SQL
CREATE TABLE `sample_table` (
  `uid` bigint NOT NULL AUTO_INCREMENT,
  `phone` varchar(255) DEFAULT NULL,
  `no1` bigint DEFAULT NULL,
  `appleid` varchar(255) DEFAULT NULL,
  
  PRIMARY KEY (`uid`) USING BTREE,
  UNIQUE KEY `no1` (`no1`) USING BTREE,
  KEY `idx_apple_id` (`appleid`) USING BTREE,
  KEY `phone` (`phone`) USING BTREE
)
ENGINE = InnoDB
AUTO_INCREMENT = 60937910
DEFAULT CHARSET = utf8mb3;
```


<span id="27aaef32"></span>
#### ByteHouse

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete an existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table with TTL
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
  `uid` Int64 NOT NULL,
  `phone` String NULL DEFAULT NULL,
  `no1` Int64 NULL DEFAULT NULL,
  `appleid` String NULL DEFAULT NULL
)
ENGINE = HaUniqueMergeTree
ORDER BY tuple(uid)
UNIQUE KEY tuple(uid)
SETTINGS 
  partition_level_unique_keys = 0,
  allow_nullable_key = 1,
  index_granularity = 8192;
```


<span id="cdf338a3"></span>
#### DDL conversion logic

Note the following conversion logic.


|Detailed comparison items |MySQL |ByteHouse |Note |
|---|---|---|---|
|Column properties |Data types |Compatibility |For details about data compatibility across different MySQL types, see [MySQL Compatibility](https://docs.byteplus.com/docs/bytehouse/mysql-compatibility). |
||AUTO_INCREMENT |Compatibility |ByteHouse now supports the auto\-increment ID capability (`generateSnowflakeID`). When creating tables, here is a comparison of usage:<br><br><br>* ByteHouse<br><br>   ```SQL```<br>```   SET dialect_type = 'CLICKHOUSE';```<br>```   ```<br>```   CREATE TABLE sampl_table (```<br>```     id Int64,```<br>```     val1 String```<br>```   )```<br>```   ENGINE = MergeTree()```<br>```   ORDER BY id;```<br>```   ```<br>   <br><br>* MySQL<br><br>   ```SQL```<br>```   SET dialect_type = 'MYSQL';```<br>```   ```<br>```   CREATE TABLE sample_table (```<br>```     id BIGINT AUTO_INCREMENT PRIMARY KEY,```<br>```     val1 VARCHAR(255)```<br>```   );```<br>```   ```<br>    |
||NULL |Compatibility |None |
||DEFAULT |Compatibility |None |
||Other definitions |Compatibility |ByteHouse is compatible with most commonly used field definitions. |
|Table attributes |Primary key: PRIMARY KEY |Unique key: UNIQUE KEY |In MySQL semantics, the primary key maps to the unique key in ByteHouse, not to ByteHouse's primary key. |
|||Sort key: ORDER BY |By default, sorting is performed by the primary key of the MySQL table. |
||UNIQUE KEY `no1` (`no1`) USING BTREE |Ignore |ByteHouse supports the Constraint syntax, but does not enforce it. |
||The remaining definitions:<br><br>ENGINE=InnoDB AUTO_INCREMENT=60937910 DEFAULT CHARSET=utf8mb3; |Ignore |Ignore |
|Settings |None |Settings |When creating a table using the MySQL dialect, ByteHouse adds the following settings by default:<br><br><br>1. partition_level_unique_keys = 0 \-\> Disables partition\-level deduplication and ensures deduplication for the entire table<br><br>2. index_granularity = 8192 \-\> default setting<br><br>3. allow_nullable_key = 1 \-\> Allows nullable keys to be used in ORDER BY clauses |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ByteHouse also provides some compatibility with the syntax of other databases. If you are interested, please contact us.</div>


<span id="7c405878"></span>
# CREATE TABLE AS SELECT（CTAS）

<span id="aa929a31"></span>
## Grammar

Create a table with a structure similar to the result of a SELECT query, use the specified engine, and populate it with data from the SELECT query.

```SQL
CREATE TABLE [IF NOT EXISTS] [db.]table_name (
    name1 [type1],
    name2 [type2],
    ...
) 
ENGINE = MergeTree 
ORDER BY expr 
[PARTITION BY expr] 
AS SELECT ...
```


<span id="f4143770"></span>
## Parameter description


|Parameters |Required field |Definition |
|---|---|---|
|IF NOT EXISTS |No |Determine whether the newly created table already exists; if the `db_name` database already exists, then ByteHouse will not create a new database and:<br><br><br>* If a clause is specified, no exception is thrown.<br><br>* If no clause is specified, an exception is thrown. |
|db. |No |Represents the database name. If omitted, the system will use the current database by default. |
|table_name |Yes |Name of the newly created table. |
|(name1 [type1], name2 [type2], ...) |No |List of column definitions If not specified, the column structure of the new table will be determined based on the result of the SELECT statement. If column names are specified, their number must match the number of columns returned by the SELECT statement, and the data types must be compatible. |
|ENGINE = MergeTree |Yes |This parameter specifies the table engine as MergeTree. Other clauses can be added after the ENGINE clause. |
|ORDER BY expr |Yes |The sort key specifies the order in which data is stored on disk, and this arrangement affects query performance. It can be a single column or an expression composed of multiple columns. |
|PARTITION BY expr |No |A partition key specifies a partition expression, allowing data to be divided into different partitions according to defined rules, which helps improve the efficiency of querying and deleting data. |
|AS SELECT ... |Yes |This section is used to retrieve data from the results of a SELECT statement and populate a newly created table. The number of columns, column order, and data types in the SELECT statement must match the column definitions of the new table, if any. |


<span id="8e458fa2"></span>
## **Example**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.user_events ON CLUSTER sample_cluster;

-- 3. Create the main table
CREATE TABLE sample_db.user_events ON CLUSTER sample_cluster (
  user_id UInt32,
  event_time DateTime,
  event_type String,
  event_data String
)
ENGINE = MergeTree()
ORDER BY user_id
PRIMARY KEY user_id;

-- 4. Insert data (with the corrected target table name)
INSERT INTO sample_db.user_events (user_id, event_time, event_type, event_data)
VALUES (10112, '2024-08-28 05:11:58', 'ERROR', 'this is a bug');

INSERT INTO sample_db.user_events (user_id, event_time, event_type)
VALUES (10112, '2024-07-28 05:11:58', 'ERROR');

-- Caution: This insert statement is missing the event_type column (a non-NULL column), which will result in an error.
INSERT INTO sample_db.user_events (user_id, event_time, event_data)
VALUES (10112, '2024-07-28 05:11:58', 'this is a bug');

-- 5. Create a subtable (correct the source table name and AS clause syntax)
CREATE TABLE IF NOT EXISTS sample_db.user_events2 ON CLUSTER sample_cluster (
  user_id UInt32,
  event_time DateTime,
  event_data String
)
ENGINE = MergeTree
ORDER BY user_id
AS SELECT 
  user_id, 
  event_time, 
  event_data 
FROM sample_db.user_events 
LIMIT 100;

-- 6. Query subtables
SELECT * FROM sample_db.user_events2;
```


<span id="44b904e3"></span>
# Create a view (CREATE VIEW)

ByteHouse supports views and materialized views.

<span id="001258d3"></span>
## Normal view

A view does not store any data; instead, it reads from another table each time it is accessed. In other words, a regular view is simply a saved query. When reading from a view, this saved query is used as a subquery in the FROM clause.

<span id="8ebf8456"></span>
### **Grammar**

```SQL
CREATE [OR REPLACE] VIEW [IF NOT EXISTS] [tableIdentifier] [UUID uuid] AS [selectUnionStmt]
```


<span id="2bf401c1"></span>
### Parameter description


|Parameters |Required field |Definition |
|---|---|---|
|OR REPLACE |No |If specified, ByteHouse will create a new view and replace the old view with the same name. |
|IF NOT EXISTS |No |If specified, the query will not return an error when the view already exists. |
|tableIdentifier |Yes |The name of the view, in the format `[db.]view_name`. If the database name `db.` is omitted, the current database is used. |
|UUID uuid |No |Specify a unique identifier (UUID) for the view. If you specify a UUID, the table will use the UUID you provide. Otherwise, an automatically generated UUID will be used. |
|AS selectUnionStmt |Yes |The SELECT query statement that defines the view. A view does not store actual data; instead, it dynamically executes this statement when queried. |


<span id="30f6bf80"></span>
### Example

<span id="7f690384"></span>
#### **Create a view**

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster (
  `order_by_column` String
)
ENGINE = MergeTree
ORDER BY (`order_by_column`)

-- 4. Create views based on existing tables
CREATE VIEW sample_view AS SELECT * FROM sample_db.sample_table
```


<span id="bf4a0930"></span>
#### **Query view**

```SQL
SELECT a, b, c FROM sample_db.sample_view
```


<span id="fcf38a7a"></span>
## Materialized view

For more information, see [materialized view](https://docs.byteplus.com/en/docs/bytehouse/materialized-view).

<span id="c222849a"></span>
# Create a dictionary (CREATE DICTIONARY)

ByteHouse data dictionaries are divided into **built\-in dictionaries** and **external dictionaries**:


* The built\-in dictionary is the dictionary content predefined by ClickHouse.

* The external extension dictionary provides various flexible and customizable data source definitions, including local files, ClickHouse tables, remote files accessible via HTTP, and other database sources such as ODBC, MySQL, ClickHouse, MongoDB, Redis, and PostgreSQL.


<span id="7453f80f"></span>
## Create a dictionary table

You can directly use DDL statements in the SQL workbench to create a dictionary table.

```SQL
CREATE DICTIONARY [IF NOT EXISTS] [db.]dictionary_name (
  key1 type1[DEFAULT|EXPRESSION expr1] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
  key2 type2[DEFAULT|EXPRESSION expr2] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
  attr1 type2 [DEFAULT|EXPRESSION expr3],
  attr2 type2 [DEFAULT|EXPRESSION expr4]
)
PRIMARY KEY key1, key2
SOURCE(SOURCE_NAME(
  [param1 value1 ... paramN valueN]
))
LAYOUT(LAYOUT_NAME([param_name param_value]))
LIFETIME({MIN min_val MAX max_val | max_val})
```


<span id="aec0d7ae"></span>
### Parameter explanation


|Parameters |Required field |Definition |
|---|---|---|
|IF NOT EXISTS |No |If specified, no error is reported when the dictionary already exists, and the creation operation is skipped. |
|[db.]dictionary_name |Yes |The name of the dictionary, in the format `[database name.]dictionary name`. If the database name is omitted, the current database is used. |
|(key1 type1 [...] , key2 type2 [...] , ...) |Yes |Define the dictionary keys and values A key is used to uniquely identify entries in a dictionary, and an attribute is the data associated with the key.<br><br>The key type of the dictionary can be set to any basic data type supported by ClickHouse, and one or more fields can be specified as the key. For details about supported data types, see [Common data types](https://docs.byteplus.com/docs/bytehouse/common-data-types). It is recommended to use types that can be specified by literals, such as numeric types and string types, to facilitate the use of dictionary functions. |
|PRIMARY KEY key1, key2 |Yes |Specify the primary key for the dictionary, which can consist of one or more keys. |
|SOURCE(SOURCE_NAME([...])) |Yes |Specify the source of dictionary data. Supported data sources include:<br><br><br>* Local file: Configuration format example `SOURCE(FILE(path './user_files/os.tsv' format 'TabSeparated'))`.<br><br>* ClickHouse table: configuration format example `SOURCE(CLICKHOUSE(DB 'test' TABLE 'students_info'))`<br><br>* Remote files accessible via HTTP: Configuration format example `SOURCE(HTTP(URL 'https://[storage-service-domain]/[dataset-category-directory]/[specific-dataset-name]/[file-name].csv' FORMAT 'CSVWithNames'))`<br><br>* Other database sources: Configuration format example `SOURCE(MySQL(host ' mysql_host.example.com' port 3306 user 'dict_reader' password 'secure_password' db 'user_db' table 'users'))` For more data source configuration examples, see [Other database source configuration examples](https://docs.byteplus.com/docs/bytehouse/ce-create-statement#e603eac8). |
|LAYOUT(LAYOUT_NAME([...])) |Yes |Define the organization of a dictionary, that is, how to implement a dictionary. A dictionary can be implemented using an array or a HashMap. It can be stored entirely in memory, or stored using a combination of disk and memory. Specificity and data volume are related to the complexity of the dictionary. Two types of classification based on the dictionary keys:<br><br><br>* Keys of the UInt64 type may use **flat**, **hashed**, range_hashed, and cache layouts.<br><br>* Other composite types: **complex_key_hashed**, complex_key_cache, and ip_trie types.<br><br><br>Usage scenarios for common types are as follows:<br><br><br>* The hash structure is a commonly used method for organizing dictionaries. The implementations of hashed and complex_key_hashed are identical, but they are suitable for different key types.<br><br>* flat stores dictionary data in an array, with a maximum array size of 500,000. An error is reported if this limit is exceeded.<br><br>* ip_trie is suitable for scenarios where IP addresses are used as keys. |
|LIFETIME({MIN min_val MAX max_val |max_val}) |Yes |


<span id="e603eac8"></span>
#### Other database source configuration examples


* ODBC

   ```SQL
   SOURCE(ODBC(
       db 'DatabaseName'
       table 'SchemaName.TableName'
       connection_string 'DSN=some_parameters'
       invalidate_query 'SQL_QUERY'
       query 'SELECT id, value_1, value_2 FROM db_name.table_name'
   ))
   ```
   

* MySQL

   ```SQL
   SOURCE(MYSQL(
       port 3306
       user 'clickhouse'
       password 'qwerty'
       replica(host 'example01-1' priority 1)
       replica(host 'example01-2' priority 1)
       db 'db_name'
       table 'table_name'
       where 'id=10'
       invalidate_query 'SQL_QUERY'
       fail_on_connection_loss 'true'
       query 'SELECT id, value_1, value_2 FROM db_name.table_name'
   ))
   ```
   

* ClickHouse

   ```SQL
   SOURCE(CLICKHOUSE(
       host 'example01-01-1'
       port 9000
       user 'default'
       password ''
       db 'default'
       table 'ids'
       where 'id=10'
       secure 1
       query 'SELECT id, value_1, value_2 FROM default.ids'
   ));
   ```
   

* MongoDB

   ```SQL
   SOURCE(MONGODB(
       host 'localhost'
       port 27017
       user ''
       password ''
       db 'test'
       collection 'dictionary_source'
       options 'ssl=true'
   ))
   ```
   

* Redis

   ```SQL
   SOURCE(REDIS(
       host 'localhost'
       port 6379
       storage_type 'simple'
       db_index 0
   ))
   ```
   

* PostgreSQL

   ```SQL
   SOURCE(POSTGRESQL(
       port 5432
       host 'postgresql-hostname'
       user 'postgres_user'
       password 'postgres_password'
       db 'db_name'
       table 'table_name'
       replica(host 'example01-1' port 5432 priority 1)
       replica(host 'example01-2' port 5432 priority 2)
       where 'id=10'
       invalidate_query 'SQL_QUERY'
       query 'SELECT id, value_1, value_2 FROM db_name.table_name'
   ))
   ```
   


<span id="4336d318"></span>
## Query dictionary tables

<span id="066a14df"></span>
### dictGet

dicGet is used to obtain mapping values.

```SQL
dictGet('dict_name', attr_names, id_expr)
dictGetOrDefault('dict_name', attr_names, id_expr, default_value_expr)
dictGetOrNull('dict_name', attr_name, id_expr)
```


**Parameter descriptions**


* `dict_name` — Dictionary name, the name specified when creating the dictionary, a string constant.

* `attr_names` — The column name containing the read value. Use the Tuple type to retrieve multiple value fields at the same time; use String when retrieving only one field name.

* `id_expr` — The specific value of a dictionary key. Supports the UInt64 or Tuple type. You can refer to the following examples.


<span id="464ec62d"></span>
### dictHas

dicHas allows the user to determine whether a key exists in the dictionary.

```SQL
dictHas('dict_name', id_expr)
The return value is 1 or 0.
```


<span id="e41ed72f"></span>
## Example

<span id="f74dad4d"></span>
### Example 1: Create a ClickHouse dictionary table

The following example demonstrates a ClickHouse dictionary source table, which is located in the cluster containing the user's tables and can be accessed directly using the DICTIONARY table.

```SQL
-- 1. Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a dictionary
CREATE DICTIONARY sample_db.sample_dict ON CLUSTER sample_cluster (
    id UInt64,
    name String
)
PRIMARY KEY id
SOURCE(CLICKHOUSE(DB 'sample_db' TABLE 'sample_dict'))
LAYOUT(FLAT())
LIFETIME(MIN 0 MAX 180)
```


<span id="b08c8591"></span>
### Example 2: Create a MySQL dictionary table

The following example demonstrates the MySQL dictionary source table. When using this example, replace the corresponding placeholders with your actual MySQL connection information.

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample ON CLUSTER sample_cluster;

-- 2. Create a dictionary
CREATE DICTIONARY IF NOT EXISTS sample.user_dict on cluster sample_cluster
(
    `user_id` UInt64,
    `username` String,
    `age` UInt8 DEFAULT 0,
    `gender` UInt8 DEFAULT 0,
    `last_login` DateTime
)
PRIMARY KEY user_id
SOURCE(MySQL(
    host 'mysql_host.example.com'
    port 3306
    user 'dict_reader'
    password 'secure_password'
    db 'user_db'
    table 'users'
))
LAYOUT(FLAT())
LIFETIME(MIN 300 MAX 900);
```


<span id="85bfa1f4"></span>
### Example 3: Use a dictionary table


* Query dictionary entries

   You can obtain data from the data dictionary by using the dictionary query functions mentioned above.

   ```SQL
   -- Query the value of a single field using a single key
   SELECT dictGet('sample_dict', 'user', toUInt64(1001));
   
   -- Use a single key to query the values of multiple fields
   SELECT dictGet('sample_dict', ('user', 'age', 'gender'), toUInt64(1001));
   
   -- Use multiple keys to query the corresponding single field value
   SELECT dictGet('sample_dict', 'age', (toUInt64(1001), 'user1'));
   
   -- Query the corresponding field values using multiple keys
   SELECT dictGet('sample_dict', ('age', 'gender'), tuple(toUInt64(1001), 'user1'));
   
   -- If the field type in the query is String, you can use:
   SELECT dictGetString('sample_dict', 'user', toUInt64(1001));
   
   -- If the queried field does not exist, return the specified default value
   SELECT dictGetOrDefault('sample_dict', 'user', toUInt64(1005), 'NULL');
   
   -- When querying fields with multiple keys, if any field does not exist, Null is returned.
   SELECT dictGetOrNull('sample_dict', ('age', 'gender'), (toUInt64(1001), 'user1'));
   
   -- Check whether a field exists for the key:
   SELECT dictHas('sample_dict', toUInt64(1001));
   ```
   

* Delete a dictionary

   ByteHouse will delete the record of the dictionary in the Catalog.

   ```SQL
   DROP DICTIONARY IF EXISTS sample_db.sample_dict;
   ```
   

* Query dictionary

   If the `FROM` clause is not specified, the query returns a list of dictionaries in the current database.

   ```SQL
   SHOW DICTIONARIES FROM sample_db; 
   ```
   

* Query statements for creating dictionaries

   ```SQL
   SHOW CREATE DICTIONARY sample_db.sample_dict;
   ```
   

   This query returns a string\-type column named "statement", which contains a value that is a CREATE query statement used to create the specified object.
