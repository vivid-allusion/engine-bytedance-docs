---
title: "String type: String, FixedString"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/string-type-string-fixedstring"
---

<span id="01d8800f"></span>
# String
Strings can be of any length. They can contain any set of bytes, including null bytes. Therefore, the string type can replace VARCHAR, BLOB, CLOB, and other types in other DBMSs.
<span id="编码 {#bian-ma}"></span>
## Encoding
ClickHouse does not have a concept of encoding. Strings can be any set of bytes, stored and output as they originally are.
If storing text, it is recommended to use UTF-8 encoding. At a minimum, if your terminal uses UTF-8 (recommended), this way, reading and writing do not need any conversion.
Similarly, ClickHouse offers different functions for processing strings depending on the encoding of the text.
For example, the `length` function calculates the length of the byte array contained in a string, while the `lengthUTF8` function assumes the string is encoded in UTF-8 and calculates the length of the Unicode characters in the string.
<span id="681eef58"></span>
# FixedString
Strings of fixed length N (where N must be a strictly positive integer).
You can use the following syntax to declare a column as `FixedString` type:
```SQL
 FixedString(N)
```

Where `N` represents a natural number.
When the length of the data exactly matches N bytes, the `FixedString` type is efficient. In other cases, this might reduce efficiency.
Examples of values that can be efficiently stored in a `FixedString` type column:

* IP addresses in binary representation (IPv6 uses `FixedString(16)`).
* Language codes (ru_RU, en_US, etc.)
* Currency codes (USD, RUB, etc.)
* Binary representation of hash values (`FixedString(16)` for MD5, `FixedString(32)` for SHA256)

Please use UUID data type to store UUID values.
When inserting data into ClickHouse,

* If the byte count of the string is less than 'N', padding with null bytes will be added to the end of the string.
* If the byte count of the string is greater than `N`, a `Too large value for FixedString(N)` exception will be thrown.

When performing data searches, ClickHouse does not delete trailing null bytes from the strings. If using `WHERE` clause, you must manually add null bytes to match the `FixedString` value. The following example illustrates how to use the `WHERE` clause with `FixedString`.
Consider a table with a `FixedString(Feb)` column:
```Plain
┌─name──┐
│ b     │
└───────┘
```

The query `SELECT * FROM FixedStringTable WHERE a = 'b'` returns no results. Please use null bytes to populate the filter conditions.
```SQL
SELECT * FROM FixedStringTableWHERE a = 'b\0'
```

```Plain
┌─a─┐
│ b │
└───┘
```

This method differs from the way MySQL's `CHAR` type is handled (MySQL uses spaces to pad strings and removes them in the output).
Note that the length of `FixedString(N)` is a constant. A string composed only of null characters, function length returns `N`, and function empty returns `1`.
