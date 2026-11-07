---
title: "JSON Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/json-functions"
---

In Yandex.Metrica, users employ JSON as an access parameter. Some functions have been implemented to process these JSONs. (Although in most cases, JSON requires additional processing beforehand, and the resulting values are placed in separate columns.) All these functions make as many assumptions as possible. To allow the functions to complete their tasks as quickly as possible.
We make the following assumptions about the JSON format:

1. The field names (parameters of the function) must be constants.
2. Field names must use standard encoding. For example: `visitParamHas('{"abc":"def"}', 'abc') = 1`, but `visitParamHas('{"\\u0061\\u0062\\u0063":"def"}', 'abc') = 0`
3. The functions can freely search for fields in multi-layer nested structures. If multiple matching fields exist, the first matching field is returned.
4. JSON does not contain spaces other than in string texts.

<span id="visitparamhas-参数，名称"></span>
## visitParamHas(parameter, name)
Check if a field named «name» exists.
<span id="visitparamextractuint-参数，名称"></span>
## visitParamExtractUInt(parameter, name)
Parse the value of the field named «name» into UInt64. If this is a string field, the function will attempt to parse a number from the beginning of the string. If the field does not exist, or if a number cannot be parsed from it, return 0.
<span id="visitparamextractint-参数，名称"></span>
## visitParamExtractInt(parameter, name)
Similar to visitParamExtractUInt, but returns Int64.
<span id="visitparamextractfloat-参数，名称"></span>
## visitParamExtractFloat(parameter, name)
Similar to visitParamExtractUInt, but returns Float64.
<span id="visitparamextractbool-参数，名称"></span>
## visitParamExtractBool(parameter, name)
Parses true/false values. The result is of type UInt8.
<span id="visitparamextractraw-参数，名称"></span>
## visitParamExtractRaw(parameter, name)
Returns the value of the field, including whitespace characters.
Example:
<span id="visitparamextractstring-参数，名称"></span>
## ```plaintext
visitParamExtractRaw('{"abc":"\\n\\u0000"}', 'abc') = '"\\n\\u0000"'
visitParamExtractRaw('{"abc":{"def":[1,2,3]}}', 'abc') = '{"def":[1,2,3]}'
```

<span id="visitparamextractstring-参数，名称"></span>
## visitParamExtractString(parameter, name)
Parses strings using double quotes. This value has not been escaped. If the escape fails, it will return an empty string.
Example:
```plaintext
visitParamExtractString('{"abc":"\\n\\u0000"}', 'abc') = '\n\0'
visitParamExtractString('{"abc":"\\u263a"}', 'abc') = '☺'
visitParamExtractString('{"abc":"\\u263"}', 'abc') = ''
visitParamExtractString('{"abc":"hello}', 'abc') = ''
```

Currently, character encodings such as `\\uXXXX\\uYYYY` are not supported as they are not in the Basic Multilingual Plane (they are converted to CESU-8 instead of UTF-8).
The following functions are based on [simdjson](https://github.com/lemire/simdjson), designed for more complex JSON parsing requirements. However, the aforementioned assumption 2 still applies.
<span id="jsonhas-json-indices-or-keys-…"></span>
## JSONHas(json[, indices_or_keys]…)
If the value exists in the JSON, it will return `1`.
If the value does not exist, it will return `0`.
Example:
```plaintext
select JSONHas('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 1
select JSONHas('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 4) = 0
```

`indices_or_keys` can be a list of zero or more parameters, each of which can be a string or an integer.

* String = Access JSON object members by member name.
* Positive integer = Access the nth member/member name from the beginning.
* Negative integer = Access the nth member/member name from the end.

You can use integers to access JSON arrays and JSON objects.
For example:
<span id="jsonlength-json-indices-or-keys-…"></span>
## ```plaintext
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', 1) = 'a'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', 2) = 'b'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', -1) = 'b'
select JSONExtractKey('{"a": "hello", "b": [-100, 200.0, 300]}', -2) = 'a'
select JSONExtractString('{"a": "hello", "b": [-100, 200.0, 300]}', 1) = 'hello'
```

<span id="jsonlength-json-indices-or-keys-…"></span>
## JSONLength(json[, indices_or_keys]…)
Returns the length of a JSON array or JSON object.
If the value does not exist or the type is incorrect, `0` will be returned.
Example:
<span id="jsontype-json-indices-or-keys-…-返回json值的类型。"></span>
## ```plaintext
select JSONLength('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 3
select JSONLength('{"a": "hello", "b": [-100, 200.0, 300]}') = 2
```

<span id="jsontype-json-indices-or-keys-…-返回json值的类型。"></span>
## JSONType(json[, indices_or_keys]…) returns the type of a JSON value.
If the value does not exist, it will return `Null`.
Example:
<span id="jsonextractuint-json-indices-or-keys-…"></span>
## ```plaintext
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}') = 'Object'
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}', 'a') = 'String'
select JSONType('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = 'Array'
```

<span id="jsonextractuint-json-indices-or-keys-…"></span>
## JSONExtractUInt(json[, indices_or_keys]…)
<span id="jsonextractint-json-indices-or-keys-…"></span>
## JSONExtractInt(json[, indices_or_keys]…)
<span id="jsonextractfloat-json-indices-or-keys-…"></span>
## JSONExtractFloat(json[, indices_or_keys]…)
<span id="jsonextractbool-json-indices-or-keys-…"></span>
## JSONExtractBool(json[, indices_or_keys]…)
Parse JSON and extract values. These functions are similar to `visitParam*` functions.
If the value does not exist or the type is incorrect, it will return `0`.
Example:
<span id="jsonextractstring-json-indices-or-keys-…"></span>
## ```plaintext
select JSONExtractInt('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 1) = -100
select JSONExtractFloat('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 2) = 200.0
select JSONExtractUInt('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', -1) = 300
```

<span id="jsonextractstring-json-indices-or-keys-…"></span>
## JSONExtractString(json[, indices_or_keys]…)
Parse JSON and extract strings. This function is similar to `visitParamExtractString`.
If the value does not exist or has a type error, it returns an empty string.
The value is not escaped. If unescaping fails, it returns an empty string.
Example:
<span id="jsonextract-json-indices-or-keys…-return-type"></span>
## ```plaintext
select JSONExtractString('{"a": "hello", "b": [-100, 200.0, 300]}', 'a') = 'hello'
select JSONExtractString('{"abc":"\\n\\u0000"}', 'abc') = '\n\0'
select JSONExtractString('{"abc":"\\u263a"}', 'abc') = '☺'
select JSONExtractString('{"abc":"\\u263"}', 'abc') = ''
select JSONExtractString('{"abc":"hello}', 'abc') = ''
```

<span id="jsonextract-json-indices-or-keys…-return-type"></span>
## JSONExtract(json[, indices_or_keys…], Return_type)
Parse JSON and extract values of the given ClickHouse data type.
This is a variant of the previous `JSONExtract` function. `This means` that JSONExtract(…, ‘String’)`returns exactly the same as`JSONExtractString()`.` JSONExtract(…, ‘Float64’)`returns exactly the same as`JSONExtractFloat().
Example:
<span id="jsonextractkeysandvalues-json-indices-or-keys…-value-type"></span>
## ```plaintext
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'Tuple(String, Array(Float64))') = ('hello',[-100,200,300])
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'Tuple(b Array(Float64), a String)') = ([-100,200,300],'hello')
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 'Array(Nullable(Int8))') = [-100, NULL, NULL]
SELECT JSONExtract('{"a": "hello", "b": [-100, 200.0, 300]}', 'b', 4, 'Nullable(Int64)') = NULL
SELECT JSONExtract('{"passed": true}', 'passed', 'UInt8') = 1
SELECT JSONExtract('{"day": "Thursday"}', 'day', 'Enum8(\'Sunday\' = 0, \'Monday\' = 1, \'Tuesday\' = 2, \'Wednesday\' = 3, \'Thursday\' = 4, \'Friday\' = 5, \'Saturday\' = 6)') = 'Thursday'
SELECT JSONExtract('{"day": 5}', 'day', 'Enum8(\'Sunday\' = 0, \'Monday\' = 1, \'Tuesday\' = 2, \'Wednesday\' = 3, \'Thursday\' = 4, \'Friday\' = 5, \'Saturday\' = 6)') = 'Friday'
```

<span id="jsonextractkeysandvalues-json-indices-or-keys…-value-type"></span>
## JSONExtractKeysAndValues(json[, indices_or_keys…], Value_type)
Parse key-value pairs from JSON, where the values are given ClickHouse data types.
Example:
<span id="jsonextractraw-json-indices-or-keys-…"></span>
## ```plaintext
SELECT JSONExtractKeysAndValues('{"x": {"a": 5, "b": 7, "c": 11}}', 'x', 'Int8') = [('a',5),('b',7),('c',11)];
```

<span id="jsonextractraw-json-indices-or-keys-…"></span>
## JSONExtractRaw(json[, indices_or_keys]…)
Returns a part of JSON.
If a component does not exist or there is a type error, an empty string is returned.
Example:
```plaintext
select JSONExtractRaw('{"a": "hello", "b": [-100, 200.0, 300]}', 'b') = '[-100, 200.0, 300]'
```
