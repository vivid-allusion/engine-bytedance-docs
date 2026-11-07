---
title: "Map Function (Self-developed)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/map-function-self-developed"
---

<span id="arrayelement-查询key"></span>
## arrayElement (search key)
**Syntax:** `arrayElement(map, key)`
**Parameters:** ***map*** is the column name of map, ***key*** is the key name to be searched
**Description:** Searches for a key in a map, **rows not containing this key will be filled with default values**, equivalent to ***map[key]***
**Example:**
```sql
select arrayElement(m, 'k1') from map_table;

┌─arrayElement(m, 'k1')─┐
│ v1                    │
│                       │
└───────────────────────┘
```

**Note:** Column names do not need to be quoted, key names need to be quoted when the key type is String
When using arrayElement with three types of Maps, it will first **search the entire map column data**, then filter out the desired key data and fill the rows where the key does not exist with **default values**, therefore, the search performance is lower. Byte Map and Byte Compact Map types ***are recommended*** to use mapElement (or {}) method to search for keys.
<span id="mapelement-查询key"></span>
## mapElement (search key)
**Syntax:** `mapElement(map,key)`
**Parameter:** ***map*** is the map column name, ***key*** is the key name to be searched
Description: Searches a specific key in a map; rows not containing this key will be filled with null, equivalent to map{key}
**Example:**
```sql
select mapElement(m, 'k1') from map_table;

-- For KV Map
┌─mapElement(m, 'k1')─┐
│ v1                  │
│ ᴺᵁᴸᴸ                │
└─────────────────────┘

-- For Byte Map and Byte Compact Map
┌─__m__'k1'─┐
│ v1        │
│ ᴺᵁᴸᴸ      │
└───────────┘
```

**Advisory:** Column names do not need quotation marks; key names need quotation marks when the key type is a String
Byte Map and Byte Compact Map types search directly in implicit columns, offering higher efficiency; KV Map first searches the entire map column, then filters the key data.
<span id="map"></span>
## map
**Syntax:** `map(key1, value1[, key2, value2, ...])`
**Parameter:** ***key1, key2*** are keys, ***value1, value2*** are values
**Description:** Constructs a map column
**Example:**
```sql
select map(1, 2, 3, 4)
insert into map_table values (1, map('k1', 'v1', 'k2', 'v2'))
```

<span id="mapkeys"></span>
## mapKeys
**Syntax:** `mapKeys(map)`
**Param:** ***map*** is a column name
**Description:** Retrieves the Key of each row from map data
**Example:**
```sql
select mapKeys(m) from map_table;

┌─mapKeys(m)──┐
│ ['k1','k2'] │
│ ['k2','k3'] │
└─────────────┘
```

**Advisory:**
For Implicit Map and Implicit Compact Map types, this method first searches the map column and then filters out the keys to return, therefore it needs to be used when the parameter **allow_map_access_without_key** is true. It is inefficient and not recommended to use this method, it's better to use the following **getMapKeys** method.
For KV Map type, this method directly searches the `.key` file.
<span id="mapvalues"></span>
## mapValues
**Syntax:** `mapValues(map)`
**Parameter:** ***map*** is the map column name
**Description:** Retrieves the Value of each row in the map data
**Example:**
```sql
select mapValues(m) from map_table;

┌─mapValues(m)─┐
│ ['v1','v2']  │
│ ['v20','v3'] │
└──────────────┘
```

**Advisory:**
For Byte Map and Byte Compact Map types, this method first searches the map column, then filters out the keys, and thus should be used when the parameter **allow_map_access_without_key** is true, which is less efficient.
For KV Map types, this method directly queries the **.value** file.
<span id="mapcontains"></span>
## mapContains
**Syntax:** `mapContains(map, key)`
**Param:** ***map*** is the column name, ***key*** is the name of the key to be searched
**Description: Returns whether each row in the map column contains the target key**
**Example:**
```sql
select mapContains(m, 'k1') from map_table;

┌─mapContains(m, 'k1')─┐
│                    1 │
│                    0 │
└──────────────────────┘
```

**Advisory:**
This method first searches the map column, so it must be used when the parameter **allow_map_access_without_key** is true.
<span id="getmapkeys"></span>
## getMapKeys
**Syntax:** `getMapKeys('database', 'table', 'map'[, 'partition_regex'])`
**Param:** ***database*** is the database name, ***table*** is the table name (can be a distributed table name), ***map*** is the column name, ***partition_regex*** is the partition regular expression
**Description:** Retrieves the key set of the map column
**Example:**
```sql
select getMapKeys('default', 'map_table', 'm')

┌─getMapKeys('default', 'map_table', 'm')─┐
│ ['k1','k2','k3']                        │
└─────────────────────────────────────────┘
```

**Advisory:** This method retrieves key information directly from the checksum, therefore it's **only applicable to** Implicit Map and Implicit Compact Map types
<span id="str-to-map"></span>
## str_to_map
**Syntax:** `str_to_map(string, item_delimiter, kv_delimiter)`
**Param:** ***String*** is the string to be parsed, ***item_delimiter*** is the delimiter between data, ***kv_delimiter*** is the delimiter between key and value in each data item
**Description:** Parses strings to construct a map
**Example:**
```sql
SELECT str_to_map('a=b&c=d', '&', '=');

┌─str_to_map('a=b&c=d', '&', '=')─┐
│ {'a':'b','c':'d'}               │
└─────────────────────────────────┘
```

<span id="删除map-key"></span>
## Delete Map Key
**Syntax:**`ALTER TABLE database.table CLEAR MAP KEY map(key1,[, key2, ... ])`
**Param:** ***Database name*** is the name of the database, ***table*** is the table name, ***map*** is the name of the map, ***key1,key2*** are the names of keys
**Restriction:** KV Map does not support this function
**Example:**
```sql
ALTER TABLE map_table CLEAR MAP KEY m('k1');
select * from map_table;

┌─id─┬─m──────────────────────┐
│  1 │ {'k2':'v2'}            │
│  2 │ {'k2':'v20','k3':'v3'} │
└────┴────────────────────────┘
```
