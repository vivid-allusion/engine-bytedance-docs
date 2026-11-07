---
title: "ATTACH statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-attach-statement"
---

`ATTACH` statement can be used to attach tables or dictionaries, and is applicable to scenarios such as migrating a database to another server.

<span id="fe28e7ea"></span>
# **Grammar**

```SQL
ATTACH TABLE|DICTIONARY|DATABASE [IF NOT EXISTS] [db.]name 
```


This query does not create data on storage; instead, it assumes that the data is already in the appropriate location and only adds information about the specified table, dictionary, or database to the server. After executing the `ATTACH` query, the server will recognize the existence of tables, dictionaries, or databases.

If the table has previously been detached (DETACH query), meaning its structure is already known, you can use the shorthand form without defining the structure.

<span id="500fbcfb"></span>
# Attach a table to an existing table

`ATTACH TABLE` statements explicitly register table metadata for existing data files and are mainly used in two scenarios:


1. **When the server starts**: The server stores table metadata as files containing `ATTACH` queries, and executes these queries during startup. Certain system tables are explicitly created on the server.

2. **Permanent separation recovery**: If a table is permanently separated, you can manually reattach the table that was permanently separated using the `ATTACH TABLE` statement.


<span id="97d9f8cc"></span>
## **Grammar**

```SQL
ATTACH TABLE [IF NOT EXISTS] [db.]name  
```


<span id="441dfc5a"></span>
## Example

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Create a table
DROP TABLE IF EXISTS sample_db.sample_detach ON CLUSTER sample_cluster;
CREATE TABLE sample_db.sample_detach ON CLUSTER sample_cluster (
  id Int64
) 
ENGINE = MergeTree() 
ORDER BY id;

-- 3. Insert test data
INSERT INTO sample_db.sample_detach SELECT number FROM numbers(10);

-- 4. Query data in the table
SELECT * FROM sample_db.sample_detach;

-- 5. Separate the table
DETACH TABLE sample_db.sample_detach;

-- 6. At this point, querying returns an error indicating that the table does not exist
SELECT * FROM sample_db.sample_detach; 

-- 7. Additional tables
ATTACH TABLE sample_db.sample_detach;

-- 8. Verify the attached table; if there is a result, it indicates successful attachment
SELECT * FROM sample_db.sample_detach; 
```


<span id="5d9ceb79"></span>
# Create a new table and attach data

<span id="73e1ddd6"></span>
## Use the specified table data path

This query creates a new table using the provided structure and appends table data from the directory provided in `user_files`.

<span id="e001060a"></span>
### **Grammar**

```SQL
ATTACH TABLE name FROM 'path/to/data/' (col1 Type1, ...) 
```


<span id="5259ceae"></span>
### Parameter description


|Parameters |Required |Note |
|---|---|---|
|FROM 'path/to/data/' |Yes |The data path under the `user_files` directory. The path must already exist and contain data files. |
|(col1 Type1, ...) |Yes |The table structure definition must match the data file format. |


<span id="8f95c680"></span>
### **Example**

The complete workflow example is as follows:

```SQL
-- 1. Create a database
CREATE DATABASE IF NOT EXISTS sample_db ON CLUSTER sample_cluster;

-- 2. Prepare test data (use a table function to write to a file)
DROP TABLE IF EXISTS sample_db.attach_from_path ON CLUSTER sample_cluster;
INSERT INTO TABLE FUNCTION file(
    '/data00/clickhouse/data/user_files/attach_test/data.TSV', 
    'TSV', 
    's String, n UInt64'
) 
VALUES ('x', 100);

-- 3. Verify whether the file exists (by attempting to read the file contents)
SELECT *
FROM file(
    '/data00/clickhouse/data/user_files/attach_test/data.TSV',  The complete file path
    'TSV',
    's String, n Int64'
)
LIMIT 1;  -- If a result is returned, it indicates that the file exists and is readable.

-- 4. Create a table structure and attach existing data
ATTACH TABLE sample_db.attach_from_path
FROM '/data00/clickhouse/data/user_files/attach_test' 
(
    s String, 
    n UInt64
) 
ENGINE = File(TSV);

-- 5. Query additional data in real time
SELECT * FROM sample_db.attach_from_path;
```


**Output result**

```SQL
┌─s────┬──n─┐
│ x        │ 100  │
└──────┴───┘
```


<span id="32fa8d44"></span>
# Attach a dictionary to an existing dictionary

Attach a previously separated dictionary.

<span id="a2381127"></span>
## **Grammar**

```SQL
ATTACH DICTIONARY [IF NOT EXISTS] [db.]name 
```


<span id="72df8ebc"></span>
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

-- 3. Separate dictionaries
DETACH DICTIONARY sample_db.sample_dict;

-- 4. Verify dictionary separation (no result)
SHOW DICTIONARIES LIKE 'sample_db.sample_dict';

-- 5. Attach the  dictionary
ATTACH DICTIONARY IF NOT EXISTS sample_db.sample_dict;

-- 6. Verify the additional dictionary, if a result is returned, it indicates success
SHOW DICTIONARIES LIKE 'sample_db.sample_dict';
```


<span id="8f53cdb7"></span>
# Add a database to an existing database

Attach a previously detached database.

<span id="2d20c897"></span>
## **Grammar**

```SQL
ATTACH DATABASE [IF NOT EXISTS] name [ENGINE=]
```


<span id="b94c8ecf"></span>
## Example

```SQL
-- 1. Create an Ordinary engine database
CREATE DATABASE IF NOT EXISTS sample_db ENGINE = Ordinary;

-- 2. Separate the database
DETACH DATABASE sample_db;

-- 3. Attach the database
ATTACH DATABASE sample_db ENGINE = Ordinary; 
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After detaching a database, if you reattach it, you must ensure that the specified database engine type is the same both before and after detaching. If the engine type is different, it will result in previously created databases and tables being unable to be deleted.</div>
