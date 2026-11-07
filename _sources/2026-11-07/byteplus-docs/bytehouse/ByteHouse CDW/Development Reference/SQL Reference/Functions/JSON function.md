---
title: "JSON function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-json"
---

Here are the assumptions we've made regarding the JSON format:


1. Field names (function parameters) must be constants.

2. Field names must use standard encoding. For example: `visitParamHas('{"abc":"def"}', 'abc') = 1`, but `visitParamHas('{"\\u0061\\u0062\\u0063":"def"}', 'abc') = 0`

3. The function can search for fields arbitrarily within multi\-layer nested structures. If multiple matching fields exist, the first matching field is returned.

4. Aside from string text, JSON does not contain spaces.


<span id="9c831f77"></span>
### visitParamHas(param, name)

Check whether a "name" field exists.

<span id="fc0cb178"></span>
### visitParamExtractUInt(Param, Name)

Parse the value of the field named "Name" into UInt64. If it is a string field, the function will try to parse a number from the beginning of the string. If the field does not exist, or if a number cannot be parsed from it, then return 0.

<span id="4e2e7af5"></span>
### visitParamExtractInt(Param, Name)

Same as visitParamExtractUInt but returns Int64.

<span id="4dae7c7e"></span>
### visitParamExtractFloat(Param, Name)

Same as visitParamExtractUInt but returns Float64.

<span id="089bcc18"></span>
### visitParamExtractBool(Param, Name)

Parse true/false values. As a result, it is of UInt8 Type.

<span id="08fd3da5"></span>
### visitParamExtractRaw(Param, Name)

Return value of the field, contains space characters.

Example:

```SQL
visitParamExtractRaw('{"abc":"\\n\\u0000"}', 'abc') = '"\\n\\u0000"'
visitParamExtractRaw('{"abc":{"def":[1,2,3]}}', 'abc') = '{"def":[1,2,3]}'
```


<span id="c3fffd31"></span>
### visitParamExtractString(Param, Name)

Use double quotes to parse strings. Value was not escaped. If conversion fails, it will return an empty string.

Example:

```SQL
visitParamExtractString('{"abc":"\\n\\u0000"}', 'abc') = '\n\0'
visitParamExtractString('{"abc":"\\u263a"}', 'abc') = '☺'
visitParamExtractString('{"abc":"\\u263"}', 'abc') = ''
visitParamExtractString('{"abc":"hello}', 'abc') = ''
```


Currently, character encodings like `\uXXXX\uYYYY` are not supported, as they are not in the Basic Multilingual Plane (they are converted to CESU\-8 instead of UTF\-8).

The functions below are based on [simdjson](https://github.com/lemire/simdjson), designed for more complex JSON parsing requirements. However, assumption 2 still applies.

<span id="90db8d73"></span>
### JSONHas(json[, indices_or_keys]…)

If the value exists in the JSON, it returns `1`.

If the value does not exist, it returns `0`.

Example:

```SQL
select JSONHas('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 1
select JSONHas('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 4) = 0
```


`Indices_or_keys` may be a list of zero or more parameters, each of which can be a string or integer.


* String = Access JSON object members by member name.

* Positive integer = Access the No. n member / member name from the beginning.

* Negative integer = Access the No. n member / member name from the end.


You can use integers to access JSON arrays and JSON objects.

For example:

```SQL
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', 1) = 'a'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', 2) = 'b'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', -1) = 'b'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', -2) = 'a'
select JSONExtractString('{"a": "hello", "b": [-100, 200.0, 300]}', 1) = 'hello'
```


<span id="60c3479d"></span>
### JSONLength(json[, indices_or_keys]…)

Returns the length of a JSON array or JSON object.

If the value does not exist or is of the wrong type, it will return `0`.

Example:

```SQL
select JSONLength('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 3
select JSONLength('{"a": "hello", "b": [-100, 200.0, 300]}') = 2
```


<span id="59f22622"></span>
### JSONType(json[, indices_or_keys]…) returns the type of the JSON value

If the value does not exist, it will return `Null`.

Example:

```SQL
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}') = 'Object'
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}', 'a') = 'String'
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 'Array'
```


<span id="d37dcd35"></span>
### JSONExtractUInt(json[, indices_or_keys]…)

<span id="21f4d92f"></span>
### JSONExtractInt(json[, indices_or_keys]…)

<span id="e36f863e"></span>
### JSONExtractFloat(json[, indices_or_keys]…)

<span id="1f5675d7"></span>
### JSONExtractBool(json[, indices_or_keys]…)

Analyze JSON and extract values. These functions are similar to `visitParam*` functions.

If the value doesn't exist or is of the incorrect type, it will return `0`.

Example:

```SQL
select JSONExtractInt('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 1) = -100
select JSONExtractFloat('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 2) = 200.0
select JSONExtractUInt('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', -1) = 300
```


<span id="68d76392"></span>
### JSONExtractString(json[, indices_or_keys]…)

Analyze JSON and extract strings. This function is similar to `visitParamExtractString` function.

An empty string will be returned if the value doesn't exist or is of the wrong type.

The value is not escaped. If unescaping fails, an empty string is returned.

Example:

```SQL
select JSONExtractString('{"a": "hello", "b": [-100, 200.0, 300]}', 'a') = 'hello'
select JSONExtractString('{"abc":"\\n\\u0000"}', 'abc') = '\n\0'
select JSONExtractString('{"abc":"\\u263a"}', 'abc') = '☺'
select JSONExtractString('{"abc":"\\u263"}', 'abc') = ''
select JSONExtractString('{"abc":"hello}', 'abc') = ''
```


<span id="c269b2ec"></span>
### JSONExtract(json[, indices_or_keys…], Return_type)

Parse JSON and extract values of the specified ClickHouse data type.

This is a variant of the previous `JSONExtract` function. `This means` JSONExtract(…, ‘String’)`returns the same as` JSONExtractString()`does.` JSONExtract(…, ‘Float64’)`returns the same as` JSONExtractFloat() does.

Example:

```SQL
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'Tuple(String, Array(Float64))') = ('hello',[-100,200,300])
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'Tuple(b Array(Float64), a String)') = ([-100,200,300],'hello')
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 'Array(Nullable(Int8))') = [-100, NULL, NULL]
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 4, 'Nullable(Int64)') = NULL
SELECT JSONExtract('{"passed": true}', 'passed', 'UInt8') = 1
SELECT JSONExtract('{"day": "Thursday"}', 'day', 'Enum8(\'Sunday\' = 0, \'Monday\' = 1, \'Tuesday\' = 2, \'Wednesday\' = 3, \'Thursday\' = 4, \'Friday\' = 5, \'Saturday\' = 6)') = 'Thursday'
SELECT JSONExtract('{"day": 5}', 'day', 'Enum8(\'Sunday\' = 0, \'Monday\' = 1, \'Tuesday\' = 2, \'Wednesday\' = 3, \'Thursday\' = 4, \'Friday\' = 5, \'Saturday\' = 6)') = 'Friday'
```


<span id="5e16d2c4"></span>
### JSONExtractKeysAndValues(json[, indices_or_keys…], Value_type)

Extract key\-value pairs from JSON, where the values are of a specified ClickHouse data type.

Example:

```SQL
SELECT JSONExtractKeysAndValues('{"x": {"a": 5, "b": 7, "c": 11}}', 'x', 'Int8') = [('a',5),('b',7),('c',11)];
```


<span id="d599f59d"></span>
### JSONExtractRaw(json[, indices_or_keys]…)

Returns a part of the JSON.

If the part does not exist or is of the wrong type, an empty string will be returned.

Example:

```SQL
select JSONExtractRaw('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = '[-100, 200.0, 300]'
```


<span id="e3cf3e54"></span>
### JSON_EXISTS

Checks if a json path exists; 1 for exists, 0 for does not exist

**Syntax**

```SQL
JSON_EXISTS(json, path)
```


**Param**


* **`json`** — valid Json format. String/Object.

* **`path`** — Json sub\-element path. String


**Return value**


* 1 indicates the path exists in Json, otherwise it is 0


**Example**

```SQL
SELECT JSON_EXISTS('{"hello":1}', '$.hello');
SELECT JSON_EXISTS('{"hello":{"world":1}}', '$.hello.world');
SELECT JSON_EXISTS('{"hello":["world"]}', '$.hello[*]');
SELECT JSON_EXISTS('{"hello":["world"]}', '$.hello[0]');
```


<span id="f63c1089"></span>
### JSON_QUERY

Analyze the Json object or Json array pointed to by the path; return an empty string if the path does not exist

**Syntax**

```SQL
JSON_QUERY(json, path)
```


**Param**


* **`json`** — A valid json. String/Object

* **`path`** — Json path in String form. [String](https://clickhouse.com/docs/en/sql-reference/data-types/string).


**Return value**


* Returns a json object or json array in String form; if the path does not exist, returns an empty string


**Example**

Query:

```SQL
SELECT JSON_QUERY('{"hello":"world"}', '$.hello');
SELECT JSON_QUERY('{"array":[[0, 1, 2, 3, 4, 5], [0, -1, -2, -3, -4, -5]]}', '$.array[*][0 to 2, 4]');
SELECT JSON_QUERY('{"hello":2}', '$.hello');
SELECT toTypeName(JSON_QUERY('{"hello":2}', '$.hello'));
```


Result:

```Plain
["world"]
[0, 1, 4, 0, -1, -4]
[2]
String
```


<span id="74ae0e26"></span>
### JSON_VALUE

Analyze the scalar value of the JSON object pointed to by json path; if it doesn't exist, return an empty string.


* **`function_json_value_return_type_allow_nullable`** = **`true`**, if the json path points to a complex type (such as: struct, array, map), it will return NULL.

* **`function_json_value_return_type_allow_complex`** = **`true`**, if the json path points to a complex type, it will return a String form of the value.


**Syntax**

```SQL
JSON_VALUE(json, path)
```


**Param**


* **`json`** — A string with valid JSON. String/Object

* **`path`** — A string representing the path. String


**Return value**


* If the path exists, it returns the scalar value in string form; otherwise, it returns an empty string


**Example**

Query:

```SQL
SELECT JSON_VALUE('{"hello":"world"}', '$.hello');
SELECT JSON_VALUE('{"array":[[0, 1, 2, 3, 4, 5], [0, -1, -2, -3, -4, -5]]}', '$.array[*][0 to 2, 4]');
SELECT JSON_VALUE('{"hello":2}', '$.hello');
SELECT toTypeName(JSON_VALUE('{"hello":2}', '$.hello'));
select JSON_VALUE('{"hello":"world"}', '$.b') settings function_json_value_return_type_allow_nullable=true;
select JSON_VALUE('{"hello":{"world":"!"}}', '$.hello') settings function_json_value_return_type_allow_complex=true;
```


Result:

```Plain
world
0
2
String
```


<span id="b76b6a7b"></span>
### toJSONString

Serializes the type into a JSON form string

**Syntax**

```SQL
toJSONString(value)
```


Param


* **`value`** — Value to serialize. Value may be of any data type.


**Return value**


* JSON representation of the value. [String](https://clickhouse.com/docs/en/sql-reference/data-types/string).


**Example**

Query:

```SQL
SELECT toJSONString(map('key1', 1, 'key2', 2));
SELECT toJSONString(tuple(1.25, NULL, NaN, +inf, -inf, [])) SETTINGS output_format_json_quote_denormals = 1;
```


Result:

```Plain
{"key1":1,"key2":2}
[1.25,null,"nan","inf","-inf",[]]
```


<span id="6c783a5c"></span>
### JSONArrayLength

Returns the number of outer elements in the JSON array.

**Syntax**

```SQL
JSONArrayLength(json)
```


Alias: **`JSON_ARRAY_LENGTH(json)`** .

**Parameters**


* **`json`** — A valid json. String/Object


**Return Value**


* The number of the outermost elements in the json array; return NULL if json is invalid.


**Example**

```SQL
SELECT
    JSONArrayLength(''),
    JSONArrayLength('[1,2,3]')

┌─JSONArrayLength('')─┬─JSONArrayLength('[1,2,3]')─┐
│                ᴺᵁᴸᴸ │                          3 │
└─────────────────────┴────────────────────────────┘
```


<span id="0089973d"></span>
### get_json_object

Returns

**Syntax**

```SQL
get_json_object(json, path)
```


**Param**


* **json** — Valid json. String/Object, json content is considered invalid if it contains escape characters like `'{"test_key":"\\ntest_value"}'`

* **path** — Subpath in json, in the form '$.key'


**Return value**


* If json is of a nullable type, then it returns Nullable(String), otherwise it returns String


**Example**

```SQL
select get_json_object('{"key":"value"}', '$.key'); --value
select get_json_object(null, '$.key'); --NULL
select get_json_object('{"key":"\nvalue"}', '$.key'); --
select get_json_object('{"key":"\nvalue"}', '$.key'); --\nvalue
```
