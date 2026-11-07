---
title: "Import using the Insert method"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Import_using_the_Insert_method"
---

This article describes how to use the INSERT statement to import data into StarRocks. The images and content in this article are sourced from the open\-source StarRocks [Importing data using the INSERT statement](https://docs.starrocks.io/zh/docs/loading/InsertInto) section.

<span id="_1-适用场景"></span>
## 1 **use cases**


* The INSERT statement synchronously returns the result of the import operation.

* If any data does not conform to the target table format, executing the INSERT statement will fail. Set the session variable `enable_insert_strict` to `false` to filter out data that does not conform to the target table format and continue executing the INSERT operation.

* Frequent use of the INSERT statement to import small batches of data will generate excessive data versions, which can affect query performance. Therefore, it is not recommended to frequently use the INSERT statement for data import or as a routine import job in production environments. To import only a few test records and verify the functionality of the StarRocks system, use the INSERT INTO VALUES statement.

* To import ETL\-transformed data from StarRocks into a new StarRocks table, use the INSERT INTO SELECT statement.

* After executing the INSERT OVERWRITE statement, the system creates corresponding temporary partitions for the target partition, writes data to the temporary partitions, and finally uses the temporary partitions to [atomically replace](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-definition/ALTER_TABLE#%E4%BD%BF%E7%94%A8%E4%B8%B4%E6%97%B6%E5%88%86%E5%8C%BA%E6%9B%BF%E6%8D%A2%E5%8E%9F%E5%88%86%E5%8C%BA) the target partitions to overwrite the target partitions. All processes are executed on the Leader FE node. Therefore, if the Leader FE node fails during the overwrite process, the INSERT OVERWRITE import will fail, and any temporary partitions created during the process will be deleted.


<span id="_2-基本操作"></span>
## 2 **Basic operations**

<span id="_2-1-语法"></span>
### 2.1 **Syntax**

```sql
INSERT { INTO | OVERWRITE } [db_name.]<table_name>
[ PARTITION (<partition_name> [, ...) ]
[ TEMPORARY_PARTITION (<temporary_partition_name>[, ...) ]
[ WITH LABEL <label>]
[ (<column_name>[, ...]) ]
{ VALUES ( { <expression> | DEFAULT }[, ...] ) | <query> }
```


The parameter descriptions are as follows, and you can also [refer to the official website](https://docs.starrocks.io/zh/docs/sql-reference/sql-statements/data-manipulation/INSERT):


|Parameter |Note |
|---|---|
|PARTITION |The target partitions for import. Multiple partition names are separated by commas (,). |
|label |The identifier of the import job, unique within the database. If not specified, StarRocks will automatically generate a Label for the job.<br><br>We recommend specifying a Label. Otherwise, if the current import job cannot return a result due to a network error, you will not be able to determine whether the import operation was successful. If a Label is specified, you can view the task result using the Label. |
|column_name |The target columns for import, which must exist in the target table.<br><br>The mapping of this parameter is not related to column names, but matches the order exactly. If the target columns are not specified, all columns in the target table are used by default. If a column in the source table does not exist in the target columns, a default value will be written. If the current column does not have a default value, the import job will fail. If the result column type of the query statement is inconsistent with the target column type, implicit conversion will be performed. If conversion cannot be performed, the INSERT INTO statement will report a syntax error. |
|expression |An expression used to assign a value to the corresponding column. |
|DEFAULT |Assign a default value to the corresponding column. |
|query |The query statement whose results will be imported into the target table. The query statement supports any SQL query syntax supported by StarRocks. |


<span id="_2-2-导入结果介绍"></span>
### 2.2 **Introduction to import results**

After executing the Insert import statement, the result is synchronously returned as follows:

```sql
Query OK, 7 rows affected (0.044 sec)
{'label':'my_lable', 'status':'VISIBLE', 'txnId':'43864'}
```


The parameter descriptions are as follows:


|Parameter |Description |
|---|---|
|rows affected |Indicates the total number of rows imported. `warnings` indicates the number of filtered rows. |
|label |The Label specified by the user or automatically generated. The Label is the identifier for the INSERT import job and is unique within the current database. |
|status |Indicates whether the imported data is visible. VISIBLE means visible, COMMITTED means committed but temporarily not visible. |
|txnId |The import transaction ID corresponding to the INSERT import. |
|err |If the import execution fails, StarRocks will return the corresponding error and `tracking_url`. You can use `tracking_url` to view log information related to the error and troubleshoot the issue.<br><br>For example: ERROR 1064 (HY000): Insert has filtered data in strict mode, tracking_url=http://x.x.x.x:yyyy/api/_load_error_log?file=error_log_9f0a4fd0b64e11ec_906bbede076e9d08 |


**Note** The return result of the row\-store table does not contain the 'lable' keyword.

<span id="_3-相关配置"></span>
## 3 Related configuration


* FE configuration

   
   |FE configuration item |Note |
   |---|---|
   |insert_load_default_timeout_second |The timeout period for INSERT import jobs, unit: seconds. The default value is 3600 seconds (1 hour).<br><br>If the current INSERT import job is not completed within the time specified by this parameter, it will be canceled by the system and its status will be CANCELLED. Currently, this parameter only supports setting a unified timeout period for all INSERT import jobs. Setting a timeout period for individual import jobs is not supported. If the import job cannot be completed within the specified time, you can extend the timeout period by adjusting this parameter. |
   

* Session variables

   
   |Session variable |Note |
   |---|---|
   |enable_insert_strict |Whether the INSERT import allows erroneous data rows. The default value for this parameter is `true`.<br><br>When set to `true`, if any row contains an error, the import will fail. When set to `false`, if at least one row is imported successfully, the import will be considered successful and a Label will be returned. You can set this parameter using the `SET enable_insert_strict = {true or false};` command. |
   |query_timeout |The timeout period for SQL commands, unit: seconds.<br><br>The INSERT statement, as an SQL command, is also subject to the restrictions of this Session variable. You can set this parameter using the `SET query_timeout = xxx;` command. |
   


<span id="_4-导入示例"></span>
## 4 **Import example**

This section introduces an example of importing row\-store table data into a column\-store table.


1. Execute the following commands to create a database and a row\-store table.


```sql
--Create a row-store table
CREATE DATABASE IF NOT EXISTS demo;
CREATE TABLE IF NOT EXISTS demo.row_store_table(
    k1 int,
    k2 int,
    v1 varchar(16),
    v2 DATE NOT NULL COMMENT "YYYY-MM-DD",
    v3 TINYINT COMMENT "range [-128, 127]"
) ENGINE=ROW_STORE
PRIMARY KEY (k1, k2);
```



2. Import several records to verify the data


```sql
INSERT INTO demo.row_store_table(k1, k2, v1, v2, v3) VALUES
     (1, 2, 'a', "2222-12-22", 33),
     (1, 3, 'b', "2222-12-22", 34),
     (1, 4, 'c', "2222-12-22", 35),
     (2, 2, 'd', "2222-12-22", 36),
     (2, 3, 'd', "2222-12-22", 37),
     (3, 3, 'e', "2222-12-22", 100),
     (4, 4, 'f', "2222-12-22", 101);
SELECT * FROM demo.row_store_table;
```



3. Create a column\-store table


```sql
-- Create a column-store table and import some test data
CREATE TABLE IF NOT EXISTS demo.column_store_table(
    k1 int,
    k2 int,
    v1 varchar(16),
    v2 DATE NOT NULL COMMENT "YYYY-MM-DD",
    v3 TINYINT COMMENT "range [-128, 127]"
)
DISTRIBUTED BY HASH(k1, k2) BUCKETS 3;
```



4. Create an import task


```sql
INSERT INTO demo.column_store_table WITH LABEL insert_column_store_load SELECT * FROM  demo.row_store_table;
```



5. View column\-store table data


```sql
SELECT * FROM demo.column_store_table;
```
