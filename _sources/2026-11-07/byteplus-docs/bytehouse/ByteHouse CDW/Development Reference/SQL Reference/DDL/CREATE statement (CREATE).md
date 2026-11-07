---
title: "CREATE statement (CREATE)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/create-statement"
---

<span id="e38dcd13"></span>
### Create database `(CREATE DATABASE)`

<span id="60c6a73f"></span>
#### Syntax

```SQL
CREATE DATABASE [IF NOT EXISTS] db_name [ENGINE=Cnch]
```


**IF NOT EXISTS**

If the database `db_name` already exists, ByteHouse will not create a new database and:


* If the clause is specified, it will not raise an exception.

* If the clause is not specified, it will throw an exception.


<span id="bb074d23"></span>
#### **Example**


* Create a database using the default engine.


```SQL
CREATE DATABASE IF NOT EXISTS test;
```



* Create a database using an optional engine, currently only Cnch is supported.


```SQL
CREATE DATABASE IF NOT EXISTS test ENGINE=Cnch;
```


<span id="dedcf2a4"></span>
### Create table (`CREATE TABLE`)

<span id="d411472d"></span>
#### Syntax

```SQL
CREATE TABLE [IF NOT EXISTS] [db.]table_name
(
name1 [type1] [NULL|NOT NULL] [DEFAULT|ALIAS expr1 | MATERIALIZED expr1] [COMMENT 'string'][compression_codec][TTL expr1],
name2 [type2] [NULL|NOT NULL] [DEFAULT|ALIAS expr2 | MATERIALIZED expr1] [COMMENT 'string'] [compression_codec] [TTL expr2],
...
 ) ENGINE = CnchMergeTree()
ORDER BY expr
[PARTITION BY expr]
[CLUSTER BY (column, expression, ...) INTO value1 BUCKETS SPLIT_NUMBER value2 WITH_RANGE]
[PRIMARY KEY expr]
[UNIQUE KEY expr]
[SAMPLE BY expr]
[TTL expr]
[SETTINGS name=value, ...]
[COMMENT='COMMENT']
```


<span id="a4576013"></span>
#### Example

```SQL
CREATE TABLE IF NOT EXISTS test.createTable(
id UInt32,
name String DEFAULT '',
CONSTRAINT constraint1 CHECK id > 10
) 
ENGINE=CnchMergeTree
ORDER BY id
```


<span id="3ac2265c"></span>
#### Configuration parameters

<span id="342529fa"></span>
##### NULL or NOT NULL Modifiers

In column definitions, the NULL and NOT NULL modifiers following the data type specify whether the column is nullable.

If the data type is not nullable and NULL is specified, the column will be considered nullable; if NOT NULL is specified, it will not.

For example, INT NULL is the same as Nullable(INT). If the data type is nullable and the NULL or NOT NULL modifier is specified, an exception will be thrown.

<span id="f5d1f5bb"></span>
##### Default value (**DEFAULT VALUES**)

Column descriptions can specify a default value expression, formatted as DEFAULT expr, MATERIALIZED expr, or ALIAS expr. Example: URLDomain String DEFAULT domain(URL).

The expression expr is optional. If omitted, the column type must be explicitly specified, and the default values are 0 for numeric columns, '' (empty string) for string columns, [] (empty array) for array columns, 1970\-01\-01 for date columns, and NULL for nullable columns.

The column type for a default value can be omitted, in which case it will be inferred from the type of expr. For example, the type for the column EventDate DEFAULT toDate(EventTime) will be date.

If both data type and default value expression are specified, an implicit type conversion function will be inserted to convert the expression to the specified type. For example: Hits UInt32 DEFAULT 0 is internally represented as Hits UInt32 DEFAULT toUInt32(0).

Default value expressions expr can refer to any table column or constant. ByteHouse ensures that changes to the table structure do not introduce cycles in expression evaluation. For INSERT operations, it checks whether the expressions are solvable—that is, all required columns to be computed are provided.

<span id="99259651"></span>
##### **DEFAULT**

Standard default value. If the value of such columns is not specified in the INSERT query, it will be calculated based on **`expr`**.

```SQL
CREATE TABLE [db.]test
(
id UInt64,
updated_at DateTime DEFAULT now(),
updated_at_date Date DEFAULT toDate(updated_at)
)
ENGINE = CnchMergeTree
ORDER BY id;

INSERT INTO test (id) Values (1);

SELECT * FROM test;
┌─id─┬──────────updated_at─┬─updated_at_date─┐
│1   │ 2023-02-24 17:06:46 │2023-02-24       │
└────┴─────────────────────┴─────────────────┘
```


<span id="13a04211"></span>
##### MATERIALIZED

Materialized expressions. The values of such columns are automatically calculated based on the specified materialized expressions when a row is inserted. During `INSERT` operations, the values of these columns cannot be explicitly specified.

Furthermore, this type of default value columns is not included in the results of `SELECT *`. This is to ensure that the results of `SELECT *` can always be inserted back into the table with `INSERT` for consistency. This behavior can be disabled by setting `asterisk_include_materialized_columns`.

```SQL
CREATE TABLE [db.]test
(
id UInt64,
updated_at DateTime MATERIALIZED now(),
updated_at_date Date MATERIALIZED toDate(updated_at)
)
ENGINE = CnchMergeTree
ORDER BY id;

INSERT INTO test Values (1);

SELECT * FROM test;
┌─id─┐
│1   │
└────┘

SELECT id, updated_at, updated_at_date FROM test;
┌─id─┬──────────updated_at─┬─updated_at_date─┐
│1   │ 2023-02-24 17:08:08 │2023-02-24       │
└────┴─────────────────────┴─────────────────┘

SELECT * FROM test SETTINGS asterisk_include_materialized_columns=1;
┌─id─┬──────────updated_at─┬─updated_at_date─┐
│1   │ 2023-02-24 17:08:08 │2023-02-24       │
└────┴─────────────────────┴─────────────────┘
```


<span id="d33d47ce"></span>
##### ALIAS

Calculated column (synonym). This type of column is not stored in the table, nor can values be inserted into it.

When a SELECT query explicitly references this type of column, the value is calculated at the time of the query from **`expr`**. By default, SELECT \* excludes ALIAS columns. This behavior can be disabled by setting asterisk_include_alias_columns.

When adding new columns with an ALTER query, old data for these columns is not written. Conversely, when reading old data that lacks new column values, expressions are calculated on the fly by default. However, if running these expressions requires querying different columns not specified in the query, those columns will also be read additionally, but only for the required data blocks.

If new columns are added to the table but their default expressions are later modified, the values used for old data will change as well (for those not stored on the disk). Please note, when background merges are run, data for missing columns in some parts will be written into these columns during the merge.

It is not possible to set default values for elements within nested data structures.

```SQL
CREATE TABLE [db.]test
(
id UInt64,
size_bytes Int64,
size String Alias formatReadableSize(size_bytes)
)
ENGINE = CnchMergeTree
ORDER BY id;

INSERT INTO test Values (1, 4678899);

SELECT id, size_bytes, size FROM test;
┌─id─┬─size_bytes─┬─size─────┐
│1   │ 4678899    │ 4.46 MiB │
└────┴────────────┴──────────┘

SELECT * FROM test SETTINGS asterisk_include_alias_columns=1;
┌─id─┬─size_bytes─┬─size─────┐
│ 1  │ 4678899    │ 4.46 MiB │
└────┴────────────┴──────────┘
```


<span id="c22a1a72"></span>
##### Designing a partition key (PARTITION BY)

A partition key defines partitions, which are logical data sets formed within a table by specified rules. Partitions can be made according to any standard, such as by date. To reduce the amount of data that needs to be handled, each partition is stored separately. When querying, ByteHouse strives to use the smallest subset of these partitions. The table is created by specifying through the `PARTITION BY expr` clause. A partition key can be any expression in the columns of a table. For instance, to specify monthly partitioning, use the expression `toYYYYMM(date)`; or partition by tuples such as `(toMonday(date), EventType)` etc.

It is important to note that the range of values derived from the partition expression in the table should not be too large (it is recommended not to exceed ten thousand), as too many partitions can occupy significant memory and lead to considerable IO and computational overhead.

A well\-designed partition key can greatly reduce the amount of data that needs to be scanned during queries. Commonly, columns that are frequently used in queries with a value range not exceeding ten thousand, such as dates, are ideal for partition key design.

**Example 1: A partition key defined by columnExpr**

```SQL
CREATE TABLE test.partitionByClause
(
VisitDate Date,
Hour UInt8,
ClientID UUID
)
ENGINE = CnchMergeTree
PARTITION BY VisitDate
ORDER BY Hour;
```


**Example 2: A partition key defined within a tuple in columnExpr**

```SQL
CREATE TABLE test.partitionByClause
(
VisitDate Date,
Hour UInt8,
ClientID UUID
)
ENGINE = CnchMergeTree
PARTITION BY (VisitDate,Hour)
ORDER BY Hour;
```


<span id="0ada580c"></span>
##### Designing sorting keys (ORDER BY)

It can be a tuple of columns or any expression. For example: `ORDER BY (OrderID, Date)`.

If sorting is not needed, you can use `ORDER BY tuple()`, and the DataPart will store data in the order it is inserted.

**Grammar**

```SQL
[columnExpr] [ASCENDING|ASC|DESCENDING|DESC] [NULLS [FIRST|LAST] [COLLATE STRING_LITERAL]
```



* `[ASCENDING|ASC|DESCENDING|DESC]`: Determines the sorting direction. If no direction is specified, `ASC` is the default.

* `[NULLS [FIRST|LAST]`: Determines the sorting order of `NaN` and `NULL`.

   \* By default or when using the `NULLS LAST` modifier: values first, then `NaN`, and finally `NULL`.

   \* When using the `NULLS FIRST` modifier: `NULL` first, then `NaN`, and finally other values.

* `[COLLATE STRING_LITERAL]`: Allows specifying a collation rule for string value sorting.

   \* Sorting rules support LowCardinality, Nullable, Array, and Tuple.

   \* When using `COLLATE`, the sorting is always case\-insensitive.

   \* It is only recommended to use `COLLATE` for final sorting of a small number of rows, as sorting with `COLLATE` is less efficient than normal byte\-based sorting.


**Example 1: Sort by multiple orderExprs**

```SQL
CREATE TABLE IF NOT EXISTS test.orderByClause (id UInt32, val UInt32) ENGINE=CnchMergeTree() ORDER BY id;
INSERT INTO TABLE test.orderByClause VALUES (1,5),(1,15),(2,5),(2,15);
SELECT * FROM test.orderByClause ORDER BY id ASC, val DESC;
```


**Example 2: Sort by NULL FIRST**

```SQL
CREATE TABLE IF NOT EXISTS test.orderByClause (id UInt32, val Nullable(UInt32)) ENGINE=CnchMergeTree() ORDER BY id;
INSERT INTO test.orderByClause VALUES (1,2),(2,NULL),(3,2),(3,3),(3,NULL);
SELECT * FROM test.orderByClause ORDER BY val DESC NULLS FIRST;
```


**Example 3: Sort by COLLATE**

```SQL
CREATE TABLE IF NOT EXISTS test.orderByClause (x UInt32, s Nullable(String)) ENGINE=CnchMergeTree ORDER BY x;
INSERT INTO test.orderByClause VALUES (1,'bca'),(2,NULL),(3,'ABC'),(4,'123a'),(5,'abc'),(6,NULL),(7,'BCA');
SELECT * FROM test.orderByClause ORDER BY s ASC COLLATE 'ru';
```


<span id="b671e60b"></span>
##### Design the PRIMARY KEY

In default situations, there is no need to explicitly specify it; ByteHouse will use the sort key as the primary key. When there are special scenarios where the primary key and the sort key are not consistent, the primary key must be the leftmost prefix of the sort key. If the sort key is (OrderID, Date), the primary key must be OrderID and not Date.

ByteHouse will create a sparse index on the primary key by granule, (in contrast, a so\-called dense index is built with index information for each row).

If the search conditions can match the leftmost prefix of the primary key index, the primary key index can quickly filter out potentially needed data granules, which is usually much more efficient than scanning the entire DataPart.

Additionally, it is important to note that the PRIMARY KEY does not guarantee uniqueness, so it is possible to insert data rows with duplicate primary keys.

Partitioning (PARTITION BY) and primary keys (PRIMARY KEY) are two different ways to accelerate data queries. When defining, try to use different columns for each to cover more query scenarios. For example, never repeatedly include the first column of an order by in a partition by. Here are some considerations for choosing a primary key:


* Whether it is a column commonly used in query conditions.

* Not the first column of a non\-partitioned key.

* The selectivity of the column, for instance, columns with few optional values such as gender or yes/no, are not recommended for primary keys.

* If the current primary key is (a, b) and most of the time, the data range corresponding to (a, b) is large (covering multiple Granules), consider adding a new column frequently used in queries to the primary key for filtering more data.

* Overly long primary keys can negatively impact insertion performance and memory consumption, but have no effect on query performance.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.sampleByClause 
(
id UInt32
) 
ENGINE=CnchMergeTree 
ORDER BY id 
SAMPLE BY id;
```


<span id="8370fdcb"></span>
##### UNIQUE KEY

A PRIMARY KEY does not ensure data deduplication. A unique key index must be set during table creation for deduplication requirements. After setting the unique key, ByteHouse provides upsert update semantics that allow for efficient row data updates based on the unique key, or you can use the virtual column `*delete_flag*=1` to delete specific keys during an upsert. Queries automatically return the latest values for each unique key. For details, refer to [Upsert usage examples](https://docs.byteplus.com/en/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables).

Unique keys can be tuples of columns or any expression, such as `UNIQUE KEY (product_id, sipHash64(city))`.

Querying with the unique key utilizes its index to filter data, thereby speeding up searches. Therefore, primary keys can cover more query conditions if set with different columns than the unique keys. However, if partial column updates are needed, the unique key should be the leading prefix in the sort key.

**Example 1: Single Field Unique Key**

```SQL
CREATE TABLE test.uniqueKeyClause
(
`event_date` Date,
`order_id` UInt64,
`state` UInt32,
`amount` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY event_date
ORDER BY state
UNIQUE KEY order_id;

-- rows with the same key will replace previous rows
INSERT INTO test.uniqueKeyClause VALUES
('2021-03-01', 1001, 1, 100),
('2021-03-01', 1002, 1, 200),
('2021-03-01', 1001, 2, 100),
('2021-03-02', 1001, 1, 400);

SELECT * FROM test.uniqueKeyClause ORDER BY event_date, order_id;
┌─event_date─┬─order_id─┬─state─┬─amount─┐
│ 2021-03-01 │ 1001     │ 2     │100     │
│ 2021-03-01 │ 1002     │ 1     │200     │
│ 2021-03-02 │ 1001     │ 1     │400     │
└────────────┴──────────┴───────┴────────┘

INSERT INTO test.uniqueKeyClause VALUES
('2021-03-01', 1002, 2, 200),
('2021-03-02', 1001, 2, 400),
('2021-03-02', 1002, 1, 300);

SELECT * FROM test.uniqueKeyClause ORDER BY event_date, order_id;
┌─event_date─┬─order_id─┬─state─┬─amount─┐
│ 2021-03-01 │ 1001     │ 2     │ 100    │
│ 2021-03-01 │ 1002     │ 2     │ 200    │
│ 2021-03-02 │ 1001     │ 2     │ 400    │
│ 2021-03-02 │ 1002     │ 1     │ 300    │
└────────────┴──────────┴───────┴────────┘
```


**Example 2: Multi\-field unique key**

```SQL
CREATE TABLE test.uniqueKeyClause
(
`event_date` Date,
`region` UInt64,
`state` String,
`amount` UInt64
)
ENGINE = CnchMergeTree
PARTITION BY event_date
ORDER BY state
UNIQUE KEY (region, state);
```


<span id="ea232149"></span>
##### CONSTRAINT

ByteHouse supports CONSTRAINT in terms of syntax, but with the exception of NOT NULL, **these constraints are not enforced**.


* **Unique Constraint (UNIQUE)** : If your business logic strongly depends on the uniqueness of columns, use UNIQUE KEY instead of UNIQUE CONSTRAINT.

* **Foreign Key Constraint (FOREIGN KEY)** : Foreign key constraints are only used for query optimization and do not perform data integrity verification.


<span id="8005d332"></span>
##### Bucketing (Cluster By)

Bucketing is often used in the following scenarios:


1. **Common scenarios:**  Uneven data distribution

   \* **Definition and Principles**: When partitioning fails to achieve uniform data distribution, bucketing fields can be utilized. Bucketing fields ensure that a column of data is evenly distributed across each node in the cluster. This maximizes cluster performance for queries. The rational configuration of partitioning fields also helps address data skew issues, ensuring more uniform data distribution.

   \* **Field restrictions**: Does not support Nullable.

   \* **Configuration recommendations**: Choose fields that frequently appear as the basis for grouping.

   \* Once a table is created, the field is not allowed to change its column type.

2. **Specific scenario**: Slow duplicate data deletion

   \* **Definition and Principles**: When a Unique Key is set and an excessive amount of data exists in a single partition (e.g., over 100 million rows), data ingestion speeds can be impacted. This is because locking is necessary to delete duplicate data. In this case, you can partition your data into buckets to enhance data ingestion speed.

   \* **Field Constraints**: Does not support Nullable.

   \* **Configuration Recommendation**: The Bucket Key should be the same as the Unique Key. (Each bucket should have fewer than 10 million rows)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying existing tables to add buckets will only affect new partitions but will not impact existing partitions.</div>


**Bucketing use cases**

Suppose a ByteHouse subscription user has enabled six compute nodes. Due to the large volume of data in a single partition, exceeding 200 million records, the application frequently performs aggregation and join operations based on fields `c1` and `c2`. Therefore, it has been decided to optimize using bucket tables. The design options for the bucket table are as follows:


* Bucket key (CLUSTER Key) selection: Choose columns `c1` and `c2` as bucket keys.

* Number of buckets: Twice the number of nodes: 12.


```SQL
-- Create table with bucketing
create or replace table table_01 (c1 timestamp, c2 string, c3 number) cluster by (to_date(c1), c2) INTO 12 BUCKETS;

-- Add bucket to existing data
ALTER TABLE t CLUSTER BY (column, expression, ...) INTO 64 BUCKETS

-- Add bucket to cluster by multiple columns
ALTER TABLE t CLUSTER BY sipHash(a,b,c) INTO 64 BUCKETS

-- Add or change the cluster properties
ALTER TABLE t MODIFY CLUSTER BY (column, expression, ...) INTO 64 BUCKETS
```


<span id="1c4450a7"></span>
##### Sampling

An expression used for sampling, which is an optional configuration.

If a sampling expression is to be used, it must be included in the primary key. For example: `SAMPLE BY intHash32(UserID) ORDER BY (CounterID, EventDate, intHash32(UserID))`.

<span id="e0b7923b"></span>
##### Column and Table TTL

List the rules that specify the duration of row storage and define the movement logic of data segments on the disk and volumes, as an optional item. The expression must include at least one column of type `Date` or `DateTime`, such as: `TTL date + INTERVAL 1 DAY`.

```SQL
CREATE TABLE test.ttlClause
(
VisitDate Date,
Hour UInt8,
ClientID UUID
)
ENGINE = CnchMergeTree
ORDER BY Hour
PARTITION BY VisitDate
TTL VisitDate + INTERVAL 1 DAY；
```


If you need to implement TTL based on a string\-type field, you must first convert the field to a `Date` or `DateTime` type using the `toDate` function when creating the table, and then set the TTL based on this converted date\-time column. For the usage of the `toDate` function, refer to [toDate](https://docs.byteplus.com/docs/bytehouse/docs-type-conversion#bc2c1c26).

```SQL
CREATE TABLE test.ttlClause ( 
 start_date STRING, -- Date field of string type
 Hour UInt8,
 ClientID UUID
) ENGINE = CnchMergeTree 
ORDER BY Hour 
TTL toDate(start_date) + INTERVAL 1 DAY; -- Set TTL after converting the string to Date type
```


<span id="172cb312"></span>
##### Compression

The compression_codec field can be used to configure the codec, which is optional with a default value of LZ4.

ByteHouse supports both general\-purpose and specific encodings, with general\-purpose codecs resembling the default codecs (LZ4, ZTSD) and their modified versions. Specific codecs are designed to make compression more effective by leveraging the specific characteristics of the data.

**General encoding**


* None: No compression.

* LZ4: Default value, lossless high\-speed compression algorithm.

* LZ4HC[(level)]: LZ4HC algorithm with a high compression rate and configurable level. The default level is 9, supporting values from [1 ~ 12], with recommended choices between [4 ~ 9].

* ZSTD (level): A ZSTD compression algorithm with configurable levels. The default value of level is 1, supporting a range of [1 ~ 22].


**Specific encoding algorithm**


* Delta (delta_bytes): An incremental encoding method that keeps the first value and stores the differences between every two subsequent values. The default value is sizeof(type), with optional values of 1, 2, 4, or 8. If set to other values, it is treated as 1.


**Multiple codecs**


* Use the multiple codecs mentioned above. Compression will be performed in the order declared by the codecs, while decompression will be executed in the reverse order.


For example, refer to:

```SQL
CREATE TABLE codec_example
(date Date CODEC(Delta, ZSTD),
ts DateTime CODEC(LZ4HC),
float_value Float32 CODEC(NONE),
double_value Float64 CODEC(LZ4HC(9))
)
ENGINE = CnchMergeTree
PARTITION BY tuple()
ORDER BY date
```


<span id="3bda105b"></span>
###### Table engine

The table engine, or table type, determines:


* How data is organized and stored

* How indexing is done and the types of indexes

* Which queries are supported and how they are supported

* Some other specific features and configurations


The most commonly used table engine in ByteHouse cloud data warehouse is CnchMergeTree; other special types of table engines include Hive external tables, Kafka tables, etc. This article focuses on sharing the principles of the CnchMergeTree table engine.

<span id="40dbc0dc"></span>
##### CNCHMergeTree table engine

CNCHMergeTree is the most commonly used table engine. Its core idea is similar to LSM\-Tree, partitioning data by the partition key and storing it in order by the sort key. It has the following main characteristics:


* **Logical Partition**

   If a partition key is specified, data is divided into different logical data sets (logical partitions, Partition).

   Each logical partition may have zero to multiple data fragments (DataPart). If the query conditions can prune partitions, it often speeds up the query. If no partition key is specified, all data resides in a single logical partition.

* **Data Fragment**

   The data in each data fragment is sorted by the sort key. Each data fragment also has a min/max index to accelerate partition selection.

* **Data Granule**

   Each data fragment is logically split into granules, with the default Granule being 8192 rows (determined by the table's index_granularity setting). A granule is the smallest indivisible dataset when querying data in ByteHouse. The first line of each granule is marked by the primary key value of that line, and ByteHouse creates an index file for each data slice to store these markers. For each column, whether it is part of the primary key or not, ByteHouse stores similar markers. These markers allow you to directly find data in the column files. As the index target of ByteHouse's sparse index, Granule also serves as the unit for data scanning in memory.

* **Background Merge**

   Background tasks periodically merge DataParts in the same partition, maintaining them in sorted order by the sort key. The background merge reduces the number of Parts, enabling more efficient storage and enhancing query performance.


<span id="69a4dc11"></span>
#### MySQL compatibility

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">MySQL compatible syntax, recommended for use in relevant dialects.</div>


ByteHouse CDW 2.1 is compatible with most of MySQL's DDL and allows direct execution of MySQL table creation statements in ByteHouse. Please refer to the following examples

<span id="4ba10595"></span>
##### MySQL

```SQL
CREATE TABLE `table1` (
`uid` bigint NOT NULL AUTO_INCREMENT,
`phone` varchar(255) DEFAULT NULL,
`no1` bigint DEFAULT NULL,
`appleid` varchar(255) DEFAULT NULL,
PRIMARY KEY (`uid`) USING BTREE,
UNIQUE KEY `no1` (`no1`) USING BTREE,
KEY `idx_apple_id` (`appleid`) USING BTREE,
KEY `phone` (`phone`) USING BTREE
) ENGINE=InnoDB AUTO_INCREMENT=60937910 DEFAULT CHARSET=utf8mb3;
```


<span id="936f1a4f"></span>
##### ByteHouse

```SQL
CREATE TABLE table1 (
`uid` Int64 NOT NULL,
`phone` String NULL DEFAULT NULL,
`no1` Int64 NULL DEFAULT NULL,
`appleid` String NULL DEFAULT NULL
)
ENGINE = CnchMergeTree
ORDER BY tuple(uid)
UNIQUE KEY tuple(uid)
SETTINGS partition_level_unique_keys = 0, storage_policy = 'cnch_default_hdfs', allow_nullable_key = 1, storage_dialect_type = 'MYSQL', index_granularity = 8192
```


<span id="b131328f"></span>
##### DDL Conversion Logic

Observe the following conversion logic


|Break down contrast items |MySQL |ByteHouse |Description |
|---|---|---|---|
|Column Attributes |Data Type |Compatible |For details on data compatibility of various MySQL types, refer to [Basic data types](https://docs.byteplus.com/docs/bytehouse/docs-data-types). |
||AUTO_INCREMENT |Compatible |ByteHouse currently supports the capability for self\-increasing IDs (`generateSnowflakeID`). A comparison of their use during table creation is as follows:<br><br><br>* ByteHouse<br><br>   ```SQL```<br>```   set dialect_type='CLICKHOUSE';```<br>```   CREATE TABLE t1(id Int64 DEFAULT generateSnowflakeID(), val1 String)```<br>```   Engine=CnchMergeTree() Order by id;```<br>```   ```<br>   <br><br>* MySQL<br><br>   ```SQL```<br>```   set dialect_type='MYSQL';```<br>```   create table t1(id Int64 auto_increment primary key, val1 String);```<br>```   ```<br>   <br><br><br>For more information on using the self\-increasing function of ByteHouse, refer to [Auto incremental function](https://docs.byteplus.com/docs/bytehouse/auto-incremental-function). |
||NULL |Compatible |None |
||DEFAULT |Compatible |None |
||Other definitions |Compatible |ByteHouse is compatible with most commonly used field definitions |
|Table attributes |Primary key: PRIMARY KEY |Unique key: UNIQUE KEY |**In the semantics of MySQL, 'primary key' corresponds to 'unique key' in ByteHouse, not 'primary key'.**  |
|| |Sorting key: ORDER BY |Default sorting by MySQL's primary key |
||UNIQUE KEY `no1` (`no1`) USING BTREE |Ignore |ByteHouse syntactically supports Constraints, but functionally ignores them |
||Other definitions:<br><br>ENGINE=InnoDB AUTO_INCREMENT=60937910 DEFAULT CHARSET=utf8mb3; |Ignore |Ignore |
|Settings |None |Settings |In the MySQL dialect, ByteHouse will add the following settings by default when creating tables<br><br><br>1. partition_level_unique_keys = 0 \-\> Terminate partition deduplication, ensuring deduplication across the entire table<br><br>2. storage_policy = 'cnch_default_hdfs', index_granularity = 8192 \-\> Default settings<br><br>3. allow_nullable_key = 1 \-\> Allows nullable key to be used for unique key<br><br>4. storage_dialect_type = 'MYSQL' \-\> Storage dialect type |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ByteHouse also offers a certain level of compatibility with other database syntaxes. If you are interested, please contact us.</div>


<span id="01caa26d"></span>
### CREATE TABLE AS SELECT（CTAS）

Create a table with a structure similar to the results of a SELECT query, using the specified engine, and populate it with data from the SELECT.

<span id="ada7c9fa"></span>
#### Syntax

```SQL
CREATE TABLE [IF NOT EXISTS] [db.]table_name[(name1 [type1], name2 [type2], ...)] ENGINE = CnchMergeTree ORDER BY expr [PARTITION BY expr] AS SELECT ...
```


If the table already exists and the IF NOT EXISTS clause is specified, the query will do nothing. There can be additional clauses after the ENGINE clause in the query.

<span id="4388849f"></span>
#### **Example**

```SQL
CREATETABLE DB2.unique_user_events (
user_id UInt32,
event_time DateTime,
event_type String,
event_data String
) ENGINE = CnchMergeTree()
ORDER BY user_id 
PRIMARY KEY user_id 
UNIQUE KEY event_time;

INSERT into DB2.unique_user_events(user_id,event_time,event_type,event_data) values(10112,'2024-08-28 05:11:58','ERROR','this is a bug');
INSERT into DB2.unique_user_events(user_id,event_time,event_type) values(10112,'2024-07-28 05:11:58','ERROR');
INSERT into DB2.unique_user_events(user_id,event_time,event_data) values(10112,'2024-07-28 05:11:58','this is a bug');

CREATE TABLE IF NOT EXISTS DB2.table_name2(user_id UInt32,event_time DateTime,event_data String) 
ENGINE = CnchMergeTree 
ORDER BY user_id 
AS 
select user_id,event_time,event_data from DB2.unique_user_events limit 100;

select * from DB2.table_name2;
```


<span id="dd83b29d"></span>
### Create view (`CREATE VIEW`)

A normal view does not store any actual data; it is only used to define a preset query. When reading view data, the preset query is automatically used as a subquery and embedded into the FROM clause of the final SQL statement for execution.

In versions of the ByteHouse Cloud Data Warehouse Engine prior to v2.3, the execution permission for a normal view depends on both the view's own read permission and the underlying table's read permission. However, in some scenarios, users want to manage only the view's permissions without needing to consider the underlying table's permissions. Starting from v2.3, ByteHouse Cloud Data Warehouse introduces the view SQL Security feature, which adds DEFINER and INVOKER to views to control their execution behavior. This feature is suitable for scenarios where restricted data access privileges need to be provided to different users.

Explanation of the differences between `Definer (DEFINER)`, `Invoker (INVOKER)`, and not using the SQL Security feature is as follows:


|Roles |Description |
|---|---|
|`Definer (DEFINER)` |The definer is the user specified when creating the view. When selecting a user, ensure that the user has all privileges for the view as well as query privileges for the base table.<br><br>When using this mode to create a view, users who subsequently query the view only need query privilege on the view to query it successfully; privilege on the underlying table is not required. |
|`Invoker (INVOKER)` |The invoker is the user initiating the view query and must have query privileges for both the view and the base table in order to run the view query. |
|SQL Security not set |By default, views use the `invoker (INVOKER)` role, which means that the user initiating the view query must have query privileges on both the view and the underlying table in order to run the view query. |


View SQL Security serves only as a proxy for underlying table privileges during view query execution by the ByteHouse engine; the actual privileges obtained by the user querying the view are not affected. For existing views, the ByteHouse engine uses the INVOKER role by default. You can refer to the "Modify view SQL Security" subsection below to adjust the view's SQL Security.

This section introduces how to create and manage views, with a focus on how to use the SQL Security feature for fine\-grained access control.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, only engine versions v2.3 and above support the view SQL Security feature.</div>


<span id="85451fb4"></span>
#### Syntax

<span id="f6baf42f"></span>
##### Create a view

```SQL
CREATE [OR REPLACE] VIEW [IF NOT EXISTS] [db.]view_name
[DEFINER = { `user` | CURRENT_USER }] [SQL SECURITY { DEFINER | INVOKER }]
AS SELECT ...
```


**Parameter description**


|Parameter |Required |Description |
|---|---|---|
|OR REPLACE |No |Depending on whether a view with the same name currently exists in ByteHouse, select the corresponding rule to create the view. The specific rules are as follows:<br><br><br>* If there is no view with the same name, ByteHouse will create a new view.<br><br>* If a view with a duplicate name exists, ByteHouse will first delete the existing view with the duplicate name and then recreate it. |
|IF NOT EXISTS |No |If the newly created view `view_name` already exists, ByteHouse will not create a new database and:<br><br><br>* If this clause is specified, no exception is thrown.<br><br>* If the clause is not specified, an exception is thrown. |
|[db.]view_name |Yes |Define the database where the view is located, and customize the view name. Database name is an optional parameter. If you have already executed `USE database_name`, there is no need to fill in the database name here. |
|DEFINER |No |Save the view definer's information for privilege checking when running SELECT on the base table. This parameter must be used together with the `SQL SECURITY DEFINER` parameter to explicitly designate a user as the definer. The user specified by DEFINER must have privileges for all underlying tables. For the operation of granting data privileges to users, see [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission).<br><br>The default value is the user who initiates the current query, that is, CURRENT_USER.<br><br>This parameter value can be set to a user or CURRENT_USER:<br><br><br>* user: The parameter value is constructed by concatenating the BytePlus account ID and user ID, with the format `{byteplus_ID}.{bytehouse_ID}`. It must be enclosed in backticks. Example:<br><br>   ```SQL```<br>```   DEFINER = `21xxxxxx68.45xxxx79````<br>```   ```<br>   <br><br>   The methods for obtaining BytePlus account ID and user ID are as follows:<br><br>   * BytePlus account ID: In the ByteHouse Cloud Data Warehouse console, click the user profile picture in the upper right corner to view and copy the account ID.<br><br>   * User ID: In the ByteHouse ByteHouse Cloud Data Warehouse console, click the **Access control** at the top; click **User**; in the **User list**, click **User ID** to copy the ID.<br><br>* CURRENT_USER: Represents the user executing the current statement. |
|SQL SECURITY |No |Set the privilege mode for running base table queries. The parameter value can be set to `DEFINER` or `INVOKER`, with the default value being `INVOKER`.<br><br><br>* `DEFINER`: Indicates that view\-related statements are executed using the definer's identity. When using this privilege mode, you must configure both the `DEFINER` parameter and the `SQL SECURITY DEFINER` parameter.<br><br>   In this privilege mode, when executing a SELECT statement to query view data, the system only verifies whether the user performing the query has the query privilege on the view; privileges on the underlying table are not required.<br><br>* `INVOKER`: Indicates that view\-related statements are executed using the caller's identity. When using this privilege mode, the `DEFINER` clause can be omitted, and the engine sets the `DEFINER` clause to `CURRENT_USER` by default.<br><br>   In this privilege mode, when a SELECT statement is subsequently executed to query view data, the privileges of the user who actually initiates the query are used. The system will verify whether the user has the following privileges:<br><br>   * The read privilege of the view;<br><br>   * The read privilege of the base table referenced by the view.<br><br>      If the user does not have view or base table privileges, the system will report an error. |
|AS SELECT |Yes |Use the SELECT statement to specify the data source of the view. |


<span id="5285347d"></span>
##### Query view

The grammar is the same as that of a normal query.

```SQL
SELECT a, b, c FROM view_name
```


<span id="e3be55d8"></span>
##### Modify view SQL security

You can use the `ALTER` statement to adjust a view's usage privileges.


* When adjusting the view SQL Security from `INVOKER` to `DEFINER`, it is recommended to adjust both `DEFINER` and `SQL SECURITY` at the same time to ensure accurate configuration. If only one is adjusted, ByteHouse will automatically reset the other to its default value.

* To change the view SQL Security from `DEFINER` to `INVOKER`, you only need to set `SQL SECURITY INVOKER`.


```SQL
# Option 1
ALTER TABLE [db.]view_name 
MODIFY SQL SECURITY  { DEFINER | INVOKER }
[DEFINER = { user | CURRENT_USER }]

# Option 2
ALTER TABLE [db.]view_name 
MODIFY [DEFINER = {user | CURRENT_USER }]
SQL SECURITY { DEFINER | INVOKER }
```


<span id="d9cbe29f"></span>
##### Grant view\-related privileges to users

You can use the `GRANT` statement to grant view\-related privileges to users.


* **Privilege to create views**

   Creating a view requires the `CREATE VIEW` privilege. To use the SQL Security feature when creating a view, if the user performing the `CREATE VIEW` operation is different from the specified `DEFINER`, grant the `SET DEFINER` privilege to that user.

   Example:

   ```SQL
   GRANT CREATE VIEW ON [db.]view_name TO user;
   
   GRANT SET DEFINER ON another_user TO user;
   ```
   

   **Parameter description**

   
   |Parameter |Required |Description |
   |---|---|---|
   |CREATE VIEW |Yes |The privilege to create views. |
   |SET DEFINER ON |Yes |Grant the user privilege to specify `DEFINER = user` when creating a view in the schema. Only users who have obtained this privilege can specify `DEFINER` information when creating a view, and the `DEFINER` information can only be set to a username that has obtained the `SET DEFINER` privilege.<br><br><br>* If the user executing the create view (`CREATE VIEW`) operation is the same as the username specified in the `DEFINER` parameter of the create view statement, explicit granting of the `SET DEFINER` privilege is not required.<br><br>* When creating a view, if the `DEFINER` needs to be specified as another user, you must explicitly grant the `SET DEFINER` privilege to that user. If this privilege is not granted, the user will not have privileges to use `DEFINER = user` and `SQL SECURITY` when creating a view.<br><br>* Ensure that the username authorized in `GRANT SET DEFINER` matches the username specified in `DEFINER = xxx` when creating the view; otherwise, users will not be able to obtain the corresponding DEFINER usage privilege. |
   |TO user |Yes |Specify the user to be granted privileges. This parameter value can be set to user or CURRENT_USER:<br><br><br>* user: This parameter value is formed by concatenating the BytePlus account ID and user ID. The format is `{byteplus_ID}.{bytehouse_ID}`, and it must be enclosed in backticks (````). Example: `21xxxxxx68.45xxxx79`. You can obtain BytePlus account ID and user ID following the instructions below:<br><br>   * BytePlus account ID: In the ByteHouse Cloud Data Warehouse console, click the user avatar in the upper right corner to view and copy the account ID.<br><br>   * User ID: In the ByteHouse Cloud Data Warehouse Console, click the top menu **Access control**. Then, click **User**. In the **User list**, click **User ID** to copy the ID.<br><br>* CURRENT_USER: Indicates the user who executes the current statement. |
   

* **Privileges to use view**

   Only grant users the `SELECT` privilege on the view.

   ```SQL
   GRANT SELECT ON [db.]view_name TO user;
   ```
   

* **Privileges to delete and modify views**

   To delete a view, you only need to grant the user the `DROP VIEW` privilege.

   ```SQL
   GRANT DROP VIEW ON [db.]view_name TO user;
   ```
   

   Modifying a view requires granting the user the `ALTER VIEW MODIFY SQL SECURITY` and `SET DEFINER` privileges. For granting the `SET DEFINER` privilege, refer to the subsection above titled "Privileges for creating views."

   ```SQL
   GRANT ALTER VIEW MODIFY SQL SECURITY ON [db.]view_name TO user;
   
   -- You can also grant the user the privilege collection of ALTER VIEW
   GRANT ALTER VIEW ON [db.]view_name TO user;
   ```
   


<span id="1cc6f8e7"></span>
#### Example

To facilitate the demonstration of different user privileges, the following examples use three users—Admin, ViewAdmin, and ViewUser—for illustration. In actual use, replace these placeholders with the actual usernames (which are formed by concatenating the BytePlus ID and ByteHouse ID). For information on how to obtain these usernames, refer to the parameter description in the **create view** subsection above.


* Administrator: System Administrator (AccountAdmin), has the highest level of access.

* ViewAdmin: View administrator.

* ViewUser: View user.


**Steps**:


1. Create test users and base tables

   ```SQL
   -- Use the admin account to create the database and table
   -- Create the demo database
   CREATE DATABASE IF NOT EXISTS test_db;
   
   -- Create the underlying table of the view
   CREATE TABLE test_db.employee (
       id INT,
       name STRING,
       salary INT
   ) ENGINE = MergeTree() ORDER BY id;
   
   -- Insert data
   INSERT INTO test_db.employee VALUES (1, 'Alice', 5000), (2, 'Bob', 6000);
   
   -- Grant the underlying table access permission and view management privilege to the ViewAdmin user
   GRANT SELECT ON test_db.employee TO ViewAdmin;
   GRANT CREATE VIEW ON test_db.* TO ViewAdmin;
   -- Optional. In this example, if the ViewAdmin user is used to create the view and the DEFINER is the ViewAdmin user, there is no need to explicitly specify the SET DEFINER permission.
   GRANT SET DEFINER ON ViewAdmin TO ViewAdmin;
   ```
   

2. Create views for different permission modes.

   * Create an SQL SECURITY DEFINER view

      ```SQL
      -- Switch to the ViewAdmin account to execute the command below
      CREATE VIEW test_db.employee_view_definer
      DEFINER = ViewAdmin
      SQL SECURITY DEFINER
      AS SELECT id, name FROM test_db.employee; 
      
      -- Grant the view query privilege to the ViewUser user (no need to grant underlying underlying table permissions).
      GRANT SELECT ON test_db.employee_view_definer TO ViewUser;
      ```
      

      Verification results:

      ```SQL
      -- Use the ViewUser account to query the view and this view can be queried successfully
      SELECT * FROM test_db.employee_view_definer;
      -- Result：
      -- 1        Alice
      -- 2        Bob
      
      -- Query the underlying table directly using the ViewUser account; the query fails due to insufficient privileges
      SELECT * FROM test_db.employee;
      -- Error message: Access denied
      ```
      

   * Create an SQL SECURITY INVOKER view

      ```SQL
      -- Switch to the ViewUser account to execute the command below
      CREATE VIEW test_db.employee_view_invoker
      SQL SECURITY INVOKER
      AS SELECT id, salary FROM test_db.employee;
      
      -- Grant only view privileges to the ViewUser account (underlying table privilege is not granted)
      GRANT SELECT ON test_db.employee_view_invoker TO ViewUser;
      ```
      

      Verification result:

      ```SQL
      -- Query the view using the ViewUser account; the query fails due to lack of underlying table privileges
      SELECT * FROM test_db.employee_view_invoker;
      
      -- After the administrator account supplements the underlying table privileges for the ViewUser account, query again, and the query succeeds
      GRANT SELECT ON test_db.employee TO ViewUser;
      SELECT * FROM test_db.employee_view_invoker;
      -- Result：
      -- 1        5000
      -- 2        6000
      ```
      

   * Create views that do not use SQL Security

      ```SQL
      -- Switch to the ViewAdmin account to execute; the view uses SQL SECURITY INVOKER by default.
      CREATE VIEW test_db.employee_view_normal
      AS SELECT id, name FROM test_db.employee; 
      
      -- Grant only view query privileges to the ViewUser account
      GRANT SELECT ON test_db.employee_view_normal TO ViewUser;
      ```
      

      Verification results:

      ```SQL
      -- Query the view using the ViewUser account; the query fails due to lack of underlying table privileges
      SELECT * FROM test_db.employee_view_normal;
      -- Error message: Access denied
      
      -- Query the underlying table directly using the ViewUser account; the query fails due to lack of underlying table privileges
      SELECT * FROM test_db.employee;
      -- Error message: Access denied
      ```
      

      At this point, grant ViewUser the query privilege on the base table; then ViewUser can query data from the view.

      ```SQL
      -- Use the administrator account to grants underlying table query privileges to the ViewUser account
      GRANT SELECT ON test_db.employee TO ViewUser;
      
      -- Use the ViewUser account to execute the view query again, and the query succeeds
      SELECT * FROM test_db.employee_view_normal;
      -- Result：
      -- 1        Alice
      -- 2        Bob
      ```
      

3. Modify view allow mode.

   ```SQL
   -- Use the administrator account to grant view modification privileges to the ViewAdmin account
   GRANT ALTER VIEW MODIFY SQL SECURITY ON test_db.employee_view_definer TO ViewAdmin;
   
   -- Use the ViewAdmin account to change the DEFINER view to INVOKER mode
   ALTER TABLE test_db.employee_view_definer
   MODIFY SQL SECURITY INVOKER;
   
   -- Query the view using the ViewUser account
   SELECT * FROM test_db.employee_view_definer;
   -- If the ViewUser is not granted underlying table privileges, an error will be reported
   ```
   

4. Delete view.

   ```SQL
   -- Use the administrator account to grant deletion privileges to the ViewAdmin account
   GRANT DROP VIEW ON test_db.employee_view_definer TO ViewAdmin;
   
   -- Use the ViewAdmin account to delete the view
   DROP VIEW test_db.employee_view_definer;
   ```
   


<span id="c62ac1de"></span>
#### Common errors and solutions

The following error examples take ViewCreator and ViewUser as examples to demonstrate common privilege errors.

<span id="2e6f4b2d"></span>
##### Missing SET DEFINER privilege

**Error message**:

```SQL
ViewCreator: Not enough privileges. To execute this query it's necessary to have grant SET DEFINER ON ViewAdmin
```


**Reason**:

When querying the user's privileges, it is found that the user lacks the SET DEFINER privilege.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3914acf120654f90925093ec2f81d42e~tplv-goo7wpa0wc-image.image) </span>

**Solution**:

Grant the `SET DEFINER` privilege to irregular users, and the specified DEFINER username must match the DEFINER specified in the query.

Example:

```SQL
GRANT SET DEFINER ON ViewCreator TO ViewCreator;
```


<span id="bf771f6a"></span>
##### Missing ALTER VIEW MODIFY SQL SECURITY privilege

**Error message**:

```SQL
 ViewCreator: Not enough privileges. To execute this query it's necessary to have grant ALTER VIEW MODIFY SQL SECURITY ON testdb.test_view3
```


**Reason**:

Upon checking the user's privileges, it was found that the user does not have privilege to modify the view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5f1b5ff816a46c0b74480e7f256bec6~tplv-goo7wpa0wc-image.image) </span>

**Solution**:

Grant the `ALTER VIEW` privilege to the user. Example:

```SQL
GRANT ALTER VIEW ON db_name.view_name TO ViewCreator;
```


<span id="7846ea8d"></span>
##### Missing underlying table privilege when running a view query

**Error message**:

```SQL
ViewUser: Not enough privileges. To execute this query it's necessary to have grant SELECT(tag, value) ON testdb.test_table
```


**Reason**:

Querying the view schema reveals that the execution privilege is `INVOKER`, and ViewUser does not have privileges on the base table.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70f44067bbfc4e60be1c947b1e8d39b4~tplv-goo7wpa0wc-image.image) </span>

**Solutions**:


* Option 1: Modify the view and change the parameter value for execution privilege to DEFINER, while ensuring that the user specified by DEFINER has privilege on the underlying table.

   ```SQL
   ALTER TABLE db_name.view_name
   MODIFY SQL SECURITY DEFINER
   DEFINER = `user`;
   ```
   

* Option 2: Grant base table privilege to the query user.

   ```SQL
   GRANT SELECT ON db_name.table_name TO ViewUser;
   ```
   


<span id="78519365"></span>
#### Materialized View

For details, see the [Materialized View](https://docs.byteplus.com/docs/bytehouse/create-statement#7b0debdb) section.

<span id="08e1e6c3"></span>
### Create Dictionary (`CREATE DICTIONARY`)

ByteHouse Data Dictionary is divided into **builtin dictionaries** and **external extension dictionaries**:


* The builtin dictionary contains preset dictionary content for ClickHouse.

* External extension dictionaries provide a variety of flexible custom data source definitions, currently supporting MySQL, PostgreSQL, and ClickHouse. Dictionary data is updated regularly and supports dynamic loading.


This article focuses on how to operate the external extension dictionary of ByteHouse.

<span id="8b4ebfc5"></span>
#### Create Dictionary Table

You can create a dictionary table directly using DDL statements at the SQL workspace.

```SQL
CREATE DICTIONARY [IF NOT EXISTS] [db.]dictionary_name
(
key1 type1[DEFAULT|EXPRESSION expr1] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
key2 type2[DEFAULT|EXPRESSION expr2] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
attr1 type2 [DEFAULT|EXPRESSION expr3],
attr2 type2 [DEFAULT|EXPRESSION expr4]
)
PRIMARY KEY key1, key2
SOURCE(SOURCE_NAME([param1 value1 ... paramN valueN]))
LAYOUT(LAYOUT_NAME([param_name param_value]))
LIFETIME({MIN min_val MAX max_val | max_val})
```


<span id="a38ee2c1"></span>
#### Use Dictionary Table


1. Search dictionary data.

   Retrieve data from the data dictionary using dictGet / dictGetOrDefault statements and functions.

   ```SQL
   dictGet('db.dict_name', 'attr_name', id_expr)
   dictGetOrDefault('db.dict_name', 'attr_name', id_expr, default_value_expr)
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The format of the first parameter of the dictGet function must be similar to db.dict_name, as the dictionary cache indexes through this field.   </div>
   

2. Delete dictionary.

   ByteHouse will delete the record of this dictionary from the Catalog.

   ```SQL
   DROP DICTIONARY [IF EXISTS] [db.]dictionary_name;
   ```
   

3. Search dictionary.

   ```SQL
   SHOW DICTIONARIES [FROM ]; 
   ```
   

   If the `FROM` clause is not specified, the search will return a list of dictionaries in the current database.

4. Search the created dictionary statements.

   ```SQL
   SHOW CREATE DICTIONARY [db.] dictionary_name
   ```
   

   This search statement returns a column of type "string" named "statement" containing a value — the CREATE query statement used to create the specified object.


<span id="b9a1a39f"></span>
### **Create dynamic partitioned tables**

ByteHouse supports dynamic configuration of bucket numbers at the partition level. You can create dynamic partitioned tables by using expressions to define bucket keys and leveraging settings parameters. For a practical example, refer to [Bucket table dynamic expansion](https://docs.byteplus.com/docs/bytehouse/bucket-table-dynamic-expansion).

<span id="61926f77"></span>
#### Caution

This feature is currently undergoing a gradual rollout (gray release). If you encounter any issues during use, please submit a support ticket or contact the ByteHouse team.

<span id="63b6c9d0"></span>
#### **Syntax**

```SQL
CREATE TABLE t(name1 type1, name2 type2, ...)
engine=CnchMergeTree()
PARTITION BY ...
CLUSTER BY EXPRESSION expr INTO 4 BUCKETS
ORDER BY ...
[UNIQUE KEY ...]
SETTINGS enable_recluster_multiple_parts=1, enable_scale_bucket_optimization=1
```


Parameter descriptions:


|Parameter |Required |Description |
|---|---|---|
|`CREATE TABLE t(name1 type1, name2 type2, ...)` |Yes |Specifies the table name and column information, including column names and data types. |
|`engine=CnchMergeTree()` |Yes |Defines the table engine as `CnchMergeTree`. |
|`PARTITION BY ...` |Yes |Defines the partition key for the partitioned table. |
|`CLUSTER BY EXPRESSION expr INTO 4 BUCKETS` |Yes |Defines the bucket key using an expression. The expression must output an unsigned integer (`uint`). For optimal performance, it is recommended to encapsulate the expression with the `cityHash64V2` function. |
|`ORDER BY ...` |Yes |Defines the sorting key. |
|`[UNIQUE KEY ...]` |No |Specifies the unique key. |
|`SETTINGS` |Yes |Configuration parameters. Use these settings to enable dynamic scaling for bucket tables. Supported parameters include:<br><br><br>* **`enable_recluster_multiple_parts`**: Table\-level setting. Enables reducing the number of output parts after bucketing to improve query performance. Default: `0` (disabled). Set to `1` (enabled).<br><br>* **`enable_scale_bucket_optimization`**: Table\-level setting. Enables using new bucket key expressions during `SELECT` queries. This also applies to scenarios where adjusting bucket counts results in varying total buckets across partitions. If disabled, queries will continue to use the old bucket key. Default: `0` (disabled). Set to `1` (enabled).<br><br>* **`force_modify_unique_table_cluster_by`**: Query\-level setting. Allows modifying `CLUSTER BY` statements in tables with unique keys. Default: `0` (disabled). Set to `1` (enabled).<br><br>* **`enable_legacy_cluster_by`**: Query\-level setting. Enables compatibility with both new bucket key expressions (`CLUSTER BY EXPRESSION`) and legacy syntax (`CLUSTER BY <column_name>`). Default: `1` (enabled). If set to `0`, only the new expression\-based syntax is allowed for creating or modifying bucket counts.<br><br>   To modify the number of buckets using the new bucket key expression syntax:<br><br>   ```SQL```<br>```   ALTER TABLE t MODIFY BUCKET NUMBER xx```<br>```   ```<br>    |


**Related documents**:


* If you want to dynamically expand the bucket table, please refer to [Bucket table dynamic expansion](https://docs.byteplus.com/docs/bytehouse/bucket-table-dynamic-expansion).

* If you want to use bucket to realize deduplication optimization for a unique key table, please refer to [Bucket deduplication optimizations](https://docs.byteplus.com/docs/bytehouse/bytehouse-best-practice-for-unique-key-tables#a8c5dffd).
