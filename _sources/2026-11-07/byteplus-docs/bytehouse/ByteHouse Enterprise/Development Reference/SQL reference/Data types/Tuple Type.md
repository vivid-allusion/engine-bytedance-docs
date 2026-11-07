---
title: "Tuple Type"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/tuple-type"
---

<span id="Tuple(T1, T2, …) {#tuplet1-t2}"></span>
# Tuple(T1, T2, …)
A tuple where each element has its own Type.
Tuples cannot be stored in tables (except in-memory tables). They can be used for temporary column grouping. In the query, the IN Expression and lambda functions with specific Params can be used to group by temporary Columns.
Tuples can be the result of a query. In this case, for text formats other than JSON, the values in the parentheses are separated by commas. In Json format, tuples are output as arrays (in square brackets).
<span id="创建元组 {#chuang-jian-yuan-zu}"></span>
## Create tuple
Tuples can be created using functions:
```Plain
tuple(T1, T2, ...)
```

Example of creating a tuple:
```sql
SELECT tuple(1,'a') AS x, toTypeName(x)
```

```response
┌─x───────┬─toTypeName(tuple(1, 'a'))─┐
│ (1,'a') │ Tuple(UInt8, String)      │
└─────────┴───────────────────────────┘
```

<span id="元组中的数据类型 {#yuan-zu-zhong-de-shu-ju-lei-xing}"></span>
## Data type in the tuple
When dynamically creating a tuple, ByteHouse automatically assigns the smallest expressible type to each parameter of the tuple. If the parameter is NULL, then this tuple element is nullable.
Automatic data type detection example:
```sql
SELECT tuple(1, NULL) AS x, toTypeName(x)
```

```response
┌─x────────┬─toTypeName(tuple(1, NULL))──────┐
│ (1,NULL) │ Tuple(UInt8, Nullable(Nothing)) │
└──────────┴─────────────────────────────────┘
```
