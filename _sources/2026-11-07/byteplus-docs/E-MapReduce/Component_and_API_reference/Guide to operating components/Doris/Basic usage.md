---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/doris_basic_usage"
---

This article provides an introduction to the basic usage of a semi\-managed EMR Doris cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For guidance on using Doris clusters in EMR Serverless instances, see: <a href="https://www.volcengine.com/docs/6491/1946703">EMR Serverless instance\-Doris best practices</a>. It is more recommended to use EMR Serverless instances, which are maintenance\-free and worry\-free.</div>


<span id="_1-前提条件"></span>
## **1. Prerequisites**


* An E\-MapReduce (EMR) cluster has been created and the **Doris** service has been installed. For details, see: [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).


<span id="_2-mysql-client连接doris集群"></span>
## 2. Connect to Doris cluster with MySQL Client

Doris is compatible with the MySQL protocol. You can use MySQL Client to directly connect to FE for relevant SQL operations.


1. In the **Cluster Management \> Cluster List \> Specific Cluster Name** page, go to the cluster details.

2. In the navigation bar, click **Service List**, then click the **Doris** service to enter.

3. Click the ECS ID of the EMR cluster node (host name emr\-master\-1) to jump to the cloud server instance page. Click the **Remote Connection** button in the upper right corner, enter the root password set during cluster creation, and access the remote terminal.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The domain naming conventions for nodes may differ across EMR versions, so the above "emr\-master\-1 host name" can be adjusted according to EMR's <a href="https://docs.byteplus.com/docs/E-MapReduce/104402">Domain name rules</a> as appropriate.   </div>
   

4. The MySQL client is already installed on the master node machine. You can connect to the Doris cluster using the following command:


```Plain
mysql -h 127.0.0.1 -P9030 -u root -p
```



5. For the initial login, you can log in with the root user and an empty password. After the initial login, please promptly change the root account password. You can change the root account password using the following command:


```Plain
SET PASSWORD FOR 'root' = PASSWORD('my_root_password');
```


Subsequently, authorized users can create sub\-users. For detailed user permissions, refer to the [open-source documentation](https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Account-Management-Statements/CREATE-USER).

<span id="_3-doris-支持的-sql-语法说明"></span>
## 3. Doris\-supported SQL syntax

EMR Doris is fully compatible with open\-source Doris syntax. The following provides an example of basic database and table operations. For other detailed guides, refer to [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109207).

The following uses MySQL Client as an example to execute sample SQL statements.

<span id="_3-1-创建用户"></span>
### **3.1 Create a user**

Create a regular user with the following command:

```Plain
CREATE USER 'test_user' IDENTIFIED BY 'test_user_passwd';
```


For subsequent logins, you can log in using the following connection command:

```Plain
mysql -h 127.0.0.1 -P9030 -u test_user -ptest_user_passwd
```


By default, newly created regular users have no permissions.

<span id="_3-2-创建数据库"></span>
### **3.2 Create a database**

Initially, you can create a database using the root user with the following command:

```Plain
CREATE DATABASE test_db;
```


After the database is created, you can view database information using `SHOW DATABASES;`.

```Plain
MySQL> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| example_db         |
| information_schema |
+--------------------+
3 rows in set (0.00 sec)
```


`information_schema` exists for MySQL protocol compatibility. The information may not be very accurate in practice, so for specific database information, it is recommended to query the corresponding database directly.

<span id="_3-3-账号授权"></span>
### **3.3 Account authorization**

After example_db is created, you can use the root account to grant read and write permissions for example_db to the previously created user: test_user. After authorization, you can log in and operate the example_db database using the test_user account.

```Plain
-- 授权test_user在example_db的全部权限
GRANT ALL ON example_db TO test_user;
-- 只授权test_user在example_db的SELECT在\权限
GRANT SELECT_PRIV ON example_db TO test_user;
```


<span id="_3-4-建表"></span>
### **3.4 Create tables**

From here onward, you can switch the user to the `test_user` account to log in to Doris.

Use the CREATE TABLE command to create a table. For more detailed parameters, visit the [official documentation](https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Data-Definition-Statements/Create/CREATE-TABLE) for further information.

The command to switch databases is as follows:

```Plain
USE example_db;
```


Doris supports two table creation methods: single partition and composite partition.

The following examples use the aggregate model to demonstrate table creation statements for both partition types.

<span id="_3-4-1-非分区表"></span>
#### **3.4.1 Non\-partitioned table**

Create a logical table named table1. The bucket column is siteid, and the number of buckets is 10.

The schema for this table is as follows:


|Field name |Note |
|---|---|
|siteid |Type: INT (4 bytes), default value: 10. |
|citycode |Type: SMALLINT (2 bytes). |
|username |Type: VARCHAR, maximum length: 32, default value: empty string. |
|pv |Type: BIGINT (8 bytes), default value: 0;<br><br>This is a metric column. Doris will aggregate metric columns internally, and the aggregation method for this column is SUM. |


The table creation statement is as follows:

```sql
CREATE TABLE table1
(
    siteid INT DEFAULT '10',
    citycode SMALLINT,
    username VARCHAR(32) DEFAULT '',
    pv BIGINT SUM DEFAULT '0'
)
AGGREGATE KEY(siteid, citycode, username)
DISTRIBUTED BY HASH(siteid) BUCKETS 10
```


<span id="_3-4-2-分区表"></span>
#### **3.4.2 Partitioned table**

Create a logical table named table2.

The schema for this table is as follows:


|Field name |Note |
|---|---|
|event_day |Type: DATE, no default value. |
|siteid |Type: INT (4 bytes), default value: 10. |
|citycode |Type: SMALLINT (2 bytes). |
|username |Type: VARCHAR, maximum length: 32, default value: empty string. |
|pv |Type: BIGINT (8 bytes), default value: 0.<br><br>This is a metric column. Doris will aggregate metric columns internally, and the aggregation method for this column is SUM. |


Additionally, use the event_day column as the partition column to create three partitions: p201706, p201707, p201708:

Important: The interval is left\-closed and right\-open.


* p201706: Range is [minimum value, 2017\-07\-01)

* p201707: Range is [2017\-07\-01, 2017\-08\-01)

* p201708: Range is [2017\-08\-01, 2017\-09\-01)


Each partition uses siteid for hash bucketing, with 10 buckets.

The table creation statement is as follows:

```sql
CREATE TABLE table2
(
    event_day DATE,
    siteid INT DEFAULT '10',
    citycode SMALLINT,
    username VARCHAR(32) DEFAULT '',
    pv BIGINT SUM DEFAULT '0'
)
AGGREGATE KEY(event_day, siteid, citycode, username)
PARTITION BY RANGE(event_day)
(
    PARTITION p201706 VALUES LESS THAN ('2017-07-01'),
    PARTITION p201707 VALUES LESS THAN ('2017-08-01'),
    PARTITION p201708 VALUES LESS THAN ('2017-09-01')
)
DISTRIBUTED BY HASH(siteid) BUCKETS 10
PROPERTIES("replication_num" = "1");
```


After the table is created, you can view information about the tables in example_db:

```sql
MySQL> SHOW TABLES;
+----------------------+
| Tables_in_example_db |
+----------------------+
| table1               |
| table2               |
+----------------------+
2 rows in set (0.01 sec)

MySQL> DESC table1;
+----------+-------------+------+-------+---------+-------+
| Field    | Type        | Null | Key   | Default | Extra |
+----------+-------------+------+-------+---------+-------+
| siteid   | int(11)     | Yes  | true  | 10      |       |
| citycode | smallint(6) | Yes  | true  | N/A     |       |
| username | varchar(32) | Yes  | true  |         |       |
| pv       | bigint(20)  | Yes  | false | 0       | SUM   |
+----------+-------------+------+-------+---------+-------+
4 rows in set (0.00 sec)

MySQL> DESC table2;
+-----------+-------------+------+-------+---------+-------+
| Field     | Type        | Null | Key   | Default | Extra |
+-----------+-------------+------+-------+---------+-------+
| event_day | date        | Yes  | true  | N/A     |       |
| siteid    | int(11)     | Yes  | true  | 10      |       |
| citycode  | smallint(6) | Yes  | true  | N/A     |       |
| username  | varchar(32) | Yes  | true  |         |       |
| pv        | bigint(20)  | Yes  | false | 0       | SUM   |
+-----------+-------------+------+-------+---------+-------+
5 rows in set (0.00 sec)
```


<span id="_3-4-3-注意事项"></span>
#### **3.4.3 Important notes**


1. The tables above are all single\-replica tables created by setting replication_num. Doris recommends using the default three\-replica setting to ensure high availability.

2. You can dynamically add or remove partitions in composite partition tables. For details, see the partition section in [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109207).

3. Data import can be performed for a specified partition. For details, see [Basic usage](https://docs.byteplus.com/docs/E-MapReduce/109207).

4. The table schema can be modified dynamically.

5. You can add rollup tables to a table to improve query performance. For details, refer to the advanced usage guide description of [Rollup](https://doris.apache.org/zh-CN/docs/1.2/data-table/hit-the-rollup).

6. The null property of table columns is true by default, which may have some impact on query performance.


<span id="_3-5-插入数据"></span>
### **3.5 Insert data**

<span id="_3-5-1-insert-into-插入"></span>
#### 3.5.1 Insert Into insertion

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more detailed syntax and best practices regarding Insert usage, refer to the <a href="https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Data-Manipulation-Statements/Manipulation/INSERT">Insert</a> command manual.</div>


The usage of the Insert Into statement is similar to that in MySQL and other databases. However, in Doris, all data writes are independent import jobs. Therefore, Insert Into is also introduced here as an import method.

The main Insert Into commands include the following two types:


* INSERT INTO tbl SELECT ...

* INSERT INTO tbl (col1, col2, ...) VALUES (1, 2, ...), (1,3, ...);


The Insert Into command must be submitted via the MySQL protocol. Creating an import request will synchronously return the import result.

Syntax reference:

```sql
INSERT INTO table_name [partition_info] [WITH LABEL label] [col_list] [query_stmt] [VALUES];
```


`label` is a user\-specified label or an automatically generated label. The label is the identifier for the Insert Into import job. Each import job has a Label that is unique within a single database.

Example:

```sql
INSERT INTO tbl2 WITH LABEL label1 SELECT * FROM tbl3;
INSERT INTO tbl1 VALUES ("qweasdzxcqweasdzxc"),("a");
```


**Important:** 

When it is necessary to use `CTE(Common Table Expressions)` as the query part of an insert operation, you must specify the `WITH LABEL` and `column list` sections. Example

```sql
INSERT INTO tbl1 WITH LABEL label1
WITH cte1 AS (SELECT * FROM tbl1), cte2 AS (SELECT * FROM tbl2)
SELECT k1 FROM cte1 JOIN cte2 WHERE cte1.k1 = 1;


INSERT INTO tbl1 (k1)
WITH cte1 AS (SELECT * FROM tbl1), cte2 AS (SELECT * FROM tbl2)
SELECT k1 FROM cte1 JOIN cte2 WHERE cte1.k1 = 1;
```


Insert Into is itself an SQL command. Its return result varies depending on the execution outcome, as follows:


* If the return result is `ERROR 1064 (HY000)`, it indicates the import failed.

* If the return result is `Query OK`, it indicates successful execution.

   * If `rows affected` is 0, it means the result set is empty and no data was imported.

   * If `rows affected` is greater than 0:

      * If `status` is `committed`, the data is not yet visible. You need to check the status using the `show transaction` statement until it becomes `visible`.

      * If `status` is `visible`, it means the data import was successful.

   * If `warnings` is greater than 0, it means some data was filtered. You can use the `show load` statement to obtain the URL and view the filtered rows.


For more detailed information, please refer to the [Insert](https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Data-Manipulation-Statements/Manipulation/INSERT) command manual.

<span id="_3-5-2-批量导入"></span>
#### 3.5.2 Batch import

Doris supports multiple data import methods. Here, we use Stream\-Load and Broker\-Load imports as examples.

**1. Stream\-Load**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more detailed syntax and best practices regarding Stream\-Load usage, refer to the <a href="https://doris.apache.org/zh-CN/docs/1.2/sql-manual/sql-reference/Data-Manipulation-Statements/Load/STREAM-LOAD">Stream\-Load</a> command manual.</div>


Stream\-Load imports data into Doris via the HTTP protocol, allowing direct import of local data without relying on other systems or components. For detailed syntax help, refer to: [HELP STREAM LOAD](https://doris.apache.org/zh-CN/docs/1.2/data-operate/import/import-way/stream-load-manual?_highlight=stre).

**Example 1:** 

Using "table1_20170707" as the Label, import the local file table1_data into the table1 table.

```plain
curl --location-trusted -u test:test_passwd -H "label:table1_20170707" -H "column_separator:," -T table1_data http://FE_HOST:8030/api/example_db/table1/_stream_load
```


The local file `table1_data` uses `,` as the delimiter between data entries. The specific content is as follows:

```plain
1,1,jim,2
2,1,grace,2
3,2,tom,2
4,3,bush,3
5,3,helen,3
```


**Example 2:** 

Using "table2_20170707" as the Label, import the local file table2_data into the table2 table.

```plain
curl --location-trusted -u test:test -H "label:table2_20170707" -H "column_separator:|" -T table2_data http://127.0.0.1:8030/api/example_db/table2/_stream_load
```


The local file `table2_data` uses `|` as the delimiter between data entries. The specific content is as follows:

```plain
2017-07-03|1|1|jim|2
2017-07-05|2|1|grace|2
2017-07-12|3|2|tom|2
2017-07-15|4|3|bush|3
2017-07-12|5|3|helen|3
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">When using stream loading, it is recommended to limit file size to within 10 GB. Excessively large files will increase the cost of failure retries.</div>


2. <div data-tips="true" data-tips-type="warning">Each batch of imported data requires a Label. The Label should preferably be a string related to the batch of data for easier reading and management. Doris uses the Label to ensure that within a Database, each batch of data can only be imported successfully once. Labels for failed tasks can be reused.</div>


3. <div data-tips="true" data-tips-type="warning">Stream loading is a synchronous command. If the command returns success, the data has been imported; if it returns failure, the batch of data has not been imported.</div>



**2. Broker\-Load**

Broker import reads data from external storage for import by deploying the Broker process.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For more detailed syntax and best practices regarding Broker Load usage, refer to the <a href="https://doris.apache.org/zh-CN/docs/1.2/data-operate/import/import-way/broker-load-manual">Broker Load</a> command manual. You can also enter <code>HELP BROKER LOAD</code> in the MySql client command line for more help information.</div>


**Example:** 

Using "table1_20170708" as the Label, import files from HDFS into the table1 table.

```plain
LOAD LABEL table1_20170708
(
    DATA INFILE("hdfs://your.namenode.host:port/dir/table1_data")
    INTO TABLE table1
)
WITH BROKER hdfs 
(
    "username"="hdfs_user",
    "password"="hdfs_password"
);
```


Broker import is an asynchronous command. Successful execution of the above command only indicates that the task was submitted successfully. To determine whether the import was successful, check using `SHOW LOAD;`. For example:

```plain
SHOW LOAD WHERE LABEL = "table1_20170708";
```


If the `State` field in the return result is FINISHED, it indicates the import was successful.

For more information about `SHOW LOAD`, refer to `HELP SHOW LOAD;`

Asynchronous import tasks can be canceled before completion:

```plain
CANCEL LOAD WHERE LABEL = "table1_20170708";
```


For more detailed information, see [community documentation](https://doris.apache.org/zh-CN/docs/1.2/data-operate/import/import-way/broker-load-manual)

<span id="_3-6-查询数据"></span>
### **3.6 Query data**

<span id="_3-6-1-简单查询"></span>
#### **3.6.1 Simple query**

```sql
MySQL> SELECT * FROM table1 LIMIT 3;
+--------+----------+----------+------+
| siteid | citycode | username | pv   |
+--------+----------+----------+------+
|      2 |        1 | 'grace'  |    2 |
|      5 |        3 | 'helen'  |    3 |
|      3 |        2 | 'tom'    |    2 |
+--------+----------+----------+------+
3 rows in set (0.01 sec)
MySQL> SELECT * FROM table1 ORDER BY citycode;
+--------+----------+----------+------+
| siteid | citycode | username | pv   |
+--------+----------+----------+------+
|      2 |        1 | 'grace'  |    2 |
|      1 |        1 | 'jim'    |    2 |
|      3 |        2 | 'tom'    |    2 |
|      4 |        3 | 'bush'   |    3 |
|      5 |        3 | 'helen'  |    3 |
+--------+----------+----------+------+
5 rows in set (0.01 sec)
```


<span id="_3-6-2-join-查询"></span>
#### **3.6.2 Join query**

```sql
MySQL> SELECT SUM(table1.pv) FROM table1 JOIN table2 WHERE table1.siteid = table2.siteid;
+--------------------+
| sum(`table1`.`pv`) |
+--------------------+
|                 12 |
+--------------------+
1 row in set (0.20 sec)
```


<span id="_3-6-3-子查询"></span>
#### **3.6.3 Subquery**

```sql
MySQL> SELECT SUM(pv) FROM table2 WHERE siteid IN (SELECT siteid FROM table1 WHERE siteid > 2);
+-----------+
| sum(`pv`) |
+-----------+
|         8 |
+-----------+
1 row in set (0.13 sec)
```
