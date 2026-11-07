---
title: "DETACH statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-detach-statement"
---

`DETACH` statement is used to detach tables, materialized views, dictionaries, or databases from the server. It does not delete their data or metadata.

<span id="dc8b50d5"></span>
## **Grammar**

```SQL
DETACH TABLE|VIEW|DICTIONARY|DATABASE [IF EXISTS] [db.]name  [PERMANENTLY] [SYNC] 
```


After running the separation actions, the impact on data is as follows:


1. **Temporary separation** (Default): When the server restarts, it will automatically reload metadata and recognize entities.

2. **Permanent separation** (`PERMANENTLY`): After a server restart, it will not be automatically recognized; you must manually execute `ATTACH` to reattach.

3. **All separated entities**, whether or not permanently separated, can be reattached using the `ATTACH` statement. System log tables, such as query_log, text_log, and others, can also be reattached, but other system tables do not support reattachment.

4. After performing the temporary separation operation, tables in the separated state cannot be permanently separated directly. You must first perform `ATTACH` to reattach them; only then can you perform the permanent separation operation.

5. **Limitations**:

   * Permanently separated tables will prevent creating tables with the same name or performing `RENAME` operations.

   * You cannot delete a separated table directly or permanently separate it; you must reattach it first.


<span id="47b1b803"></span>
## Parameter description


|Param |Required |Meaning and role |
|---|---|---|
|TABLE |VIEW |DICTIONARY |
|IF EXISTS |No |When the object does not exist, no error is reported, and the operation is skipped. |
|[db.]name |Yes |Specify the database (optional) to which the object belongs, and its name. Use the current database when no database is specified. |
|PERMANENTLY |No |Permanent separation of entities. Metadata will not be automatically restored after a server restart.<br><br>Completely remove metadata (including table structure, privileges, and others). Only physical data will be retained. After the server restarts, metadata will not be automatically restored; manual rebuilding is required. |
|SYNC |No |Immediately run actions synchronously; if not specified, the default is asynchronous. |


<span id="653becd6"></span>
## **Example**


1. Create a table.

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
   
   -- 4. Search data in the table
   SELECT * FROM sample_db.sample_detach;
   
   ┌─number─┐
   │      0  │
   │      1  │
   │      2  │
   │      3  │
   │      4  │
   │      5  │
   │      6  │
   │      7  │
   │      8  │
   │      9  │
   └─────┘
   ```
   

2. Extract a table and search it.

   ```SQL
   DETACH TABLE sample_db.sample_detach;
   
   SELECT * FROM sample_db.sample_detach; 
   ```
   

   The output result is as follows, indicating that the table has been detached:

   ```Plain
   Code: 60, e.displayText() = DB::Exception: Table sample_db.sample_detach doesn't exist SQLSTATE: 42P01 (version 21.9.1)
   ```
