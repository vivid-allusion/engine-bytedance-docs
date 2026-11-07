---
title: "DDL statements"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DDL_statements"
---

In Apache Spark SQL, DDL (Data Definition Language) statements are used to define and modify the structure of a database. The following are some examples of how to use Spark SQL DDL statements, including execution statements and their corresponding results:

<span id="_1-create-database"></span>
## 1 CREATE DATABASE

Create a new database.


* Syntax


```sql
CREATE { DATABASE | SCHEMA } [ IF NOT EXISTS ] database_name
    [ COMMENT database_comment ]
    [ LOCATION database_directory ]
    [ WITH DBPROPERTIES ( property_name = property_value [ , ... ] ) ]
```



* Example execution statement


```sql
CREATE DATABASE IF NOT EXISTS my_database;
```



* Execution result

   A new database named my_database is created. If the database already exists, no action is taken.


<span id="_2-use-database"></span>
## 2 USE DATABASE

Switch the current database in use.


* Syntax


```sql
USE database_name
```



* Example execution statement


```sql
USE my_database;
```



* Execution result

   my_database is set as the current database. Subsequent SQL statements will be executed in this database by default.


<span id="_3-alter-database"></span>
## 3 ALTER DATABASE

Modify the properties of a database.


* Syntax


```sql
ALTER { DATABASE | SCHEMA } database_nameSET DBPROPERTIES ( property_name = property_value [ , ... ] )
```



* Example execution statement


```sql
ALTER DATABASE my_database SET DBPROPERTIES ('property_name'='property_value');
```



* Execution result

   The properties of the my_database database are modified.


<span id="_4-drop-database"></span>
## 4 DROP DATABASE

Delete a database.


* Syntax


```sql
DROP { DATABASE | SCHEMA } [ IF EXISTS ] dbname [ RESTRICT | CASCADE ]
```



* Example execution statement


```sql
DROP DATABASE IF EXISTS my_database CASCADE;
```



* Execution result

   The my_database database and all its tables are deleted. The CASCADE option ensures that all related objects are removed.


<span id="_5-create-table"></span>
## 5 CREATE TABLE

Create a new table.


* Syntax


<span id="create-table-using-datasource"></span>
### CREATE TABLE USING DATASOURCE

```sql
CREATE TABLE [ IF NOT EXISTS ] 
    table_identifier[ ( col_name1 col_type1 [ COMMENT col_comment1 ], ... ) ]
    USING data_source
    [ OPTIONS ( key1=val1, key2=val2, ... ) ]
    [ PARTITIONED BY ( col_name1, col_name2, ... ) ]
    [ CLUSTERED BY ( col_name3, col_name4, ... ) 
        [ SORTED BY ( col_name [ ASC | DESC ], ... ) ] 
        INTO num_buckets BUCKETS ]
    [ LOCATION path ]
    [ COMMENT table_comment ]
    [ TBLPROPERTIES ( key1=val1, key2=val2, ... ) ][ AS select_statement ]
```


<span id="create-hiveformat-table"></span>
### CREATE HIVEFORMAT TABLE

```sql
CREATE [ EXTERNAL ] TABLE [ IF NOT EXISTS ] table_identifier
    [ ( col_name1[:] col_type1 
    [ COMMENT col_comment1 ], ... ) ]
    [ COMMENT table_comment ]
    [ PARTITIONED BY ( col_name2[:] col_type2 [ COMMENT col_comment2 ], ... ) 
        | ( col_name1, col_name2, ... ) ]
    [ CLUSTERED BY ( col_name1, col_name2, ...) 
        [ SORTED BY ( col_name1 [ ASC | DESC ], col_name2 [ ASC | DESC ], ... ) ] 
        INTO num_buckets BUCKETS ]
    [ ROW FORMAT row_format ]
    [ STORED AS file_format ]
    [ LOCATION path ]
    [ TBLPROPERTIES ( key1=val1, key2=val2, ... ) ]
    [ AS select_statement ]

row_format:    
    : SERDE serde_class [ WITH SERDEPROPERTIES (k1=v1, k2=v2, ... ) ]
    | DELIMITED [ FIELDS TERMINATED BY fields_terminated_char [ ESCAPED BY escaped_char ] ] 
        [ COLLECTION ITEMS TERMINATED BY collection_items_terminated_char ] 
        [ MAP KEYS TERMINATED BY map_key_terminated_char ]
        [ LINES TERMINATED BY row_terminated_char ]
        [ NULL DEFINED AS null_char ]
```


<span id="create-table-like"></span>
### CREATE TABLE LIKE

```sql
CREATE TABLE [IF NOT EXISTS] table_identifier LIKE source_table_identifier
    USING data_source[ ROW FORMAT row_format ]
    [ STORED AS file_format ]
    [ TBLPROPERTIES ( key1=val1, key2=val2, ... ) ]
    [ LOCATION path ]
```



* Example execution statement


```sql
CREATE TABLE [IF NOT EXISTS] my_database.my_table (
  id INT,
  name STRING,
  value DOUBLE
);
```



* Execution result

   A new table named my_table is created in the my_database database. If the table already exists, no action is taken. If `IF NOT EXISTS` is not provided and the table already exists, an error is reported indicating that the table already exists.


<span id="_6-alter-table"></span>
## 6 ALTER TABLE

Modify the structure of a table, such as adding or replacing columns.


* Syntax


```sql
ALTER TABLE table_identifier RENAME TO table_identifier
ALTER TABLE table_identifier partition_spec RENAME TO partition_spec
```



* Example execution statement


```sql
ALTER TABLE my_database.my_table ADD COLUMNS (new_col1 STRING, new_col2 INT);
```



* Execution result

   Two columns, new_col1 and new_col2, are added to the my_table table.


<span id="_7-truncate-table"></span>
## 7 TRUNCATE TABLE

Delete all data in a table.


* Syntax


```sql
TRUNCATE TABLE table_identifier [ partition_spec ]
```



* Example execution statement


```sql
TRUNCATE TABLE my_database.my_table;
```



* Execution result

   All data in the my_table table is deleted, but the table structure remains unchanged.


<span id="_8-repair-table"></span>
## 8 REPAIR TABLE

Repair a corrupted table.


* Syntax


```sql
MSCK REPAIR TABLE table_identifier
```



* Example execution statement


```sql
REPAIR TABLE my_database.my_table;
```



* Execution result

   The my_table table is repaired and restored to a usable state.


<span id="_9-drop-table"></span>
## 9 DROP TABLE

Delete a table.


* Syntax


```sql
DROP TABLE [ IF EXISTS ] table_identifier
```



* Example execution statement


```sql
DROP TABLE IF EXISTS my_database.my_table;
```



* Execution result

   The my_table table in the my_database database is deleted.


<span id="_10-create-view"></span>
## 10 CREATE VIEW

Create a new view.


* Syntax


```sql
CREATE [ OR REPLACE ] [ [ GLOBAL ] TEMPORARY ] VIEW [ IF NOT EXISTS ] view_identifiercreate_view_clauses AS query
```



* Example execution statement


```sql
CREATE VIEW [IF NOT EXISTS] my_database.my_view AS
SELECT name, SUM(value) AS total_value
FROM my_database.my_table
GROUP BY name;
```



* Execution result

   A new view named my_view is created in the my_database database. This view displays the total value for each name in the my_table table. If `IF NOT EXISTS` is not provided and the view already exists, an error is reported indicating that the view already exists.


<span id="_11-alter-view"></span>
## 11 ALTER VIEW

Modify the definition of a view.


* Syntax


```sql
ALTER VIEW view_identifier RENAME TO view_identifier
```



* Example execution statement


```sql
ALTER VIEW my_database.my_view AS
SELECT name, SUM(value) AS total_value, id
FROM my_database.my_table
GROUP BY name, id;
```



* Execution result

   The definition of the my_view view has been modified to now include the id column and to group by name and id.


<span id="_12-drop-view"></span>
## 12 DROP VIEW

Delete a view.


* Syntax


```sql
DROP VIEW [ IF EXISTS ] view_identifier
```



* Example execution statement


```sql
DROP VIEW IF EXISTS my_database.my_view;
```



* Execution result

   The my_view view in the my_database database has been deleted.


<span id="_13-create-function"></span>
## 13 CREATE FUNCTION

Create a custom Scala or Java function.


* Syntax


```sql
CREATE [ OR REPLACE ] [ TEMPORARY ] FUNCTION [ IF NOT EXISTS ]function_name AS class_name [ resource_locations ]
```



* Example execution statement


```sql
CREATE FUNCTION [IF NOT EXISTS] my_database.my_function
AS 'full.class.name.of.your.UDAF';
```



* Execution result

   A new function named my_function has been created in the my_database database. If `IF NOT EXISTS` is not provided and the function already exists, an error is reported indicating that the function already exists.


<span id="_14-drop-function"></span>
## 14 DROP FUNCTION

Delete a custom function.


* Syntax


```sql
DROP [ TEMPORARY ] FUNCTION [ IF EXISTS ] function_name
```



* Example execution statement:


```sql
DROP FUNCTION IF EXISTS my_database.my_function;
```



* Execution result

   The my_function function in the my_database database has been deleted.
