---
title: "Nullable function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-nullable"
---

<span id="e363f0e3"></span>
### assumeNotNull

Result is the non\-`Nullable` equivalent of a Nullable type value. If the original value is `NULL`, the result is uncertain. Also see `ifNull` and `coalesce` functions.

**Syntax**

```SQL
assumeNotNull(x)
```


**Parameters:** 


* `x`—original value.


**Return value**


* `If not NULL, it is the raw value of the non-Nullable type.`

* If the raw value is NULL, the implementation\-specific result occurs.


**Example**

```SQL
CREATE TABLE IF NOT EXISTS test.functionAssumeNotNull ( x Int8,  y Nullable(Int8)) ENGINE = CnchMergeTree ORDER BY x;
INSERT INTO test.functionAssumeNotNull VALUES (1,NULL),(2,3);
SELECT * FROM test.functionAssumeNotNull;
```


```Plain
┌─x─┬─y────┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │ 3    │
└───┴──────┘
```


Apply the assumeNotNull function to column y.

```SQL
SELECT assumeNotNull(y),toTypeName(assumeNotNull(y))  FROM test.functionAssumeNotNull;
```


```Plain
┌─assumeNotNull(y)─┬─toTypeName(assumeNotNull(y))─┐
│ 0                │ Int8                         │
│ 3                │ Int8                         │
└──────────────────┴──────────────────────────────┘
```


<span id="92a9f04f"></span>
### coalesce

From left to right, check if a `NULL` parameter has been passed and return the first non\-`NULL` parameter.

**Syntax**

```SQL
coalesce(x,...)
```


**Param**


* An arbitrary number of non\-composite type parameters. All parameters' data types must be compatible.


**Return value**


* The first non\-`NULL` argument.

* `NULL`, if all arguments are `NULL`.


**Example**

Consider a contact list that may specify several ways to contact a client.

```SQL
CREATE TABLE IF NOT EXISTS test.functionCoalesce (name String, mail Nullable(String), phone Nullable(String), icq Nullable(UInt32)) ENGINE=CnchMergeTree ORDER BY name;
INSERT INTO test.functionCoalesce VALUES ('client 1', NULL, '123-45-67', 123), ('client 2', NULL, NULL, NULL);
SELECT * FROM test.functionCoalesce;
```


```Plain
┌─name─────┬─mail─┬─phone─────┬─icq──┐
│ client 1 │ ᴺᵁᴸᴸ │ 123-45-67 │ 123  │
│ client 2 │ ᴺᵁᴸᴸ │ ᴺᵁᴸᴸ      │ ᴺᵁᴸᴸ │
└──────────┴──────┴───────────┴──────┘
```


`mail` and the `phone` field's Type is String, but the type of the `icq` field is `UInt32`, so it needs to be converted to `String`.

Retrieve the first available contact method from the contact list:

```SQL
SELECT name, coalesce(mail, phone, CAST(icq,'Nullable(String)')) FROM test.functionCoalesce;
```


```Plain
┌─name─────┬─coalesce(mail, phone, CAST(icq, 'Nullable(String)'))─┐
│ client 1 │ 123-45-67                                            │
│ client 2 │ ᴺᵁᴸᴸ                                                 │
└──────────┴──────────────────────────────────────────────────────┘
```


<span id="1beb49c9"></span>
### ifNull

If the main argument is `NULL`, then return another value.

**Syntax**

```SQL
ifNull(x,alt)
```


**Parameters:** 


* `x`— The value to check `NULL`.

* `altx`— If so, the function returns the value `NULL`.


**Return value**


* `x` If `x` is not, the value is `NULL`.

* `alt` its value is. `xNULL`


**Example**

```SQL
SELECT ifNull('a', 'b');
```


```Plain
┌─ifNull('a', 'b')─┐
│ a                │
└──────────────────┘
```


```SQL
SELECT ifNull(NULL, 'b');
```


```Plain
┌─ifNull(NULL, 'b')─┐
│ b                 │
└───────────────────┘
```


<span id="58b415ef"></span>
### isNotNull

Check whether the parameter is NULL.

**Syntax**

```SQL
isNotNull(x)
```


**Param:** 


* `x`— has a value of non\-compound data type.


**Return value**


* `0` if `x` is `NULL`.

* `1` if `x` is not `NULL`.


**Example**

Input Table:

```SQL
CREATE TABLE IF NOT EXISTS test.functionIsNotNull (x UInt8, y Nullable(UInt8)) ENGINE=CnchMergeTree ORDER BY x;
INSERT INTO test.functionIsNotNull VALUES (1, NULL),(2,3);
SELECT * FROM test.functionIsNotNull;
```


```Plain
┌─x─┬─y────┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │ 3    │
└───┴──────┘
```


Search:

```SQL
SELECT x FROM test.functionIsNotNull WHERE isNotNull(y);
```


```Plain
┌─x─┐
│ 2 │
└───┘
```


<span id="4a4faa4a"></span>
### isNull

Check if the parameter is NULL.

**Syntax**

```SQL
isNull(x)
```


**Param**


* `x`— has a value with a non\-composite data type.


**Return value**


* `1` if `x` is `NULL`.

* `0` if `x` is not `NULL`.


**Example**

Input table:

```SQL
CREATE TABLE IF NOT EXISTS test.functionIsNull (x UInt8, y Nullable(UInt8)) ENGINE=CnchMergeTree ORDER BY x;
INSERT INTO test.functionIsNull VALUES (1, NULL),(2,3);
SELECT * FROM test.functionIsNull;
```


```Plain
┌─x─┬─y────┐
│ 1 │ ᴺᵁᴸᴸ │
│ 2 │ 3    │
└───┴──────┘
```


Query:

```SQL
SELECT x FROM test.functionIsNull WHERE isNull(y);
```


```Plain
┌─x─┐
│ 1 │
└───┘
```


<span id="ddca5d87"></span>
### nullIf

If the parameters are equal, it returns `NULL`.

**Syntax**

```SQL
nullIf(x, y)
```


**Parameter**


* `x`, `y`— Values for comparison. They must be compatible types, otherwise Bytehouse will generate an exception.


**Return value**


* `NULL`, if the parameters are equal.

* `x` if the parameters are not equal, then this value.


**Example**

```SQL
SELECT nullIf(1, 1);
```


```Plain
┌─nullIf(1, 1)─┐
│ ᴺᵁᴸᴸ         │
└──────────────┘
```


```SQL
SELECT nullIf(1, 2);
```


```Plain
┌─nullIf(1, 2)─┐
│ 1            │
└──────────────┘
```


<span id="ced09ec2"></span>
### toNullable

Convert the parameter type to `Nullable`.

**Syntax**

```SQL
toNullable(x)
```


**Parameter**


* `x`— Any non\-compound type value.


**Return value**


* Enter a value with type `Nullable`.


**Example**

```SQL
SELECT toTypeName(10);
```


```Plain
┌─toTypeName(10)─┐
│ UInt8          │
└────────────────┘
```


```SQL
SELECT toTypeName(toNullable(10));
```


```Plain
┌─toTypeName(toNullable(10))─┐
│ Nullable(UInt8)            │
└────────────────────────────┘
```
