---
title: "DROP statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-drop-statement"
---

`DROP` statement can be used to drop databases, tables, views, and dictionaries. ByteHouse also supports removing all data from a table using `TRUNCATE TABLE`.

<span id="4c321e3e"></span>
# Delete a database (`DROP DATABASE`)

Delete the specified database.

<span id="4c818db2"></span>
## **Grammar**

```SQL
DROP DATABASE [IF EXISTS] [databaseIdentifier]
```


<span id="f3db7a11"></span>
## Parameter description


|**Parameters** |**Description** |
|---|---|
|IF EXISTS |* If `IF EXISTS` is specified, the system will return success after executing the delete statement, regardless of whether the target table exists.<br><br>* If `IF EXISTS` is not specified, when the target table does not exist, the system returns an `ERROR: table "non_exist_table" does not exist` error. |
|databaseIdentifier |The name of the table to be deleted. |


<span id="eac4a0cf"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXIST sample_db ON CLUSTER sample_cluster;

-- 2. Delete a database
DROP DATABASE sample_db ON CLUSTER CLUSTER sample_cluster;
```


<span id="9aff1c45"></span>
# Drop a table (`DROP TABLE`)

Delete a specified table.

<span id="60ce7ac9"></span>
## **Grammar**

```SQL
DROP TABLE [IF EXISTS] [tableIdentifier]
```


<span id="d2969e65"></span>
## **Example**

```SQL
-- 1: Create a library
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create tables
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster(
    `order_by_column` String
)
ENGINE = MergeTree
ORDER BY (`order_by_column`);

-- 4. Delete a table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;
```


<span id="ca3c9ec9"></span>
# Delete a view (`DROP VIEW`)

Delete a view.

Difference from `DROP TABLE`:


* Although the `DROP TABLE` command can also be used to delete a view, `DROP VIEW` is the standard and recommended method for deleting views.

* `DROP VIEW` proactively verifies whether the target object (`[db.]name`) is a view before performing the delete operation, in order to prevent errors caused by object type mismatches.

* When using `DROP TABLE` to delete a view, the system does not verify whether the specified object is a view. If the target object is not a view (for example, a table), `DROP TABLE` will directly delete the specified object. If the target object does not exist, an error will be reported.


<span id="648a547c"></span>
## **Grammar**

```SQL
DROP VIEW [IF EXISTS] [db.]name 
```


<span id="f7c3b419"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2: Delete an existing table
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3: Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster(
    `order_by_column` String
)
ENGINE = MergeTree
ORDER BY (`order_by_column`);

-- 4: Create a view
CREATE VIEW sample_view AS SELECT * FROM sample_db.sample_table

-- 5. Delete a view
DROP VIEW IF EXISTS sample_view ON CLUSTER sample_cluster
```


<span id="55987e75"></span>
# Delete a dictionary (`DROP DICTIONARY`)

Delete dictionaries.

<span id="95cd9856"></span>
## **Grammar**

```SQL
DROP DICTIONARY [IF EXISTS] [db.]name
```


<span id="547c8501"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a dictionary
CREATE DICTIONARY IF NOT EXISTS sample_db.sample_dict ON CLUSTER sample_cluster (
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

-- 3. Delete a dictionary
DROP DICTIONARY IF EXISTS sample_db.sample_dict ON CLUSTER sample_cluster;
```


<span id="7e1a2cdd"></span>
# TRUNCATE TABLE

Remove all data from a table.

<span id="c0bcc45e"></span>
## **Grammar**

```SQL
TRUNCATE TABLE [IF EXISTS] [tableIdentifier]
```


<span id="6413ab03"></span>
## **Example**

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Delete existing tables
DROP TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 3. Create a table
CREATE TABLE IF NOT EXISTS sample_db.sample_table ON CLUSTER sample_cluster(
    `order_by_column` String
)
ENGINE = MergeTree
ORDER BY (`order_by_column`);

-- 4. Insert data
INSERT INTO sample_db.sample_table VALUES ('data_1'), ('data_2'), ('data_3');

-- 5. Verify data insertion
SELECT * FROM sample_db.sample_table;

-- 6. Remove all data from the sample_table table
TRUNCATE TABLE IF EXISTS sample_db.sample_table ON CLUSTER sample_cluster;

-- 7. Verification data has been cleared
SELECT count(*) FROM sample_db.sample_table;
```
