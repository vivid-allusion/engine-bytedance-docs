---
title: "ATTACH statement (ATTACH)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/attach-statement"
---

Attach a table or dictionary.

**Syntax**

```SQL
ATTACH TABLE|DICTIONARY|DATABASE [IF NOT EXISTS] [db.]name
```


This query does not create data on storage but assumes the data is already at the appropriate location, adding information of the specified table, dictionary, or database to the server. After running the ATTACH query, the server will recognize the existence of the table, dictionary, or database.

If the table was previously detached (DETACH query), meaning its structure is known, a shorthand form can be used without defining the structure.

<span id="e900eb12"></span>
### Attach an existing table

**Syntax**

```SQL
ATTACH TABLE [IF NOT EXISTS] [db.]name 
```


This query is used at server startup. The server stores the metadata of the table in a file that contains the ATTACH query and runs these queries at startup (excluding some system tables which are explicitly created on the server).

If a table is permanently detached, it will not reattach when the server launches, therefore an explicit ATTACH query is necessary.

<span id="b198a1c5"></span>
### Create a new table and attach data

<span id="4810aeeb"></span>
#### Use the specified table data path

This query creates a new table using the provided structure and attaches table data from the directory provided in `user_files`.

**Syntax**

```SQL
ATTACH TABLE name FROM 'path/to/data/' (col1 Type1, ...)
```


**Example**

```SQL
DROP TABLE IF EXISTS test;
INSERT INTO TABLE FUNCTION file('01188_attach/test/data.TSV', 'TSV', 's String, n UInt8') VALUES ('test', 42);
ATTACH TABLE test FROM '01188_attach/test' (s String, n UInt8) ENGINE = File(TSV);
SELECT * FROM test;

┌─s────┬──n─┐
│ test │ 42 │
└──────┴────┘
```


<span id="8efd13ef"></span>
#### Use the specified table UUID

This query creates a new table using the provided structure and attaches the data from the table with the specified UUID. This feature is supported by the Atomic database engine.

**Syntax**

```SQL
ATTACH TABLE name UUID '' (col1 Type1, ...)
```


<span id="53069d34"></span>
### Add to existing dictionary

Add a previously separate dictionary.

**Syntax**

```SQL
ATTACH DICTIONARY [IF NOT EXISTS] [db.]name 
```


<span id="443627ee"></span>
### Attach existing database

Add a previously separate database.

**Syntax**

```SQL
ATTACH DATABASE [IF NOT EXISTS] name [ENGINE=]
```
