---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/spark_basic_usage"
---

This article provides basic operation examples for Spark\-supported resilient distributed datasets (RDD), Spark SQL, PySpark, and database tables.

<span id="_1-使用前提"></span>
## 1 Prerequisites

An E\-MapReduce (EMR) cluster has been created. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456) **.** 

<span id="_2-rdd基础操作"></span>
## **2 Basic RDD operations**

Spark is built around the concept of RDD. An RDD is a fault\-tolerant collection of elements that can be operated on in parallel. Spark supports two ways to create an RDD: by using a collection or by constructing an RDD from an external dataset. For example, a shared file system, HDFS, HBase, or any dataset that provides Hadoop InputFormat.

<span id="_2-1-创建rdd示例："></span>
### 2.1 Example of creating an RDD:


* Create an RDD from a collection


```Plain
val data = Array(1, 2, 3, 4, 5)
val distData = sc.parallelize(data)
```



* Create an RDD from an external dataset


```Plain
val distFile = sc.textFile("data.txt")
```


After an RDD is successfully constructed, a series of operations can be performed on it, such as Map and Reduce.

For example, by running the following code, a text file is first read from an external storage system to construct an RDD. Then, the Map transformation of the RDD is used to calculate the length of each line in the text file, and finally, the Reduce transformation is used to calculate the sum of the lengths of all lines in the text file.

```Plain
val lines = sc.textFile("data.txt")
val lineLengths = lines.map(s => s.length)
val totalLength = lineLengths.reduce((a, b) => a + b)
```


<span id="_2-2-spark-rdd常用操作"></span>
### 2.2 Common Spark RDD operations

Typically, there are two common types of operations for Spark RDDs: transformation operations and action operations. Transformation operations are not executed immediately; they are only executed when an action operation is performed.


* Transformation operations



|Operation |Description |
|---|---|
|map() |The parameter is a function, which is applied to each element of the RDD. The return value is a new RDD. |
|flatMap() |The parameter is a function, which is applied to each element of the RDD. The element data is split into multiple elements, resulting in an iterator. The return value is a new RDD. |
|filter() |The parameter is a function, which filters out elements that do not meet the criteria. The return value is a new RDD. |
|distinct() |No parameters. Removes duplicates from the elements in the RDD. |
|union() |The parameter is an RDD. Generates a new RDD containing all elements from both RDDs. |
|intersection() |The parameter is an RDD. Returns the common elements of the two RDDs. |
|subtract() |The parameter is an RDD. Removes elements from the original RDD that are also present in the parameter RDD. |
|cartesian() |The parameter is an RDD. Returns the Cartesian product of the two RDDs. |



* Action operations



|Operation |Description |
|---|---|
|collect() |Returns all elements of the RDD. |
|count() |Returns the number of elements in the RDD. |
|countByValue() |Returns the number of occurrences of each element in the RDD. |
|reduce() |Combines all elements of the RDD in parallel, for example, summing. |
|fold(0)(func) |Has the same functionality as reduce(), but fold takes an initial value. |
|aggregate(0)(seqOp,combop) |Has the same functionality as reduce(), but the data type of the returned value is different from that of the original RDD. |
|foreach(func) |Applies a specific function to each element of the RDD. |


<span id="_3-spark-sql-基础操作"></span>
## **3 Basic Spark SQL operations**

Spark SQL supports directly operating on data using SQL statements. Spark parses, optimizes, and executes the SQL statements.

The following examples demonstrate how to use Spark SQL to read files. The examples are as follows:


* Example 1: Spark supports multiple data formats. In this example, data from a JSON format file is read and output as Parquet format.


```Plain
val peopleDF = spark.read.json("examples/src/main/resources/people.json")
peopleDF.write.parquet("people.parquet")
```



* Example 2: Using SQL, the names of young people aged between 13 and 19 are read from the parquetFile table and converted to a DataFrame. Then, the Map transformation is used to convert the names into a readable form and output them.


```Plain
val namesDF = spark.sql("SELECT name FROM parquetFile WHERE age BETWEEN 13 AND 19")
namesDF.map(attributes => "Name: " + attributes(0)).show()
```


<span id="_4-pyspark基础操作"></span>
## 4 Basic PySpark operations

PySpark is the Python API provided by Spark. Various computation logic can be completed using the DataFrame interface provided by PySpark.

**Procedure**


1. Initialize SparkSession.

2. Initialize SparkSession as the entry point for PySpark execution.


```Plain
from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()
```



3. Create a DataFrame.


```Plain
from datetime import datetime, date
import pandas as pd
from pyspark.sql import Row

df = spark.createDataFrame([
    (1, 2., 'string1', date(2000, 1, 1), datetime(2000, 1, 1, 12, 0)),
    (2, 3., 'string2', date(2000, 2, 1), datetime(2000, 1, 2, 12, 0)),
    (3, 4., 'string3', date(2000, 3, 1), datetime(2000, 1, 3, 12, 0))
], schema='a long, b double, c string, d date, e timestamp')
```



4. After the DataFrame is created, various types of transformations can be used to perform data computation.

5. Print the DataFrame and schema.


```Plain
df.show()
df.printSchema()
```


<span id="_5-基础库表操作"></span>
## 5 Basic database table operations

EMR SparkSQL is fully compatible with open\-source SparkSQL syntax. The following provides a Note on basic database and table operations. For more detailed guidance, refer to the [open-source SparkSQL syntax Note](https://spark.apache.org/docs/3.1.1/sql-programming-guide.html).

<span id="_5-1-数据库操作"></span>
### **5.1 Database operations**

<span id="_5-1-1-创建数据库"></span>
#### **5.1.1 Create a database**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> create database db_demo;
+---------+
| Result  |
+---------+
+---------+
No rows selected (0.285 seconds)
```


<span id="_5-1-2-查看数据库信息"></span>
#### **5.1.2 View database information**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> desc database db_demo;
+----------------------------+----------------------------------------------------+
| database_description_item  |             database_description_value             |
+----------------------------+----------------------------------------------------+
| Database Name              | db_demo                                            |
| Comment                    |                                                    |
| Location                   | hdfs://emr-master-1-1:8020/apps/spark/warehouse/db_demo.db |
| Owner                      | hive                                               |
+----------------------------+----------------------------------------------------
```


<span id="_5-1-3-删除数据库"></span>
#### **5.1.3 Delete a database**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> drop database db_demo;
+---------+
| Result  |
+---------+
+---------+
No rows selected (0.266 seconds)
```


<span id="_5-2-表操作"></span>
### **5.2 Table operations**

<span id="_5-2-1-创建表"></span>
#### **5.2.1 Create a table**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> create table tb_demo(id int, name string);
+---------+
| Result  |
+---------+
+---------+
No rows selected (0.128 seconds)
```


<span id="_5-2-2-描述表信息"></span>
#### **5.2.2 Describe table**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> desc table tb_demo;
+-----------+------------+----------+
| col_name  | data_type  | comment  |
+-----------+------------+----------+
| id        | int        | NULL     |
| name      | string     | NULL     |
+-----------+------------+----------+
```


<span id="_5-2-3-删除表"></span>
#### **5.2.3 Delete a table**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> drop table tb_demo;
+---------+
| Result  |
+---------+
+---------+
```


<span id="_5-2-4-插入数据"></span>
#### **5.2.4 Insert data**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> insert into tb_demo select 1,'name1';
+---------+
| Result  |
+---------+
+---------+
```


<span id="_5-2-5-查询表数据"></span>
#### **5.2.5 Query table data**

```Plain
0: jdbc:hive2://emr-master-1-1:10005> select * from tb_demo;
+-----+-------+
| id  | name  |
+-----+-------+
+ 1   + name1 +
+-----+-------+
1 rows selected (0.116 seconds)
```
