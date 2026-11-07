---
title: "DETACH statement (DETACH)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/detach-statement"
---

Detaches a table, materialized view, dictionary, or database.

**Syntax**

```SQL
DETACH TABLE|VIEW|DICTIONARY|DATABASE [IF EXISTS] [db.]name  [PERMANENTLY] [SYNC]
```


Detaching does not delete the data or metadata of the table, materialized view, dictionary, or database. If the entity is not permanently detached, the server will read the metadata and recognize the table/view/dictionary/database again at the next server launch. If the entity is permanently detached, it will not be automatically recognized again.

Whether the table, dictionary, or database is permanently detached or not, they can be reattached using the ATTACH query. System log tables (such as query_log, text_log, etc.) can also be reattached. Other system tables cannot be reattached. At the next server launch, the server will recognize these tables again.

Please note that a table that has been temporarily separated cannot be permanently separated. But you can reattach it first and then permanently separate it again.

Furthermore, you cannot delete a detached table, nor can you create a table with the same name as a permanently detached table, or replace it with another table using the RENAME TABLE query.

SYNC modifier performs the action immediately.

**Example**

Create a table:

```SQL
CREATE TABLE db1.test (i Int64) ENGINE = CnchMergeTree() ORDER BY i 
INSERT INTO db1.test  SELECT number FROM numbers(10);
SELECT * FROM db1.test;

┌─number─┐
│      0 │
│      1 │
│      2 │
│      3 │
│      4 │
│      5 │
│      6 │
│      7 │
│      8 │
│      9 │
└────────┘
```


**Detach a table**

Query statement:

```SQL
DETACH TABLE test;
SELECT * FROM test;
```


Result:

```Plain
Received exception from server (version 21.4.1):
Code: 60. DB::Exception: Received from localhost:9000. DB::Exception: Table default.test does not exist.
```
