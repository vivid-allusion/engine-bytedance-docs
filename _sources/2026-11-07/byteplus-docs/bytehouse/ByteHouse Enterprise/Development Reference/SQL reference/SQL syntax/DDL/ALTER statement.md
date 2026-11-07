---
title: "ALTER statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-alter-statement"
---

`ALTER TABLE` statements can be used to modify columns and partitions, as well as to update data, delete data, add table constraints, change table settings, adjust indexes, change TTL, and more.

<span id="0e467929"></span>
# Column operations (COLUMN)

<span id="5ec31ff0"></span>
## Add a column (ADD COLUMN)

Add columns to an existing table, with support for specifying the name, type, encoding, and default expression.

<span id="db8ecf14"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier]
ADD COLUMN [IF NOT EXISTS] [tableColumnDfnt]
[AFTER name_after];
```


<span id="b616cf0b"></span>
### Parameter description


|Parameters |Required |Function |
|---|---|---|
|tableIdentifier |Yes |Target table name (format: `[db_name.]table_name`) |
|IF NOT EXISTS |No |If you add the `IF NOT EXISTS` clause, the query will not return an error if the column already exists. |
|tableColumnDfnt |Yes |**Column definition**: `column_name data_type [CODEC(codec_name)] [DEFAULT expr]` |
|AFTER name_after |No |If `AFTER name_after` is specified, the new column will be added after the specified column. |
|FIRST |No |The `FIRST` clause can be used to add a column to the beginning of a table. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If neither <code>AFTER name_after</code> nor <code>FIRST</code> is specified, the new column will be added to the end of the table.</div>


* <div data-tips="true" data-tips-type="warning">When performing multi\-column operations in the same statement, <code>AFTER</code> can reference columns that have already been added by this statement.</div>



<span id="ab9dd3b5"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3: Add a column
ALTER TABLE sample_db.sample_table 
ADD COLUMN IF NOT EXISTS column_name String 
  COMMENT 'column comment here' 
AFTER order_by_column;
```


<span id="49b83600"></span>
## Modify column (MODIFY COLUMN)

`MODIFY COLUMN` statement can be used to adjust column attributes in a table, such as type, default value, encoding, and more.

<span id="7a8f0a28"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] MODIFY COLUMN [IF EXISTS] [tableColumnDfnt]
```


The following operations can be performed for different types of columns:


* Order by column: You can modify its default_expr, comment, and codec.

* Partition by column: You can modify its comment (comment).

* Normal column: You can modify its type (type), default_expr, comment (comment), and codec (codec).


<span id="2e275fd9"></span>
### Parameter description


|Parameters |Required |Function |
|---|---|---|
|IF EXISTS |No |Perform the operation only if the column exists (to avoid errors caused by invalid columns). |
|tableColumnDfnt |Yes |Add a new column definition, for example: `column_name [NEW_TYPE] [CODEC(...)] [DEFAULT ...] [COMMENT ...]` |


<span id="e3ad9281"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64 DEFAULT 0
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Modify the column normal_column, and update its data type, comment, and default value</TRANSLATION>
ALTER TABLE sample_db.sample_table
MODIFY COLUMN IF EXISTS normal_column String 
DEFAULT 'new_default_value' 
COMMENT 'new comment';
```


<span id="7a877a90"></span>
### Remove table attributes (MODIFY COLUMN REMOVE)

Remove table attributes, including `DEFAULT`, `ALIAS`, `MATERIALIZED`, `CODEC`, `COMMENT`, `TTL`, `SETTINGS` **.** 

<span id="d9cfdf8e"></span>
#### Grammar

```SQL
ALTER TABLE table_name MODIFY COLUMN column_name REMOVE property; 
```


<span id="528d7335"></span>
#### Example: **Remove DEFAULT**

```SQL
-- 1: Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64 DEFAULT 0
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Remove the DEFAULT attribute
ALTER TABLE sample_db.sample_table
MODIFY COLUMN normal_column
REMOVE DEFAULT;
```


<span id="5806d2fc"></span>
### Modify table parameter configurations (MODIFY SETTING)

Modify the table parameter settings.

<span id="57a15b55"></span>
#### Grammar

```SQL
ALTER TABLE table_name MODIFY SETTING name=value,...; 
```


<span id="e2c91cff"></span>
#### Example

Change the field `max_compress_block_size` to `1MB`:

```SQL
-- 1: Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64 DEFAULT 0
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Modify the max_compress_block_size field to 1MB
ALTER TABLE sample_db.sample_table 
MODIFY SETTING max_compress_block_size = 1048576; 
```


<span id="1b932be8"></span>
### Reset table parameter settings (RESET SETTING)

Reset table parameter settings, and remove parameter setting declarations from the list expression in the `CREATE` table statement.

<span id="75a21723"></span>
#### Grammar

```SQL
ALTER TABLE table_name RESET SETTING name,...; 
```


<span id="c7526c52"></span>
#### Example

Reset the table parameter `max_compress_block_size` to the default value:

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64 DEFAULT 0
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Reset table parameter max_compress_block_size to the default value
ALTER TABLE sample_db.sample_table 
RESET SETTING max_compress_block_size; 
```


<span id="62a3c331"></span>
## Delete a column (DROP COLUMN)

Delete a column from the table. Partition by columns and order by columns cannot be deleted.

<span id="3b2ed71c"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] DROP COLUMN [IF EXISTS] column_name; 
```


<span id="d7a8a1a2"></span>
### **Parameter description**

When the `IF EXISTS` clause is specified, the query will not return an error if the column does not exist.

<span id="1513b2fe"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Delete the normal_column column
ALTER TABLE sample_db.sample_table DROP COLUMN IF EXISTS normal_column;
```


<span id="57e5122f"></span>
## Rename column (RENAME COLUMN)

Rename columns in the table. Caution:


* You cannot name a new column with an existing column name.

* You cannot rename a column to itself.

* The original column to be renamed must exist.


<span id="68fcc8ca"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] RENAME COLUMN [IF EXISTS] column_name_from TO column_name_to; 
```


<span id="2e051627"></span>
### Parameter description


|**Parameters** |**Required** |**Note** |
|---|---|---|
|column_name_from |Yes |Original column name (must exist in the table). |
|column_name_to |Yes |New column name (must be unique and different from the original column name). |
|IF EXISTS |No |If the original column does not exist, skip the operation to avoid throwing an error. |


<span id="085ae9a6"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column ` String,
    `normal_column` Int64
)
ENGINE = `MergeTree`
ORDER BY (`order_by_column`);

-- 3. Rename columns
ALTER TABLE sample_db.sample_table 
RENAME COLUMN IF EXISTS column_name TO new_column_name
```


<span id="6ca22b24"></span>
## Clear column (CLEAR COLUMN)

Clear all data from a column in the specified partition.

<span id="4762066b"></span>
### Grammar

```SQL
ALTER TABLE table_name CLEAR COLUMN [IF EXISTS] name IN PARTITION partition_name
```


<span id="2f1dc686"></span>
### Example

```SQL
ALTER TABLE sample_db.sample_table CLEAR COLUMN browser IN PARTITION tuple()
```


<span id="bb0dc30c"></span>
## The comment column (COMMENT COLUMN)

Add comments to columns.

<span id="fdd4be3b"></span>
### Grammar

```SQL
ALTER TABLE table_name COMMENT COLUMN [IF EXISTS] name 'Text comment'
```


<span id="2aa07108"></span>
### Example

```SQL
ALTER TABLE sample_db.sample_table COMMENT COLUMN browser 'This column shows the browser used for accessing the site.' 
```


<span id="c1538918"></span>
# Partition operations (PARTITION)

<span id="e35472e6"></span>
## Detach partition | data block (DETACH PARTITION|PART)

Move the data of the specified partition or data part in the table to a separate directory. After detachment, the server no longer recognizes the partition, but you can use the `ATTACH` statement to reattach it.

After performing the separation operation, you can perform any operation on the data in the separated directory, including deleting it from the file system or simply retaining it.

<span id="d1f97c87"></span>
### Grammar

```SQL
ALTER TABLE table_name DETACH PARTITION|PART partition_expr 
```


<span id="1000acd9"></span>
### Example 1: Partition separation

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2019-01-01', 'firefox', 9, 20, 2);

-- 4. Separate partitions
ALTER TABLE sample_db.sample_table DETACH PARTITION '2020-11-21';
```


<span id="fb63c8e0"></span>
### Example 2: Separate data blocks

```SQL
-- 1. Create a database (if it does not exist)
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.detachPart ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.detachPart ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column  
ORDER BY (`order_by_column`); 

-- 3: Insert test data (generate multiple data blocks)
INSERT INTO sample_db.detachPart
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),  
('order2', '2019-01-01', 'firefox', 9, 20, 2), 
('order3', '2020-11-21', 'safari', 10, 30, 3); 

-- 4. Query data block information (obtain the name of the Part to be separated)
SELECT 
  name,
  partition,         
  rows               
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'detachPart' 
  AND active = 1; 

-- 5. Detach the specified data block (DETACH PART)
-- Use the part_name obtained in Step 4, for example, split '20201121_1_1_0'
ALTER TABLE sample_db.detachPart
DETACH PART '20201121_1_1_0';  

-- 6. Verify whether the data block has been separated
SELECT 
  name,
  partition,         
  rows               
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'detachPart'; 
```


<span id="3d9c7765"></span>
## Delete partition | data block (DROP PARTITION|PART)

Delete the specified partition or data part from the table. After execution, the system will mark the partition as inactive and completely delete its data within approximately 10 minutes.

<span id="65a6d77b"></span>
### Grammar

```SQL
ALTER TABLE table_name  DROP PARTITION|PART partition_expr 
```


<span id="71458722"></span>
### Example 1: Delete a partition

This method supports all tables, deletes directories directly at the underlying level, has good performance, and is recommended to be used as a priority.

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2019-01-01', 'firefox', 9, 20, 2);

-- 4. Delete partitions
ALTER TABLE sample_db.sample_table DROP PARTITION '2020-11-21';
```


<span id="3c10e7fb"></span>
### Example 2: Delete partitions based on conditions

You can use the `where` clause to specify conditions, and the system will filter and delete partitions based on the conditions you set. Specifically, `toDate(toStartOfDay(date1))` is a syntax parameter used after PARTITION BY.

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete partitions based on conditions
ALTER TABLE sample_db.sample_table
DROP PARTITION WHERE toDate(partition_column) > '2024-10-06';
```


<span id="dad912ea"></span>
### Example 3: Delete data blocks

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2019-01-01', 'firefox', 9, 20, 2);

-- 4. Query data block information (obtain the name of the Part that needs to be separated)
SELECT 
  name,
  partition,         
  rows               
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'samppe_table' 
  AND active = 1; 

-- 5. Delete a part
-- Use the part_name obtained in Step 4, for example, separating '20201121_1_1_0'
ALTER TABLE sample_db.sample_table DROP PART '20201121_1_1_0';
```


<span id="1d1833f5"></span>
## Delete partitions or data blocks from detached directory (DROP DETACHED PARTITION|PART)

Remove the specified part or all parts of the specified partition from the detached directory.

<span id="5394a62c"></span>
### Grammar

```SQL
ALTER TABLE table_name DROP DETACHED PARTITION|PART partition_expr
```


<span id="9177ed00"></span>
### Example 1: Delete a partition from the detached directory

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete a partition from the detached directory
ALTER TABLE sample_db.sample_table DROP DETACHED PARTITION '2020-10-05'
SETTINGS allow_drop_detached = 1;
```


<span id="e41fc090"></span>
### Example 2: Delete data blocks from the detached directory

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Query data block information (obtain the names of the Parts to be separated)
SELECT 
  name,
  partition,         
  rows               
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'samppe_table' 
  AND active = 1; 

--5. Delete Part from detached directory
-- Use the part_name obtained in Step 4, for example, separating "20201121_1_1_0"
ALTER TABLE sample_db.sample_table DROP DETACHED PART '20201121_1_1_0'
SETTINGS allow_drop_detached = 1;
```


<span id="22507df7"></span>
## **Restore partition from** detached **directory** | data block \*\*(\*\*ATTACH PARTITION|PART)

Add partition data that has been separated into the `detached` directory back to the table. You can add data for an entire partition or for individual partitions. After the association is restored, partitions can be queried and accessed again.

<span id="9a240fbe"></span>
### Grammar

```SQL
ALTER TABLE table_name  ATTACH PARTITION|PART partition_expr 
```


<span id="f58bd71a"></span>
### Example 1: **From** detached **directory restore partition(s)** 

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete partition from the detached directory
ALTER TABLE sample_db.sample_table DROP DETACHED PARTITION '2020-10-05';

-- 5. Restore a partition from the detached directory
ALTER TABLE sample_db.sample_table ATTACH PARTITION '2020-10-05'; 
```


<span id="6a9e7f2b"></span>
### Example 2: **Restore data blocks from** detached **directory**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Query data block information (obtain the names of Parts to be separated)
SELECT 
  name,
  partition,         
  rows               
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'samppe_table' 
  AND active = 1; 
 
-- 5. Delete Part from detached directory
-- Use the part_name obtained in Step 4, for example, split the part_name "20201121_1_1_0"
ALTER TABLE sample_db.sample_table DROP DETACHED PART '20201121_1_1_0';

-- 6. Restore Part from the detached directory
ALTER TABLE sample_db.sample_table ATTACH PART '20201121_1_1_0'; 
```


<span id="ead92335"></span>
## ATTACH PARTITION FROM

Copy the specified partition data from the source table (`table1`) to the target table (`table2`), and register it as a partition of the target table.

<span id="d064f982"></span>
### Grammar

```SQL
ALTER TABLE table2 ATTACH PARTITION partition_expr FROM table1 
```


Caution:


* Data will not be deleted from table1 or table2.

* table1 can be a temporary table.


Before execution, please ensure that the table you specified meets the following conditions:


* Two tables must have the same structure.

* Two tables must have the same partition key, sort key, and primary key.

* Both tables must have the same indexes and projections.

* The two tables must have the same storage strategy.


<span id="8ca4d33b"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table2 ON CLUSTER sample_cluster;

-- 3. Create table 1
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 4. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 5. Create table 2
CREATE TABLE IF NOT EXISTS sample_db.sample_table2 ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 6. Copy specified partition data from the source table (sample_db.sample_table) to the target table (sample_db.sample_table2)
ALTER TABLE sample_db.sample_table2
ATTACH PARTITION '2020-10-05' 
FROM sample_db.sample_table;
```


<span id="b5bfe8bf"></span>
## Replace partition (REPLACE PARTITION)

Overwrite the same\-named partition in the target table (`table2`) with the specified partition data from the source table (`table1`). Atomic replacement is supported to ensure data consistency.

<span id="f3967b96"></span>
### Grammar

```SQL
ALTER TABLE table2 REPLACE PARTITION partition_expr FROM table1 
```


Caution:


* The data in the source table (table1) will not be deleted.

* The source table (table1) can be a temporary table.


Before you execute, please ensure that the table you specified meets the following conditions:


* The two tables must have the same structure.

* The two tables must have the same partition key, sort key, and primary key.

* The two tables must have the same indexes and projections.

* The two tables must have the same storage strategy.


<span id="0ddc95a3"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table2 ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 4. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 5. Create table 2
CREATE TABLE IF NOT EXISTS sample_db.sample_table2 ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 6. Overwrite the specified partition data from the source table (sample_db.sample_table) to the partition with the same name in the target table (sample_db.sample_table2)
ALTER TABLE sample_db.sample_table2
REPLACE PARTITION '2020-10-05' 
FROM sample_db.sample_table;
```


<span id="7f0905e6"></span>
## **Move partition data across tables (MOVE PARTITION TO TABLE)** 

Migrate the data from the specified partition of the source table (`table_source`) to the destination table (`table_dest`), and then delete that partition from the source table.

<span id="257e54eb"></span>
### Grammar

```SQL
ALTER TABLE table_source MOVE PARTITION partition_expr TO TABLE table_dest 
```


Before executing, ensure that the tables you specified meet the following conditions:


* Both tables must have the same structure.

* The two tables must have the same partition key, sort key, and primary key.

* Both tables must have the same index and projection.

* The two tables must have the same storage strategy.

* Both tables must belong to the same engine family (for example, both are of the `MergeTree` engine or both are of the `ReplicatedMergeTree` engine).


<span id="b0e71356"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table_source ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table_dest ON CLUSTER sample_cluster;

-- 3. Create table 1
CREATE TABLE IF NOT EXISTS sample_db.sample_table_source ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 4. Insert data
INSERT INTO sample_db.sample_table_source
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 5. Create table 2
CREATE TABLE IF NOT EXISTS sample_db.sample_table_dest ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 6. Migrate the data in the specified partition of the source table (sample_db.sample_table_source) to the destination table (sample_db.sample_table_dest), and then delete that partition from the source table
ALTER TABLE sample_db.sample_table_source
MOVE PARTITION '2020-10-05' 
TO TABLE sample_db.sample_table_dest;

-- 7. Verify that the target table has received partitioned data
SELECT 
    partition_column AS partition,
    COUNT(*) AS rows,
    any(browser) AS browser_example, 
    any(hour) AS hour_example     
FROM sample_db.sample_table_dest
GROUP BY partition_column;

-- 8. Verify that the source table partition has been deleted
SELECT 
    partition_column AS partition,
    COUNT(*) AS rows
FROM sample_db.sample_table_source
GROUP BY partition_column;
```


<span id="12c599b2"></span>
## **Reset column values in partition (CLEAR COLUMN IN PARTITION)** 

Reset all values of the specified column in the partition. If a DEFAULT clause is specified when creating the table, this query will set the column values to the specified default value.

<span id="f5db2256"></span>
### Grammar

```SQL
ALTER TABLE table_name CLEAR COLUMN column_name IN PARTITION partition_expr 
```


<span id="91271e71"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete the existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32 DEFAULT 0,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 4. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 5. Reset column values in a partition
ALTER TABLE sample_db.sample_table CLEAR COLUMN hour in PARTITION '2020-10-05';

-- 6. Verify whether the value of the hour column has been reset
SELECT *
FROM sample_db.sample_table
WHERE `partition_column` = '2020-10-05';
```


<span id="078c2594"></span>
## **Reset the secondary index in partition (** CLEAR INDEX IN PARTITION)

Reset specified secondary indexes in the partition. `CLEAR INDEX IN PARTITION` statement is similar to the `CLEAR COLUMN` statement, but the `CLEAR INDEX IN PARTITION` statement resets indexes rather than column data.

<span id="9d3f1cc7"></span>
### Grammar

```SQL
ALTER TABLE table_name CLEAR INDEX index_name IN PARTITION partition_expr 
```


<span id="f4f33d2a"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_table ON CLUSTER CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32,
    INDEX idx_browser (`browser`) TYPE minmax GRANULARITY 32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Reset secondary indexes in the partition
ALTER TABLE sample_db.sample_table 
CLEAR INDEX idx_browser 
IN PARTITION '2020-10-05';
```


<span id="a719f493"></span>
## **Create a partition backup (** FREEZE PARTITION)

Create a local backup for the specified partition. If the `PARTITION` clause is omitted, executing the statement will create backups for all partitions at once.

<span id="4ed1fae1"></span>
### Grammar

```SQL
ALTER TABLE table_name FREEZE [PARTITION partition_expr] [WITH NAME 'backup_name'] 
```


<span id="52e86b44"></span>
### Parameter description


|**Parameters** |**Required** |**Note** |
|---|---|---|
|PARTITION |No |Specify the expression for partitions to be backed up. If omitted, a full backup of all partitions will be performed. |
|WITH NAME |No |Specify a backup set name (for identification). If omitted, the system automatically generates a timestamp\-based name. |


<span id="866075ef"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Create a local backup of the specified partition
ALTER TABLE sample_db.sample_table 
FREEZE PARTITION '2020-11-02' 
WITH NAME 'backup_20201102';
```


<span id="0b47ae86"></span>
## **Remove partition backup (UNFREEZE PARTITION)** 

Remove the `frozen` partition with the specified name from the disk. If the `PARTITION` clause is omitted, the query will remove all partition backups at once.

<span id="cf8bcba1"></span>
### Grammar

```SQL
ALTER TABLE table_name UNFREEZE [PARTITION 'part_expr'] WITH NAME 'backup_name' 
```


<span id="5ab47d6d"></span>
### Parameter description


|**Parameters** |**Required** |**Note** |
|---|---|---|
|PARTITION |No |Specify the expression for partitions whose backups need to be deleted. If omitted, all partitions in the backup set will be deleted. |
|WITH NAME |No |Specify the backup set name (the name used for `FREEZE`). |


<span id="757ae610"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Create a local backup of the specified partition
ALTER TABLE sample_db.sample_table 
FREEZE PARTITION '2020-11-02' 
WITH NAME 'backup_20201102';

-- 5. Remove partition backup
ALTER TABLE sample_db.sample_table 
UNFREEZE PARTITION '2020-11-02' 
WITH NAME 'backup_20201102';
```


<span id="de88c082"></span>
## **Synchronize partition data across nodes (FETCH PARTITION|PART)** 

This clause is used to synchronize partitions or data blocks (Part) between different replicas within the same shard, and is applicable to scenarios such as data repair and supplementing missing data in replicas.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This synchronization operation is only applicable to tables of the HaMergeTree type. For more information about HaMergeTree, see <a href="https://docs.byteplus.com/docs/bytehouse/hamergetree">HaMergeTree</a>.</div>


* <div data-tips="true" data-tips-type="warning">Before use, please ensure that the cluster you are using is a multi\-replica cluster.</div>



<span id="38c822d8"></span>
### Grammar

```SQL
ALTER TABLE [db.]table_name FETCH PARTITION|PART partition_expr FROM '{another_replica_name}'
```


<span id="e4b73615"></span>
### Parameter description


|Parameters |Required |Note |
|---|---|---|
|FROM another_replica_name |Yes |Specify the replica of the data source and configure it with the IP address of the HaMergeTree replica. You can query using the following commands:<br><br>```SQL```<br>```SELECT replica_name, replica_path```<br>```FROM system.ha_replicas```<br>```WHERE database = 'sample_db' AND table = 'fetchPart_local';```<br> |


<span id="377ed7bb"></span>
### Example

```SQL
-- 1. Create a table
Local table
CREATE TABLE IF NOT EXISTS sample_db.fetchPart_local (
  `id` Int16,
  `name` String
) 
ENGINE = HaMergeTree(
    '/clickhouse/2100957468/sample_cluster/sample_db.fetchPart_local/{shard}',
    '{replica}'
)
PARTITION BY id
ORDER BY id
SETTINGS
  storage_policy = 's3_cold', -- Before using this setting, ensure that cold and hot storage service is enabled for your cluster.
  index_granularity = 8192;

Distributed table
CREATE TABLE IF NOT EXISTS sample_db.fetchPart
AS sample_db.fetchPart_local 
Engine = Distributed (
    sample_cluster,
    `sample_db`,
    `fetchPart_local`,
    intHash64(id)
  );

-- 2. Insert test data
INSERT INTO sample_db.fetchPart (id, name) VALUES (1, 'Alice'), (2, 'Bob'), (3, 'Eve');

-- 3. Query partition and data block information to obtain information required for synchronization
-- 3.1. Query a partition ID
SELECT DISTINCT partition_id 
FROM system.parts 
WHERE database = 'sample_db' AND table = 'fetchPart_local' AND active=1;

-- 3.2 Query all parts under partition 1
SELECT name 
FROM system.parts 
WHERE database = 'sample_db' AND table = 'fetchPart_local' AND partition='1' AND active;

-- 3.3 Query replica name and replica path
SELECT replica_name, replica_path 
FROM system.ha_replicas 
WHERE database = 'sample_db' AND table = 'fetchPart_local';

-- 4. FETCH operation examples
-- 4.1 Synchronize the entire partition using the partition ID
-- Scenario: Replica 1 (192.xxx.xx.27) is missing data for partition 1, which is synchronized from replica 2 (192.xxx.xx.26) in the same shard
ALTER TABLE sample_db.fetchPart_local 
FETCH PARTITION ID '1' 
FROM '192.xxx.xx.26';

-- 4.2 Use Part name to synchronize a single part
Scenario: Data block '1_0_0_0' in partition 1 of replica 1 is corrupted and then synchronized from replica 2.
ALTER TABLE sample_db.fetchPart_local 
FETCH PART '1_0_0_0' 
FROM '192.xxx.xx.26';
```


<span id="1810c7bd"></span>
## **Migrate partition data across disks (** MOVE PARTITION|PART)

Migrate the specified partition from the current disk to another disk or volume group.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you use the cluster, make sure that cold and hot storage is enabled. For details on how to perform this operation, see <a href="https://docs.byteplus.com/docs/bytehouse/cold-hot-storage">Cold\-hot storage</a>.</div>


<span id="d457409f"></span>
### Grammar

```SQL
ALTER TABLE table_name MOVE PARTITION|PART partition_expr TO DISK|VOLUME 'disk_or_volume_name' 
```


<span id="6c6beba4"></span>
### Parameter description


|**Parameters** |**Required** |**Note** |
|---|---|---|
|DISK/VOLUME |Yes |Target storage location type:<br><br><br>* `DISK`: Specify the name of a specific disk.<br><br>* `VOLUME`: Specify a volume group. |
|disk_or_volume_name |Yes |Disk name or volume group name. |


<span id="d7ce52f1"></span>
### Example

```SQL
-- 1. Create a table that supports multiple storage policies
CREATE TABLE IF NOT EXISTS sample_db.order_records (
  `order_id` Int64,
  `order_date` Date,
  `amount` Float64,
  `status` String
)
ENGINE = MergeTree()
PARTITION BY toYYYYMM(order_date) 
ORDER BY (order_id, order_date)
SETTINGS 
  storage_policy = 's3_cold';  -- Associated storage policy name

-- 2. Insert test data
-- December 2023 data (assumed to be cold data)
INSERT INTO sample_db.order_records 
VALUES 
  (1001, '2023-12-05', 199.99, 'completed'),
  (1002, '2023-12-15', 299.50, 'completed');

-- Data for January 2024 (assumed to be hot data)
INSERT INTO sample_db.order_records 
VALUES 
  (2001, '2024-01-02', 399.00, 'pending'),
  (2002, '2024-01-10', 499.99, 'completed');

-- 3. Check the partition and data block storage locations (confirm before moving)
-- View storage information for all partitions
SELECT 
  partition,  
  name,  
  disk_name  
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'order_records' 
  AND active = 1; 

-- 4. MOVE operation examples
-- 4.1 Move the entire partition to the specified disk (DISK)
-- Scenario: Migrate cold data of December 2023 from "default" to "s3"
ALTER TABLE sample_db.order_records
MOVE PARTITION '202312'  -- Partition expression (matches PARTITION BY definition)
TO DISK 's3';     -- Target disk name (must exist in storage_policy)

Move a single data block (PART) to the specified volume (VOLUME)
Scenario: Migrate a data block from January 2024 from "default" to "s3"
-- Caution: You must first obtain the specific part_name through Step 3 (for example, 202401_1_1_0).
ALTER TABLE sample.order_records
MOVE PART '202401_2_2_0'  -- Data block name (obtained by querying system.parts)
TO VOLUME 's3';  -- Target volume name (a volume is a logical combination of disks)

-- 5. Verify the move results
-- 5.1 Verify partition migration to disk
SELECT 
  partition,
  disk_name
FROM system.parts 
WHERE 
  database = 'sample_db' 
  AND table = 'order_records' 
  AND active = 1;
  
-- 5.2 Verify that the part moves to the specified volume
SELECT path
FROM system.parts 
WHERE name = '202401_2_2_0' AND table = 'order_records';
```


<span id="63e9eb4b"></span>
## **Conditional update within a partition (** UPDATE IN PARTITION)

Bulk update data based on conditions within the specified partition.

<span id="461c03bb"></span>
### Grammar

```SQL
ALTER TABLE [db.]table
    UPDATE 
        column1 = expr1,
        column2 = expr2,  
        ...
    [IN PARTITION partition_expr]  Optional: Specify partition
    WHERE filter_expr;            Filter criteria
```


<span id="b56ccd4b"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 3. Insert data
INSERT INTO sample_db.sample_table
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Method 1: Update using partition name
ALTER TABLE sample_db.sample_table UPDATE x = x + 1 IN PARTITION '2020-11-02' WHERE p = 2;

-- Method 2: Use partition ID
-- Query partition ID
SELECT DISTINCT
    partition_id
FROM system.parts
WHERE database = 'sample_db' AND table = 'sample_table' AND active = 1;

-- Update using the partition ID
ALTER TABLE sample_db.sample_table UPDATE x = x + 1 IN PARTITION ID '20201005' WHERE p = 2; 
```


<span id="e2c7fa31"></span>
## Conditional deletion in a partition (DELETE IN PARTITION)

Delete data rows based on conditions within the specified partition.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For HaMergreTree table, <code>delete where</code> can only be used on local tables and does not yet support distributed tables.</div>


* <div data-tips="true" data-tips-type="warning">Only ByteHouse Enterprise v2.4 and later support <code>delete where</code> syntax.</div>



<span id="ef28aeda"></span>
### Grammar

```SQL
ALTER TABLE [db.]table DELETE [IN PARTITION partition_expr] WHERE filter_expr 
```


<span id="d3491fba"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
 ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
PARTITION BY partition_column
ORDER BY (`order_by_column`);

CREATE TABLE sample_db.sample_table
    AS sample_db.sample_table_local
    ENGINE = Distributed(sample_cluster, sample_db, sample_table_local, hour);

-- 3. Insert data
INSERT INTO sample_db.sample_table_local ON CLUSTER sample_cluster
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete using partition name
ALTER TABLE sample_db.sample_table_local ON CLUSTER sample_cluster DELETE IN PARTITION '2020-11-02' WHERE p = 2; 

-- Delete using partition ID
ALTER TABLE sample_db.sample_table_local ON CLUSTER sample_cluster DELETE IN PARTITION ID '2' WHERE p = 2;
```


<span id="5af6af32"></span>
# The update operation (UPDATE)

You can use this basic query format to update data.

<span id="44108399"></span>
## Cautions


1. `filter_expr` must be of type `UInt8`. This query updates the value of the specified column to the value of the corresponding expression in the row for rows where `filter_expr` is nonzero. Use the `CAST` operator to map a numeric value to the type of the column. Updating columns used to compute the primary key or partition key is not supported.

2. A single query statement allows multiple commands to be separated by commas.

3. Query processing for this statement is performed asynchronously by default.


<span id="3a9031bf"></span>
## Grammar

The `ALTER TABLE` prefix makes this syntax different from most other systems that support SQL. Its purpose is to indicate that, unlike similar queries in OLTP databases, this is a resource\-intensive operation and is not designed for frequent use.

```SQL
ALTER TABLE [db.]table
    UPDATE 
        column1 = expr1,
        column2 = expr2, 
        ...
    [IN PARTITION partition_id]  Optional partitions
    WHERE filter_expr;          Filter criteria
```


<span id="7742a81a"></span>
## **Parameter description**

IN PARTITION partition_id: Optional. If the table contains a large amount of data or has many partitions, it is recommended to add this condition to perform the update operation at the partition level, which is faster and more stable.

<span id="9102b859"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
 ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
PARTITION BY partition_column
ORDER BY (`order_by_column`);

CREATE TABLE sample_db.sample_table
    AS sample_db.sample_table_local
    ENGINE = Distributed(sample_cluster, sample_db, sample_table_local, hour);

-- 3. Insert data
INSERT INTO sample_db.sample_table_local ON CLUSTER sample_cluster
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Update data
ALTER TABLE testample_db.sample_table_nlocal ON CLUSTER sample_cluster 
    UPDATE browser = 'edge' 
    WHERE order_by_column = 'order1';
```


<span id="122d09c9"></span>
# The delete operation (DELETE)

Delete data from the table.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For HaMergreTree table, <code>delete where</code> can only be used on local tables and does not yet support distributed tables.</div>


* <div data-tips="true" data-tips-type="warning">Only ByteHouse Enterprise v2.4 and later support <code>delete where</code> syntax.</div>



<span id="1190211b"></span>
## Grammar

```SQL
ALTER TABLE [tableIdentifier] DELETE [IN PARTITION partition_id] WHERE filter_expr;
```


<span id="6b1a6472"></span>
## **Parameter description**

IN PARTITION partition_id: Optional. If the table contains a large amount of data or has many partitions, it is recommended to add this condition to perform delete operations at the partition level, which is faster and more stable.

<span id="a19f7ba4"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster;
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table_local ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
) ENGINE = HaMergeTree('/clickhouse/tables/{shard}/{database}/local_table_name', '{replica}')
PARTITION BY partition_column
ORDER BY (`order_by_column`);

CREATE TABLE sample_db.sample_table
    AS sample_db.sample_table_local
    ENGINE = Distributed(sample_cluster, sample_db, sample_table_local, hour);

-- 3. Insert data
INSERT INTO sample_db.sample_table_local ON CLUSTER sample_cluster
VALUES
('order1', '2020-11-21', 'chrome', 8, 10, 2),
('order2', '2020-11-02', 'chrome', 8, 10, 2),
('order3', '2020-10-05', 'firefox', 9, 20, 2);

-- 4. Delete data
ALTER TABLE sample_db.sample_table_local ON CLUSTER sample_cluster 
    DELETE WHERE browser = 'firefox';
```


<span id="ad0c725f"></span>
# FAST DELETE

FAST DELETE operates via mutation, but is considered a lightweight mutation operation. The underlying execution logic is as follows: FAST DELETE creates a HardLink to the original part data file and generates a small Bitmap file to record the row numbers of data marked for deletion. This process is relatively lightweight and is suitable for quickly deleting a portion of data or for scenarios requiring large\-scale data deletion. Currently, this feature only supports the HaUniqueMergeTree and HaMergeTree table engines.

The differences between the FAST DELETE statement and the DELETE statement are as follows:


|Syntax |Deletion method |Execution method |Execution cost |
|---|---|---|---|
|Delete Where |Physical deletion |Asynchronous Mutation |Heavy, high cost |
|Fastdelete Where |Marked deletion |Asynchronous Mutation |Lightweight, lower cost |


<span id="dff4e5e6"></span>
## Grammar

```SQL
ALTER TABLE db.table FASTDELETE [col_name [, ...]] 
[IN PARTITION {(ID partition_id) | (partition_name)}] 
WHERE filter_expr
```



|Parameters |Required |Configuration description |
|---|---|---|
|db.table |Yes |It specifies the target data object.<br><br><br>* db: Specifies the database.<br><br>* table: Specifies the local table. |
|col_name |No |It specifies the column name to be deleted. To specify multiple columns, separate them with a comma (`,`). |
|IN PARTITION |No |It specifies the target partition for the deletion operation. It supports specifying partition ID or partition name.<br><br>When the table contains a large amount of data or has many parts, it is recommended to add this condition to perform the delete operation at the partition level for faster and more stable execution. |
|WHERE |Yes |It specifies the data filter condition expression; only data that meets this condition will be deleted. |


<span id="941b56b7"></span>
## Example

```SQL
-- 1. Create test tables
DROP TABLE IF EXISTS test.test_fd;

-- Create a local table
CREATE TABLE test.test_fd
(
    `p_date` Date,
    `id` Int32,
    `age` Int32,
    `event` String,
    `ab` Array(Int32)
)
ENGINE = HaUniqueMergeTree(concat('/clickhouse/tables/', currentDatabase(), '/test_fd'), '1')
PARTITION BY p_date
ORDER BY id
UNIQUE KEY id
SETTINGS index_granularity = 8192;

-- Create a distributed table
CREATE TABLE test.test_fd_dis on cluster your_cluster_name
(
    `p_date` Date,
    `id` Int32,
    `age` Int32,
    `event` String,
    `ab` Array(Int32)
)
ENGINE = Distributed('your_cluster_name', 'test', 'test_fd_cluster_local', id);

-- 2. Insert data
INSERT INTO test.test_fd VALUES ('2021-01-01', 1, 18, 'a', [1,2,3]),('2021-01-01', 2, 18, 'b', [1,2,3]),('2021-01-01', 3, 18, 'c', [1,2,3]),('2021-01-02', 2, 21, 'a', [1,2,3]),('2021-01-02', 3, 22, 'b', [1,2,3]),('2021-01-03', 3, 23, 'c', [1,2,3]);

-- 3. Delete data
ALTER TABLE test.test_fd ON CLUSTER your_cluster_name FASTDELETE WHERE p_date = '2021-01-01' and id > 1;
```


<span id="59756429"></span>
# Constraint operations (CONSTRAINT)

<span id="b8f327fa"></span>
## Add a constraint (**ADD CONSTRAINT**)

Add constraints to a table

<span id="d060d9e4"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] 
    ADD CONSTRAINT [IF NOT EXISTS] constraint_name 
    CHECK columnExpr; 
```


<span id="0e427c32"></span>
### Parameter description


|Parameters |Required |Note |
|---|---|---|
|IF NOT EXISTS |No |Optional parameter. It ensures no error is reported if the constraint does not exist. |
|constraint_name |Yes |Constraint name. It must be unique. |
|CHECK columnExpr |Yes |Define constraint rules. |


<span id="10e291e5"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

--  3. Add constraint check_str
ALTER TABLE sample_db.sample_table
    ADD CONSTRAINT IF NOT EXISTS check_str 
    CHECK order_by_column != 'forbidden_string'
```


<span id="7337862a"></span>
## Delete constraint (**DROP CONSTRAINT**)

Delete constraints in the specified table.

<span id="fa022584"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] DROP CONSTRAINT [IF EXISTS] constraint_name; 
```


When the `IF EXISTS` clause is specified, if the constraint does not exist, the query will not return an error.

<span id="f47d54fa"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table that includes the check_str constraint
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `order_by_column` String,
    `partition_column` Date,
    `browser` String,
    `hour` Int32,
    `x` Int32,
    `p` Int32,
    CONSTRAINT check_str CHECK (`order_by_column` != 'forbidden_string')
)
ENGINE = MergeTree
PARTITION BY partition_column
ORDER BY (`order_by_column`);

-- 4. Delete the check_str constraint
ALTER TABLE sample_db.sample_table DROP CONSTRAINT IF EXISTS check_str
```


<span id="9a11e47f"></span>
# Table settings operations (Settings)

This is a set of operations for changing table settings. You can modify table settings or reset them to their default values, and multiple settings can be changed at the same time in a single query. If the setting with the specified name does not exist, the query will raise an exception.

<span id="480c23c9"></span>
## Grammar

```SQL
ALTER TABLE [db].name MODIFY|RESET SETTING ... 
```


<span id="6f68fcd4"></span>
## Modify settings

Change table settings.

<span id="0f7b6139"></span>
### Grammar

```SQL
MODIFY SETTING setting_name=value [, ...] 
```


<span id="55238452"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `id` UInt32,
    `data` String,
    `partition_col` Date  Add a partition column
)
ENGINE = MergeTree
PARTITION BY partition_col  -- Explicitly specify partition key (number of partition expression fields is 1)
ORDER BY id;

-- 3. Modify table parameter values
ALTER TABLE sample_db.sample_table
    MODIFY SETTING 
        max_part_loading_threads = 8,
        max_parts_in_total = 50000;
```


<span id="5c5e40c9"></span>
## Reset settings

Reset table settings to default values. If the setting is in its default state, the system will not take any action.

<span id="264e8860"></span>
### Grammar

```SQL
RESET SETTING setting_name [, ...] 
```


<span id="7f85f1e4"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete the existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table, and set the max_part_loading_threads parameter to 8
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `id` UInt32,
    `data` String,
    `partition_col` Date  
)
ENGINE = MergeTree
PARTITION BY partition_col  
ORDER BY id
SETTINGS max_part_loading_threads=8;

-- 4. Reset the max_part_loading_threads parameter to the default value
ALTER TABLE sample_db.sample_table
    RESET SETTING max_part_loading_threads;
```


<span id="bd598f85"></span>
# Index operations (INDEX)

ByteHouse supports the following operations. The first two commands are lightweight and only modify metadata or delete files.

<span id="20a61feb"></span>
## Grammar


* Add an index description to table metadata

   ```SQL
   ALTER TABLE [db.]name
       ADD INDEX index_name expression
       TYPE index_type
       GRANULARITY value
       [FIRST | AFTER column_name];
   ```
   

* Delete index descriptions from table metadata and delete index files from disk

   ```SQL
   ALTER TABLE [db].name DROP INDEX name
   ```
   

* Name of the secondary index to be rebuilt in partition partition_name

   ```SQL
   ALTER TABLE [db.]table MATERIALIZE INDEX name IN PARTITION partition_name 
   ```
   


<span id="c413af7a"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a test table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `id` UInt32,
    `data` String,
    `partition_col` Date,
    INDEX idx_data (`data`) TYPE bloom_filter GRANULARITY 4
)
ENGINE = MergeTree
PARTITION BY partition_col
ORDER BY id;

-- 3. Insert test data
INSERT INTO sample_db.sample_table
VALUES 
(1, 'data_20240101', '2024-01-01'),
(2, 'data_20240102', '2024-01-02'),
(3, 'data_20240101', '2024-01-01');

-- 4. Delete indexes
ALTER TABLE sample_db.sample_table 
DROP INDEX IF EXISTS idx_data;

-- 5. Add an index
ALTER TABLE sample_db.sample_table 
ADD INDEX IF NOT EXISTS idx_data_new data 
TYPE bloom_filter 
GRANULARITY 4;

-- 6. Rebuild secondary indexes in partitions
ALTER TABLE sample_db.sample_table MATERIALIZE INDEX idx_data_new IN PARTITION '2024-01-01';
```


<span id="98e2675c"></span>
# TTL operation (TTL)

<span id="6ac6f397"></span>
## Modify TTL

Change the table TTL. TTL clauses must use fields that are part of column partitioning.

<span id="559f6ad8"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] [IF EXISTS] MODIFY [ttlClause];
```



|Parameters |Note |
|---|---|
|[IF EXISTS] |Optional parameter. It ensures no error is reported if the table does not exist (recommended for use in production environments). |
|MODIFY [ttlClause] |TTL expressions must be based on partition fields, such as `date + INTERVAL 30 DAY`. |


<span id="a96d0d92"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete the existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table with a TTL of 1 day
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `d` DateTime
)
ENGINE = `MergeTree`
PARTITION BY d
ORDER BY `d`
TTL d + INTERVAL 1 DAY

-- 4. Change TTL to 2 months
ALTER TABLE sample_db.sample_table
MODIFY TTL d + INTERVAL 2 MONTH;
```


<span id="ff5596c6"></span>
## Remove TTL

Remove the table TTL.

<span id="5f8ed565"></span>
### Grammar

```SQL
ALTER TABLE [tableIdentifier] REMOVE TTL; 
```


<span id="91043111"></span>
### Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table with a TTL of 1 day
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster
(
    `d` DateTime
)
ENGINE = `MergeTree`
PARTITION BY d
ORDER BY d
TTL d + INTERVAL 1 DAY

-- 4. Remove the table TTL
ALTER TABLE sample_db.sample_table
REMOVE TTL
```
