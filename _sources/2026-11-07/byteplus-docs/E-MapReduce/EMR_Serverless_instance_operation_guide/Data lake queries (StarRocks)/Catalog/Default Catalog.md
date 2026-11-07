---
title: "Default Catalog"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Default_Catalog"
---

Each StarRocks instance has one and only one Internal Catalog, named `default_catalog`. StarRocks currently does not support modifying the name of the Internal Catalog, nor does it support creating new Internal Catalogs.

This article describes how to use the Default Catalog to query internal data in StarRocks.

<span id="_1-查询内部数据"></span>
## Step 1: Query internal data


1. Connect to StarRocks. The connection methods are as follows:

   1. Connect to StarRocks from a MySQL client. For details, see "Connect to a StarRocks instance using a client." After connecting, you enter `default_catalog` by default.

   2. Connect to StarRocks using JDBC. You can specify the database to connect to by using `default_catalog.db_name` during the connection. For details, see "Connect to a StarRocks instance using JDBC."

2. (Optional) Execute the following command to view all databases in the current StarRocks instance:

   ```sql
   SHOW DATABASES;
   -- Or: Specify the catalog name
   SHOW DATABASES FROM default_catalog;
   ```
   

3. (Optional) Execute the following command to switch to the specified database:

   ```sql
   -- Specify the database effective for the current session using [USE](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/USE)
   USE <db_name>;
   -- Or: Specify the catalog name
   USE <catalog_name>.<db_name>;
   ```
   

4. Query internal data using [SELECT](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/SELECT):

   ```sql
   SELECT * FROM <table_name>;
   -- Without specifying the catalog name
   SELECT * FROM <db_name>.<table_name>;
   -- Specify the catalog name
   SELECT * FROM default_catalog.<db_name>.<table_name>;
   ```
   


<span id="_2-示例"></span>
## Step 2: Example

To query data in `olap_db.olap_table`, proceed as follows:

```sql
USE olap_db;
SELECT * FROM olap_table limit 1;
-- Or
SELECT * FROM olap_db.olap_table limit 1;   
-- Or
SELECT * FROM default_catalog.olap_db.olap_table limit 1;
```
