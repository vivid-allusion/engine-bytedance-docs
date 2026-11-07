---
title: "EXISTS statement (EXISTS)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/exists-statement"
---

Returns a single `UInt8` type column that contains a `0` value if the table or database does not exist, or a `1` value if the table exists in the specified database.

**Syntax**

```SQL
EXISTS [TEMPORARY] [TABLE|DICTIONARY] [db.]name
```


**Example**

```SQL
exists table db1.describe_example
```
