---
title: "RENAME statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-rename-statement"
---

`RENAME` statements can be used to rename databases, tables, or dictionaries, and support renaming multiple entities in a single query.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A <code>RENAME</code> query with multiple entities is a non\-atomic operation.</div>


<span id="0d095caf"></span>
# RENAME DATABASE

Alias database.

<span id="d8c0488d"></span>
## **Grammar**

```SQL
RENAME DATABASE [databaseIdentifier] TO [databaseIdentifier2] [,...] 
```


<span id="b7f2341e"></span>
## Example

```SQL
-- You can modify the cluster and database name, i.e. sample_cluster,sample_db according to your need
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. If the target database sample1 exists，delete the existing database first to avoid conflict
DROP DATABASE IF EXISTS sample_db1 ON CLUSTER sample_cluster;

-- 3. Rename the name of the database from sampel _db to sample_db1
RENAME DATABASE sample_db to sample_db1 ON CLUSTER sample_cluster;
```


<span id="5256b73b"></span>
# RENAME TABLE

Rename one or more tables.

Renaming a table is a lightweight operation. If a different database name is specified in the `TO` clause, the table will be moved to the target database. However, the storage directories of the source database and the target database must be located within the same file system; otherwise, the operation will fail and return an error.

When renaming multiple tables at the same time in a `RENAME TABLE` statement, this operation is not atomic. Actions may be partially successful. If the operation is interrupted during execution, only some tables will be successfully renamed or moved. When querying in other sessions for tables that are being renamed, you may encounter `Table ... does not exist ...` or similar errors, until all renaming operations are complete.

<span id="4fab82ad"></span>
## **Grammar**

```SQL
RENAME TABLE
  [tableIdentifier] TO [tableIdentifier],
  [tableIdentifier] TO [tableIdentifier];
```


<span id="ba6f11e8"></span>
## **Example**

```SQL
-- Modify sample_cluster,sample_db,sample_table,sample_table_local in the example according to the actual situation
-- Purpose: Rename the table sample_db.sample_table to sample_db.sample_table01
-- 1. Create database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create tables
-- local table
CREATE TABLE IF NOT EXISTS
  `sample_db`.`sample_table_local`
  ON CLUSTER sample_cluster(`k1` String NOT NULL) ENGINE = HaMergeTree
ORDER BY
  (k1)
SETTINGS
  index_granularity = 8192;

-- distributed table
CREATE TABLE IF NOT EXISTS
  `sample_db`.`sample_table`
  ON CLUSTER sample_cluster AS `sample_db`.`sample_table_local` ENGINE = Distributed(
    'sample_cluster',
    'sample_db',
    'sample_table_local',
    rand()
  );

-- 3. Rename the local table sample_table_local to sample_table01_local

RENAME TABLE sample_db.sample_table_local to sample_db.sample_table01_local ON CLUSTER sample_cluster;

-- 4. Create a new distributed table sample_table01 (The distributed table does not actually store data, the local table mapped by the new table is sample_table01_local)
DROP TABLE sample_db.sample_table ON CLUSTER sample_cluster;

-- Create new distributed table
CREATE TABLE IF NOT EXISTS
  `sample_db`.`sample_table01`
  ON CLUSTER sample_cluster AS `sample_db`.`sample_table01_local` ENGINE = Distributed(
    'sample_cluster',
    'sample_db',
    'sample_table01_local',
    rand()
  );
```


<span id="39e9c053"></span>
# RENAME DICTIONARY

Rename one or more dictionaries. This query can be used to move dictionaries between databases.

<span id="95c8793d"></span>
## **Grammar**

```SQL
RENAME DICTIONARY
  [databaseIdentifier.]dict_name TO [databaseIdentifier.]dict_name
  [, ...];
```


<span id="12a4752a"></span>
## Example


* Rename a single dictionary

   Rename the dictionary `dict_A` in the `db0` Database to `dict_B` in the `db1` Database:

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
   
   -- 3. If the target dictionary new_sample_dict already exists, delete it first to avoid renaming conflicts
   DROP DICTIONARY IF EXISTS sample_db.new_sample_dict;
   
   -- 4. Rename dictionary
   RENAME DICTIONARY sample_db.sample_dict TO sample_db.new_sample_dict;
   ```
   

* Rename multiple dictionaries

   Rename `dict_A` in `db0` to `db1.dict_B`, and at the same time rename `dict_C` in `db2` to `db2.dict_D`:

   ```SQL
   -- 1. Create a database
   CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;
   
   -- 2. Create Dictionary 1
   CREATE DICTIONARY IF NOT EXISTS sample_db.sample_dict1 ON CLUSTER sample_cluster (
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
   
   -- 3. Create dictionary 2
   CREATE DICTIONARY IF NOT EXISTS sample_db.sample_dict2 ON CLUSTER sample_cluster (
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
   
   -- 4. If the target dictionary new_sample_dict already exists, delete it first to avoid renaming conflicts
   DROP DICTIONARY IF EXISTS sample_db.new_sample_dict1;
   DROP DICTIONARY IF EXISTS sample_db.new_sample_dict2;
   
   -- 5. Rename multiple dictionaries
   RENAME DICTIONARY 
      sample_db.sample_dict1 TO sample_db.new_sample_dict1, 
      sample_db.sample_dict2 TO sample_db.new_sample_dict2;
   ```
