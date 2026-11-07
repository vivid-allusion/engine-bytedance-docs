---
title: "UUID Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/uuid-function"
---

List of all UUID-related functions
<span id="generateuidv4"></span>
## generateuidv4
Generate a UUID [(Version 4)](https://tools.ietf.org/html/rfc4122#section-4.4).
generateUUIDv4()
Return value
Value of UUID Type.
Usage example
This example demonstrates how to create a column of UUID Type in a table and write data to it.
```SQL
:) CREATE TABLE t_uuid (x UUID) ENGINE=TinyLog :) INSERT INTO t_uuid SELECT generateUUIDv4() :) SELECT * FROM t_uuid 
┌────────────────────────────────────x─┐ 
│ f4bf890f-f9dc-4332-ad5c-0c18e73f28e9 │ 
└──────────────────────────────────────┘
```


<span id="touuid-x-touuid-x"></span>
## toUUID(x) {#touuid-x}
Convert the value of the String Type to a UUID Type.
toUUID(String)
Return value
Value of UUID Type
Usage example
```SQL
:) SELECT toUUID('61f0c404-5cb3-11e7-907b-a6006ad3dba0') AS uuid 
┌─────────────────────────────────uuid─┐ 
│ 61f0c404-5cb3-11e7-907b-a6006ad3dba0 │ 
└──────────────────────────────────────┘
```

<span id="uuidstringtonum"></span>
## UUIDStringToNum
Accepts a String Type value containing 36 characters in the format `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`, converts it to a UUID numerical value and returns it as a [Fixed String(16)](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/en/sql-reference/functions/uuid-functions.md).
UUIDStringToNum(String)
Return value
Fixed string (16)
Usage example
```SQL
:) SELECT'612f3c40-5d3b-217e-707b-6a546a3d7b29' AS uuid, UUIDStringToNum(uuid) AS bytes 
┌─uuid─────────────────────────────────┬─bytes────────────┐ 
│ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │ a/<@];!~p{jTj={) │ 
└──────────────────────────────────────┴──────────────────┘
```

<span id="uuidnumtostring"></span>
## UUIDNumToString
Accepts a [fixed string (16)](https://github.com/ClickHouse/ClickHouse/blob/21.8/docs/zh/sql-reference/functions/uuid-functions.md) type value and returns its corresponding String representation.
UUIDNumToString(FixedString(16))
Return value
String.
Usage example
```SQL
SELECT'a/<@];!~p{jTj={)' AS bytes, UUIDNumToString(toFixedString(bytes, 16)) AS uuid 
┌─bytes────────────┬─uuid─────────────────────────────────┐ 
│ a/<@];!~p{jTj={) │ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │ 
└──────────────────┴──────────────────────────────────────┘
```
