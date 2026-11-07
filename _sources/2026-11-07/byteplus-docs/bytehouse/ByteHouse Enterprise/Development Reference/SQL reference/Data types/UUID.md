---
title: "UUID"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/uuid"
---

UUID, a 16-byte number, is used for identifying records. For more details on UUID, see [Wikipedia](https://en.wikipedia.org/wiki/Universally_unique_identifier).
The examples are as follows:
```Plain
61f0c404-5cb3-11e7-907b-a6006ad3dba0
```

If the value of the UUID column is not specified when inserting a new record, the UUID value will be filled with zero:
```Plain
00000000-0000-0000-0000-000000000000
```

<span id="7367cdfb"></span>
## How to generate
To generate a UUID value, ClickHouse offers the generateuidv4 function.
<span id="023d6c62"></span>
## Usage example
**Example 1**
This example demonstrates creating a table with a UUID type column and inserting a value into the table.
```SQL
CREATE TABLE t_uuid (x UUID, y String) ENGINE=TinyLog
```

```SQL
INSERT INTO t_uuid SELECT generateUUIDv4(), 'Example 1'
```

```SQL
SELECT * FROM t_uuid
```

```Plain
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
└──────────────────────────────────────┴───────────┘
```

**Example 2**
In this example, the value for the UUID column wasn't specified when inserting a new record.
```SQL
INSERT INTO t_uuid (y) VALUES ('Example 2')
```

```SQL
SELECT * FROM t_uuid
```

```Plain
┌────────────────────────────────────x─┬─y─────────┐
│ 417ddc5d-e556-4d27-95dd-a34d84e46a50 │ Example 1 │
│ 00000000-0000-0000-0000-000000000000 │ Example 2 │
└──────────────────────────────────────┴───────────┘
```

<span id="92084ae1"></span>
## Restrictions
The UUID data type only supports functions (such as Min, Max, and count) that the String data type also supports.
Arithmetic operations and Aggregate functions such as sum and avg do not support the UUID data type (for example, abs).
