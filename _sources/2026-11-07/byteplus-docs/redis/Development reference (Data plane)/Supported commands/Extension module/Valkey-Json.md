---
title: "Valkey-Json"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Valkey-Json"
---

Cache for Redis provides the Valkey\-Json extension module, based on the Valkey module, which supports natively storing, querying, and modifying JSON data. This eliminates the tedious process of serializing JSON into strings or splitting it into HASH fields. The Valkey\-Json implementation fully complies with RFC7159 and ECMA\-404 JSON data exchange standards. It provides advanced query capabilities through the JSONPath query language, including wildcard selection, filter expressions, array slicing, union operations, and recursive search. This topic introduces relevant information about the Valkey\-Json extension module in Cache for Redis, including its features, limits, and specific command syntax.

<span id="UavOqgKs"></span>
## Prerequisites


* To use the Valkey\-Json extension module, instance versions must meet all the following requirements:

   * The database version must be Redis 7.0.

   * The minor version of proxy must be greater than or equal to 1.604.0.

   * The minor version of server must be greater than or equal to 7.604.0.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the database version and minor version information of an instance on the <strong>Summary</strong> tab. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id="EIaXLPAo"></span>
## Features

The Valkey\-Json extension module of Cache for Redis provides the following core capabilities:


* **Native JSON storage**: Store JSON documents as native data types in Redis, avoiding performance overhead caused by serialization and deserialization.

* **JSONPath query**: Precisely locate and batch update using JSONPath expressions, supporting advanced syntax such as wildcards (`*`), recursive descent (`..`), array slicing (`[start:end:step]`), union (`[ , ]`), and filter expressions (`?()`).

* **In\-place updates**: Support atomic updates for specific fields or elements within JSON documents, without rewriting the entire document.

* **Complete type support**: Fully support JSON types such as `object`, `array`, `string`, number, `integer`, `boolean`, and`null`.


<span id="Hm9WYzH6"></span>
## Limits


* **Performance characteristics**: The performance of JSON operations is mainly affected by the complexity of JSONPath expressions and the size and depth of JSON documents. When using direct paths (e.g., `$.user.name`), most commands such as `JSON.GET`, `JSON.SET`, `JSON.DEL`, `JSON.NUMINCRBY`, `JSON.STRAPPEND`, and `JSON.ARRAPPEND` typically have a time complexity of O(1); however, when using recursive or filter paths (e.g., `$..[?(@.active==true)]`), the complexity may increase to O(N). Minimize deep nesting and use filter paths appropriately for optimal performance.

* **Common error prefixes**: Each error message has a specific prefix to facilitate troubleshooting:

   * `ERR`: General error.

   * `LIMIT`: Size limit exceeded error, e.g., document size or nesting depth exceeded.

   * `NONEXISTENT`: Key or path does not exist.

   * `OUTOFBOUNDARIES`: Array index out of bounds.

   * `SYNTAXERR`: Syntax error.

   * `WRONGTYPE`: Value type error.


<span id="kv76yNMV"></span>
## Path syntax

Valkey\-Json supports two types of path syntax:


* **Enhanced Syntax**: Starts with `$` and follows [JSONPath syntax proposed by Goessner](https://goessner.net/articles/JsonPath/). It is recommended to consistently use enhanced syntax for new services.

* **Restricted Syntax**: Has limited query capabilities, only supporting basic operators like `.` and `[]`.


If the query path starts with `$`, use enhanced syntax; otherwise, use restricted syntax.

<span id="8LFrdELd"></span>
### Enhanced Syntax Symbols and Expressions


|Symbol / Expression |Description |
|---|---|
|`$` |Root element. |
|`.` or `[]` |Sub\-element operator. |
|`..` |Recursive descent. |
|`*` |Wildcard, matches all elements in an object or array. |
|`[]` |Array subscript operator, indexes start from 0. |
|`[ , ]` |Union Operator. |
|`[start:end:step]` |Array slicing operator. |
|`?()` |Apply filter expressions to the current array or object. |
|`()` |Filter expression. |
|`@` |Reference the currently processed node in the filter expression. |
|`==` |Equals, used to filter expressions. |
|`!=` |Not equal to, used for filter expressions. |
|`>` |Greater than. Used for filter expressions. |
|`>=` |Greater than or equal to, used for filtering expressions. |
|`<` |Less than, for filtering expressions. |
|`<=` |Less than or equal to, for filter expressions. |
|`&&` |Logical AND, used to combine multiple filter expressions. |
|`\|\|` |Logical OR, used to combine multiple filter expressions. |


<span id="EQHs6gWc"></span>
### Restricted Syntax Symbols and Expressions


|Symbols / Expressions |Description |
|---|---|
|`.` Or `[]` |Sub\-element operator |
|`[]` |Array index operator; indexes start from 0. |


<span id="ySx2ZDBp"></span>
## Command syntax

<span id="qyE49Bow"></span>
### Command list

Valkey\-Json supported commands are listed in the following table.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="default"><code>Uppercase keyword</code>: Command keyword, such as JSON.SET.</div>


* <div data-tips="true" data-tips-type="default"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="default"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>


* <div data-tips="true" data-tips-type="default"><code><Option 1>|<Option 2>|<Option n></code>: A set of mutually exclusive parameter options, meaning only one parameter can be selected from the options for setting.</div>




|command |Syntax |Description |
|---|---|---|
|JSON.SET |`JSON.SET <key> <path> <json> [NX \| XX]` |Write JSON values at the specified `path`. |
|JSON.GET |`JSON.GET <key> [INDENT <indent>] [NEWLINE <newline>] [SPACE <space>] [NOESCAPE] [path ...]` |Reads JSON values from one or more paths and returns them as serialized JSON strings. |
|JSON.MGET |`JSON.MGET <key> [<key> ...] <path>` |Read values from the same path across multiple JSON keys. |
|JSON.MSET |`JSON.MSET <key> <path> <json> [<key> <path> <json> ...]` |Atomically set JSON values for multiple keys. |
|JSON.DEL |`JSON.DEL <key> [path]` |Delete the JSON value at the specified path. |
|JSON.FORGET |`JSON.FORGET <key> [path]` |Alias for `JSON.DEL`. |
|JSON.CLEAR |`JSON.CLEAR <key> [path]` |Clear array or object content, but retain the container. |
|JSON.TYPE |`JSON.TYPE <key> [path]` |Return the JSON type of the value at the specified path. |
|JSON.RESP |`JSON.RESP <key> [path]` |Return the JSON value at the specified path in RESP format. |
|JSON.NUMINCRBY |`JSON.NUMINCRBY <key> <path> <number>` |Increase the numeric value on the path by a specified increment. |
|JSON.NUMMULTBY |`JSON.NUMMULTBY <key> <path> <number>` |Multiply the numerical value at the path by a given factor. |
|JSON.STRAPPEND |`JSON.STRAPPEND <key> [path] <json_string>` |Appends content to the JSON string at the path. |
|JSON.STRLEN |`JSON.STRLEN <key> [path]` |Return the length of the JSON string at the path. |
|JSON.TOGGLE |`JSON.TOGGLE <key> [path]` |Toggle the boolean value on the path between true and false. |
|JSON.ARRAPPEND |`JSON.ARRAPPEND <key> <path> <json> [<json> ...]` |Append one or more JSON values to the end of an array. |
|JSON.ARRINDEX |`JSON.ARRINDEX <key> <path> <json-scalar> [start [end]]` |Finds the position of the first occurrence of a specified scalar value in an array. |
|JSON.ARRINSERT |`JSON.ARRINSERT <key> <path> <index> <json> [<json> ...]` |Insert one or more values before the specified index in the array. |
|JSON.ARRLEN |`JSON.ARRLEN <key> [path]` |Returns the length of the array at the path. |
|JSON.ARRPOP |`JSON.ARRPOP <key> [path [index]]` |Pops the element at the specified index from the array. |
|JSON.ARRTRIM |`JSON.ARRTRIM <key> <path> <start> <end>` |Crop the array to the sub\-array corresponding to the closed interval [start, end]. |
|JSON.OBJKEYS |`JSON.OBJKEYS <key> [path]` |Returns a list of key names for objects at the path. |
|JSON.OBJLEN |`JSON.OBJLEN <key> [path]` |Returns the number of keys contained in the object at the path. |


<span id="mGAwITpf"></span>
### Precautions


* To use the Valkey\-Json feature, [submit a support ticket](https://console.byteplus.com/workorder/create/) to contact technical support and request access.

* After the application is completed, accounts with the Administrator role will have all permissions for Valkey\-Json related commands by default. You can also create new roles according to your business needs, and then after logging in to Redis with an account for that role, use Valkey\-Json related commands. For specific procedures about creating a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role).

* The Cache for Redis supports big and hot key analysis for the Valkey\-Json data type. It can help timely discover and analyze the details of hot keys and big keys in the database, providing data references for you to optimize hot keys and big keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).


<span id="1ZiJSDxo"></span>
### JSON.SET


|Category |Description |
|---|---|
|Command syntax |`JSON.SET <key> <path> <json> [NX \| XX]` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Write JSON values at the specified `path`. This command can overwrite existing values or add new members to an object when path rules are met. An error is returned if the path points to a non\-existent parent node, if types do not match, or if the array index is out of bounds. |
|Option |* `<key>`: JSON document key name, required.<br><br>* `<path>`: Target JSON path, required.<br><br>* `<json>`: The JSON serialized value to be written, required.<br><br>* `NX`: Set only if the target path does not exist, optional.<br><br>* `XX`: Set only if the target path already exists, optional. |
|Response |* On success, returns `OK`.<br><br>* When `NX`/`XX` conditions are not met: RESP2 returns `Nil`, RESP3 returns `Null`.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>`JSON.SET k1 . '{"firstName":"John","lastName":"Smith","age":27}'`<br><br>&nbsp;<br><br>Response example.<br><br>`OK` |


<span id="CKqo8Gks"></span>
### JSON.GET


|Category |Description |
|---|---|
|Command syntax |`JSON.GET <key> [INDENT <indent>] [NEWLINE <newline>] [SPACE <space>] [NOESCAPE] [path ...]` |
|Time complexity |O(N), where N is the number of paths. |
|Command description |Reads JSON values from one or more paths and returns them as serialized JSON strings. Supports controlling formatted output with `INDENT`, `NEWLINE`, `SPACE`, and escape behavior with `NOESCAPE`. |
|Option |* `<key>`: JSON document key name, required.<br><br>* `INDENT < indent >`: Indent character, optional.<br><br>* `NEWLINE < newline >`: newline character, optional.<br><br>* `SPACE <space>`: Space character, optional.<br><br>* `NOESCAPE`: Do not escape non\-ASCII characters when outputting, optional.<br><br>* `<Path>`: The JSON path to read, you can specify multiple; read the root value when omitted. |
|Response |* For enhanced paths, a single path returns a serialized string of the matching result array; multiple paths return a JSON object string with paths as keys and results as values.<br><br>* Under a restricted path, returns the serialized JSON of the corresponding value.<br><br>* When the path or key does not exist, returns an empty array, `Nil`/`Null`, depending on the path syntax and protocol version. |
|Example |Command example.<br><br>`JSON.GET k1 $.firstName $.lastName $.age`<br><br>&nbsp;<br><br>Response example.<br><br>`"{\"$.firstName\":[\"John\"],\"$.lastName\":[\"Smith\"],\"$.age\":[27]}"` |


<span id="S5b5x21B"></span>
### JSON.MGET


|Category |Description |
|---|---|
|Command syntax |`JSON.MGET <key> [<key> ...] <path>` |
|Time complexity |O(N), where N is the number of keys. |
|Command description |Read values from multiple JSON keys at the same path and return a corresponding array of serialized results. For non\-existent keys, non\-existent or invalid paths, the corresponding position returns a null value, and the overall command will not be interrupted. |
|Option |* `<key>`: One or more JSON document key names, required.<br><br>* `<path>`: Target JSON path shared by all keys, required. |
|Response |* Returns an array with the same length as the number of input keys.<br><br>* Each element is either the serialized JSON at the corresponding path or a null value (`Nil` for RESP2, `Null` for RESP3).<br><br>* If a key exists but is not a JSON key, a `WRONGTYPE` error is returned. |
|Example |Example command.<br><br>`JSON.MGET k1 k2 k3 $.address.city`<br><br>&nbsp;<br><br>Response example.<br><br>`1) "[\"New York\"]"`<br><br>`2) "[\"Boston\"]"`<br><br>`3) "[\"Seattle\"]"` |


<span id="GrZnNhEU"></span>
### JSON.MSET


|Category |Description |
|---|---|
|Command syntax |`JSON.MSET <key> <path> <json> [<key> <path> <json> ...]` |
|Time complexity |O(N), where N is the number of keys. |
|Command description |Atomically set JSON values for multiple keys; either all succeed or all fail. Its path writing rules are consistent with JSON.SET, including adding object members, array index replacement, and related path error handling. |
|Option |* `<key>`: Key name for the target JSON document. Multiple occurrences are allowed, and it is required.<br><br>* `<path>`: The JSON path to write under this key, required.<br><br>* `<json>`: The JSON serialized value to write at the corresponding path, required. |
|Response |* Returns `OK` when all succeed<br><br>* Returns an error if any key's path parsing, type, or bounds check fails, and no partial write occurs |
|Example |Command example.<br><br>`JSON.MSET k1 . '[1,2,3,4,5]' k2 . '{"a":{"a":1,"b":2,"c":3}}' k3 . '{"a":[1,2,3,4,5]}'`<br><br>&nbsp;<br><br>Response example.<br><br>`OK` |


<span id="b52ZDU6e"></span>
### JSON.DEL


|Category |Description |
|---|---|
|Command syntax |`JSON.DEL <key> [path]` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Delete JSON values at the specified path in the document. Deleting the root path is equivalent to deleting the entire Redis key. |
|Option |* `<key>`: The target JSON document key name, required.<br><br>* `<path>`: The JSON path to delete, optional. When omitted, it indicates the root path. |
|Response |* Returns the number of deleted elements.<br><br>* Returns `0` if the key or path does not exist, or if the path is invalid. |
|Example |Command example.<br><br>`JSON.DEL k1 $.d.*`<br><br>&nbsp;<br><br>Response example.<br><br>`(integer) 3` |


<span id="BJWDzMIl"></span>
### JSON.FORGET


|Category |Description |
|---|---|
|Command syntax |`JSON.FORGET <key> [path]` |
|Time complexity |Same as JSON.DEL. |
|Command description |`JSON.FORGET` is an alias for `JSON.DEL`, with identical semantics.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In actual use, you can delete JSON values at the specified path using the JSON.DEL parameter method.</div><br> |
|Option |* `<key>`: The key name of the target JSON document, required.<br><br>* `<path>`: The JSON path to delete, optional. |
|Response |Consistent with `JSON.DEL`, returns the number of deleted elements; returns `0` if the key or path does not exist. |
|Example |Command example.<br><br>`JSON.FORGET k1 $.a`<br><br>&nbsp;<br><br>Response example.<br><br>`(integer) 1` |


<span id="r3wvWhpl"></span>
### JSON.CLEAR


|Category |Description |
|---|---|
|Command syntax |`JSON.CLEAR <key> [path]` |
|Time complexity |O(N), where N is the number of JSON arrays or objects matched by the path. |
|Command description |Clear the content of an array or object at the specified path, but retain the container itself. For empty containers, non\-container values, or unmatched paths, no error is reported; instead, `0` is returned. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Path of the array or object to clear, optional; applies to the root value if omitted. |
|Response |* Return the number of emptied containers.<br><br>* If the target is already an empty array/object, not a container, or the path does not match a container, return `0`. |
|Example |Command example.<br><br>`JSON.CLEAR k2 .children`<br><br>&nbsp;<br><br>Response example.<br><br>`(integer) 1` |


<span id="lB3kgspG"></span>
### JSON.TYPE


|Category |Description |
|---|---|
|Command syntax |`JSON.TYPE <key> [path]` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Return the JSON type of the value at the given path. Recognizable types include `boolean`, `string`, `number`, `integer`, `object`, `array`, and null types. |
|Option |* `<key>`: The target JSON document key name, required.<br><br>* `<path>`: The target JSON path, optional. |
|Response |* For an enhanced path, it returns a string array where each element is the type name of a matching value; if the path does not exist, it returns a null value; if the key does not exist, it can return an empty array.<br><br>* In RESP2, the null value type string is `nil`, and in RESP3, it is`null`。<br><br>* For a restricted path, it returns a single type string. |
|Example |Command example.<br><br>`JSON.TYPE k1 $[*]`<br><br>&nbsp;<br><br>Response example.<br><br>`1) integer`<br><br>`2) number`<br><br>`3) string`<br><br>`4) boolean`<br><br>`5) null`<br><br>`6) object`<br><br>`7) array` |


<span id="zpbgITEm"></span>
### JSON.RESP


|Category |Description |
|---|---|
|Command syntax |`JSON.RESP <key> [path]` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Return the JSON value at the specified path in RESP representation, rather than as a serialized JSON string. Container types are mapped to RESP arrays or nested arrays;`null`booleans, integers, floats, and strings are all mapped to their corresponding RESP representations. |
|Option |* `<key>`: Target JSON document key, required.<br><br>* `<path>`: JSON path to read, optional. |
|Response |* For an enhanced path, an array is returned, with each element being the RESP representation of a matched value.<br><br>* For a restricted path, it directly returns the RESP representation of the value.<br><br>* If the key does not exist, an enhanced path returns an empty array; for a restricted path, RESP2 is `Nil`, and RESP3 is `Null`. |
|Example |Command example.<br><br>`JSON.RESP k1 $.address`<br><br>&nbsp;<br><br>Response example.<br><br>`1) 1) "{"`<br><br>`2) 1) "street"`<br><br>`2) "21 2nd Street"` |


<span id="5MDrSCH8"></span>
### JSON.NUMINCRBY


|Category |Description |
|---|---|
|Command syntax |`JSON.NUMINCRBY <key> <path> <number>` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Increases the numeric value(s) matched by the path by a specified increment. This command only applies to numeric types; when non\-numeric values are encountered, it returns null at the corresponding position. |
|Option |* `<key>`: Target JSON document key, required.<br><br>* `<path>`: Target numeric path, required.<br><br>* `<number>`: The number to add, required. |
|Response |* For enhanced paths, returns an array where each element is an updated numeric string; non\-numeric values return null (RESP2 `Nil` / RESP3 `Null`).<br><br>* For restricted paths, returns a single updated numeric string.<br><br>* An invalid path or type error returns an error. |
|Example |Command example.<br><br>`JSON.NUMINCRBY k1 $.d[*] 10`<br><br>&nbsp;<br><br>Response example.<br><br>`"[11,12,13]"` |


<span id="76XGpZo6"></span>
### JSON.NUMMULTBY


|Category |Description |
|---|---|
|Command syntax |`JSON.NUMMULTBY <key> <path> <number>` |
|Time complexity |O(N), where N is the number of JSON values matched by the path. |
|Command description |Multiply the numeric value at the matched path by the given factor. This command only applies to numeric types; non\-numeric positions will not be updated and will be reflected as null values in the return. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target numeric path, required.<br><br>* `<number>`: Multiplier, required. |
|Response |* In enhanced path mode, return an array where each element is an updated numeric string; non\-numeric values return null (RESP2 `Nil` / RESP3 `Null`).<br><br>* In restricted path mode, return a single updated numeric string. |
|Example |Command example.<br><br>`JSON.NUMMULTBY k1 $.d[*] 2`<br><br>&nbsp;<br><br>Response example.<br><br>`"[2,4,6]"` |


<span id="7hWXQMOd"></span>
### JSON.STRAPPEND


|Category |Description |
|---|---|
|Command syntax |`JSON.STRAPPEND <key> [path] <json_string>` |
|Time complexity |O(N), where N is the number of string values matching the path. |
|Command description |Appends content to the end of the JSON string matching the path. This command only applies to string types and returns the new length after appending. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target string path, optional.<br><br>* `<json_string>`: JSON string value to append, required. |
|Response |* For augmented paths, return an integer array representing the new lengths after appending to each string; return null for non\-string values (RESP2 `Nil` / RESP3 `Null`).<br><br>* For restricted paths, return a single integer length. |
|Example |Example command.<br><br>`JSON.STRAPPEND k1 $.a.a '"a"'`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 2` |


<span id="uo0byugy"></span>
### JSON.STRLEN


|Category |Description |
|---|---|
|Command syntax |`JSON.STRLEN <key> [path]` |
|Time complexity |O(N), where N is the number of string values matching the path. |
|Command description |Returns the length of the JSON string value on the path. Does not report an error for non\-string values; instead, it returns null at the corresponding position. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target string path, optional. |
|Response |* For augmented paths, returns an integer array representing the length of each string value.<br><br>* For non\-string or non\-existent keys/paths, returns null (RESP2 `Nil` / RESP3 `Null`).<br><br>* For restricted paths, returns a single integer length. |
|Example |Example command.<br><br>`JSON.STRLEN k1 $.a.a`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 1` |


<span id="bS21LEXo"></span>
### JSON.TOGGLE


|Category |Description |
|---|---|
|Command syntax |`JSON.TOGGLE <key> [path]` |
|Time complexity |O(N), where N is the number of boolean values matched by the path. |
|Command description |Toggle the boolean value on the path between `true` and `false`. This command is only valid for boolean types; for non\-boolean values, it returns null or an error, depending on the path syntax. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target boolean path, optional. |
|Response |* For enhanced paths, an integer array is returned, where `0` represents `false` and `1` represents `true`. Non\-boolean values return an empty value (RESP2 `Nil` / RESP3 `Null`).<br><br>* For restricted paths, the string `true` or `false` is returned. |
|Example |Example command.<br><br>`JSON.TOGGLE k1 $.*`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 0`<br><br>`2) (integer) 1`<br><br>`3) (nil)`<br><br>`4) (nil)` |


<span id="cbPICMqq"></span>
### JSON.ARRAPPEND


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRAPPEND <key> <path> <json> [<json> ...]` |
|Time complexity |O(N), where N is the number of values to append. |
|Command description |Append one or more JSON values to the end of the array matching the path. This command only works for arrays. Null is returned in the result when non\-array values are encountered. |
|Option |* `<key>`: The target JSON document key name, required.<br><br>* `<path>`: The target array path, required.<br><br>* `<json>`: One or more JSON serialized values to append, required. |
|Response |* In enhanced path mode, an array is returned where each element represents the new length of the corresponding array after appending; for non\-array types, a null value is returned (RESP2 `Nil` / RESP3 `Null`).<br><br>* In restricted path mode, a single integer is returned, representing the new array length.<br><br>* A path error returns an error. |
|Example |Command example.<br><br>`JSON.ARRAPPEND k1 $[*] '"c"'`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 1`<br><br>`2) (integer) 2`<br><br>`3) (integer) 3` |


<span id="iu94GhZx"></span>
### JSON.ARRINDEX


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRINDEX <key> <path> <json-scalar> [start [end]]` |
|Time complexity |O(N), where N is the array length |
|Command description |Find the position of the first occurrence of a scalar JSON value in the array matched by the path. Out\-of\-bounds `start`/`end` will be clipped to array boundaries; if `start > end`, return `-1`. |
|Option |* `<key>`: Target JSON document key, required.<br><br>* `<path>`: Target array path, required.<br><br>* `<json-scalar>`: Scalar JSON value to look up, required.<br><br>* `<start>`: Optional starting index.<br><br>* `<end>`: Optional ending index. |
|Response |* In enhanced path mode, return an integer array; each element is the index of the matching value in the corresponding array, or `-1` if not found; for non\-array values, return null (RESP2 `Nil` / RESP3 `Null`).<br><br>* In restricted path mode, return a single integer index; illegal key types will cause an error. |
|Example |Command example.<br><br>`JSON.ARRINDEX k1 $[*] '"b"'`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) -1`<br><br>`2) (integer) -1`<br><br>`3) (integer) 1`<br><br>`4) (integer) 1` |


<span id="yzEzXFRF"></span>
### JSON.ARRINSERT


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRINSERT <key> <path> <index> <json> [<json> ...]` |
|Time complexity |O(N), where N is the array length. |
|Command description |Insert one or more values before the specified index in the array matched by the path. `index=0` means insertion at the beginning; negative indices count backward from the end of the array; indices must be within array bounds. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target array path, required.<br><br>* `<index>`: Insertion position, required.<br><br>* `<json>`: One or more JSON serialized values to insert, required. |
|Response |* In the enhanced path, returns an integer array indicating the new length after each array insertion; for empty or non\-array inputs, returns null (RESP2 `Nil` / RESP3 `Null`).<br><br>* In the restricted path, returns a single integer indicating the new length.<br><br>* Out of bounds or type mismatch returns an error. |
|Example |Command example.<br><br>`JSON.ARRINSERT k1 $[*] 0 '"c"'`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 1`<br><br>`2) (integer) 2`<br><br>`3) (integer) 3` |


<span id="O8RWnmHY"></span>
### JSON.ARRLEN


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRLEN <key> [path]` |
|Time complexity |O(N), where N is the number of arrays matched by the path. |
|Command description |Returns the length of the array at the path. This command only counts array values; if the path matches a non\-array, the result will be an empty value. |
|Option |* `<key>`: The target JSON document key name, required.<br><br>* `<path>`: The target array path, optional. |
|Response |* For enhanced paths, returns an integer array representing the length of each matching array.<br><br>* For non\-array or non\-existent keys/paths, return null values (RESP2 `Nil` / RESP3 `Null`).<br><br>* Under a restricted path, return a single integer length. |
|Example |Command example.<br><br>`JSON.ARRLEN k1 $[*]`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 0`<br><br>`2) (integer) 1`<br><br>`3) (integer) 2`<br><br>`4) (integer) 3` |


<span id="vCZose00"></span>
### JSON.ARRPOP


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRPOP <key> [path [index]]` |
|Time complexity |O(N), where N is the number of arrays matched by the path. |
|Command description |Pop the element at the specified index from the array and return it. If `index` is not provided, pop the last element; popping from an empty array returns null. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target array path, optional.<br><br>* `<index>`: Array index to pop, optional. |
|Response |* For enhanced paths, returns an array where each element is a popped JSON serialized value; returns null for empty arrays or non\-arrays (RESP2 `Nil` / RESP3 `Null`).<br><br>* For restricted paths, returns a single popped value; returns null if the array is empty. |
|Example |Command example.<br><br>`JSON.ARRPOP k1 $[*]`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (nil)`<br><br>`2) "\"a\""`<br><br>`3) "\"b\""` |


<span id="O4nQ4AqG"></span>
### JSON.ARRTRIM


|Category |Description |
|---|---|
|Command syntax |`JSON.ARRTRIM <key> <path> <start> <end>` |
|Time complexity |O(N), where N is the number of arrays matched by the path. |
|Command description |Crop the array at the path to a sub\-array corresponding to the closed interval `[start, end]`. If `start` is less than `0`, it will be treated as `0`. If `end` exceeds the array length, it will be truncated. If `start >= size` or `start > end`, the result is an empty array. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target array path, required.<br><br>* `<start>`: Starting index for slicing, required.<br><br>* `<end>`: End index for slicing (inclusive), required. |
|Response |* Under enhanced paths, returns an integer array indicating the new lengths of the trimmed arrays; returns null for empty or non\-array values (RESP2 `Nil` / RESP3 `Null`).<br><br>* Under restricted paths, returns a single integer length; returns null if the array does not exist or is not an array. |
|Example |Command example.<br><br>`JSON.ARRTRIM k1 $[*] 0 1`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 0`<br><br>`2) (integer) 1`<br><br>`3) (integer) 2`<br><br>`4) (integer) 2` |


<span id="EJLXEDuX"></span>
### JSON.OBJKEYS


|Category |Description |
|---|---|
|Command syntax |`JSON.OBJKEYS <key> [path]` |
|Time complexity |O(N), where N is the number of objects matched by the path. |
|Command description |Returns a list of key names of the object values at the path. For enhanced paths, multiple objects return their respective key name arrays; for non\-object values, an empty array or null is returned. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target object path, optional. |
|Response |* For enhanced paths, an array of arrays is returned, with each inner array containing all key names of a matching object.<br><br>* For non\-object matches, an empty array is returned; if the key does not exist, RESP2 is `Nil`, and RESP3 is `Null`.<br><br>* For restricted paths, an array of key names for the object is returned directly. |
|Example |Command example.<br><br>`JSON.OBJKEYS k1 $.d`<br><br>&nbsp;<br><br>Response example.<br><br>`1) "a"`<br><br>`2) "b"`<br><br>`3) "c"` |


<span id="NTYLSzyX"></span>
### JSON.OBJLEN


|Category |Description |
|---|---|
|Command syntax |`JSON.OBJLEN <key> [path]` |
|Time complexity |O(N), where N is the number of objects matched by the path. |
|Command description |Returns the number of keys contained by the object at the path. This command is only meaningful for object types; it returns null for non\-object locations. |
|Option |* `<key>`: Target JSON document key name, required.<br><br>* `<path>`: Target object path, optional. |
|Response |* In enhanced paths, returns an integer array indicating the number of keys for each matching object.<br><br>* For non\-objects or non\-existent keys/paths, returns null (RESP2 `Nil` / RESP3 `Null`).<br><br>* In restricted paths, returns a single integer. |
|Example |Command example.<br><br>`JSON.OBJLEN k1 $.a`<br><br>&nbsp;<br><br>Response example.<br><br>`1) (integer) 0` |


&nbsp;
