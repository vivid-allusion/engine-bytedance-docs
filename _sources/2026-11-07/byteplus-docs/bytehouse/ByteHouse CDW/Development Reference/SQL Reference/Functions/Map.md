---
title: "Map"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-map"
---

<span id="906f5a05"></span>
### map

Construct a Map column using any number of key/value pairs

**Syntax**

```SQL
map(key1, value1 [, key2, value2, ...])
```


**Parameters**


* key1, key2: Keys in the Map column

* value1, value2: Values in the Map column


**Return Value**


* Constructed Map column


**Example**

```SQL
SELECT map(1, 2, 3, 4), map('k1', 'v1', 'k2', 'v2');
```


Query results

```SQL
{1:2,3:4}    {'k1':'v1','k2':'v2'}
```


<span id="db5bc046"></span>
### arrayElement

Search a specific key in a Map. Rows not containing this key will be filled with a default value, equivalent to `map[Key]`

**Syntax**

```SQL
arrayElement(map, key)
```


**Param**


* Map: the Map column to search

* Key: the Key name to be searched


**Return value**


* Value corresponding to the key name


**Example**

```SQL
WITH map('k1', 1) AS m 
SELECT arrayElement(m, 'k1'), m['k1'], m['k2'];
```


Query results

```SQL
1    1    0
```


**Advisory**

When using arrayElement, the entire map column is read first before filtering, which results in lower query performance for implicit column Map. For implicit column Map, it is recommended to use \*\* `mapElement` (or `{}`) method to query keys.

<span id="5827be5b"></span>
### mapElement

Searching for a specific key in a Map, rows not containing this key will be filled with NULL, which is equivalent to `map{key}`

**Syntax**

```SQL
mapElement(map, key)
```


**Parameter**


* Map: the Map column to be searched

* Key: the key name to be searched


**Return value**


* Key corresponds to Value


**Example**

```SQL
WITH map('k1', 1) AS m 
SELECT mapElement(m, 'k1'), m{'k1'}, m{'k2'};
```


Query results

```SQL
1    1    NULL
```


**Advisory**

Using an implicit column Map this way requires reading only the corresponding implicit columns, which is more efficient than using arrayElement;

<span id="66c37a24"></span>
### mapKeys

Retrieves the key for each row of Map data and returns it as an Array

**Syntax**

```SQL
mapKeys(map)
```


**Param**


* Map to be queried


**Return value**


* Array of keys contained in each row


**Example**

```SQL
WITH map('k1', 'v1', 'k2', 'v2') AS m
SELECT mapKeys(m);
```


Query results

```SQL
['k1','k2']
```


**Advisory**

For implicit Map columns, this method will first read the entire Map column, then extract and return the keys. The efficiency is low, it is `recommended` to use the getMapKeys method below.

<span id="ee66785d"></span>
### mapValues

Retrieve and return the values of the Map data for each row as an Array

**Grammar**

```SQL
mapValues(map)
```


**Parameter**


* Map: The Map Column to be queried


**Return value**


* Array of values contained in each row


**Example**

```SQL
WITH map('k1', 'v1', 'k2', 'v2') AS m
SELECT mapValues(m);
```


Query results

```SQL
['v1','v2']
```


<span id="ac109d09"></span>
### getMapKeys

Retrieve the list of keys contained in the Map column (in the specified partition), where each key appears only once

**Grammar**

```SQL
getMapKeys('database', 'table', 'map' [, 'partition_regex'])
```


**Param**


* Database: "Database name", needs to be written as a string constant enclosed in quotes

* Table: "Table name", needs to be written as a string constant enclosed in quotes

* Map: "Column name", needs to be written as a string constant enclosed in quotes

* Partition_regex: Regular expression for the partition


**Return value**


* The array of keys contained in the map column (in the specified partition)


**Example**

```SQL
INSERT INTO some_db.map_table (m) VALUES {'k1': 'v1', 'k2': 'v2'};
SELECT getMapKeys('some_db', 'map_table', 'm');
```


Query results

```SQL
['k1','k2']  
```


**Advisory**

This function searches for keys by reading the metadata of each part, and thus is only applicable to the implicit column Map.

<span id="164450c9"></span>
### mapContains

Returns whether each row in the Map column contains the target Key

**Syntax**

```SQL
mapContains(map, key)
```


**Param**


* map: Map Column

* Key: the Name of the Key to be queried


**Return value**


* Whether each row contains the specified Key, 1 means contains, 0 means does not contain, Type: UInt8


**Example**

```SQL
WITH map('k1', 'v1', 'k2', 'v2') AS m
SELECT mapContains(m, 'k1'), mapContains(m, 'k3');
```


Query results

```SQL
1    0
```


<span id="6ccd469c"></span>
### str_to_map

Use the specified delimiter to parse a String into a Map(String, String) type.

**Syntax**

```SQL
str_to_map(pattern, pair_delimiter, key_value_delimiter)
```


**Parameters**


* pattern: The String to be parsed

* key_value_delimiter: The delimiter between key and value

* pair_delimiter: The delimiter between key\-value pairs


**Return value**


* List of constructed Maps


**Example**

```SQL
SELECT str_to_map('k1=v1, k2=v2', ',', '=');
```


Query results

```SQL
{'k1':'v1','k2':'v2'}
```


<span id="d76fdced"></span>
### mapFromArrays

Use two arrays to construct a Map column, the first array as keys, and the second array as values.

**Syntax**

```SQL
mapFromArrays(keys, values)
```


**Parameter**


* keys: List used as keys

* values: List used as values, must be of the same length as keys per row


**Return value**


* Constructed Map column


**Example**

```SQL
SELECT mapFromArrays(['a', 'b', 'c'], [1, 2, 3]);
```


Query results

```SQL
{'a':1,'b':2,'c':3}
```


<span id="b1b3c9e2"></span>
### mapAdd

Adds the values of corresponding keys across multiple Map Columns

**Syntax**

```SQL
mapAdd(map1, map2 [, ...])
```


**Param**


* map1, map2: Map Columns to be added


**Return value**


* Map Column after summation


**Example**

```SQL
SELECT mapAdd(map(1,1), map(1,2), map(2,2));
```


Query results

```SQL
{1:3,2:2}
```


<span id="dd856fad"></span>
### mapSubtract

Subtract the values of corresponding keys from multiple Map columns (subtract all the subsequent values from the first value)

**Syntax**

```SQL
mapAdd(map1, map2 [, ...])
```


**Param**


* map1: The Map column to be subtracted from

* map2: The Map column that serves as the subtractor


**Return value**


* The Map column after subtraction


**Example**

```SQL
SELECT mapSubtract(map(1, 2)::Map(Int16,Int16), map(1, 1)::Map(Int16,Int16), map(2, -2)::Map(Int16,Int16));
```


Query results

```SQL
{1:1,2:2}
```


<span id="11ee2ef4"></span>
### mapPopulateSeries

Requires the Map key type to be Integer, and populates the Map with all key values between the smallest key and the largest key, filling the value with the default value of the corresponding type. The largest key can also be specified by the second parameter.

This function can also accept two Arrays, the first as keys and the second as values.

**Syntax**

```SQL
mapPopulateSeries(map[, max])
mapPopulateSeries(keys, values[, max])
```


**Parameter**


* map: The Map column to be populated, key type needs to be Integer

* keys: List of keys to be populated, Type: Array(Integer)

* values: List of values to be populated, Type: Array

* Max: Specifies the maximum key value to be padded


**Return value**


* If the first parameter is a Map, returns the filled Map column

* If the first two parameters are keys and values, returns the filled Array placed in a Tuple Type is Tuple(Array, Array)


**Example**

```SQL
SELECT mapPopulateSeries(map(2, 10, 5, 20)), mapPopulateSeries(map(2, 10, 5, 20), 3);
SELECT mapPopulateSeries([1, 5], [5, 20], 6);
```


Query results

```SQL
{2:10,3:0,4:0,5:20}    {2:10,3:0}
([1,2,3,4,5,6],[5,0,0,0,20,0])
```


<span id="6d1f6345"></span>
### mapContainsKeyLike

Returns whether each row in the Map column contains a key that meets the specified pattern

**Syntax**

```SQL
mapContainsKeyLike(map, pattern)
```


**Param**


* Map: The map column to be queried, key must be of String or FixedString type

* Pattern: The pattern of the specified key, syntax similar to like clause


**Return value**


* Whether each row contains a key that meets the specified pattern, 1 means it contains, 0 means it does not contain, type is UInt8


**Example**

```SQL
WITH map('k1', 'v1', 'k2', 'v2') AS m
SELECT mapContainsKeyLike(m, 'k%'), mapContainsKeyLike(m, 'm%');
```


Query results

```SQL
1    0
```


<span id="e6067063"></span>
### mapExtractKeyLike

Filter the keys in the Map column that meet the specified pattern and their corresponding values

**Syntax**

```SQL
mapExtractKeyLike(map, pattern)
```


**Param**


* map: Column to query, key must be String or FixedString Type

* pattern: The pattern for specified key, syntax follows like Expression


**Return Value**


* Filtered Map Column


**Example**

```SQL
WITH map('k1', 'v1', 'k2', 'v2') AS m
SELECT mapExtractKeyLike(m, 'k%'), mapExtractKeyLike(m, 'm%');
```


Query Results

```SQL
{'k1':'v1','k2':'v2'}    {}
```


<span id="070f14b2"></span>
### mapApply

Run the specified lambda expression on each key\-value pair in the Map.

**Syntax**

```SQL
mapApply(lambda, map)
```


**Parameter**


* Lambda: A lambda expression with key\-value pairs

* Map: Map Column


**Return value**


* A new Map Column composed of key\-value pairs returned by lambda


**Example**

```SQL
WITH map(1, 1, 2, 2) AS m
SELECT mapApply((k, v) -> (toString(k), v * 2), m);
```


Query results

```SQL
{'1':2,'2':4}
```


<span id="1b895e37"></span>
### mapFilter

Use the given condition to filter the key\-value pairs in the Map.

**Syntax**

```SQL
mapFilter(lambda, map)
```


**Parameter**


* lambda: A lambda expression that accepts key\-value pairs as parameters, returning UInt8 or Nullable(UInt8) types, where 0 and NULL will be filtered out, and values \> 0 indicate retention.

* map: The Map Column that needs to be filtered


**Return value**


* Filtered Map Column


**Example**

```SQL
SELECT _map, mapFilter((k, v) -> ((v % 2) = 0), _map)
FROM
(
    SELECT map('key1', number, 'key2', number * 2) AS _map
    FROM numbers(3)
)
```


Query results

```SQL
{'key1':0,'key2':0}    {'key1':0,'key2':0}
{'key1':1,'key2':2}    {'key2':2}
{'key1':2,'key2':4}    {'key1':2,'key2':4}
```


<span id="dc8b9de8"></span>
### mapUpdate

Copy map1 and use the values in map2 to update the copied Map Column, then return it. For keys that exist in both map1 and map2, the corresponding values from map2 will be retained.

**Grammar**

```SQL
mapUpdate(map1, map2)
```


**Param**


* Map Column that is being updated (copied)

* Map Column used to update map1


**Return value**


* Updated Map Column


**Example**

```SQL
WITH map('k1', 1, 'k2', 1) AS m1, map('k1', 2, 'k3', 2) AS m2
SELECT mapUpdate(m1, m2), mapUpdate(m2, m1);
```


Query results

```SQL
{'k1':2,'k2':1,'k3':2}    {'k1':1,'k2':1,'k3':2}
```
