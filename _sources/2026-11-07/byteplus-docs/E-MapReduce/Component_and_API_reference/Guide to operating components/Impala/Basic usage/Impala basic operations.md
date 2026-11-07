---
title: "Impala basic operations"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala_basic_operations"
---

This document describes basic operations for Impala, including creating databases, creating tables, writing data, and querying tables.

<span id="_1-前提条件"></span>
## 1 Prerequisites


1. An E\-MapReduce (EMR) cluster with the Impala component service has been created. For details, see [创建集群](https://docs.byteplus.com/docs/undefined/68da347342e561058e056b92).

2. Log in to the cluster's master\-1 node using SSH, which is the node where statestored and catalogd are located. For details, see [Log in to the cluster](https://docs.byteplus.com/docs/E-MapReduce/104404).

3. Currently, the Impala component is available through an allowlist. You can apply for access using [Impala basic operations](https://docs.byteplus.com/docs/E-MapReduce/109298).


<span id="_2-创建数据库"></span>
## 2 Create a database


1. After logging in to the cluster node, you can use the impala\-shell command to access Impala:


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For Impala\-shell command operations, refer to "<a href="https://docs.byteplus.com/docs/E-MapReduce/109294">Impala\-shell tool</a>".</div>


```Plain
root@emr-4nw5w1f78f3xxx-master-1:~# impala-shell 
/opt/emr/2.0.0/impala-3.4.1/shell/impala-shell-3.4.1-RELEASE/ext-py2/bitarray-0.9.0-py2.7-linux-x86_64.egg/bitarray/_bitarray.py:3: UserWarning: Module backports was already imported from None, but /usr/lib/python2.7/dist-packages is being added to sys.path
Starting Impala Shell without Kerberos authentication
Opened TCP connection to emr-4nw5w1f78f3xxx-master-1:21000
Connected to emr-4nw5w1f78f3xxx-master-1:21000
Server version: impalad version 3.4.1-RELEASE RELEASE (build eb1ed66fa435a722fa8c6a7c58ff53edc10c572e)
***********************************************************************************
Welcome to the Impala shell.
(Impala Shell v3.4.1-RELEASE (eb1ed66) built on Fri Sep 16 15:03:38 CST 2022)
 
Want to know what version of Impala you're connected to? Run the VERSION command to
find out!
***********************************************************************************
[emr-4nw5w1f78f3xxx-master-1:21000] default>
```



2. Create a database


```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] default> create database first_db;
Query: create database first_db
+----------------------------+
| summary                    |
+----------------------------+
| Database has been created. |
+----------------------------+
Fetched 1 row(s) in 5.36s
```


<span id="_3-创建表"></span>
## 3 Create a table


1. Select a database


```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] default> use first_db;
Query: use first_db
```



2. Create a table in Parquet format


```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] first_db> CREATE TABLE parquet_table ( id INT) STORED AS PARQUET;
Query: CREATE TABLE parquet_table ( id INT) STORED AS PARQUET
+-------------------------+
| summary                 |
+-------------------------+
| Table has been created. |
+-------------------------+
Fetched 1 row(s) in 5.26s
```


<span id="_4-写入数据"></span>
## 4 Write data

```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] first_db> insert into parquet_table values(1);
Query: insert into parquet_table values(1)
Query submitted at: 2022-10-17 16:52:34 (Coordinator: http://emr-4nw5w1f78f3xxx-core-1:25000)
Query progress can be monitored at: http://emr-4nw5w1f78f3xxx-core-1:25000/query_plan?query_id=8549b1a1cd09d63d:f8d8828f00000000
Modified 1 row(s) in 15.70s
```


<span id="_5-查询数据"></span>
## 5 Query data

```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] first_db> select * from parquet_table;
Query: select * from parquet_table
Query submitted at: 2022-10-17 16:53:10 (Coordinator: http://emr-4nw5w1f78f3xxx-core-1:25000)
Query progress can be monitored at: http://emr-4nw5w1f78f3xxx-core-1:25000/query_plan?query_id=5744559c2307a8b9:a411428400000000
+----+
| id |
+----+
| 1  |
+----+
Fetched 1 row(s) in 0.26s
```


<span id="_6-删除表"></span>
## 6 Delete a table

```Plain
[emr-4nw5w1f78f3xxx-master-1:21000] first_db> drop table parquet_table;
Query: drop table parquet_table
+-------------------------+
| summary                 |
+-------------------------+
| Table has been dropped. |
+-------------------------+
Fetched 1 row(s) in 5.23s
```
