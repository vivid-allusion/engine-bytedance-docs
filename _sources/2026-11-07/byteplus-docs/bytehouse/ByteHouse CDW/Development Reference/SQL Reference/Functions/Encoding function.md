---
title: "Encoding function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-encoding"
---

<span id="2f87fd4e"></span>
## UUIDNumToString

Accepts a FixedString(16) value, and returns a string containing 36 characters in text format.

**Syntax**

```sql
UUIDNumToString(FixedString(16))
```


**Arguments**


* a FixedString(16) value


**Returned value**


* String.


**Example**

```sql
SELECT
    'a/<@];!~p{jTj={)' AS bytes,
    UUIDNumToString(toFixedString(bytes, 16)) AS uuid
```


```plain%20text
┌─bytes────────────┬─uuid─────────────────────────────────┐
│ a/<@];!~p{jTj={) │ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │
└──────────────────┴──────────────────────────────────────┘
```


<span id="uuidstringtonum"></span>
## UUIDStringToNum

Accepts a string containing 36 characters in the format `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx` , and returns it as a set of bytes in a FixedString(16).

**Syntax**

```sql
UUIDStringToNum(String)
```


**Arguments**


* a string in uuid format


**Returned value**


* FixedString(16)


**Example**

```sql
SELECT
    '612f3c40-5d3b-217e-707b-6a546a3d7b29' AS uuid,
    UUIDStringToNum(uuid) AS bytes
```


```plain%20text
┌─uuid─────────────────────────────────┬─bytes────────────┐
│ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │ a/<@];!~p{jTj={) │
└──────────────────────────────────────┴──────────────────┘
```


<span id="bitmasktoarray"></span>
## bitmaskToArray

Accepts an integer. Returns an array of UInt64 numbers containing the list of powers of two that total the source number when summed. Numbers in the array are in ascending order.

**Syntax**

```sql
bitmaskToArray(num)
```


**Arguments**


* `num` – an integer


**Returned value**


* an array of UInt64 numbers containing the list of powers of two that total the source number when summed.


**Example**

```sql
SELECT bitmaskToArray(1), bitmaskToArray(3), bitmaskToArray(4)
```


```plain%20text
┌─bitmaskToArray(1)─┬─bitmaskToArray(3)─┬─bitmaskToArray(4)─┐
│ [1]               │ [1, 2]            │ [4]               │
└───────────────────┴───────────────────┴───────────────────┘
```


1 = power(2,0)

3 = power(2,0) + power(2,1)

4 = power(2,2)

<span id="bitmasktolist"></span>
## bitmaskToList

Accepts an integer. Returns a string containing the list of powers of two that total the source number when summed. They are comma\-separated without spaces in text format, in ascending order.

**Syntax**

```sql
bitmaskToList(num)
```


**Arguments**


* `num` – an integer


**Returned value**


* a string containing the list of powers of two that total the source number when summed


**Example**

```sql
SELECT bitmaskToList(1), bitmaskToList(3), bitmaskToList(4)
```


```plain%20text
┌─bitmaskToList(1)─┬─bitmaskToList(3)─┬─bitmaskToList(4)─┐
│ 1                │ 1,2              │ 4                │
└──────────────────┴──────────────────┴──────────────────┘
```


1 = power(2,0)

3 = power(2,0) + power(2,1)

4 = power(2,2)

<span id="hex"></span>
## hex

Returns a string containing the argument’s hexadecimal representation.

**Syntax**

```sql
hex(arg)
```


The function is using uppercase letters `A-F` and not using any prefixes (like `0x` ) or suffixes (like `h` ).

For integer arguments, it prints hex digits (“nibbles”) from the most significant to least significant (big endian or “human readable” order). It starts with the most significant non\-zero byte (leading zero bytes are omitted) but always prints both digits of every byte even if leading digit is zero.

Values of type `Date` and `DateTime` are formatted as corresponding integers (the number of days since Epoch for Date and the value of Unix Timestamp for DateTime).

For `String` and `FixedString` , all bytes are simply encoded as two hexadecimal numbers. Zero bytes are not omitted.
