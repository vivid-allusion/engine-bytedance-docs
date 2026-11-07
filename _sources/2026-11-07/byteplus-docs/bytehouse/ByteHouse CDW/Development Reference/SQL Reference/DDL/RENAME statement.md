---
title: "RENAME statement"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/rename-statement"
---

Rename a database, table, or dictionary. Multiple entities can be renamed in a single query.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please note that a <strong><code>RENAME</code></strong> search involving multiple entities is not an atomic operation.</div>


<span id="2a2fd5e5"></span>
### RENAME DATABASE

Rename a database.

**Syntax**

```SQL
RENAME DATABASE atomic_database1 TO atomic_database2 [,...] 
```


<span id="3d18389b"></span>
### RENAME TABLE

Rename one or more tables

Renaming a table is a lightweight operation. If a different database is passed **`after TO`**, the table will be moved to that database. However, the directory that contains the database must be on the same file system. Otherwise, it returns an error. If multiple tables are renamed in one query, the operation is not atomic. It might be partially executed, and other sessions may encounter a **`Table ...`**  **`does not exist ...`**  error.

**Syntax**

```SQL
RENAME TABLE [tableIdentifier] TO [tableIdentifier], [tableIdentifier] TO [tableIdentifier]
```


**Example**

```SQL
-- step 1: create a table
CREATE TABLE `example_table`
(
    `a` Int8,
    `b` String,
    `c` Date
)
ENGINE = `CnchMergeTree`
ORDER BY (`a`)

-- step 2: rename the new created table
RENAME TABLE example_table to new_table_name
```


<span id="c98a9059"></span>
### RENAME DICTIONARY

Rename one or more dictionaries. This query can be used to move dictionaries between databases.

**Grammar**

```SQL
RENAME DICTIONARY [db0.]dict_A TO [db1.]dict_B [,...] 
```
