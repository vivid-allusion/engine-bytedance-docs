---
title: "Encoding Function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/encoding-function"
---

<span id="char"></span>
## char
Returns a string of the length equal to the number of passed parameters, with each byte representing the value of the corresponding parameter. Accepts multiple arguments of the numerical type. If the value of a parameter exceeds the range of the UInt8 data type, it is converted to UInt8, which may involve rounding and overflow.
<span id="语法"></span>
### Syntax
char(number_1, [number_2, ..., number_n]);
<span id="参数"></span>
### Parameters
number_1, number_2, ..., number_n — Numerical value parameters interpreted as integers. Type: Int, Float.
<span id="返回值"></span>
### Return value
String with a given number of bytes.
Type: String.
<span id="示例"></span>
## Example
Search:
```sql
SELECT char(104.1, 101, 108.9, 108.9, 111) AS hello
```

As a result:
```sql
┌─hello─┐
│ hello │
└───────┘
```

You can construct a string of any encoding by passing the corresponding bytes. This is an example of UTF-8:
Search:
```sql
SELECT char(0xD0, 0xBF, 0xD1, 0x80, 0xD0, 0xB8, 0xD0, 0xB2, 0xD0, 0xB5, 0xD1, 0x82) AS hello;
```

As a result:
```sql
┌─hello──┐
│ привет │
└────────┘
```

Search:
```sql
SELECT char(0xE4, 0xBD, 0xA0, 0xE5, 0xA5, 0xBD) AS hello;
```

As a result:
```sql
┌─hello─┐
│ hello │
└───────┘
```

<span id="hex"></span>
## hex
Accepts parameters of type String, unsigned integer, Date, or DateTime. Returns a string that contains the hexadecimal representation of the parameter. Uses uppercase letters A-F. Does not use the 0x prefix or h suffix. For strings, all bytes are simply encoded as two hexadecimal digits. Numbers are converted to big-endian (“easy to read”) format. For numbers, older zeros are removed but only for entire bytes. For example, hex(1)='01'. Date is encoded as the number of days since the Unix time start. DateTime is encoded as the number of seconds since the Unix time start.
<span id="unhex-str"></span>
## unhex(str)
Accepts a string containing any quantity of hexadecimal digits and returns a string containing the corresponding bytes. Supports both uppercase and lowercase letters A-F. The quantity of hexadecimal digits does not need to be even. If it is an odd number, the last digit is interpreted as the low byte of 00-0F. If the parameter string contains anything other than hexadecimal digits, some implementation-defined result is returned (no exception is thrown). If you want to convert the result to a number, you can use "reverse" and "reinterpretAsType" functions.
<span id="uuidstringtonum-str"></span>
## UUIDStringToNum(str)
Accepts a string containing 36 characters in the format "123e4567-e89b-12d3-a456-426655440000" and returns a FixedString(16).
<span id="uuidnumtostring-str"></span>
## UUIDNumToString(str)
Accepts a FixedString(16) value. Returns a text-formatted string containing 36 characters.
<span id="bitmasktolist-num"></span>
## bitmaskToList(num)
Accepts an integer. Returns a string that contains a list of powers of 2, the sum of all values in the list equals the integer. The list is comma-separated and sorted in ascending order.
<span id="bitmasktoarray-num"></span>
## bitmaskToArray(num)
Accept an integer. Return a UInt64 type array that contains a list of power of twos whose values sum up to this integer. The numbers in the array are in ascending order.
