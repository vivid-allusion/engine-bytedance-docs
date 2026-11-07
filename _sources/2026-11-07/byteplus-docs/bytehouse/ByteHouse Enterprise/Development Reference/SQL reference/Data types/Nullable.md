---
title: "Nullable"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/nullable"
---

<span id="可为空（类型名称) {#data_type-nullable}"></span>
# Can be null: Nullable
Allows the use of special markers (NULL) to represent "missing values," which can be stored together with the normal values of `TypeName`. For example, a column of type `Nullable(Int8)` can store values of type `Int8`, and rows without values will store `NULL`.
For `TypeName`, composite data types such as Array and Tuple cannot be used. Composite data types can contain values of type `Nullable`, for example, `Array(Nullable(Int8))`.
Fields of type `Nullable` cannot be included in table indexes.
Unless otherwise stated in the ClickHouse server configuration, `NULL` is the default value for any `Nullable` type.
<span id="存储特性 {#cun-chu-te-xing}"></span>
## Storage Characteristics
To store values of type `Nullable` in the columns of a table, ClickHouse uses not only normal files with values but also separate files with a `NULL` mask. Entries in the mask file allow ClickHouse to distinguish between NULL and the default value for each row `of data type`. Because new files are attached, `Nullable` columns consume additional storage space compared with similar normal files.
!!! Advisory point "Advisory point"
Using `Nullable` almost always has a negative impact on performance, keep this in mind when designing databases.
Entries in the mask file allow ClickHouse to distinguish between the corresponding data type's «NULL» and default values as there are extra files, «Nullable» columns consume more storage space than normal columns.
<span id="用法示例 {#yong-fa-shi-li}"></span>
## Usage Example
```sql
CREATE TABLE t_null(x Int8, y Nullable(Int8)) ENGINE TinyLog
```

```sql
INSERT INTO t_null VALUES (1, NULL), (2, 3)
```

```sql
SELECT x + y FROM t_null
```

```text
┌─plus(x, y)─┐
│       ᴺᵁᴸᴸ │
│          5 │
└────────────┘
```
