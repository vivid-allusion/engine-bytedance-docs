---
title: "Regular function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/regular-function"
---

<span id="be58b24a"></span>
### UUIDNumToString

Accepts a FixedString(16) value and returns a string in text format containing 36 characters.

**Syntax**

```SQL
UUIDNumToString(FixedString(16))
```


**Parameter**


* A FixedString(16) value


**Return value**


* String.


**Example**

```SQL
SELECT'a/<@];!~p{jTj={)' AS bytes,
    UUIDNumToString(toFixedString(bytes, 16)) AS uuid
```


```Plain
┌─bytes────────────┬─uuid─────────────────────────────────┐
│ a/<@];!~p{jTj={) │ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │
└──────────────────┴──────────────────────────────────────┘
```


<span id="7e525187"></span>
### UUIDStringToNum

Accepts a string in the format containing 36 characters `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`, and returns it as a set of bytes in FixedString(16).

**Syntax**

```SQL
UUIDStringToNum(String)
```


**Param**


* String in UUID format


**Return value**


* Fixed String(16)


**Example**

```SQL
SELECT'612f3c40-5d3b-217e-707b-6a546a3d7b29' AS uuid,
    UUIDStringToNum(uuid) AS bytes
```


```Plain
┌─uuid─────────────────────────────────┬─bytes────────────┐
│ 612f3c40-5d3b-217e-707b-6a546a3d7b29 │ a/<@];!~p{jTj={) │
└──────────────────────────────────────┴──────────────────┘
```


<span id="1ab0c7b5"></span>
### bitmaskToArray

Accepts an integer. Returns a UInt64 Number array, containing a list of powers of 2 which, when summed up, equals to the source Number. Numbers in the array are arranged in ascending order.

**Syntax**

```SQL
bitmaskToArray(num)
```


**Param**


* `num` \- an Integer


**Return value**


* A UInt64 number array that contains a list of powers of two, which sum up to the source number.


**Example**

```SQL
SELECT bitmaskToArray(1), bitmaskToArray(3), bitmaskToArray(4)
```


```Plain
┌─bitmaskToArray(1)─┬─bitmaskToArray(3)─┬─bitmaskToArray(4)─┐
│ [1]               │ [1, 2]            │ [4]               │
└───────────────────┴───────────────────┴───────────────────┘
```


1 = power(2,0)

3 = power(2,0) + power(2,1)

4 = power(2,2)

<span id="c7e01d7c"></span>
### bitmaskToList

Accepts an Integer. Returns a string that contains a list of powers of two that add up to equal the source number. They are listed in ascending order in text format, separated by commas without spaces.

**Syntax**

```SQL
bitmaskToList(num)
```


**Parameter**


* `num` \- An integer


**Return value**


* A string containing a list of powers of two which, when added, equals the source number


**Example**

```SQL
SELECT bitmaskToList(1), bitmaskToList(3), bitmaskToList(4)
```


```Plain
┌─bitmaskToList(1)─┬─bitmaskToList(3)─┬─bitmaskToList(4)─┐
│ 1                │ 1,2              │ 4                │
└──────────────────┴──────────────────┴──────────────────┘
```


1 = power(2,0)

3 = power(2,0) + power(2,1)

4 = power(2,2)

<span id="3ed159ae"></span>
### hex

Returns a string containing the hexadecimal representation of the parameter.

**Syntax**

```SQL
hex(arg)
```


This function uses uppercase letters `A-F` without any prefix (like `0x`) or suffix (like `h`).

For integer parameters, it prints the hexadecimal digits ("nibbles") from the highest significant bit to the lowest significant bit (big\-endian or "human\-readable" order). It starts at the highest significant non\-zero byte (omitting leading zero bytes) but always prints two digits for each byte, even if the leading digit is zero.

`Date` and the value of type `DateTime` are formatted as the corresponding integers (Date as the number of days since the epoch, DateTime as the value of the Unix timestamp).

For `String` and `FixedString`, all bytes are simply encoded as two hexadecimal numbers. Zero bytes are not omitted.
