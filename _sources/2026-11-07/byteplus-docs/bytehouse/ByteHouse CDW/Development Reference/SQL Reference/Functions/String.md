---
title: "String"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-string"
---

<span id="e27fcf06"></span>
### CHARACTER_LENGTH

It returns the length of the string in Unicode code points (not characters), assuming the string `string` contains a set of bytes that make up UTF\-8 encoded text. If this assumption is not met, it returns certain results (no exceptions raised).

**Syntax**

```SQL
CHARACTER_LENGTH(string)
```


**Parameters**


* `string` – String.


**Return Value**


* Length of the char.


Type: `UInt64`

**Example**

```SQL
select CHARACTER_LENGTH('abcdef123')
```


As a result:

```Plain
┌─CHARACTER_LENGTH('abcdef123')─┐
│ 9                             │
└───────────────────────────────┘
```


<span id="b3eb0fe8"></span>
### **CHAR_LENGTH**

Returns the length of a string in Unicode code points, not characters, assuming the string `string` contains a set of bytes forming UTF\-8 encoded text. If this assumption is not met, returns some result (without raising an exception).

**Syntax**

```SQL
CHAR_LENGTH(s)
```


**Param**


* `s` – String.


**Return value**


* Length of characters.


Type: `UInt64`

**Example**

```SQL
SELECT CHAR_LENGTH('abcdef123')
```


As a result:

```Plain
┌─CHAR_LENGTH('abcdef123')─┐
│ 9                        │
└──────────────────────────┘
```


<span id="d020267b"></span>
### ASCII

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the ASCII value of the character or the leftmost character of the string.

**Syntax**

```SQL
SELECT ascii('2');
```


**Param**


* `varchar` \- String


**Return value**


* `bigint`


**Example**

```SQL
SELECT ascii('dx');   
```


```SQL
+-------------+
| ascii('dx') |
+-------------+
|         100 |
+-------------+ 
```


<span id="65bc6b04"></span>
### bin

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Return `N`'s binary string. If `N` is `null`, the result is `NULL`.

**Syntax**

```SQL
SELECT bin(12);
```


**Parameter**


* `BIGINT`


**Return value**


* `VARCHAR`


<span id="b3eff611"></span>
### alphaTokens

Select a substring of consecutive bytes from the range az and AZ. Return an array of substrings.

**Syntax**

```SQL
alphaTokens(string)
```


**Param**


* `String` – String.


**Return value**


* Array of substrings.


**Example**

```SQL
SELECT alphaTokens('abca1abc');
```


```Plain
┌─alphaTokens('abca1abc')─┐
│ [abca, abc]             │
└─────────────────────────┘
```


<span id="4690c7c1"></span>
### appendTrailingCharIfAbsent

If not null and the end does not contain `string`, append it to the end. `charactercharacter`

**Grammar**

```SQL
appendTrailingCharIfAbsent(string, character)
```


**Param**


* `String` \- String.

* `Character` \- Character.


**Return value**


* Characters appended to the string.


Type: `String`

**Example**

```SQL
appendTrailingCharIfAbsent('abc', '2');
```


As a result:

```Plain
┌─appendTrailingCharIfAbsent('abc', '2')─┐
│ abc2                                   │
└────────────────────────────────────────┘
```


<span id="d96adab8"></span>
### arrayStringConcat

Connect the strings listed in the array with the delimiter. `Separator` is an optional param: a constant string, default set to empty string.

**Grammar**

```SQL
arrayStringConcat(array[, separator])
```


**Param**


* `Array` \- Array.

* `Separator` \- Optional, delimiter.


**Return value**


* Connected string.


Type: `String`

**Example**

```SQL
SELECT arrayStringConcat(['abc','123']);
```


As a result:

```Plain
┌─arrayStringConcat(['abc', '123'])─┐
│ abc123                            │
└───────────────────────────────────┘
```


Other example

```SQL
SELECT arrayStringConcat(['abc', '123'], ',')
```


As a result:

```Plain
┌─arrayStringConcat(['abc', '123'], ',')─┐
│ abc,123                                │
└────────────────────────────────────────┘
```


<span id="3833cbdf"></span>
### base64Decode

Decoding the base64 encoded `string` back to the original string. If it fails, an exception will be thrown.

Alias: `FROM_BASE64`.

**Syntax**

```SQL
base64Decode(string)
```


**Param**


* `String` \- string.


**Return value**


* The decoded string.


Type: `string`

**Example**

```SQL
SELECT base64Decode('SGVsbG8gQmFzZTY0');
```


As a result:

```Plain
┌─base64Decode('SGVsbG8gQmFzZTY0')─┐
│ Hello Base64                     │
└──────────────────────────────────┘
```


<span id="6597243a"></span>
### base64Encode

Encode `string` as base64

Alias: `TO_BASE64`.

**Syntax**

```SQL
base64Encode(string)
```


**Param**


* `String` \- String.


**Return value**


* Encoded string.


Type: `String`

**Example**

```SQL
SELECT base64Encode('Hello Base64')
```


As a result:

```Plain
┌─base64Encode('Hello Base64')─┐
│ SGVsbG8gQmFzZTY0             │
└──────────────────────────────┘
```


<span id="2ee6329e"></span>
### bit_length

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the length of the string `str` in bits.

**Syntax**

```SQL
bit_length(str)
```


**Parameter**


* `VARCHAR`


**Return Value**


* `BIGINT`


**Example**

```SQL
SELECT bit_length('text');
```


```SQL
+--------------------+
| bit_length('text') |
+--------------------+
|                 32 |
+--------------------+    
```


<span id="60dc25c2"></span>
### char

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Return `N1`, `N2`, and so on, as strings composed of decimal ASCII codes corresponding to the integers.

**Syntax**

```SQL
char(N1, N2, ...)
```


**Parameter**


* `BIGINT`


**Return Value**


* `VARBINARY`


**Example**

```SQL
SELECT char(97,110,97,108,121,116,105,99);
```


```SQL

┌─char(97, 110, 97, 108, 121, 116, 105, 99)─┐
│ analytic                                  │
└───────────────────────────────────────────┘ 
```


<span id="770cf582"></span>
### concat

Concatenates strings listed in the parameters without a separator.

**Syntax**

```SQL
concat(s1, s2, ...)
```


**Parameter**


* `s1`, `s2`... – Value of string or fixed string type.


**Return Value**


* The string generated after appending parameters.


If any parameter value is `NULL`, `concat` returns `NULL`.

**Example**

```SQL
SELECT concat('Hello, ', 'World!');
```


Result:

```Plain
┌─concat('Hello, ', 'World!')─┐
│ Hello, World!               │
└─────────────────────────────┘
```


<span id="ecfb174e"></span>
### concat_ws

String concatenation operation, where the first parameter `separator` is the delimiter for the rest of the parameters, skipping any strings with `null` values.

**Syntax**

```SQL
concat_ws(separator, str 1, …, str n)
```


**Parameters**


* `VARCHAR`


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT concat_ws(',', 'First name', 'Second name', 'Last Name')AS result;
```


```SQL
┌─result───────────────────────────┐
│ First name,Second name,Last Name │
└──────────────────────────────────┘
```


<span id="f5d4a654"></span>
### concatAssumeInjective

Similar to concat, the difference is that you need to ensure it is `concat(s1, s2, ...) → sn` injective, which will be used for optimization in GROUP BY.

If a function always returns different results for different parameters, it is called "injective." In other words: different parameters will never produce the same result.

**Syntax**

```SQL
concatAssumeInjective(s1, s2, ...)
```


**Parameters**


* `s1`, `s2`... – Values of string or fixed string type.


**Return Value**


* String obtained after concatenating parameters.


Note: If any parameter value is `NULL`, `concatAssumeInjective` returns `NULL`.

**Example 1**

```SQL
CREATE TABLE test.key_val(key1 String, key2 String, `value` UInt32) ENGINE = CnchMergeTree ORDER BY key2;
INSERT INTO test.key_val VALUES ('Hello, ','World',1), ('Hello, ','World',2), ('Hello, ','World!',3), ('Hello',', World!',2);
SELECT * from test.key_val;
```


```Plain
┌─key1───┬─key2─────┬─value─┐
│ Hello  │ , World! │ 2     │
│ Hello, │ World    │ 1     │
│ Hello, │ World    │ 2     │
│ Hello, │ World!   │ 3     │
└────────┴──────────┴───────┘
```


**Example 2**

```SQL
SELECT concat(key1, key2), sum(value) FROM test.key_val GROUP BY concatAssumeInjective(key1, key2);
```


```Plain
┌─concat(key1, key2)─┬─sum(value)─┐
│ Hello,World        │ 3          │
│ Hello,World!       │ 3          │
│ Hello, World!      │ 2          │
└────────────────────┴────────────┘
```


<span id="297e2015"></span>
### convertCharset

Converts the encoding of `string` from `from` encoding to `to` encoding.

**Syntax**

```SQL
convertCharset(s, from, to)
```


**Parameters**


* `string` – A string.

* From—Decoding from character encoding types.

* To—Encoding to character encoding types.


**Return Value**


* To character encoding type.


**Example**

```SQL
SELECT base64Encode(toString(convertCharset('abc', 'Unicode', 'UTF-8')))
```


Result:

```Plain
┌─base64Encode(toString(convertCharset('abc', 'Unicode', 'UTF-8')))─┐
│ 5oWi77+9                                                          │
└───────────────────────────────────────────────────────────────────┘
```


<span id="a12d4f13"></span>
### count

Calculate the number of rows or non\-null values.

**Syntax**

CNCH supports the following syntax `count`:


* `count(expr)` or `COUNT(DISTINCT expr)`.

* `count()` or `COUNT(*)`.


**Parameter**

This function can take:


* No parameters.

* No expressions.


**Return value**


* If the function is called without any parameters, it calculates the number of rows.

* If an expression is passed, the function counts the number of times this expression returns a non\-null value. If the expression returns a value of Nullable type, the result `count` remains 'not'. If the expression returns `Nullable` for all rows, the function returns 0. `NULL`

* In both cases, the return type is UInt64.


**Details**

CNCH supports the `COUNT(DISTINCT ...)` syntax. The behavior of this construction depends on the count_distinct_implementation setting. It defines which uniq\* function to use for the operation. The default is the uniqExact function.

The `SELECT count() FROM table` query is unoptimized because the number of entries in the table is not stored separately. It selects a small column from the table and calculates the number of values in it.

However, you can optimize the query by enabling the optimize_functions_to_subcolumns`SELECT count(nullable_column) FROM table` setting. This function only reads the null sub\-column instead of reading and processing the entire column data. The query is converted to. `optimize_functions_to_subcolumns = 1SELECT count(n) FROM tableSELECT sum(NOT n.null) FROM table`

**Example**

Example 1:

```SQL
CREATE TABLE test.test_count (id Int32) ENGINE = CnchMergeTree ORDER BY id;
INSERT INTO test.test_count(id) VALUES(1),(2),(3),(4),(5),(5);
select count() from test.test_count;
```


```Plain
┌─count()─┐
│ 6       │
└─────────┘
```


Example 2:

```SQL
SELECT name, value FROM system.settings WHERE name = 'count_distinct_implementation'
sql
```


```Plain
┌─name──────────────────────────┬─value─────┐
│ count_distinct_implementation │ uniqExact │
└───────────────────────────────┴───────────┘
```


```SQL
select count(distinct(id)) from test.test_count
```


```Plain
┌─uniqExact(id)─┐
│ 5             │
└───────────────┘
```


This example demonstrates the function executed according to the set value`count(DISTINCT num)`. `uniqExactcount_distinct_implementation`

<span id="7e7edd59"></span>
### e

Returns a Float64 number close to the number e.

**Syntax**

```SQL
e()
```


**Parameters**


* Not applicable


**Return Value**


* Returns a Float64 number close to the number e.


Type: `Float64`

**Example**

```SQL
SELECT e();
```


Result:

```Plain
┌─e()───────────────────┐
│ 2.718281828459045e+00 │
└───────────────────────┘
```


<span id="c47e25c5"></span>
### elt

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Return the `N`th string.

**Syntax**

```SQL
elt(N, str 1, ...,str n);
```


**Parameters**


* `N` is of BIGINT type, `str` is of VARCHAR type.


**Return Value**


* `VARCHAR`


**Examples**

```SQL
SELECT elt(4, 'Aa', 'Bb', 'Cc', 'Dd');  
```


```SQL
┌─ELT(4, 'Aa', 'Bb', 'Cc', 'Dd')─┐
│ Dd                             │
└────────────────────────────────┘
```


<span id="0a4246da"></span>
### **empty**

Return 1 for an empty string, and 0 for a non\-empty string.

If a string contains at least one byte, even if that byte is a space or null, it is considered non\-empty.

This function is also applicable to arrays.

**Syntax**

```SQL
empty(string)
```


**Parameters**


* `string` – String.


**Return Value**


* Returns 1 for an empty string, and 0 for a non\-empty string.


Type: `UInt8`

**Example**

```SQL
SELECT empty('');
```


Result:

```Plain
┌─empty('')─┐
│ 1         │
└───────────┘
```


Other Examples

```SQL
SELECT empty('test')
```


Result:

```Plain
┌─empty('12312')─┐
│ 0              │
└────────────────┘
```


<span id="196119a4"></span>
### endsWith

Returns whether it ends with the specified suffix. If `string` ends with the specified suffix, return 1 `suffix`, otherwise return 0.

**Syntax**

```SQL
endsWith(string, suffix)
```


**Parameters**


* `string` \- A string.

* `suffix` \- The suffix to test if `s` ends with the specified suffix.


**Return Value**


* If the string ends with the specified suffix, return 1, otherwise return 0.


Type: `UInt8`

**Example**

```SQL
SELECT endsWith('test_end_with','with');
```


Result:

```Plain
┌─endsWith('test_end_with', 'with')─┐
│ 1                                 │
└───────────────────────────────────┘
```


Other Examples

```SQL
SELECT endsWith('test_end_with','error');
```


Result:

```Plain
┌─endsWith('test_end_with', 'error')─┐
│ 0                                  │
└────────────────────────────────────┘
```


<span id="6dde6046"></span>
### export_set

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Convert `bits` into binary values. In which:


* The system checks the binary values from right to left. If the binary value is 1, it will be replaced with `onstr` value; if the binary value is 0, it will be replaced with `offstr` value.

* The return values are separated by `separator`.

* `Number_of_bits` specifies the number of check bits, the default value is 64. If the specified `number_of_bits` is greater than 64, it will be trimmed to 64 bits; if the specified `number_of_bits` is \-1, the number of check bits will still default to 64.


**Syntax**

```SQL
export_set(bits, onstr, offstr [, separator[,number_of_bits]]);
```


**Parameters**


* `Bits` and `number_of_bits` are of `BIGINT` type, `onstr`, `offstr`, and `separator` are of `VARCHAR` type.


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT export_set(5,'a','b',',',2);
```


```SQL
┌─export_set(5, 'a', 'b', ',', 2)─┐
│ a,b                             │
└─────────────────────────────────┘
```


<span id="412cf8b9"></span>
### extract

Extract fragments of a string using regular expressions. If the `string` does not match the `pattern` regular expression, an empty string is returned. If the regular expression does not include subpatterns, extract the segment that matches the entire regular expression. Otherwise, extract the segment that matches the first subpattern.

**Syntax**

```SQL
extract(haystack, pattern)
```


**Parameters**


* `string` – String.

* `pattern` – Regular expression pattern.


**Return Value**


* Matched string.


Type: `string`

**Example**

```SQL
SELECT extract('abc<regex1>abc<regex2>abc','<.*?>');
```


Result:

```Plain
┌─extract('abc<regex1>abc<regex2>', '<.*?>')─┐
│ <regex1>                                   │
└────────────────────────────────────────────┘
```


<span id="2c68358c"></span>
### extractAll

Extract all segments of a string using regular expressions. If `string` does not match the `pattern` regular expression, return an empty string. Return an array of strings comprised of all matches to the regular expression. Generally, its behavior is the same as the function `extract` (which takes the first subpattern, or the entire expression if there is no subpattern).

**Syntax**

```SQL
extractAll(string, pattern)
```


**Parameters**


* `string` \- String.

* `Pattern` – Regular expression pattern


**Return value**


* Matched string.


Type: `string`

**Example**

```SQL
SELECT extractAll('abc<regex1>abc<regex2>abc','<.*?>');
```


Result:

```Plain
┌─extractAll('abc<regex1>abc<regex2>abc', '<.*?>')─┐
│ [<regex1>, <regex2>]                             │
└──────────────────────────────────────────────────┘
```


<span id="ec1aac8f"></span>
### field

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the index position of `str` in the list of `str 1`, `str 2`, `str n`. If `str` is not found, returns `0`.

**Syntax**

```SQL
FIELD(str, str 1, str 2,..., str n);
```


**Parameter**


* `VARCHAR`


**Return Value**


* `BIGINT`


**Example**

```SQL
SELECT FIELD('Bb', 'Aa', 'Bb', 'Cc', 'Dd', 'Ff');
```


```SQL
┌─field('Bb', 'Aa', 'Bb', 'Cc', 'Dd', 'Ff')─┐
│                                         2 │
└───────────────────────────────────────────┘
```


<span id="8d66cfb8"></span>
### find_in_set

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the position of `str` in the list `strlist`.

If `str` is not in `strlist` or `strlist` is an empty string, the result is `0`.

If any of the parameters `str`, `strlist` is `null`, the result is `null`.

**Syntax**

```SQL
find_in_set(str, strlist)            
```


**Parameter**


* `str` and `strlist` are both of the VARCHAR type.


**Return value**


* `BIGINT`


**Example**

```SQL
SELECT find_in_set('b','a,b,c,d');
```


```SQL
┌─find_in_set('b', 'a,b,c,d')─┐
│                           2 │
└─────────────────────────────┘
```


<span id="d56dc27b"></span>
### from_base64

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Decode the Base64 encoded parameter `x` and return the result

**Syntax**

```SQL
from_base64(x)          
```


**Parameter**


* `VARCHAR`


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT from_base64('Q2hpbmE=');  
```


```SQL
┌─FROM_BASE64('Q2hpbmE=')─┐
│ China                   │
└─────────────────────────┘
```


<span id="760bfd83"></span>
### from_utf8

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>



* `from_utf8(x)`: Decodes the UTF\-8 encoded `x` and returns the result.

* `from_utf8(x, y)`: Decodes arguments not encoded in UTF\-8 `x`, replacing them with designated illegal characters.


**Syntax**

```SQL
from_utf8(x)
from_utf8(x, y)        
```


**Parameter**


* `VARCHAR`


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT from_utf8(to_utf8('hello'));
```


```SQL
┌─FROM_UTF8(TO_UTF8('hello'))─┐
│ hello                       │
└─────────────────────────────┘
```


<span id="ec3edbd7"></span>
### hex

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Convert the parameter `x` into its corresponding hexadecimal format string.

**Syntax**

```SQL
hex(x)      
```


**Parameter**


* `BIGINT`/`VARCHAR`


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT hex(16);
```


```SQL
┌─hex(16)─┐
│ 10      │
└─────────┘
```


<span id="9d2883dd"></span>
### instr

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the position where the substring substr first appears in the string str.`substr first appears in the string str`.

**Syntax**

```SQL
instr(str, substr)
```


**Parameters**


* `Both str and substr are of VARCHAR type.`


**Return Value**


* `BIGINT`


**Example**

```SQL
SELECT instr('foobarbar', 'bar');
```


```SQL
┌─positionCaseInsensitive('foobarbar', 'bar')─┐
│                                           4 │
└─────────────────────────────────────────────┘
```


<span id="42c63c78"></span>
### lcase

Converts ASCII Latin symbols to lowercase in `string`.

**Syntax**

```SQL
lcase(string)
```


**Parameters**


* `string` – A string.


**Return Value**


* A string in lowercase letters.


Type: `string`

**Example**

```SQL
SELECT lcase('ABCdef');
```


Result:

```Plain
┌─lcase('ABCdef')─┐
│ abcdef          │
└─────────────────┘
```


<span id="df27332d"></span>
### length

Returns the length of the string in integer form; this function is also applicable to arrays.

**Syntax**

```SQL
length(x)
```


**Parameters**


* `x` \- string or array.


**Return value**


* Length of the string or array.


Type: `UInt64`

**Examples**

```SQL
SELECT length('Hello');
```


Result:

```Plain
┌─length('Hello')─┐
│ 5               │
└─────────────────┘
```


Additional examples

```SQL
SELECT length([1,2,3,4]);
```


Result:

```Plain
┌─length([1, 2, 3, 4])─┐
│ 4                    │
└──────────────────────┘
```


<span id="bf5c211d"></span>
### lengthUTF8

Returns the length of the string (expressed as an integer), assuming the string consists of bytes that form UTF\-8 encoded text. If this assumption is not met, it returns some result (without throwing an exception).

**Syntax**

```SQL
lengthUTF8(x)
```


**Parameters**


* `x` – String or array.


**Return Value**


* Length of the string or array.


Type: `UInt64`

**Examples**

Encoding 'Hello test' as UTF\-8, we obtain `\\x48\\x65\\x6C\\x6C\\x6F\\x20\\x74\\x65\\x73\\x74`

```SQL
SELECT lengthUTF8('\x48\x65\x6C\x6C\x6F\x20\x74\x65\x73\x74');
```


Result:

```Plain
┌─lengthUTF8('Hello test')─┐
│ 10                       │
└──────────────────────────┘
```


<span id="abff580f"></span>
### **like**

like(string, pattern) — The string LIKE operator checks if a string matches a simple regular expression.

**Syntax**

```SQL
like(string, pattern)
string LIKE pattern
```


**Parameters**


* `string` – String.

* `pattern` – This string matches a simple regular expression.


Regular expressions can include wildcard characters `%` and `_`.

`%` represents any number of any bytes (including zero characters).

`_` represents any single byte.

Use a backslash (`\\`) to escape metacharacters. Please refer to the notes on escaping in the description of the "match" function.

For regular expressions like `%needle%`, the code is more optimized and as fast as the `position` function.

For other regular expressions, the code performs the same as the "match" function.

**Return Value**


* 1 or 0.


Type: `UInt8`

**Example**

```SQL
SELECT like('abc','ab')
```


Type

Result:

```Plain
┌─like('abc', 'ab')─┐
│ 0                 │
└───────────────────┘
```


Other examples

```SQL
SELECT 'abc' LIKE 'ab%'
```


Result:

```Plain
┌─like('abc', 'ab%')─┐
│ 1                  │
└────────────────────┘
```


<span id="c601f6ab"></span>
### locate

The locate() function returns the position of the first occurrence of the substring in `string`.

Alias of position(string, substring)

**Syntax**

```SQL
locate(string, substring[, start_pos]) .
```


**Parameters**


* `String` \- The string in which to search for the substring. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `substring` \- The substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `start_pos` \- Optional parameter that indicates the position of the first character in the string to start the search[.](https://www.volcengine.com/docs/6517/102207) [String](https://docs.byteplus.com/docs/bytehouse/docs-string).


**Return Value**


* The position of the first occurrence of the substring in the string.


Type: `UInt64`

**Example**

```SQL
SELECT locate('Hello World', 'Wor')
```


Result:

```Plain
┌─locate('Hello World', 'Wor')─┐
│ 7                            │
└──────────────────────────────┘
```


<span id="a50030c3"></span>
### lower

Convert ASCII Latin symbols in strings to lowercase.

**Grammar**

```SQL
lower(string)
```


**Parameters**


* `String` – String.


**Return value**


* String of lowercase letters.


Type: `String`

**Example**

```SQL
SELECT lower('ABCdef');
```


Result:

```Plain
┌─lower('ABCdef')─┐
│ abcdef          │
└─────────────────┘
```


<span id="a1a63b5c"></span>
### lowerUTF8

Convert the string to lowercase, assuming it contains a sequence of bytes that make up UTF\-8 encoded text.

Note: It does not detect language. Therefore, for Turkish, the results may not be completely correct.

If the UTF\-8 byte sequences for uppercase and lowercase versions of a code point differ in length, the result for that code point may be incorrect.

If the string contains a set of non\-UTF\-8 bytes, the behavior is undefined.

**Syntax**

```SQL
lowerUTF8(s)
```


**Parameters**


* `s` – String.


**Return value**


* A string of lowercase letters.


Type: `string`

**Example**

Encoding 'Hello test' as UTF\-8, we can obtain '\x48\x65\x6C\x6C\x6F\x20\x74\x65\x73\x74'.

```SQL
SELECT lowerUTF8('\x48\x65\x6C\x6C\x6F\x20\x74\x65\x73\x74');
```


As a result

```Plain
┌─lowerUTF8('Hello test')─┐
│ hello test              │
└─────────────────────────┘
```


<span id="90191218"></span>
### lpad

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Pad the left side of string `str` with `padstr` until it reaches a length of `len`, and return the padded string.

If `str` is longer than `len`, the return value will be shortened to `len` characters.

**Syntax**

```SQL
lpad(str, len, padstr)
```


**Param**


* `str` and `padstr` are both of `VARCHAR` type, and len is of `BIGINT` type.


**Return value**


* `VARCHAR`


**Example**

```SQL
SELECT lpad('Aliyun',9,'#');
```


```SQL
┌─leftPad('Aliyun', 9, '#')─┐
│ ###Aliyun                 │
└───────────────────────────┘
```


<span id="82f6c582"></span>
### ltrim

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Delete all leading spaces from the string `str`.

**Syntax**

```SQL
ltrim(str)
```


**Param**


* `VARCHAR`


**Return value**


* `VARCHAR`


**Example**

```SQL
SELECT ltrim('  abc');
```


```SQL
┌─trimLeft('  abc')─┐
│ abc               │
└───────────────────┘
```


<span id="61aa1e70"></span>
### make_set

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns a value by separating a set of substrings specific into a string, where the string contains settings with corresponding bits.

**Syntax**

```SQL
make_set(bits, str 1, str 2,...);
```


**Parameters**


* `Bits` is of `BIGINT` type, `str` is of `VARCHAR` type


**Return value**


* `VARCHAR`


**Example**

```SQL
SELECT make_set(5,'hello','nice','world');
```


```SQL
┌─make_set(5, 'hello', 'nice', 'world')─┐
│ hello,world                           │
└───────────────────────────────────────┘
```


<span id="c612cf8e"></span>
### match

Check if the string matches the `regular expression` pattern. `regular expression`. The syntax of regular expressions `re2` is more restricted compared with Perl regular expressions.

Please note that the backslash symbol () is used for escaping in regular expressions. The same symbol is also used for escaping string literals. Therefore, to escape a symbol in a regular expression, you must write two backslashes (\) in the string literal.

Regular expressions treat strings as a set of bytes. Regular expressions cannot contain null bytes.

For searching substrings in a string, it is best to use LIKE or "position" since they operate faster.

**Grammar**

```SQL
match(string, pattern)
```


**Param**


* `String`– string.

* `Mode`– matching mode


**Return value**


* If there is no match, return 0; if there is a match, return 1.


Type: `UInt8`

**Example**

```SQL
SELECT match('abc<regex1>abc<regex2>abc','<.*?>');
```


As a result:

```Plain
┌─match('abc<regex1>abc<regex2>abc', '<.*?>')─┐
│ 1                                           │
└─────────────────────────────────────────────┘
```


<span id="ce275d93"></span>
### mid

Returns a substring starting at the "offset" index and of "length" length. Character indexing starts from one (same as standard SQL). The "offset" and "length" parameters must be constants.

**Syntax**

```SQL
mid(s, offset, length)
```


**Parameters**


* `s` – String.

* `offset` – Starting offset of the substring.

* `length` – Length of the substring.


**Return value**


* Substring.


Type: `string`

**Example**

```SQL
SELECT mid('Hello CNCH',7,4);
```


As a result:

```Plain
┌─mid('Hello CNCH', 7, 4)─┐
│ CNCH                    │
└─────────────────────────┘
```


<span id="d9f1eeab"></span>
### multiFuzzyMatchAny

Similar to multiMatchAny, but returns 1 if any mode matches the string within a specified edit distance. This function is also in experimental mode and may be very slow. For more details, please refer to [hyperscan document](https://intel.github.io/hyperscan/dev-reference/compilation.html#approximate-matching).

**Grammar**

```SQL
multiFuzzyMatchAny(string, distance, [pattern_1, pattern_2, …, pattern_n])
```


**Param**


* `String` \- String.

* `Integer` \- Please refer to [edit distance](https://en.wikipedia.org/wiki/Edit_distance).

* Mode used in fuzzy matching: `pattern`.


**Return value**


* Return 1 if any mode matches the string; otherwise, return 0.


Type: `UInt8`

**Example**

```SQL
SELECT multiFuzzyMatchAny('123ab12cdef',2,['abcd']);
```


As a result

```Plain
┌─multiFuzzyMatchAny('123ab12cdef', 2, ['abcd'])─┐
│ 1                                              │
└────────────────────────────────────────────────┘
```


<span id="3f9fbd77"></span>
### multiFuzzyMatchAnyIndex

`multiFuzzyMatchAnyIndex` is the same as `multiFuzzyMatchAny`, but it returns any index that matches the string within a constant edit distance.

**Grammar**

```SQL
multiFuzzyMatchAnyIndex(string, distance, [pattern_1, pattern_2, …, pattern_n])
```


**Param**


* `String` – String.

* `Distance` – Integer, please refer to [edit distance](https://en.wikipedia.org/wiki/Edit_distance).

* `Pattern` – Mode used in fuzzy matching.


**Return value**


* Returns any index that matches the string.


Type: `UInt64`

**Example**

```SQL
SELECT multiFuzzyMatchAnyIndex('111333444CN1CH',1,['abc','def','CNCH']);
```


Result:

```Plain
┌─multiFuzzyMatchAnyIndex('111333444CN1CH', 1, ['abc', 'def', 'CNCH'])─┐
│ 3                                                                    │
└──────────────────────────────────────────────────────────────────────┘
```


<span id="8ace3e5d"></span>
### multiMatchAny

multiMatchAny(haystack，[pattern_1，pattern_2，…，pattern_n]）

Similar to `match`, but returns 0 if there is no matching regular expression, and returns 1 if any pattern matches. It uses the [hyperscan](https://github.com/intel/hyperscan) library. For patterns searching for substrings within a string, it is best to use `multiSearchAny` as it operates faster.

Advisory: The length of any string `haystack` must be smaller than 2 (32) bytes, otherwise, an exception will be thrown. This limitation is due to the hyperscan API.

**Syntax**

```SQL
multiMatchAny(string, [pattern_1, pattern_2, …, pattern_n])
```


**Param**


* `string` \- String.

* `pattern` \- The matching mode


**Return value**


* If it doesn't match, return 0; if it matches, return 1.


Type: `UInt8`

**Example**

```SQL
SELECT multiMatchAny('abc<regex1>abc<regex2>abc',['<.*?>','error_patten']);
```


As a result:

```Plain
┌─multiMatchAny('abc<regex1>abc<regex2>abc', ['<.*?>', 'error_patten'])─┐
│ 1                                                                     │
└───────────────────────────────────────────────────────────────────────┘
```


<span id="be0f0357"></span>
### multiMatchAnyIndex

Similar to `multiMatchAny`, but returns any index that matches the string.

**Syntax**

```SQL
multiMatchAnyIndex(string, [pattern_1, pattern_2, …, pattern_n])
```


**Param**


* `String` – String.

* `Mode` – Matching pattern.


**Return value**


* Return any indices that match the string.


Type: `UInt64`

**Example**

```SQL
SELECT multiMatchAnyIndex('abc<regex1>abc<regex2>abc',['error_patten', '<.*?>']);
```


As a result:

```Plain
┌─multiMatchAnyIndex('abc<regex1>abc<regex2>abc', ['error_patten', '<.*?>'])─┐
│ 2                                                                          │
└────────────────────────────────────────────────────────────────────────────┘
```


<span id="20078ca0"></span>
### multiSearchAllPositions

Same as [position](https://docs.byteplus.com/docs/bytehouse/docs-string#e250992b) but returns `Array` indicating the positions of the corresponding substrings found in the string. Index positions start from 0.

Searches are conducted on byte sequences and are independent of string encoding and sorting.


* For case\-insensitive ASCII searches, use the function `multiSearchAllPositionsCaseInsensitive`.

* To search using UTF\-8, use the function [multiSearchAllPositionsUTF8](https://docs.byteplus.com/docs/bytehouse/docs-string#185e5df2).

* For case\-insensitive UTF\-8 search, use the function multiSearchAllPositionsCaseInsensitiveUTF8.


**Syntax**

```SQL
multiSearchAllPositions(string, [substring_1, substring_2, ..., Substring_n])
```


**Param**


* `String`— The string in which to search for a substring. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `Substring`— The substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).


**Return value**


* If a corresponding substring is found, it is an array of starting positions (counting begins from 1), if not found, then it is 0.


Type: `Array(UInt64)`

**Example**

```SQL
SELECT multiSearchAllPositions('Hello, World!', ['hello', '!', 'world']);
```


As a result:

```Plain
┌─multiSearchAllPositions('Hello, World!', ['hello', '!', 'world'])─┐
│ [0, 13, 0]                                                        │
└───────────────────────────────────────────────────────────────────┘
```


<span id="185e5df2"></span>
### multiSearchAllPositionsUTF8

Please refer to `multiSearchAllPositions`. ## multiSearchAny

If at least one string needle_i`string` matches this string, return 1; otherwise, return 0.

For case\-insensitive search and/or UTF\-8 format, use functions `multiSearchAnyCaseInsensitive, multiSearchAnyUTF8, multiSearchAnyCaseInsensitiveUTF8`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In all functions, due to implementation standards, the quantity of <code>multiSearch*</code> modes should be smaller than 2 (Augt).</div>


**Syntax**

```SQL
multiSearchAny(string, [pattern_1, pattern_2, …, pattern_n]) 
```


**Param**


* `String` \- String.

* `Mode` \- Matching mode


**Return value**


* If there is at least one match between the mode and the string, return 1, `otherwise` return 0.


Type: `UInt8`

**Example**

```SQL
SELECT multiSearchAny('can_you_find_CNCH?',['abc','CNCH']);
```


As a result:

```Plain
┌─multiSearchAny('can_you_find_CNCH?', ['abc', 'CNCH'])─┐
│ 1                                                     │
└───────────────────────────────────────────────────────┘
```


<span id="339f10ea"></span>
### multiSearchFirstIndex

Returns the index of pattern_i found on the far left `i` (starting at 1), `otherwise` return 0.

For case\-insensitive or/and UTF\-8 formats, use the function `multiSearchFirstIndexCaseInsensitive, multiSearchFirstIndexUTF8, multiSearchFirstIndexCaseInsensitiveUTF8`.

**Grammar**

```SQL
multiSearchFirstIndex(string, [pattern_1, pattern_2, …, pattern_n]) 
```


**Param**


* `string`– String.

* `pattern`– Match Mode


**Return value**


* Returns the index of the first found pattern_i `i` (starting from 1) in `string`, otherwise returns 0.


Type: `UInt8`

**Example**

```SQL
SELECT multiSearchFirstIndex('which_pattern_matchs_CNCH?',['abc','CNCH']);
```


Result:

```Plain
┌─multiSearchFirstIndex('which_pattern_matchs_CNCH?', ['abc', 'CNCH'])─┐
│ 2                                                                    │
└──────────────────────────────────────────────────────────────────────┘
```


<span id="47e2bc05"></span>
### multiSearchFirstPosition

Same as the original, `Location` but returns the leftmost offset of the string that matches some substrings.

For case\-insensitive searches or and UTF\-8 format, use the functions `multiSearchFirstPositionCaseInsensitive, multiSearchFirstPositionUTF8, multiSearchFirstPositionCaseInsensitiveUTF8`.

**Syntax**

```SQL
multiSearchFirstPosition(string, [pattern_1, pattern_2, …, pattern_n]) 
```


**Param**


* `String` – String.

* `Substring` – Substring to match.


**Return value**


* Returns the index `i` of the pattern_i found on the far left (starting from 1), `String` otherwise returns zero.


Type: `UInt8`

**Example**

```SQL
SELECT multiSearchFirstPosition('123_abc_abc_CNCH?',['abc','CNCH']);
```


As a result

```Plain
┌─multiSearchFirstPosition('123_abc_abc_CNCH?', ['abc', 'CNCH'])─┐
│ 5                                                              │
└────────────────────────────────────────────────────────────────┘
```


<span id="e288d737"></span>
### ngramDistance

`String` calculates the 4\-gram distance between `substring`: Calculate the symmetric difference between two 4\-gram multi sets and normalize it by their sum of cardinalities. Returns a floating\-point number between 0 and 1 \- the closer to zero, the more similar the strings are to each other. If constants `substring` or `substring` exceed 32Kb, then an exception is thrown. If some non\-constant `substring` or `substring` strings exceed 32Kb, the distance is always 1.

For case\-insensitive searches or/and UTF\-8 format, use the functions `ngramDistanceCaseInsensitive, ngramDistanceUTF8, ngramDistanceCaseInsensitiveUTF8`.

**Syntax**

```SQL
ngramDistance(string, [substring_1, substring_2, …, substring_n]) 
sql
```


**Param**


* `String` \- String.

* `substring` – the substring needed to match.


**Return value**


* Returns the index of substring_i found on the far left `i` (starting from 1), `string` or returns 0 otherwise.


Type: `Float32`

**Example**

```SQL
SELECT ngramDistance('abc123ascCNCH_83q','CNCH'):
```


Result:

```Plain
┌─ngramDistance('abc123ascCNCH_83q', 'CNCH')─┐
│ 8.666667e-01                               │
└────────────────────────────────────────────┘
```


<span id="37061005"></span>
### **not**

The result of the logical NOT calculation. Corresponds to [the logical NOT operator](https://docs.byteplus.com/en/docs/bytehouse/docs-string).

**Syntax**

```SQL
not(val);
sql
```


**Param**


* `val`— Value. Int, [UInt](https://docs.byteplus.com/en/docs/bytehouse/docs-string), Float or [Nullable.](https://docs.byteplus.com/en/docs/bytehouse/docs-string)


**Return value**


* `1` if `val` is `0`.

* `0` if `val` is not zero.

* `NULL` if `val` is a `NULL` value.


Type: [UInt8](https://docs.byteplus.com/en/docs/bytehouse/docs-string) or [Nullable](https://docs.byteplus.com/en/docs/bytehouse/docs-string) ([UInt8](https://docs.byteplus.com/en/docs/bytehouse/docs-string)).

**Example**

```SQL
SELECT NOT(1);
```


Result:

```Plain
┌─not(1)─┐
│ 0      │
└────────┘
```


<span id="554b1b69"></span>
### notEmpty

If it is empty, return 0 `string`; if it is not empty, return 1 `string`.

This function also applies to arrays.

**Syntax**

```SQL
notEmpty(string)
```


**Parameters**


* `s` \- String.


**Return value**


* For an empty string return 1, for a non\-empty string return 0.


Type: `UInt8`

**Example**

```SQL
SELECT notEmpty('test');
```


Result:

```Plain
┌─notEmpty('test')─┐
│ 1                │
└──────────────────┘
```


Other examples

```SQL
SELECT notEmpty('')
```


Result:

```Plain
┌─notEmpty('')─┐
│ 0            │
└──────────────┘
```


<span id="666cdf5a"></span>
### notLike

notLike(string, pattern), the string operator does not resemble the pattern.

Has the same meaning as "like," but in a negative form.

**Syntax**

```SQL
notLike(string, pattern)
```


**Parameter**


* `string` \- String.

* `pattern` \- Matching pattern.


**Return value**


* If it doesn’t match, returns 0; if it matches, returns 1.


Type: `UInt8`

**Example**

```SQL
SELECT notLike('test1','test2');
```


Result:

```Plain
┌─notLike('test1', 'test2')─┐
│ 1                         │
└───────────────────────────┘
```


<span id="24169d9c"></span>
### oct

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


Returns the octal string representation of integer `N`.

**Syntax**

```SQL
oct(N)
```


**Param**


* `BIGINT`


**Return value**


* `VARCHAR`


**Example**

```SQL
SELECT oct(12);
```


```SQL
┌─oct(12)─┐
│ 14      │
└─────────┘
```


<span id="457bf7cb"></span>
### ord

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it within associated dialects.</div>


If the leftmost character of string `x` is a multibyte character, it returns the code of that character.

**Syntax**

```SQL
ord(x)
```


**Param**


* `VARCHAR`


**Return value**


* `BIGINT`


**Example**

```SQL
SELECT ord('China');
```


```SQL
┌─ord('China')─┐
│           67 │
└──────────────┘
```


<span id="e250992b"></span>
### position

`substring` is searched for in `string`.

Return the position of the substring found in the string, starting from 1.

Note: The search is case\-sensitive by default. For a case\-insensitive search, use the [positionCaseInsensitive](https://docs.byteplus.com/docs/bytehouse/docs-string#f8e46d9a) function.

**Syntax**

```SQL
position(substring IN string)
position(string, substring[, start_pos])
```


Alias: `locate(string, substring[, start_pos])`.

Note: The syntax `position(substring IN string)` provides SQL compatibility; the function works the same as `position(string, substring)`.

**Param**


* `string`– the string in which the substring is searched. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `Substring` – The substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `Start_pos` – Optional parameter, the position of the first character in the string, used to start the search. [UInt](https://docs.byteplus.com/en/docs/bytehouse/docs-string).


**Return value**


* Returns the location of the substring found in the string, starting from 1.


Type: `Integer`

**Example 1**

The phrase "Hello, world!" contains a set of bytes representing single\-byte encoded text. The function returns some expected results:

```SQL
SELECT position('Hello, world!', '!');
```


As a result:

```Plain
┌─position('Hello, world!', '!')─┐
│ 13                             │
└────────────────────────────────┘
```


**Example 2**

```SQL
SELECT position('Hello, world!', 'o', 1),position('Hello, world!', 'o', 7);
```


```Plain
┌─position('Hello, world!', 'o', 1)─┬─position('Hello, world!', 'o', 7)─┐
│                                 5 │                                 9 │
└───────────────────────────────────┴───────────────────────────────────┘
```


The same phrase in Russian contains characters that cannot be represented by a single byte. The function returned some unexpected results (using the positionUTF8 function on multi\-byte encoded text):

```SQL
SELECT position('Привет, мир!', '!');
```


As a result:

```Plain
┌─position('Привет, мир!', '!')─┐
│                            21 │
└───────────────────────────────┘
```


**position(substring IN string) Syntax Example**

```SQL
SELECT 3 = position('c' IN 'abc');
```


As a result:

```Plain
┌─equals(3, position('abc', 'c'))─┐
│                               1 │
└─────────────────────────────────┘
```


Example:

```SQL
SELECT 6 = position('/' IN s) FROM (SELECT 'Hello/World' AS s);
```


As a result:

```Plain
┌─equals(6, position(s, '/'))─┐
│                           1 │
└─────────────────────────────┘
```


<span id="f8e46d9a"></span>
### positionCaseInsensitive

Like *position*, returns the position of the substring found in the string, starting from 1. Use this function for case insensitive search.

Assume the string contains a set of bytes representing single\-byte encoded text. If this assumption is not met and the character cannot be represented with a single byte, the function will not throw an exception but will return some unexpected results. If a character can be represented with two bytes, it will use two bytes, and so on.

**Syntax**

```SQL
positionCaseInsensitive(string, substring[, start_pos])
```


**Parameter**


* `string` – The string in which to search for the substring. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `substring` \- Substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `start_pos` \- Optional parameter, the location of the first character in the string, used to start searching. [UInt](https://docs.byteplus.com/en/docs/bytehouse/docs-string).


**Return value**


* If the substring is found, the starting location in bytes (starting from 1).

* If the substring is not found, it is 0.


Type: `Integer`.

**Example**

```SQL
SELECT positionCaseInsensitive('Hello, world!', 'hello');
```


As a result:

```Plain
┌─positionCaseInsensitive('Hello, world!', 'hello')─┐
│ 1                                                 │
└───────────────────────────────────────────────────┘
```


<span id="aed0e42a"></span>
### positionCaseInsensitiveUTF8

Similar to positionUTF8, but case\-insensitive Returns the position (in Unicode points) of `substring` found in `string`, starting at 1

Works assuming the string contains a set of bytes representing UTF\-8 encoded text If this assumption is not met, the function will not throw an exception but will return some unexpected results If the character can be represented by two Unicode points, it will use two, and so on

**Syntax**

```SQL
positionCaseInsensitiveUTF8(string, substring[, start_pos])
```


**Param**


* `String` \- The string in which to search for the substring [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `substring` \- Substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `start_pos` \- An optional parameter, the position of the first character in the string, used to start the search. [UInt](https://docs.byteplus.com/en/docs/bytehouse/docs-string).


**Return value**


* If the substring is found, the starting position in Unicode points (starting from 1).

* If the substring is not found, it is 0.


Type: `Integer`.

**Example**

Query:

```SQL
SELECT positionCaseInsensitiveUTF8('Привет, мир!', 'Мир');
```


As a result:

```Plain
┌─positionCaseInsensitiveUTF8('Привет, мир!', 'Мир')─┐
│ 9                                                  │
└────────────────────────────────────────────────────┘
```


<span id="dc558363"></span>
### positionUTF8

`substring` returns the Location of `string` found in Medium, Use unit Unicode hour, Start from 1.

Work under the assumption that the String contains a set of bytes representing UTF\-8 encoded text. If this assumption is No Satisfy, the function does No throw an Abnormal and returns some unexpected results. If a character can be represented by two Unicode hours, it will use two, and so forth.

For case\-insensitive Search, use the function positionCaseInsensitiveUTF8.

**Syntax**

```SQL
positionUTF8(string, substring[, start_pos])
```


**Param**


* `string` \- The String in which to search for the substring. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `substring` \- substring to search for. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `start_pos` — optional parameter, the position of the first character in the string to start the search[.](https://www.volcengine.com/docs/6517/102207) [UInt](https://docs.byteplus.com/en/docs/bytehouse/docs-string).


**Return value**


* If the substring is found, the starting position in Unicode points (starting from 1).

* If the substring is not found, it is 0.


Type: `Integer`.

**Example**

```SQL
SELECT positionUTF8('Привет, мир!', '!') as example
```


The phrase "Hello, world!" contains a set of Unicode points representing a single dot\-encoded text. The function returns some expected outcomes:

Result:

```Plain
┌─example─┐
│ 12      │
└─────────┘
```


<span id="8106077a"></span>
### regexpExtract

regexpExtract extracts the first string in `haystack` that matches the regexp pattern and corresponds to the regex group index.

**Syntax**

```SQL
regexpExtract(haystack, pattern[, index])
```


**Aliases**: `REGEXP_EXTRACT`

**Arguments**


* `haystack` — A string with which regexp pattern will be matched. `String`.

* `pattern` — Regexp expression. `pattern` may contain multiple regexp groups, `index` indicates which regex group to extract. An index of 0 means matching the entire regular expression. `const String`.

* `index` — Optional. An integer number greater or equal 0 with default 1. It represents which regex group to extract. `(U)Int*`.


**Returned value**

This functin returns a string that matches `String`.

**Examples**

**Usage example**

Query

```SQL
SELECT
    regexpExtract('100-200', '(\\d+)-(\\d+)', 1),
    regexpExtract('100-200', '(\\d+)-(\\d+)', 2),
    regexpExtract('100-200', '(\\d+)-(\\d+)', 0),
    regexpExtract('100-200', '(\\d+)-(\\d+)');
```


Response

```Plain
┌─regexpExtract('100-200', '(\\d+)-(\\d+)', 1)─┬─regexpExtract('100-200', '(\\d+)-(\\d+)', 2)─┬─regexpExtract('100-200', '(\\d+)-(\\d+)', 0)─┬─regexpExtract('100-200', '(\\d+)-(\\d+)')─┐
│ 100                                          │ 200                                          │ 100-200                                      │ 100                                       │
└──────────────────────────────────────────────┴──────────────────────────────────────────────┴──────────────────────────────────────────────┴───────────────────────────────────────────┘
```


<span id="272aea20"></span>
### regexpQuoteMeta

The function in `string` adds a backslash before some predefined characters.

Predefined characters: `\\0`,,,,,,,,,,,,,,,,,. `|()^$.[]?*+{:-`

This implementation slightly differs from re2::RE2::QuoteMeta. It escapes the zero byte as `\\0` instead of , `\\x00` and only escapes the necessary characters.

**Syntax**

```SQL
regexpQuoteMeta(string)
```


**Param**


* `String` – String.


**Return value**

– String.

Type: `string`

**Example**

```SQL
SELECT regexpQuoteMeta(' | , ( , ) , ^ , $ , . , [ , ] , ? ,');
```


As a result:

```Plain
┌─regexpQuoteMeta(' | , ( , ) , ^ , $ , . , [ , ] , ? ,')─┐
│  \| , \( , \) , \^ , \$ , \. , \[ , \] , \? ,           │
└─────────────────────────────────────────────────────────┘
```


<span id="68c2db1c"></span>
### regexp/rlike

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it in relevant dialects.</div>


Matches the string `expression` with the `pattern` in regular matching, if successful returns `1`, otherwise returns `0`.

**Syntax**

```SQL
expression RLIKE pattern;
expression REGEXP pattern;
```


**Param**


* `VARCHAR`


**Return value**


* `BOOLEAN`


**Example**

```SQL
SELECT 'Michael!' REGEXP '.*';
```


```SQL
┌─rlike('Michael!', '.*')─┐
│                       1 │
└─────────────────────────┘
```


<span id="9096def6"></span>
### rpad

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it in relevant dialects.</div>


Appends `str` to the right with `padstr` until the length reaches `len`, and returns the concatenated string.

**Syntax**

```SQL
rpad(str, len, padstr)
```


**Param**


* `str` and `padstr` are both `VARCHAR` type, `len` is `BIGINT` type.


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT rpad('abc',9,'#');  
```


```SQL
┌─rightPad('abc', 9, '#')─┐
│ abc######               │
└─────────────────────────┘
```


<span id="d6240eef"></span>
### repeat

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it in relevant dialects.</div>


Returns a string consisting of the string `str` repeated `count` times

**Syntax**

```SQL
repeat(str, count);
```


**Param**


* `str` is of `VARCHAR` type, `count` is of `BIGINT` type.


**Return Value**


* `VARCHAR`


**Example**

```SQL
SELECT repeat('a', 3);  
```


```SQL
┌─repeat('a', 3)─┐
│ aaa            │
└────────────────┘
```


<span id="db77b092"></span>
### replace

Replace all occurrences in `substring` with . `stringreplacement`

Alias for replaceAll

**Syntax**

```SQL
replace(string, substring, replacement)
```


**Param**


* `String`— The string to search for substrings.

* `Substring`— The substring to search for.

* `Replacement`— Use the replacement string to replace the matching substring.


**Return value**


* Replace all in `substring` with . `stringreplacement`


Type: `string`

**Example**

```SQL
SELECT replace('test target_string test','target_string','CNCH');
```


As a result:

```Plain
┌─replace('test target_string test', 'target_string', 'CNCH')─┐
│ test CNCH test                                              │
└─────────────────────────────────────────────────────────────┘
```


<span id="375d6b5b"></span>
### replaceAll

Replace all in `substring` with `stringreplacement`.

Please refer to [replace](https://docs.byteplus.com/docs/bytehouse/docs-string#db77b092).

<span id="52d75165"></span>
### replaceOne

If it exists, replace the first occurrence of `substring` in it. `stringreplacement`

**Syntax**

```SQL
replaceOne(string, substring, replacement)
```


**Param**


* `string` – The string in which to search for the substring. `string`.

* `substring` – The substring to search for. `string`

* `start_pos` – An optional parameter, the position of the first character in the string to start the search. UInt.


**Return value**


* Replace the first occurrence of a substring in the string with replacement content.


Type: `string`

**Example**

```SQL
SELECT replaceOne('test target_string test target_string','target_string','CNCH');
```


As a result:

```Plain
┌─replaceOne('test target_string test target_string', 'target_string', 'CNCH')─┐
│ test CNCH test target_string                                                 │
└──────────────────────────────────────────────────────────────────────────────┘
```


<span id="0e578c63"></span>
### replaceRegexpAll

This functions the same as replaceAll, but uses regular expressions.


* The pattern can be specified as "replacement". This pattern may contain replacements `\\0-\\9`.

* Replacement of `\\0` includes the entire regular expression. Replacement of `\\1-\\9` corresponds to the subpattern numbers. To `\\` use this character in the template, escape it with `\\`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use re2 regular expression for replacement.</div>


**Syntax**

```SQL
replaceRegexpAll(string, pattern, replacement)
```


**Param**


* `String` – String.

* `Pattern` – Matching pattern.

* `Replacement` – Replaces matched substrings with the replacement String.


**Return Value**


* Replace all occurrences of substrings in the string with replacement content.


Type: `String`

**Example**

```SQL
SELECT replaceRegexpAll('Hello, World!', '.', '\\0\\0');
```


```Plain
┌─replaceRegexpAll('Hello, World!', '.', '\\0\\0')─┐
│ HHeelllloo,,  WWoorrlldd!!                       │
└──────────────────────────────────────────────────┘
```


However, if the regular expression works with empty substrings, multiple replacements will not be performed.

Example:

```SQL
SELECT replaceRegexpAll('Hello, World!', '^', 'here: ');
```


```Plain
┌─replaceRegexpAll('Hello, World!', '^', 'here: ')─┐
│ here: Hello, World!                              │
└──────────────────────────────────────────────────┘
```


<span id="b765395b"></span>
### replaceRegexpOne

If it exists, only the first match is replaced.

Advisory: Replace using pattern regular expressions. re2 regular expressions.

The pattern can be specified as “replacement”. This mode can contain replacement`\\0-\\9`.

Replacement `\0` includes the entire regular expression. Replacement `\1-\9` corresponds to subpattern numbers. To use the character `\` in the template, escape it with `\`.

Also remember that string literals require additional escaping.

**Syntax**

```SQL
replaceRegexpOne(string, pattern, replacement)
```


**Param**


* `string` – String.

* `pattern` – Match mode.

* `replacement` – Replace the matched substring using the replacement string.


**Return Value**


* Replace the first occurrence of a substring in the string with another content.


Type: `string`

**Example**

```SQL
SELECT replaceRegexpOne('test <target_string> test <target_string>','<.*?>','CNCH');
```


As a result:

```Plain
┌─replaceRegexpOne('test <target_string> test <target_string>', '<.*?>', 'CNCH')─┐
│ test CNCH test <target_string>                                                 │
└────────────────────────────────────────────────────────────────────────────────┘
```


**Other examples**

Example 1. Convert the date to American Format:

```SQL
select '2014-03-17', replaceRegexpOne(toString('2014-03-17'), '(\\d{4})-(\\d{2})-(\\d{2})', '\\2/\\3/\\1')
```


```Plain
┌─'2014-03-17'─┬─replaceRegexpOne(toString('2014-03-17'), '(\\d{4})-(\\d{2})-(\\d{2})', '\\2/\\3/\\1')─┐
│ 2014-03-17   │ 03/17/2014                                                                            │
└──────────────┴───────────────────────────────────────────────────────────────────────────────────────┘
```


Example 2. Copy the string ten times:

```SQL
SELECT replaceRegexpOne('Hello, World!', '.*', '\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0');
```


As a result:

```Plain
┌─replaceRegexpOne('Hello, World!', '.*', '\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0')──────────────────────────────────────────────────────────┐
│ Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World!Hello, World! │
└────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```


<span id="5734adf2"></span>
### reverse

Reverse the string (as a byte sequence).

**Grammar**

```SQL
reverse(string)
```


**Parameter**


* `String` – String.


**Return value**


* Reversed string.


Type: `String`

**Example**

```SQL
SELECT reverse('abcd1234')
```


As a result:

```Plain
┌─reverse('abcd1234')─┐
│ 4321dcba            │
└─────────────────────┘
```


<span id="c8674e2f"></span>
### reverseUTF8

Reverses the sequence of Unicode code points, assuming the string contains a series of bytes representing UTF\-8 text. Otherwise, it will carry out other actions (will not raise an exception).

**Syntax**

```SQL
reverseUTF8(string)
```


**Parameters**


* `string` – UTF8 String.


**Return Value**


* The reversed string.


Type: `string`

**Example**

```SQL
SELECT reverseUTF8('\x61\x62\x63\x64\x31\x32\x33\x34')
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">'\x61\x62\x63\x64\x31\x32\x33\x34' in UTF8 format is 'abcd1234'.</div>


As a result:

```Plain
┌─reverseUTF8('abcd1234')─┐
│ 4321dcba                │
└─────────────────────────┘
```


<span id="5f2a2f45"></span>
### size

Returns the length of the string in bytes (not characters or code points).

> Note: This function also applies to arrays.


"length" is an alias.

**Syntax**

```SQL
size(x)
```


**Param**


* `x` – A string or an array.


**Return value**


* The length of the string or array.


Type: `UInt64`

**Example**

```SQL
SELECT size('Hello');
```


Result:

```Plain
┌─size('Hello')─┐
│ 5             │
└───────────────┘
```


Other examples

```SQL
SELECT size([1,2,3,4]);
```


Result:

```Plain
┌─size([1, 2, 3, 4])─┐
│ 4                  │
└────────────────────┘
```


<span id="a3964561"></span>
### splitByChar

Split the string into substrings separated by a specified character. It uses a constant string composed of one character as a `separator`.

Returns an array of the selected substrings. If the separator appears at the beginning or end of the string, or if there are multiple consecutive separators, empty substrings may be selected.

**Syntax**

```SQL
splitByChar(separator, string)
sql
```


**Parameters**


* `Separator`— The separator should exactly contain one character. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `String`— The string to be split. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).


**Return Value**

Returns an array of selected substrings. In the following situations, an empty substring may be selected:


* The separator appears at the beginning or end of the string;

* There are multiple consecutive separators;

* The original `string` is empty.


Type: `array`

**Example**

```SQL
SELECT splitByChar(',', '1,2,3,abcde');
sql
```


Result:

```Plain
┌─splitByChar(',', '1,2,3,abcde')─┐
│ [1, 2, 3, abcde]                │
└─────────────────────────────────┘
```


<span id="c04e7c51"></span>
### splitByString

Split the string into substrings separated by a string. It uses a constant string of multiple characters as the `separator`. If the `separator` is empty, it splits the `string` into an array of individual characters.

**Syntax**

```SQL
splitByString(separator, string)
```


**Parameters**


* `Separator`— should contain the string's delimiter. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).

* `String` to be split. [String](https://docs.byteplus.com/docs/bytehouse/docs-string).


**Return Value**

Returns an array of the selected substrings. In the following cases, an empty substring may be selected:


* The delimiter appears at the beginning or end of the string;

* There are multiple consecutive delimiters;

* The original string `string` is empty.


Type: `array`

**Example**

```SQL
SELECT splitByString('test', 'abctestCNCHtestdef')
```


Result:

```Plain
┌─splitByString('test', 'abctestCNCHtestdef')─┐
│ [abc, CNCH, def]                            │
└─────────────────────────────────────────────┘
```


<span id="d33e73aa"></span>
### startsWith

`string` returns 1 if it starts with the specified `prefix`, otherwise returns 0.

**Syntax**

```SQL
startsWith(string, prefix)
```


**Parameters**


* `string`— String.

* `prefix`— Matching prefix.


**Return Value**


* 1, if the string starts with the specified prefix.

* If the string does not start with the specified prefix.


Type: `UInt8`

**Example**

```SQL
SELECT startsWith('Hello, world!', 'He');
```


Result:

```Plain
┌─startsWith('Hello, world!', 'He')─┐
│ 1                                 │
└───────────────────────────────────┘
```


<span id="897681c0"></span>
### strcmp

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">MySQL\-compatible syntax. It is recommended to use it in related dialects.</div>


If the strings `str 1` and `str 2` are identical, the result is `0`. If `str 1` is less than `str 2` according to the current sort order, the result is `-1`, otherwise the result is `1`.

**Syntax**

```SQL
strcmp(str 1, str 2);
```


**Parameter**


* Both `str 1` and `str 2` are of `VARCHAR` type.


**Return Value**


* `BIGINT`


**Example**

```SQL
SELECT strcmp('text', 'text2');
```


```SQL
┌─strcmp('text', 'text2')─┐
│                      -1 │
└─────────────────────────┘
```


<span id="551670a2"></span>
### substr

Please see substring

Returns a substring starting at the byte indexed in the middle, with a `offset` of `length` bytes. Character indexing starts from one (as in standard SQL).

Note: The `offset` and `length` parameters must be constants.

**Syntax**

```SQL
substring(string, offset, length)
```


**Parameter**


* `string` – String.

* `offset` – Starting offset of the substring.

* `length` – Length of the substring.


**Return value**


* Substring.


Type: `string`

**Example**

```SQL
SELECT substring('Hello CNCH', 7, 4)
```


Result:

```Plain
┌─substr('Hello CNCH', 7, 4)─┐
│ CNCH                       │
└────────────────────────────┘
```


<span id="0dc373a5"></span>
### substringUTF8

Same as [substr](https://docs.byteplus.com/docs/bytehouse/docs-string#551670a2), but targets Unicode code points. Assume the string contains a group of bytes representing UTF\-8 encoded text.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this assumption is not satisfied, it will return some results (it will not raise an Abnormal).</div>


**Syntax**

```SQL
substringUTF8(string, offset, length)
```


**Parameters**


* `string` – A string.

* `offset` – The starting offset of the substring.

* `length` – The length of the substring.


**Return Value**


* Substring.


Type: `string`

**Example**

```SQL
SELECT substringUTF8('\x48\x65\x6c\x6c\x6f\x20\x43\x4e\x43\x48H', 7, 4)
```


Result:

```Plain
┌─substringUTF8('Hello CNCHH', 7, 4)─┐
│ CNCH                               │
└────────────────────────────────────┘
```


<span id="0fba61a0"></span>
### trimBoth

Removes all leading and trailing common spaces (ASCII character 32) from a string. It does not remove other types of space characters (tab, non\-breaking space, etc.).

**Syntax**

```SQL
trimBoth(string)
```


Alias: `trim(string)`.

**Parameters**


* `string`— The string to trim. String.


**Return value**


* A string with no leading or trailing common spaces.


Type: `String`

**Example**

```SQL
SELECT trimBoth('     Hello, world!     ') as a;
```


As a result:

```Plain
┌─a─────────────┐
│ Hello, world! │
└───────────────┘
```


<span id="1a2a55f6"></span>
### trimLeft

Deletes all contiguous common spaces (ASCII character 32) from the beginning of the string. It does not remove other types of space characters (tab, non\-breaking spaces, and others).

**Syntax**

```SQL
trimLeft(string)
```


Alias: `trim(string)`.

**Param**


* `String` \- The string to be trimmed. String.


**Return value**


* String without leading or trailing spaces.


Type: `String`

**Example**

```SQL
SELECT trimLeft('     Hello, world!     ') as example
```


As a result:

```Plain
┌─example────────────┐
│ Hello, world!      │
└────────────────────┘
```


<span id="1ed3a53d"></span>
### trimRight

Deletes all consecutive spaces at the end of the string (ASCII character 32). It does not remove other types of whitespace characters (tabs, non\-breaking spaces, etc.).

**Grammar**

```SQL
trimRight(string)
```


Alias: `trim(string)`.

**Param**


* `String`— The string to trim. String.


**Return Value**


* String without trailing common spaces.


Type: `String`

**Example**

```SQL
SELECT trimRight('     Hello, world!     ');
```


As a result:

```Plain
┌─trimLeft('     Hello, world!     ')─┐
│ Hello, world!                       │
└─────────────────────────────────────┘
```


<span id="d4f388c7"></span>
### tryBase64Decode

Similar to base64Decode, but returns an empty string if an error occurs.

**Syntax**

```SQL
tryBase64Decode(string)
```


**Parameter**


* `String` \- A string that is base64 encoded.


**Return Value**


* Decoded string.


Type: `String`

**Example**

```SQL
SELECT tryBase64Decode('SGVsbG8gV29ybGQh');
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">'SGVsbG8gV29ybGQh' translates to 'Hello World!' ' into its base64 encoded Format.</div>


Result:

```Plain
┌─tryBase64Decode('SGVsbG8gV29ybGQh')─┐
│ Hello World!                        │
└─────────────────────────────────────┘
```


<span id="d0cce5ee"></span>
### ucase

Convert ASCII Latin symbols in strings to uppercase.

**Grammar**

```SQL
ucase(string)
```


**Param**


* `String` – String.


**Return Value**


* String in uppercase letters.


Type: `string`

**Example**

```SQL
SELECT ucase('ABCdef');
```


As a result

```Plain
┌─ucase('ABCdef')─┐
│ ABCDEF          │
└─────────────────┘
```


<span id="c7f73a10"></span>
### upper

Converts ASCII Latin characters in a string to uppercase.

**Syntax**

```SQL
upper(string)
```


**Param**


* `String` – String.


**Return Value**


* String with uppercase letters.


Type: `String`

**Example**

```SQL
SELECT upper('ABCdef');
```


As a result:

```Plain
┌─upper('ABCdef')─┐
│ ABCDEF          │
└─────────────────┘
```


<span id="5afec2b3"></span>
### upperUTF8

Convert the string to uppercase, assuming the string contains a set of bytes that make up UTF\-8 encoded text.


* It does not detect language. Therefore, the results may not be entirely correct for Turkish.

* If the UTF\-8 byte sequence lengths differ between uppercase and lowercase of a code point, then the result for that code point may be incorrect.

* If the string contains a set of non\-UTF\-8 bytes, then the behaviour is undefined.


**Syntax**

```SQL
upperUTF8(string)
```


**Param**


* `String` – UTF8 string.


**Return value**


* A string of uppercase letters.


Type: `string`

**Example**

Encoding 'hello world!' ' in UTF8 '\x68\x65\x6c\x6c\x6f\x20\x77\x6f\x72\x6c\x64\x20\xef\xbc\x81'

```SQL
SELECT upperUTF8('\x68\x65\x6c\x6c\x6f\x20\x77\x6f\x72\x6c\x64\x20\xef\xbc\x81');
```


As a result:

```Plain
┌─upperUTF8('hello world ！')─┐
│ HELLO WORLD ！                │
└──────────────────────────────┘
```
