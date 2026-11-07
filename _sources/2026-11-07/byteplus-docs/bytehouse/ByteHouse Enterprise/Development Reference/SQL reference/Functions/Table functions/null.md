---
title: "null"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/null-function"
---

Use Null table engine to create a temporary table with a specific structure. According to the properties of the `Null` engine, the table data will be ignored, and the table itself will be deleted immediately after the query is executed. This function is used to facilitate testing, writing, and demonstration.
**Syntax**
```SQL
null('structure')
```

**Parameters**

* `Structure` — List of columns and their types. String.

**Return value**
Temporary `Null` engine table with the specified structure.
**Example**
Use the `null` function in searches
```SQL
INSERT INTO function null('x UInt64') SELECT * FROM numbers_mt(1000000000);
```

Can replace three searches
```SQL
CREATE TABLE t (x UInt64) ENGINE = Null;
INSERT INTO t SELECT * FROM numbers_mt(1000000000);
DROP TABLE IF EXISTS t;
```
