---
title: "UUID function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-uuid"
---

<span id="b74e330e"></span>
### generateUUIDv4

Generate [version 4](https://tools.ietf.org/html/rfc4122#section-4.4) UUID.

**Syntax**

```SQL
generateUUIDv4()
```


**Return value**


* UUID type value.


**Example**

This example demonstrates how to create a table with a UUID type column and insert values into it.

```SQL
CREATE TABLE test.functionGenerateUUIDv4 (x UUID) ENGINE=CnchMergeTree ORDER BY x;
INSERT INTO test.functionGenerateUUIDv4 SELECT generateUUIDv4();
SELECT * FROM test.functionGenerateUUIDv4;
```


```Plain
┌─x────────────────────────────────────┐
│ a630fbcb-1a32-4902-b5cc-dd51eba8cf4b │
└──────────────────────────────────────┘
```


<span id="1fb96f38"></span>
### toUUID

Converts a string type value to a UUID type. If the input string is in an invalid UUID format, an exception will be raised.

**Syntax**

```SQL
toUUID(String)
```


**Param**


* `String`— a string in UUID format.


**Return Value**


* UUID Type value.


**Example**

```SQL
SELECT toUUID('61f0c404-5cb3-11e7-907b-a6006ad3dba0') AS uuid, toTypeName(uuid) AS uuid_type;
```


```Plain
┌─uuid─────────────────────────────────┬─uuid_type─┐
│ 61f0c404-5cb3-11e7-907b-a6006ad3dba0 │ UUID      │
└──────────────────────────────────────┴───────────┘
```


<span id="e756d6b8"></span>
### toUUIDOrNull

It accepts a String type parameter and attempts to parse it into a UUID. If it fails, it returns NULL.

**Syntax**

```SQL
toUUIDOrNull(String)
```


**Param**


* `String`— a string in uuid format.


**Return value**


* Nullable(UUID) type value.


**Example**

```SQL
SELECT toUUIDOrNull('61f0c404-5cb3-11e7-907b-a6006ad3dba0T') AS uuid
```


```Plain
┌─uuid─┐
│ ᴺᵁᴸᴸ │
└──────┘
```


<span id="166d3a19"></span>
### toUUIDOrZero

It accepts a String type parameter and attempts to parse it into a UUID. If it fails, it returns a zero UUID.

**Syntax**

```SQL
toUUIDOrZero(String)
```


**Param**


* `String`— UUID Format string.


**Return Value**


* UUID Type Value.


**Example**

```SQL
SELECT toUUIDOrZero('61f0c404-5cb3-11e7-907b-a6006ad3dba0T') AS uuid
```


```Plain
┌─uuid─────────────────────────────────┐
│ 00000000-0000-0000-0000-000000000000 │
└──────────────────────────────────────┘
```
