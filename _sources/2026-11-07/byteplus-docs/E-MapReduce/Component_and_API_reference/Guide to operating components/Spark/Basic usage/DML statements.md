---
title: "DML statements"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DML_statements"
---

In Apache Spark, DML (Data Manipulation Language) statements are used to manipulate data in databases.

Suppose there is a table named sales with the following structure:

```sql
CREATE TABLE sales (
  date STRING,
  amount DOUBLE
)
```


This table contains daily sales data.

<span id="_1-insert-into"></span>
## 1 INSERT INTO

This statement is used to insert data into an existing table.


* Syntax


```sql
INSERT INTO [ TABLE ] table_identifier [ partition_spec ] [ ( column_list ) ] { VALUES ( { value | NULL } [ , ... ] ) [ , ( ... ) ] | query }
```



* Example statement execution


```sql
INSERT INTO TABLE sales VALUES ('2023-04-01', 100.0), ('2023-04-02', 80.0);
```



* Execution result

   The sales table will have two new rows added:



|date |amount |
|---|---|
|2023\-04\-01 |100.0 |
|2023\-04\-02 |80.0 |


<span id="_2-insert-overwrite"></span>
## 2 INSERT OVERWRITE

This statement is used to write data into a table. If the table already exists, it will be overwritten.


* Syntax


```sql
INSERT OVERWRITE [ TABLE ] table_identifier [ partition_spec [ IF NOT EXISTS ] ] [ ( column_list ) ]{ VALUES ( { value | NULL } [ , ... ] ) [ , ( ... ) ] | query }
```



* Example statement execution


```sql
INSERT OVERWRITE TABLE sales VALUES ('2023-04-01', 300.0);
```



* Execution result



|date |amount |
|---|---|
|2023\-04\-01 |300.0 |


`INSERT OVERWRITE` If the table being overwritten is a partitioned table and the partition column values are not specified, for example

```sql
INSERT OVERWRITE partition_table PARTITION(a=1, b) SELECT *
```


Spark will take different actions based on the setting of the parameter (`spark.sql.sources.partitionOverwriteMode`):


* If set to `STATIC` (default): all partitions with `a=1, b=*` will be deleted, and then specific values will be inserted

* If set to `DYNAMIC`: only the partitions for b that are included in the results of `SELECT` will be overwritten


<span id="_3-insert-overwrite-directory"></span>
## 3 INSERT OVERWRITE DIRECTORY

This statement is used to write data as files to a specified directory. If the directory already exists, it will be overwritten.


* Syntax


```sql
INSERT OVERWRITE [ LOCAL ] DIRECTORY [ directory_path ]
    USING file_format [ OPTIONS ( key = val [ , ... ] ) ]
    { VALUES ( { value | NULL } [ , ... ] ) [ , ( ... ) ] | query }
```



* Example statement execution


```sql
INSERT OVERWRITE DIRECTORY '/path/to/sales_data'
USING parquet
SELECT * FROM sales;
```



* Execution result

   A parquet file will be created in the specified directory /path/to/sales_data, containing all data from the sales table:


```sql
date,amount
2023-04-01,100.0
2023-04-02,80.0
```


<span id="_4-insert-overwrite-directory-hive格式"></span>
## 4 INSERT OVERWRITE DIRECTORY (Hive format)


* Syntax


```sql
INSERT OVERWRITE [ LOCAL ] DIRECTORY directory_path
    [ ROW FORMAT row_format ] [ STORED AS file_format ]
    { VALUES ( { value | NULL } [ , ... ] ) [ , ( ... ) ] | query }
```



* Example statement execution


```sql
INSERT OVERWRITE DIRECTORY '/path/to/sales_data'
ROW FORMAT DELIMITED
STORED AS parquet
SELECT * FROM sales;
```



* Execution result

   A parquet file will be created in the specified directory /path/to/sales_data, containing all data from the sales table:


```sql
date,amount
2023-04-01,100.0
2023-04-02,80.0
```


<span id="_5-load"></span>
## 5 LOAD

The LOAD statement is used to load data from external storage systems into Spark SQL. Note that LOAD is usually used with data source options and may vary depending on the Spark version.


* Syntax


```sql
LOAD DATA [ LOCAL ] INPATH path [ OVERWRITE ] INTO TABLE table_identifier [ partition_spec ]
```



* Example statement execution


```sql
LOAD DATA LOCAL INPATH 'file:/path/to/external_sales_data.csv'
INTO TABLE sales
OPTIONS (header "true", delimiter ",");
```



* Execution result

   If the external_sales_data.csv file contains the following data:


```sql
date,amount
2023-04-03,120.0
2023-04-04,150.0
```


After executing the above LOAD statement, the sales table will contain two new rows loaded from the CSV file:


|date |amount |
|---|---|
|2023\-04\-01 |100.0 |
|2023\-04\-02 |80.0 |
|2023\-04\-03 |120.0 |
|2023\-04\-04 |150.0 |
