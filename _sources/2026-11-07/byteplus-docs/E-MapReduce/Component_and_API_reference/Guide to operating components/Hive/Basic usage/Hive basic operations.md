---
title: "Hive basic operations"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Hive_basic_operations"
---

This document describes how to use Hive to perform operations such as creating databases and tables on an E\-MapReduce (EMR) cluster.

<span id="_1-前提条件"></span>
## **1 Prerequisites**

The cluster has been created. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

<span id="_2-进入-hive-命令行"></span>
## **2 Access the Hive CLI**


1. Log in to an EMR cluster node:

   1. Option 1: Log in to the cluster's primary node using SSH. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

   2. Option 2: Alternatively, you can use the ECS ID in the EMR cluster's **Hive service** to navigate to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.

2. Run the following command to switch to the hive user.


```shell
su  hive
```



3. Run the following command to enter the Hive CLI.


```shell
hive
```


If the following information is returned, you have entered the Hive CLI.

> Hive Session ID = aaa9c23d\-4975\-4c10\-bb9a\-1817c5fa36e6

> Logging initialized using configuration in file:/etc/emr/hive/conf/hive\-log4j2.properties Async: true

> Hive Session ID = 258437d2\-f601\-42c9\-bab3\-731b975b0642


<span id="_3-库操作"></span>
## 3 Database operations

In the examples in this document, the database testdb is used.

<span id="_3-1-创建库"></span>
### 3.1 Create a database

```shell
CREATE DATABASE IF NOT EXISTS testdb;
```


If the returned information is:

> OK

> Time taken: 0.617 seconds


This indicates that the database was created successfully.

<span id="_3-2-查看库"></span>
### 3.2 View a database

```sql
DESC DATABASE testdb;
```


The returned information is as follows:

> OK

> testdb hdfs://iv\-ybtfk74d08kdvbpw7bf3:8020/warehouse/tablespace/managed/hive/testdb.db hive USER

> Time taken: 0.155 seconds, Fetched: 1 row(s)


<span id="_3-3-使用库"></span>
### 3.3 Use a database

```sql
USE testdb;
```


The returned information is as follows:

> OK

> Time taken: 0.034 seconds


<span id="_3-4-删除库"></span>
### 3.4 Delete a database

```sql
DROP DATABASE IF EXISTS testdb;
```


The returned information is as follows, indicating successful deletion:

> OK

> Time taken: 0.104 seconds


<span id="_4-表操作"></span>
## 4 Table operations

In the examples in this document, the table test_table is used.

<span id="_4-1-创建表"></span>
### 4.1 Create a table

```shell
CREATE TABLE IF NOT EXISTS test_table 
(
id BIGINT,
value STRING
)
STORED AS ORC;
```


The returned information is as follows, indicating successful table creation:

> OK

> Time taken: 0.426 seconds


<span id="_4-2-查看表"></span>
### 4.2 View a table

```shell
DESC FORMATTED test_table;
```


The returned information is as follows:

> OK

> <span id="col-name-data-type-comment"></span>
# col_name data_type comment

> id bigint

> value string

> <span id="detailed-table-information"></span>
# Detailed Table Information

> Database: testdb

> OwnerType: USER

> Owner: hive

> CreateTime: Mon Aug 01 17:48:56 CST 2022

> LastAccessTime: UNKNOWN

> Retention: 0

> Location: hdfs://iv\-ybtfk74d08kdvbpw7bf3:8020/warehouse/tablespace/managed/hive/testdb.db/test_table

> Table Type: MANAGED_TABLE

> Table Parameters:

> COLUMN_STATS_ACCURATE {"BASIC_STATS":"true","COLUMN_STATS":{"id":"true","value":"true"}}

> bucketing_version 2

> numFiles 0

> numRows 0

> rawDataSize 0

> totalSize 0

> transient_lastDdlTime 1659347336

> <span id="storage-information"></span>
# Storage Information

> SerDe Library: org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe

> InputFormat: org.apache.hadoop.mapred.TextInputFormat

> OutputFormat: org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat

> Compressed: No

> Num Buckets: \-1

> Bucket Columns: []

> Sort Columns: []

> Storage Desc Params:

> serialization.format 1

> Time taken: 0.259 seconds, Fetched: 32 row(s)


<span id="_4-3-查看所有表"></span>
### 4.3 View all tables

```sql
SHOW TABLES;
```


The returned information is as follows:

> OK

> test_table

> Time taken: 0.036 seconds, Fetched: 1 row(s)


<span id="_4-4-删除表"></span>
### 4.4 Delete a table

```sql
DROP TABLE IF EXISTS test_table;
```


> OK

> Time taken: 0.227 seconds


<span id="_5-sql-操作"></span>
## 5 SQL operations

<span id="_5-1-插入记录"></span>
### 5.1 Insert records

```sql
INSERT INTO TABLE test_table VALUES(1, 'value1');
```


The returned information includes:

> OK

> Time taken: 15.676 seconds


This indicates that the record was inserted successfully.

<span id="_5-2-查询表记录"></span>
### 5.2 Query table records

```sql
SELECT * FROM test_table LIMIT 5;
```


The returned information is as follows:

> OK

> 1 value1

> Time taken: 0.195 seconds, Fetched: 1 row(s)


<span id="_5-3-聚合操作"></span>
### 5.3 Perform aggregate operations

```sql
SELECT value, COUNT(*) FROM test_table GROUP BY value;
```


The returned information is as follows:

> OK

> value1 1

> Time taken: 4.207 seconds, Fetched: 1 row(s)


<span id="094ee744"></span>
## 6 Quick start with Doris

<span id="92811be8"></span>
### 6.1 Catalog

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Doris version used has the following restrictions:</div>



* <div data-tips="true" data-tips-type="warning">Version 2.x: Doris supports this feature starting from version 2.1.11.</div>


* <div data-tips="true" data-tips-type="warning">Version 3.x: Doris supports this feature starting from version 3.0.8.</div>


1. Create a catalog.

   
   <Tabs>
   <Tab zoneid="CxHtwaFPWc" title="HMS Catalog">
   <TabTitle>HMS Catalog</TabTitle>
   
   ```SQL
   CREATE CATALOG hive_hms_hdfs_test_catalog PROPERTIES (
       'type' = 'hms',
       'hive.metastore.uris' = 'thrift://127.0.0.1:9083',
       'hadoop.username' = 'doris',
       'fs.defaultFS' = 'hdfs://127.0.0.1:8320'
   );
   ```
   
   
   
   </Tab>
   <Tab zoneid="zhuNrXlMSU" title="LAS Catalog">
   <TabTitle>LAS Catalog</TabTitle>
   
   For details, see [Doris 访问 LAS Catalog](https://docs.byteplus.com/docs/undefined/698008803c928c0509be188b).
   
   
   </Tab>
   </Tabs>
   

2. Switch catalog and view databases

   ```SQL
   switch ${已创建catalog名称};
   show databases;
   use ${数据库名};
   ```
   

3. Query existing Paimon tables

   ```SQL
   show tables;
   select * from ${表名称};
   ```
