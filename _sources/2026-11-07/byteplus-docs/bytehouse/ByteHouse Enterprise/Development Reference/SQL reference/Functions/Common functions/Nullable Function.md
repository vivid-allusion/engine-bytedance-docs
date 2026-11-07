---
title: "Nullable Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/nullable-function"
---

<span id="isnull"></span>
## isNull
Check if the parameter is NULL.
```plaintext
isNull(x)
```

Param

* `x` — A non-composite data type value.

Return Value

* `1` if `x` is `NULL`.
* `0` if `x` is not `NULL`.

Example
Table with the following content
```plaintext
┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │    3 │
└───┴──────┘
```

I conduct a search
```plaintext
:) SELECT x FROM t_null WHERE isNull(y)

SELECT x
FROM t_null
WHERE isNull(y)

┌─x─┐
│ 1 │
└───┘

1 rows in set. Elapsed: 0.010 sec.
```

<span id="isnotnull"></span>
## isNotNull
Check if the parameter is not NULL.
```plaintext
isNotNull(x)
```

Parameter:

* `x` — A non-composite data type value.

Return value

* `0` if `x` is `NULL`.
* `1` if `x` is not `NULL`.

Example
Table with the following contents
```plaintext
┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │    3 │
└───┴──────┘
```

Perform a search
```plaintext
:) SELECT x FROM t_null WHERE isNotNull(y)

SELECT x
FROM t_null
WHERE isNotNull(y)

┌─x─┐
│ 2 │
└───┘

1 rows in set. Elapsed: 0.010 sec.
```

<span id="合并"></span>
## Merge
Check whether a 'NULL' parameter was passed from left to right and return the first non-`'NULL` parameter.
```plaintext
coalesce(x,...)
```

Parameter:

* Any number of non-composite type parameters. All parameters must be compatible with the data type.

Return Value

* The first non-'NULL' parameter.
* `NULL`, if all parameters are 'NULL'.

Example
Consider a contact list that allows specifying multiple methods to contact customers.
```plaintext
┌─name─────┬─mail─┬─phone─────┬──icq─┐
│ client 1 │ ᴺᵁᴸᴸ │ 123-45-67 │  123 │
│ client 2 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ      │ ᴺᵁᴸᴸ │
└──────────┴──────┴───────────┴──────┘
```

`Mail` and `phone` fields are of String type, but `icq` field is `UInt32`, so it needs to be converted to `String`.
Retrieve the first available contact method from the contact list:
```plaintext
:) SELECT coalesce(mail, phone, CAST(icq,'Nullable(String)')) FROM aBook

SELECT coalesce(mail, phone, CAST(icq, 'Nullable(String)'))
FROM aBook

┌─name─────┬─coalesce(mail, phone, CAST(icq, 'Nullable(String)'))─┐
│ client 1 │ 123-45-67                                            │
│ client 2 │ ᴺᵁᴸᴸ                                                 │
└──────────┴──────────────────────────────────────────────────────┘

2 rows in set. Elapsed: 0.006 sec.
```

<span id="ifnull"></span>
## ifNull
If the first parameter is 'NULL', then it returns the value of the second parameter.
```plaintext
ifNull(x,alt)
```

Parameters:

* `x` — the value to check for 'NULL'.
* `alt` — the value returned by the function if `x` is 'NULL'.

Return value

* Value `x` if `x` is not `NULL`.
* Value `alt`, if `x` is `NULL`.

Example
```plaintext
SELECT ifNull('a', 'b')

┌─ifNull('a', 'b')─┐
│ a                │
└──────────────────┘

SELECT ifNull(NULL, 'b')

┌─ifNull(NULL, 'b')─┐
│ b                 │
└───────────────────┘
```

<span id="nullif"></span>
## nullIf
If the parameters are equal, then returns `NULL`.
```plaintext
nullIf(x, y)
```

Param:
`x`, `y` — values for comparison. They must be type compatible, otherwise an exception will be thrown.
Return value

* If the parameters are equal, the return is `NULL`.
* If the parameters are not equal, the return is the `x` value.

Example
```plaintext
SELECT nullIf(1, 1)

┌─nullIf(1, 1)─┐
│         ᴺᵁᴸᴸ │
└──────────────┘

SELECT nullIf(1, 2)

┌─nullIf(1, 2)─┐
│            1 │
└──────────────┘
```

<span id="assumenotnull"></span>
## assumeNotNull
Convert a value of a nullable type to a non-`Nullable` type.
```plaintext
assumeNotNull(x)
```

Parameter:

* `x` — the raw value.

Return value

* If `x` is not `NULL`, return the non-`Nullable` raw value.
* If `x` is `NULL`, return the default value for the non-`Nullable` type.

Example
The following `t_null` table exists.
```plaintext
SHOW CREATE TABLE t_null

┌─statement─────────────────────────────────────────────────────────────────┐
│ CREATE TABLE default.t_null ( x Int8,  y Nullable(Int8)) ENGINE = TinyLog │
└───────────────────────────────────────────────────────────────────────────┘

┌─x─┬────y─┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │    3 │
└───┴──────┘
```

Use column `y` as a parameter for the `assumeNotNull` function.
```plaintext
SELECT assumeNotNull(y) FROM t_null

┌─assumeNotNull(y)─┐
│                0 │
│                3 │
└──────────────────┘

SELECT toTypeName(assumeNotNull(y)) FROM t_null

┌─toTypeName(assumeNotNull(y))─┐
│ Int8                         │
│ Int8                         │
└──────────────────────────────┘
```

<span id="可调整"></span>
## Adjustable
Convert the parameter's type to `Nullable`.
```plaintext
toNullable(x)
```

Parameter:

* `x` — Any non-composite type value.

Return value

* The input value, but its type as `Nullable`.

Example
```plaintext
SELECT toTypeName(10)

┌─toTypeName(10)─┐
│ UInt8          │
└────────────────┘

SELECT toTypeName(toNullable(10))

┌─toTypeName(toNullable(10))─┐
│ Nullable(UInt8)            │
└────────────────────────────┘
```
