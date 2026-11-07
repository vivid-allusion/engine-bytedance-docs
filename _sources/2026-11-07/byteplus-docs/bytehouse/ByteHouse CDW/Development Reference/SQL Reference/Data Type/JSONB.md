---
title: "JSONB"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/jsonb"
---

This tutorial introduces the syntax and usage of the JSONB data type in ByteHouse.

<span id="bd410587"></span>
# Background

JSONB data type stores data in binary format, supports efficient search and indexing, and offers better processing performance compared to text format JSON. It is suitable for storing semi\-structured data such as user behavior logs and configuration information.

<span id="c8423b6f"></span>
# Syntax

<span id="2ec3f1df"></span>
## Create table

```SQL
CREATE TABLE t_jsonb
(
    id INT,
    data JSONB
)
ENGINE = CnchMergeTree
ORDER BY tuple(); 
```


<span id="c8e562f8"></span>
## Query

<span id="b46c6261"></span>
### Use functions to extract specific type values

ByteHouse supports extracting values of JSONB, String, Int64, Float64, Bool, and other types. If the type matches, the corresponding type value is returned; otherwise returns the default value of that type.


* Extract JSONB type

   When the type matches, return the value of the corresponding type, otherwise return the default value for that type.

   ```SQL
   SELECT 
       jsonb_extract('{"a":1, "b":2}'::JSONB, '$.a') AS a,
   FROM t_jsonb;  
   ```
   

* Extract String type

   When the type matches, return the value of the corresponding type, otherwise return the default empty string for that type.

   ```SQL
   SELECT 
       jsonb_extract_string('{"a":"test", "b":2}'::JSONB, '$.a') AS a,b
   FROM t_jsonb;  
   ```
   

* Extract Int64 type

   When the type matches, return the value of the corresponding type, otherwise return the default value 0 for that type.

   ```SQL
   SELECT 
       jsonb_extract_int64('{"a":1, "b":2}'::JSONB, '$.a')
   FROM t_jsonb;  
   ```
   

* Extract Float64 type

   When the type matches, return the value of the corresponding type, otherwise return the default value 0.0 for that type.

   ```SQL
   SELECT 
       jsonb_extract_float64('{"a":1.0, "b":2}'::JSONB, '$.a')
   FROM t_jsonb; 
   ```
   

* Extract Bool type

   When the type matches, return the value of the corresponding type, otherwise return the default value false for that type.

   ```SQL
   SELECT 
       jsonb_extract_bool('{"a":true, "b":2}'::JSONB, '$.a')
   FROM t_jsonb;  
   ```
   


<span id="e5e8c3eb"></span>
### Merge JSONB objects

ByteHouse supports merging two JSONB objects and returns the merged JSONB, where keys duplicated in both objects are overwritten by the right object.

```SQL
SELECT 
    jsonb_merge_patch('{"a":true, "b":2}'::JSONB, '{"c":3}'::JSONB)
FROM t_jsonb;  
```
