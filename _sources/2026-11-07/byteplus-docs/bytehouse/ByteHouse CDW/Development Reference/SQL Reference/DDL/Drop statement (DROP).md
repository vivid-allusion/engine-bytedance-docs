---
title: "Drop statement (DROP)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/drop-statement"
---

<span id="6db5de90"></span>
### Delete database (`DROP DATABASE`)

Delete a database.

**Syntax**

```SQL
DROP DATABASE [IF EXISTS] [databaseIdentifier]
```


**Example**

```SQL
-- create a database
CREATE DATABASE example_db

-- drop a database
DROP DATABASE example_db
```


<span id="e2db8b04"></span>
### Delete Table (`DROP TABLE`)

Delete a table.

**Syntax**

```SQL
DROP TABLE [IF EXISTS] [tableIdentifier]
```


**Example**

```SQL
-- step 1: create a table
CREATE TABLE `example_table`
(
    `order_by_column` String
)
ENGINE = `CnchMergeTree`
ORDER BY (`order_by_column`)

-- step 2: drop a table
DROP TABLE example_table
```


<span id="6b884a54"></span>
### Delete View (`DROP VIEW`)

Delete the view. Views can also be deleted using the `DROP TABLE` command, but `DROP VIEW` checks whether `[db.]name` is a view.

**Syntax**

```SQL
DROP VIEW [IF EXISTS] [db.]name 
```


<span id="fa7c24f7"></span>
### Delete dictionary (`DROP DICTIONARY`)

Delete a dictionary.

**Syntax**

```SQL
DROP DICTIONARY [IF EXISTS] [db.]name
```


<span id="d60589f4"></span>
### TRUNCATE TABLE

Remove all data from a table.

**Syntax**

```SQL
TRUNCATE TABLE [IF EXISTS] [tableIdentifier]
```


**Example**

```SQL
TRUNCATE TABLE IF EXISTS example_table
```


<span id="3b95f029"></span>
### FAQ: Can a table accidentally deleted using DROP TABLE be recovered?

If you accidentally delete a table using `DROP TABLE`, you can restore it using `UNDROP TABLE`. This method is limited to recovering deletions performed by `DROP TABLE`, and its validity period is restricted; currently, it supports recovery of tables deleted within the past two days, and can be used to temporarily stop losses caused by accidental operations. It is strongly recommended that you use the **backup and restore** feature. For details, please refer to [Full backup restore](https://docs.byteplus.com/docs/bytehouse/full-backup-restore).

Example:

```SQL
# drop a table but then realize it was deleted by mistake
DROP TABLE db_name.table_name;

# Restore this table using UNDROP TABLE
UNDROP TABLE db_name.table_name;

# Query data to verify whether the restoration is successful
SELECT count() FROM db_name.table_name;
```


&nbsp;
