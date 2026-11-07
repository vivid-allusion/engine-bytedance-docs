---
title: "MAP type"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/map-type"
---

<span id="子类型简介"></span>
# Type introduction
ByteHouse Supports Three Types of Map:

* Self-developed Map Type: ByteMap, contains two sub types of Map:
   * Multiple Implicit Column Map (Implicit Byte Map)
   * Single Implicit Column Map (Implicit Compact Byte Map)
* Community Map Type: KV Map;

<span id="76882292"></span>
# Storage form
ByteHouse Supports Three Types of Map, the differences are as follows:

* Multiple Implicit Columns: Search Efficient. Creating multiple files occupies a large number of inodes and has low storage efficiency.
* Single implicit column: Offers efficient querying and helps alleviate the problem of occupying a large number of inodes on the disk. However, the storage efficiency is low, and some operations are not supported (mainly `ALTER TABLE`***`database`***`.`***`table`***`{(UPDATE) | (DELETE)`).
* KV Map: Provides high storage efficiency and helps alleviate the problem of occupying a large number of inodes on the disk. However, the querying efficiency is low.

Typically, the total number of all map keys is not large (<3000), and using multiple implicit column Maps is recommended.
When there are many keys, depending on the trade-off between functionality and efficiency, either KV Map or a single implicit column Map can be used.
The following example introduces three types of storage forms:
There is a map column named 'm', both key and value types are String, and the following three rows of data are written:
`{'k1': 'v1', 'k2': 'v2', 'k3': 'v3'}`
`{'k1': 'v4', 'k3': 'v5'}`
`{'k2': 'v6'}`
<span id="自研-map：多隐式列-map"></span>
## Multi implicit columns map
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2eb5aca91c104a23670d10c0aa8d5cff.png =602x)
Implicit Map writes every key into a data file in the form **Nullable(ValueType)**, treating it like a normal column. Because it is opaque to the user, it is called Multi Implicit Columns Map.
In this case, as each key occupies a column, the efficiency of searching values according to the key is extremely high.
<span id="自研-map：单隐式列-map"></span>
## Single implicit column map
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb1f764e01fa90ce48e604794a178a21.png =331x)
As every key in an Implicit Map forms an independent file in the form of an implicit column, excessive keys may lead to a problem of **small files wasting disk space** and **high inode consumption**. To address this issue, the Single Implicit Column (Implicit Compact Map) was developed. The basic idea is to write all implicit columns of the same map into a single file, with checksum recording the information of each implicit column, just additionally recording offset information of each file.
However, after using the Implicit Compact Map type, the following functions cannot be used:

1. The Map Value type used is LowCardinality.
2. Use ALTER TABLE database.table {(UPDATE) | (DELETE)} ... These will rewrite all part of the mutations actions.

<span id="社区-map：kv-map"></span>
## KV map
![Image](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_957a76eb7e185430a0a1b9caf71346f8.png =537x)
The advantage of using hidden columns is the improved efficiency in searching a specific key by querying the corresponding hidden column data directly. However, when writing data for each hidden column, it is required to fill rows that do not contain these keys with null. Hence, when the total number of keys is much higher than the average number of keys per row, **data swelling** issues occur, filling up hidden columns with a significant amount of null values, leading to inefficient storage problems.
To solve this problem, a KV map is introduced, with the idea of writing all keys and all values into a separate file, and recording the size information in another separate file to represent the size of each row of data.
When searching for a specific key, KV map requires reading all map data and then filtering it row by row, thus the efficiency of searching specific keys is less than optimal.
<span id="子类型支持"></span>
# Support for child types
<span id="key-类型"></span>
### Key type
Integers, Floats, Date, DateTime, String, FixedString, LowCardinality, UUID, Enums, Not supported **Nullable.**
<span id="value-类型"></span>
### Type: value
The Type of Values in KV Map is Unlimited;
The value type restrictions for Single Implicit Map and Multiple Implicit Map are as follows: Integers, Floats, Date, DateTime, String, FixedString, LowCardinality(Nullable()), Array, Not supported Type: **Nullable.**
<span id="使用方法"></span>
# Usage example
```sql
-- Create Byte Map, the default value of enable_compact_map_data is 0
CREATE TABLE map_table (id UInt32, m Map(String, String)) ENGINE MergeTree() order by id [settings enable_compact_map_data = 0];
CREATE TABLE map_table (id UInt32, m Map(String, String) BYTE) ENGINE MergeTree() order by id [settings enable_compact_map_data = 0];

-- Create Byte Compact Map
CREATE TABLE map_table (id UInt32, m Map(String, String)) ENGINE MergeTree() order by id settings enable_compact_map_data = 1;
CREATE TABLE map_table (id UInt32, m Map(String, String) BYTE) ENGINE MergeTree() order by id settings enable_compact_map_data = 1;

-- Create KV Map
CREATE TABLE map_table (id UInt32, m Map(String, String) KV) ENGINE MergeTree() order by id;

-- Insert data
INSERT INTO map_table VALUES (1, {'k1': 'v1', 'k2': 'v2'[, ...]});
INSERT INTO map_table VALUES (1, map('k1', 'v1', 'k2', 'v2'[, ...]));
INSERT INTO map_table FORMAT JSONEachRow {"id": "2", "m": {"k2": "v20", "k3": "v3"}};

-- Query Map
select m from map_table;

┌─m──────────────────────┐
│ {'k1':'v1','k2':'v2'}  │
│ {'k2':'v20','k3':'v3'} │
└────────────────────────┘

-- Query the Key of Implicit Map and Implicit Compact Map
---- Option 1: {} query
---- As can be seen from the result header, the query is for an implicit column, and null values are filled as the default values.
select m{'k1'} from map_table;
select mapElement(m, 'k1') from map_table;

┌─__m__'k1'─┐
│ v1        │
│ ᴺᵁᴸᴸ      │
└───────────┘
---- Option 2: [] query
---- As can be seen from the result header, the query is for the entire Map column m, and then a specific key k1 is filtered out. The default values are filled (for the String type, an empty string is used as the default value)
select m['k1'] from map_table;
select arrayElement(m, 'k1') from map_table;

┌─arrayElement(m, 'k1')─┐
│ v1                    │
│                       │
└───────────────────────┘

-- Query the Key of KV Map
---- Option 1: {} query
---- As can be seen from the result header, the query is for the entire Map column m, and then the specific key 'k1' is filtered out. The default value filled in for the missing value is null.
select m{'k1'} from map_table;
select mapElement(m, 'k1') from map_table;

┌─mapElement(m, 'k1')─┐
│ v1                  │
│ ᴺᵁᴸᴸ                │
└─────────────────────┘
---- Option 2: [] query
---- As can be seen from the result header, the query is for the entire Map column m, and then the specific key 'k1' is filtered out. The default value filled in for the missing value is the default value (for the String type, it is an empty string)
select m['k1'] from map_table;
select arrayElement(m, 'k1') from map_table;

┌─arrayElement(m, 'k1')─┐
│ v1                    │
│                       │
└───────────────────────┘

--  Query Map keys
select mapKeys(m) from map_table;

┌─mapKeys(m)──┐
│ ['k1','k2'] │
│ ['k2','k3'] │
└─────────────┘

-- Query the Key set of Implicit Map and Implicit Compact Map type
select getMapKeys('default', 'map_table', 'm');

┌─getMapKeys('default', 'map_table', 'm')─┐
│ ['k1','k2','k3']                        │
└─────────────────────────────────────────┘
```

<span id="相关参数"></span>
# Related parameters
<span id="profile-配置"></span>
### Profile configuration

| | | | | \
|Parameter Name |Type |No Configuration Default |Parameter Description |
|---|---|---|---|
| | | | | \
|max_map_key_num |UInt64 |0 |The limit on the number of different map keys allowed per table, where 0 indicates unlimited. This parameter limits the total number of different keys in all map columns of the table |
| | | | | \
|allow_discard_map_key |Bool |false |When exceeding the map key quantity limit, whether to allow discarding map keys; setting this parameter to false will throw an exception |

<span id="merge-tree-中配置"></span>
### Configuration in merge_tree

| | | | | \
|Parameter Name |Type |No Default Configuration |Parameter Description |
|---|---|---|---|
| | | | | \
|enable_compact_map_data |Bool |false |Activate compact map? |

<span id="faq"></span>
# FAQ
Q: What is the recommended cap for a map's key?
Suggestion: For multiple implicit column MAPs, it is recommended to set the max_map_key_num parameter to 3000. For a single implicit column MAP and KV map, it is considered unnecessary to deliberately restrict the key cap.
