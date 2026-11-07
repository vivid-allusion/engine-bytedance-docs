---
title: "bool"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/bool"
---

When creating a table in ByteHouse Enterprise Edition, it supports setting the column type to Bool or Boolean, which is internally stored as UInt8 with the value `true` (1), `false` (0). After creating the table, the Boolean type will display as the Bool type.

```SQL
select true as col, toTypeName(col);
┌─col──┬─toTypeName(true)─┐
│ 1     │ UInt8             │
└──────┴──────────────────┘

select true == 1 as col, toTypeName(col);
┌─col─┬─toTypeName(equals(true, 1))─┐
│   1 │ UInt8                       │
└─────┴─────────────────────────────┘
```


Examples are as follows:


1. Create a table and insert data.

   ```SQL
   CREATE TABLE IF NOT EXISTS db_1.test_bool_local 
   (
       `a` Int64, 
       `b` String, 
       `c` Bool, 
       `d` Boolean
   ) ENGINE = HaUniqueMergeTree(
       '/clickhouse/{Account_ID}/{Cluster_Name}/db_1.test_bool_local/{shard}',
       '{replica}'
     )
   ORDER BY a
   UNIQUE KEY a
   SETTINGS
     storage_policy = 's3_cold',
     index_granularity = 8192;
   
   
   CREATE TABLE IF NOT EXISTS db_1.test_bool
   (
       `a` Int64, 
       `b` String, 
       `c` Bool, 
       `d` Boolean
   ) 
   ENGINE = Distributed(
       '{Cluster_Name}',
       'db_1',
       'test_bool_local',
       intHash64(a)
   );
   
   INSERT INTO db_1.test_bool VALUES (1,'a', true, true), (2,'a', false, false), (3,'a', 1, 1), (4,'a', 0, 0);
   
   DESC db_1.test_bool;
   
   SELECT * from db_1.test_bool;
   ```
   

2. View the table's column definitions.

   ```SQL
   DESC db_1.test_bool;
   ```
   

   The output is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0bf2a2b44df41e19549a53af1a22878~tplv-goo7wpa0wc-image.image) </span>

   The result shows that the d column is defined as the Boolean type when creating the table, but it displays as the Bool type in the output.

3. Query the data and corresponding types in the table.

   ```SQL
   SELECT * from db_1.test_bool;
   ```
   

   The output is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/115a5099760d4e50a672076c7cf40c7b~tplv-goo7wpa0wc-image.image) </span>
