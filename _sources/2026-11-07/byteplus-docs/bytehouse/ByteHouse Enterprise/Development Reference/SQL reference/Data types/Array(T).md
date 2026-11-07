---
title: "Array(T)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/arrayt"
---

Composed of elements of type `T`.
`T` can be any type, including arrays. However, multidimensional arrays are not recommended, as ByteHouse's support for them is limited. For example, multidimensional arrays cannot be stored in `MergeTree` tables.
<span id="创建数组 {#chuang-jian-shu-zu}"></span>
## Create array
You can use the array function to create an array:
```Plain
array(T)
```

You can also use square brackets:
```Plain
[]
```

Array creation example:
```sql
SELECT array(1, 2) AS x, toTypeName(x)
```

```response
┌─x─────┬─toTypeName(array(1, 2))─┐
│ [1,2] │ Array(UInt8)            │
└───────┴─────────────────────────┘
```

```sql
SELECT [1, 2] AS x, toTypeName(x)
```

```response
┌─x─────┬─toTypeName([1, 2])─┐
│ [1,2] │ Array(UInt8)       │
└───────┴────────────────────┘
```

<span id="使用数据类型 {#shi-yong-shu-ju-lei-xing}"></span>
## Using data types
ByteHouse automatically detects array elements and calculates the smallest data type needed to store these elements. If there are NULL elements or elements of Nullable type within the array, the array's element type will become Nullable.
If ByteHouse is unable to determine the data type, it will generate an exception. This occurs when attempting to create an array containing both strings and numbers (`SELECT array(1, 'a')`).
Example of automatic data type detection:
```sql
SELECT array(1, 2, NULL) AS x, toTypeName(x)
```

```response
┌─x──────────┬─toTypeName(array(1, 2, NULL))─┐
│ [1,2,NULL] │ Array(Nullable(UInt8))        │
└────────────┴───────────────────────────────┘
```

If you try to create an array with incompatible data types, ByteHouse will raise an exception.
```sql
SELECT array(1, 'a')
```

```response
Received exception from server (version 1.1.54388):
Code: 386. DB::Exception: Received from localhost:9000, 127.0.0.1. DB::Exception: There is no supertype for types UInt8, String because some of them are String/FixedString and some of them are not.
```
