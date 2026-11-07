---
title: "Alter statement (ALTER)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/alter-statement"
---

<span id="d41d11cf"></span>
## Column operations (COLUMN)

<span id="3baa363c"></span>
##### Add Column (ADD COLUMN)

Add a new column to the table with a specified name, type, encoding, and default expression.

Syntax

```SQL
ALTER TABLE [tableIdentifier] ADD COLUMN [IF NOT EXISTS] [tableColumnDfnt] [AFTER name_after]
```



* If the `IF NOT EXISTS` clause is included, the query will not return an error if the column already exists.

* If `AFTER name_after` (name of another column) is specified, the column will be added after the specified column. If you want to add the column to the beginning of the table, use the `FIRST` clause. Otherwise, the column will be added to the end of the table. For a series of operations, `name_after` can be the name of a column added in a previous operation.


Example

```SQL
-- Step 1: create a table 
CREATE TABLE db_name.table_name
(
`order_by_column ` String
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column `)

-- Step 2: add column
ALTER TABLE db_name.table_name ADD COLUMN IF NOT EXISTS column_name String COMMENT 'column comment here' AFTER order_by_column
```


<span id="30fd05b0"></span>
##### Modify Column

Syntax

```SQL
ALTER TABLE [tableIdentifier] MODIFY COLUMN [IF EXISTS] [tableColumnDfnt] 
```



* Order by column: You can modify its default expression, comments, and encoding method.

* Partition by column: You can modify its comment.

* Normal column: You can modify its type, default expression, comments, and encoding method.


Example

```SQL
-- Step 1: create a table 
CREATE TABLE db_name.table_name
(
`order_by_column ` String,
`normal_column` Int64 DEFAULT 0
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column `)

-- Step 2: modify column normal_column_name & update its data type, comment and default value
ALTER TABLE db_name.table_name MODIFY COLUMN IF EXISTS normal_column String DEFAULT 'new_default_value' COMMENT 'new comment' 
```


<span id="7c09d2e1"></span>
##### MODIFY COLUMN REMOVE

Remove a table attribute: **`DEFAULT`**, **`ALIAS`**, **`MATERIALIZED`**, **`CODEC`**, **`COMMENT`**, **`TTL`**, **`SETTINGS`**.

Syntax

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name REMOVE property;
```


Example **Remove TTL**

```SQL
ALTER TABLE table_with_ttl MODIFY COLUMN column_ttl REMOVE TTL;
```


<span id="c9ae6485"></span>
##### MODIFY COLUMN MODIFY SETTING

Modify a table's parameter settings

Syntax

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name MODIFY SETTING name=value,...;
```


Example

Modify the field `max_compress_block_size` to `1MB`:

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name MODIFY SETTING max_compress_block_size = 1048576;
```


<span id="c261d23a"></span>
##### MODIFY COLUMN RESET SETTING

Reset column parameter settings, while removing the parameter setting declarations from the table CREATE statement expression.

Syntax

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name RESET SETTING name,...;
```


Example

Reset the parameter `max_compress_block_size` to its default value:

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name RESET SETTING max_compress_block_size;
```


<span id="6b1c701f"></span>
##### Delete column (DROP COLUMN)

Delete a column from the table. Partition by columns and order by columns cannot be deleted.

Syntax

```SQL
ALTER TABLE [tableIdentifier] DROP COLUMN [IF EXISTS] column_name;
```



* Specifies the `IF EXISTS` clause, if the column does not exist, the query will not return an error.


Example

```SQL
-- Step 1: create a table 
CREATE TABLE db_name.table_name
(
`order_by_column` String,
`normal_column` Int64
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column`)

-- Step 2: drop the normal column
ALTER TABLE db_name.table_name DROP COLUMN IF EXISTS normal_column
```


<span id="ccaf19a6"></span>
##### Rename column (RENAME COLUMN)

Rename a column in the table. There are some considerations when using:


* You cannot rename a column to an already existing column name.

* You cannot rename a column to itself.

* The original column to be renamed must exist.


Syntax

```SQL
ALTER TABLE [tableIdentifier] RENAME COLUMN [IF EXISTS] column_name_from TO column_name_to;
```



* The `IF EXISTS` clause is specified, and if the column does not exist, the query will not return an error.


Example

```SQL
-- Step 1: create a table 
CREATE TABLE db_name.table_name
(
`order_by_column` String,
`old_column_name` Int64
)
ENGINE = `CnchMergeTree`
ORDER BY (`old_column_name`)

-- Step 2: rename column
ALTER TABLE db_name.table_name RENAME COLUMN old_column_name TO new_column_name
```


<span id="f448b314"></span>
##### Clear column

Reset all data in the columns of the specified partition

Syntax

```SQL
CLEAR COLUMN [IF EXISTS] name IN PARTITION partition_name
```


Example

```SQL
ALTER TABLE visits CLEAR COLUMN browser IN PARTITION tuple()
```


<span id="4c44b4e3"></span>
##### Comment Column

Annotate a column

Syntax

```SQL
COMMENT COLUMN [IF EXISTS] name 'Text comment'
```


Example

```SQL
ALTER TABLE visits COMMENT COLUMN browser 'This column shows the browser used for accessing the site.'
```


<span id="a79d5e3a"></span>
## Partition operations

<span id="77532f4c"></span>
##### DETACH PARTITION|PART

Move the partition or data part to a detached directory and forget about it.

Syntax

```SQL
ALTER TABLE table_name  DETACH PARTITION|PART partition_expr
```


Move all data of the specified partition to a detached directory. The server will treat the detached data partition as non\-existent. Before executing the ATTACH query, the server is not aware of the existence of this data.

Example

```SQL
ALTER TABLE mt DETACH PARTITION '2020-11-21';
ALTER TABLE mt DETACH PART 'all_2_2_0';
```


After executing the query, you can perform any operation on the data in the detached directory—delete it from the file system or just keep it.

<span id="55221af5"></span>
##### DROP PARTITION|PART

Delete a partition or part of the data.


* Syntax

   ```SQL
   ALTER TABLE table_name  DROP PARTITION|PART partition_expr
   ```
   

   Delete the specified partition from the table. This query marks the partition as inactive and completely deletes the data within about 10 minutes.

* Example 1: Delete a partition (supports all tables, directly deletes the directory at the backend, offers good performance, recommended for priority use)

   ```SQL
   ALTER TABLE mt DROP PARTITION '2020-11-21';
   ALTER TABLE mt DROP PART 'all_4_4_0';
   ```
   

* Example 2: Delete a partition based on conditions

   ```SQL
   ALTER TABLE data_test_ckj.t00002 DROP PARTITION where toDate(toStartOfDay(date1)) >'2024-10-06'; 
   ```
   

   `toDate(toStartOfDay(date1))` is the syntax parameter after PARTITION BY, for example:

   ```SQL
   CREATE TABLE test.partitionByClause
   (
   VisitDate Date,
   Hour UInt8,
   ClientID UUID
   )
   ENGINE = CnchMergeTree
   PARTITION BY toDate(toStartOfDay(date1))
   ORDER BY Hour;
   ```
   

   For more details, refer to [Designing a partition key (PARTITION BY)](https://docs.byteplus.com/docs/bytehouse/create-statement#c22a1a72).


<span id="34c958ff"></span>
##### DROP DETACHED PARTITION|PART

Remove the specified part or all PARTs of a specified partition from the detached directory.

Syntax

```SQL
ALTER TABLE table_name  DROP DETACHED PARTITION|PART partition_expr
```


<span id="f7355200"></span>
##### FORGET PARTITION

If the partition is empty, delete the partition metadata.

Syntax

```SQL
ALTER TABLE table_name FORGET PARTITION partition_expr
```


If the partition is not empty or unknown, the query will fail. Ensure that this operation is performed only on partitions that will no longer be used.

Example

```SQL
ALTER TABLE mt FORGET PARTITION '20201121';
```


<span id="948f4a16"></span>
##### ATTACH PARTITION|PART

Add partitions or data parts from a detached directory to the table.

Syntax

```SQL
ALTER TABLE table_name  ATTACH PARTITION|PART partition_expr
```


Add data from a detached directory to the table. Data can be added either for an entire partition or for an individual PART.

Example

```SQL
ALTER TABLE visits ATTACH PARTITION 201901;
ALTER TABLE visits ATTACH PART 201901_2_2_0;
```


<span id="59c55e6a"></span>
##### ATTACH PARTITION FROM

Copy data partitions from one table to another and add them.

Syntax

```SQL
ALTER TABLE table2 ATTACH PARTITION partition_expr FROM table1
```


This query copies data partitions from table1 to table2.

Note:


* Data will not be deleted from table1 or table2.

* table1 can be a temporary table.


To ensure the query runs successfully, the following conditions must be met:


* Both tables must have the same structure.

* Both tables must have the same partition key, sort key, and primary key.

* Both tables must have the same indexes and projections.

* Both tables must have the same storage strategy.


<span id="d7b0c6b3"></span>
##### REPLACE PARTITION

Copy data partitions from one table to another and replace them.

Grammar

```SQL
ALTER TABLE table2 REPLACE PARTITION partition_expr FROM table1
```


This query copies data partitions from table1 to table2, replacing the existing partitions in table2. The operation is atomic.

Advisory:


* Data is not deleted from table1.

* table1 can be a temporary table.


To ensure the query runs successfully, the following conditions must be met:


* Both tables must have the same structure.

* Both tables must have the same partition key, sort key, and primary key.

* Both tables must have the same indexes and projections.

* Both tables must have the same storage strategy.


<span id="6ebb117a"></span>
##### MOVE PARTITION TO TABLE

Move the data partition from one table to another.

Syntax

```SQL
ALTER TABLE table_source MOVE PARTITION partition_expr TO TABLE table_dest
```


This query moves the data partition from table_source to table_dest and deletes the data from table_source.

To run the query successfully, the following conditions must be met:


* Both tables must have the same structure.

* Both tables must have the same partition key, sort key, and primary key.

* Both tables must have the same indexes and projections.

* Both tables must have the same storage strategy.

* Both tables must belong to the same engine family (replicated or non\-replicated).


<span id="8ff4b9a9"></span>
##### CLEAR COLUMN IN PARTITION

Reset the value of a specified column in the partition.

Syntax

```SQL
ALTER TABLE table_name CLEAR COLUMN column_name IN PARTITION partition_expr
```


Reset all values of a specified column in the partition. If a DEFAULT clause is specified when creating the table, this query will set the column value to the specified default value.

Example

```SQL
ALTER TABLE visits CLEAR COLUMN hour in PARTITION 201902
```


<span id="13fa6bb9"></span>
##### CLEAR INDEX IN PARTITION

Reset the specified secondary index in the partition.

Grammar

```SQL
ALTER TABLE table_name CLEAR INDEX index_name IN PARTITION partition_expr
```


This query is similar to CLEAR COLUMN, but it resets the index instead of column data.

<span id="b9b85a4d"></span>
##### FREEZE PARTITION

Creates a backup of the partition.

Grammar

```SQL
ALTER TABLE table_name FREEZE [PARTITION partition_expr] [WITH NAME 'backup_name']
```


This query creates a local backup of the specified partition. If the PARTITION clause is omitted, the query will create a backup of all partitions at once.

<span id="212ca794"></span>
##### UNFREEZE PARTITION

Removes the backup of the partition.

Grammar

```SQL
ALTER TABLE table_name UNFREEZE [PARTITION 'part_expr'] WITH NAME 'backup_name'
```


This query creates a local backup for the specified partition. If the PARTITION clause is omitted, the query will back up all partitions at once.

Remove the frozen partition with the specified name from the disk. If the PARTITION clause is omitted, the query will remove the backups for all partitions at once.

<span id="8a2fed6a"></span>
##### FETCH PARTITION|PART

Download a partition or part of data from another server.

Syntax

```SQL
ALTER TABLE table_name FETCH PARTITION|PART partition_expr FROM 'path-in-zookeeper'
```


Download a partition from another server. This query is only applicable to replicated tables.

Example\*\*: FETCH PARTITION\*\*

```SQL
ALTER TABLE users FETCH PARTITION 201902 FROM '/clickhouse/tables/01-01/visits';
ALTER TABLE users ATTACH PARTITION 201902;
```


Example2: **FETCH PART**

```SQL
ALTER TABLE users FETCH PART 201901_2_2_0 FROM '/clickhouse/tables/01-01/visits';
ALTER TABLE users ATTACH PART 201901_2_2_0;
```


<span id="45def719"></span>
##### MOVE PARTITION|PART

Move a partition or a part of the data to another disk or volume.

Syntax

```SQL
ALTER TABLE table_name MOVE PARTITION|PART partition_expr TO DISK|VOLUME 'disk_name'
```


Example

```SQL
ALTER TABLE hits MOVE PART '20190301_14343_16206_438' TO VOLUME 'slow'
ALTER TABLE hits MOVE PARTITION '2019-09-01' TO DISK 'fast_ssd'
```


<span id="1ddf07e0"></span>
##### UPDATE IN PARTITION

Update data within a partition by condition.

Syntax

```SQL
ALTER TABLE [db.]table UPDATE column1 = expr1 [, ...] [IN PARTITION partition_expr] WHERE filter_expr
```


Example

```SQL
-- using partition name
ALTER TABLE mt UPDATE x = x + 1 IN PARTITION 2 WHERE p = 2;

-- using partition id
ALTER TABLE mt UPDATE x = x + 1 IN PARTITION ID '2' WHERE p = 2;
```


<span id="cd40a1e0"></span>
##### DELETE IN PARTITION

Delete data within a partition based on conditions.

Syntax

```SQL
ALTER TABLE [db.]table DELETE [IN PARTITION partition_expr] WHERE filter_expr
```


Example

```SQL
-- using partition name
ALTER TABLE mt DELETE IN PARTITION 2 WHERE p = 2;

-- using partition id
ALTER TABLE mt DELETE IN PARTITION ID '2' WHERE p = 2;
```


<span id="860849f1"></span>
## Update operations

Non\-unique key tables can update data asynchronously using this query format, [Update statement (UPDATE)](https://docs.byteplus.com/docs/bytehouse/update-statement)unique key tables are not supported using this format.

Syntax

```SQL
ALTER TABLE [db.]table UPDATE column1 = expr1 [, ...] [IN PARTITION partition_id] WHERE filter_expr;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The prefix <code>ALTER TABLE</code> differentiates this syntax from most other SQL\-supporting systems. Its purpose is to indicate that, unlike similar queries in OLTP databases, this is a heavy operation and is not designed for frequent use.</div>


**Usage restrictions:** 


1. Unique key tables are not supported, please use [Update statement (UPDATE)](https://docs.byteplus.com/docs/bytehouse/update-statement) for unique key tables.

2. `filter_expr` must be of `UInt8` type. This query updates the values of specified columns to the values of corresponding expressions in the row, for those rows, `filter_expr` evaluates to non\-zero. Use the `CAST` operator to map numerical values to the type of the column. Updating columns used to calculate primary keys or partition keys is not supported.

3. A query can contain several commands separated by commas.

4. The query processing for this statement is by default asynchronous.


Example

```SQL
alter table table_alter update bool=1 where uint8=21;
```


<span id="812eb715"></span>
## Delete operations (DELETE)

Delete data from the table. Not supported for unique table. Please see "Delete Statement".

Syntax

```SQL
ALTER TABLE [tableIdentifier] DELETE WHERE filter_expr;
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>ALTER TABLE</code> prefix makes this syntax different from most other systems that support SQL. Its purpose is to indicate that unlike similar queries in OLTP databases, this is a heavy operation not designed for frequent use.</div>


**Usage Restrictions:** 


1. Unique table not supported, see "Delete From" for details.

2. The type of `filter_expr` must be `UInt8`. This query deletes rows in the table where the expression accepts non\-zero values.

3. A query can contain multiple commands separated by commas.

4. Query processing is by default asynchronous.


Example

```SQL
alter table test_common delete where id=101
```


<span id="9bfab684"></span>
## Constraint operations (CONSTRAINT)

<span id="e21f5dfe"></span>
##### Add constraints (**ADD CONSTRAINT**)

Add a constraint to a table

Syntax

```SQL
ALTER TABLE [tableIdentifier] ADD CONSTRAINT [IF NOT EXISTS] constraint_name CHECK columnExpr;
```



* If the `IF EXISTS` clause is specified, the query will not return an error if the constraint does not exist.


Example

```SQL
-- Step 1: create a table
CREATE TABLE `example_table`
(
`order_by_column` String
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column`)

-- Step 2: add constraint check_str
ALTER TABLE example_table ADD CONSTRAINT IF NOT EXISTS check_str CHECK order_by_column != 'forbidden_string'
```


<span id="eeab642b"></span>
##### Delete constraints (**DROP CONSTRAINT**)

Grammar

```SQL
ALTER TABLE [tableIdentifier] DROP CONSTRAINT [IF EXISTS] constraint_name;
```



* Specified `IF EXISTS` clause, the search will not return an error if the constraint does not exist.


Example

```SQL
-- Step 1: create a table with the constraint check_str
CREATE TABLE `example_table`
(
`order_by_column` String,
CONSTRAINT check_str CHECK order_by_column != 'forbidden_string'
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column`)

-- Step 2: drop constraint check_str
ALTER TABLE example_table DROP CONSTRAINT IF EXISTS check_str
```


<span id="feb8d8ea"></span>
## Table settings operations

This is a set of actions to change table settings. You can modify the settings or reset them to default. A single search can change multiple settings at the same time. If the specified name of the setting does not exist, the search will raise an exception.

Grammar

```SQL
ALTER TABLE [db].name MODIFY|RESET SETTING ...
```


<span id="857cd5b9"></span>
##### Change Settings

Modify Table Settings

Syntax

```SQL
MODIFY SETTING setting_name=value [, ...]
```


Example

```SQL
CREATE TABLE example_table (id UInt32, data String) ENGINE=CnchMergeTree() ORDER BY id;
ALTER TABLE example_table MODIFY SETTING max_part_loading_threads=8, max_parts_in_total=50000;
```


<span id="d61dc32f"></span>
##### Reset Settings

Reset table settings to default. If the setting is in its default state, no actions will be taken.

Syntax

```SQL
RESET SETTING setting_name [, ...]
```


Example

```SQL
CREATE TABLE example_table (id UInt32, data String) ENGINE=CnchMergeTree() ORDER BY id
SETTINGS max_part_loading_threads=8;
ALTER TABLE example_table RESET SETTING max_part_loading_threads;
```


<span id="44ddbf23"></span>
## Index operations (INDEX)

The following actions can be used:

```SQL
--Add an index description to the table metadata
ALTER TABLE [db].name ADD INDEX name expression TYPE type GRANULARITY value [FIRST|AFTER name] 

--Delete the index description from the table metadata and remove the index file from the disk
ALTER TABLE [db].name DROP INDEX name

--Query the rebuilding of the secondary index named "name" in the partition "partition_name"
ALTER TABLE [db.]table MATERIALIZE INDEX name IN PARTITION partition_name 
```


The first two commands are lightweight; they only change metadata or delete files.

<span id="ba6c76b4"></span>
## TTL operations (TTL)

<span id="d330abef"></span>
##### Modify TTL (MODIFY TTL)

Change the table TTL. Columns used in the TTL clause must be in column\-based partitioning.

Syntax

```SQL
ALTER TABLE [tableIdentifier] MODIFY [ttlClause];
```



* With the `IF EXISTS` clause specified, if the column does not exist, the query will not return an error.


Example

```SQL
-- Step 1: create a table with table TTL to be 1 day
CREATE TABLE `example_table`
(
`d` DateTime
)
ENGINE = `CnchMergeTree`
PARTITION BY d
ORDER BY `d`
TTL d + INTERVAL 1 DAY

-- Step 2: modify table ttl & change the TTL to 2 month
ALTER TABLE example_table
MODIFY TTL d + INTERVAL 2 MONTH
```


<span id="3552cdb2"></span>
##### Remove TTL (REMOVE TTL)

Remove the table's TTL

Syntax

```SQL
ALTER TABLE [tableIdentifier] REMOVE TTL;
```


Example

```SQL
-- Step 1: create a table with table TTL to be 1 day
CREATE TABLE `example_table`
(
`d` DateTime
)
ENGINE = `CnchMergeTree`
PARTITION BY d
ORDER BY d
TTL d + INTERVAL 1 DAY

-- Step 2: remove table ttl
ALTER TABLE example_table
REMOVE TTL
```


<span id="452f110d"></span>
## CLUSTER operations (MODIFY CLUSTER)

Add or change cluster attributes.

Syntax

```SQL
ALTER TABLE [tableIdentifier] MODIFY CLUSTER BY (column, expression, ...) INTO 64 BUCKETS
```
