---
title: "Default Catalog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/dla_default_catalog"
---

StarRocks version 2.3 and above provides the Internal Catalog (internal data catalog), which is used to manage StarRocks internal data. This article introduces how to query internal data.

<span id="_1-背景信息"></span>
## 1 **Context**

Each StarRocks instance has one and only one Internal Catalog, named `default_catalog`. Currently, StarRocks does not support renaming the Internal Catalog or creating a new Internal Catalog.

<span id="_2-查询内部数据"></span>
## 2 **Query internal data**


1. Database query

* Without specifying the catalog name


```sql
SHOW DATABASES;
```



* Specifying the catalog name


```sql
SHOW DATABASES FROM default_catalog;
```



2. Switch database

   1. Without specifying the catalog name

   ```sql
   USE <db_name>;
   ```
   

   3. Specifying the catalog name

   ```sql
   USE default_catalog.<db_name>;
   ```
   

3. Query internal data.

   1. Without specifying the catalog name

   ```sql
   SELECT * FROM <table_name>;
   ```
   

   3. If the database is not specified in the above steps, you can specify it directly in the query statement.

   ```sql
   SELECT * FROM <db_name>.<table_name>;
   ```
   

   5. Specifying the catalog name is mainly used for operations such as cross\-catalog joins and similar operations.

   ```sql
   SELECT * FROM default_catalog.<db_name>.<table_name>;
   ```
   


<span id="_3-示例"></span>
## 3 **Examples**

To query data in volc_db.volc_table, use the following commands:


* Method 1


```sql
USE volc_db;
SELECT * FROM volc_table limit 1;
```



* Method 2


```sql
SELECT * FROM volc_db.volc_table limit 1;
```



* Method 3


```sql
SELECT * FROM default_catalog.volc_db.volc_table limit 1;
```
