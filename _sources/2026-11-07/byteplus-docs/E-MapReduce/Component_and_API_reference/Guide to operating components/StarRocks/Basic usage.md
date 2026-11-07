---
title: "Basic usage"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/starrocks_basic_usage"
---

This article introduces the basic usage instructions for StarRocks clusters.

<span id="_1-mysql-client连接starrocks集群"></span>
## Connect to StarRocks cluster using MySQL Client

StarRocks is compatible with the MySQL protocol, allowing you to connect directly to the FE using the MySQL Client for relevant SQL operations.

```bash
mysql -h 127.0.0.1 -P9030 -u root -p
```



* For the initial login, you need to log in on the FE node itself by specifying 127.0.0.1, using the root user and an empty string as the password (must be on the FE node itself, no password required). After the initial login, please promptly change the root account password.

* Password strength requirements: at least 10 characters, including numbers, uppercase and lowercase letters, and special symbols. The password must not contain specific internal company keywords or dates, such as: bytedance@2022

* To change the root user password, log in using the method above and use the SET PASSWORD command to modify it. For details, please refer to [the open-source documentation](https://docs.starrocks.io/zh-cn/latest/sql-reference/sql-statements/account-management/SET%20PASSWORD).

* Subsequently, users with permissions can create sub\-users. For detailed user permissions, refer to [the open-source documentation](https://docs.starrocks.io/zh-cn/latest/administration/User_privilege).


<span id="_2-starrocks支持的sql语法说明"></span>
## Supported SQL syntax in StarRocks

EMR StarRocks is fully compatible with the open\-source StarRocks syntax. The following provides an example of basic database and table operations.

This article uses the MySQL Client as an example to execute sample SQL statements.

<span id="_2-1-创建用户"></span>
### Create user

Create a regular user with the following command:

```sql
CREATE USER 'test_user' IDENTIFIED BY 'test_user_passwd';
```


For subsequent logins, you can log in using the following connection command:

```sql
mysql -h 127.0.0.1 -P9030 -u test_user -ptest_user_passwd
```


By default, newly created regular users have no permissions.

<span id="_2-2-创建数据库"></span>
### Create database

Initially, you can create a database using the root user with the following command:

```sql
CREATE DATABASE example_db;
```


After the database is created, you can view database information using `SHOW DATABASES;`.

```sql
MySQL> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| example_db         |
| information_schema |
| _statistics_       |
+--------------------+
2 rows in set (0.00 sec)
```


`information_schema` exists for compatibility with the MySQL protocol. In practice, the information may not be very accurate, so it is recommended to query the specific database directly for detailed information.

<span id="_2-3-账号授权"></span>
### Account authorization

After example_db is created, you can use the root account to grant read and write permissions for example_db to test_user. After authorization, you can log in with the test_user account and operate the example_db database.

```sql
-- Grant all privileges to test_user on example_db
GRANT ALL ON example_db TO test_user;
-- Grant only SELECT privilege to test_user on example_db
GRANT SELECT_PRIV ON example_db TO test_user;
```


<span id="_2-4-建表"></span>
### Create table

From this point onward, log in to StarRocks using the `test_user` account.

Use the CREATE TABLE command to create a table. For detailed parameters, refer to [the official documentation](https://docs.starrocks.io/zh-cn/latest/sql-reference/sql-statements/data-definition/CREATE%20TABLE).

The command to switch databases is as follows:

```sql
USE example_db;
```


StarRocks supports two table creation methods: single partition and composite partition.

The following demonstrates table creation statements for both partition types using the aggregate model as an example.

<span id="_2-4-1-非分区表"></span>
#### Non\-partitioned table

Create a logical table named table1. The bucket column is siteid, with 10 buckets.

The schema of this table is as follows:


* siteid: Type is INT (4 bytes), default value is 10

* citycode: Type is SMALLINT (2 bytes)

* username: Type is VARCHAR, maximum length is 32, default value is an empty string

* pv: Type is BIGINT (8 bytes), default value is 0; this is a metric column. StarRocks performs aggregation operations on metric columns internally. The aggregation method for this column is SUM.


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
DISTRIBUTED BY HASH(siteid) BUCKETS 10;
```


<span id="_2-4-2-分区表"></span>
#### Partitioned table

Create a logical table named table2.

The schema of this table is as follows:


* event_day: Type is DATE, no default value

* siteid: Type is INT (4 bytes), default value is 10

* citycode: Type is SMALLINT (2 bytes)

* username: Type is VARCHAR, maximum length is 32, default value is an empty string

* pv: Type is BIGINT (8 bytes), default value is 0; this is a metric column. StarRocks performs aggregation operations on metric columns internally. The aggregation method for this column is SUM.


We use the event_day column as the partition column and create three partitions: p201706, p201707, and p201708.


* p201706: Range is [minimum value, 2017\-07\-01)

* p201707: Range is [2017\-07\-01, 2017\-08\-01)

* p201708: Range is [2017\-08\-01, 2017\-09\-01)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Important: The interval is left\-closed and right\-open.</div>


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


After the table is created, you can view the information of the table in example_db:

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


<span id="_2-5-插入数据"></span>
### Insert data

<span id="_2-5-1-insert-into-插入"></span>
#### Insert Into

For more detailed syntax and best practices for using Insert, refer to the [Insert](https://docs.starrocks.io/zh-cn/latest/loading/InsertInto) manual.

The usage of the Insert Into statement is similar to that in databases such as MySQL. However, in StarRocks, all data writes are independent import jobs. Therefore, Insert Into is also introduced here as an import method.

The main Insert Into commands include the following two types:


* INSERT INTO tbl SELECT ...

* INSERT INTO tbl (col1, col2, ...) VALUES (1, 2, ...), (1,3, ...);


The Insert Into command must be submitted via the MySQL protocol. Creating an import request synchronously returns the import result.

Syntax:

```sql
INSERT INTO table_name [partition_info] [WITH LABEL label] [col_list] [query_stmt] [VALUES];
```


`label` is a user\-specified label or an automatically generated label. Label is the identifier for the Insert Into import job. Each import job has a label that is unique within a single database.

Example:

```sql
INSERT INTO tbl2 WITH LABEL label1 SELECT * FROM tbl3;
INSERT INTO tbl1 VALUES ("qweasdzxcqweasdzxc"),("a");
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When <code>CTE(Common Table Expressions)</code> is used as the query part in an insert operation, the <code>WITH LABEL</code> and <code>column list</code> sections must be specified.</div>


Example:

```sql
INSERT INTO tbl1 WITH LABEL label1
WITH cte1 AS (SELECT * FROM tbl1), cte2 AS (SELECT * FROM tbl2)
SELECT k1 FROM cte1 JOIN cte2 WHERE cte1.k1 = 1;

INSERT INTO tbl1 (k1)
WITH cte1 AS (SELECT * FROM tbl1), cte2 AS (SELECT * FROM tbl2)
SELECT k1 FROM cte1 JOIN cte2 WHERE cte1.k1 = 1;
```


Insert Into itself is an SQL command. Its return result varies depending on the execution outcome and is categorized as follows:


* If the return result is `ERROR 1064 (HY000)`, it indicates the import failed.

* If the return result is `Query OK`, it indicates successful execution.

   * If `rows affected` is 0, it means the result set is empty and no data has been imported.

   * If `rows affected` is greater than 0:

      * If `status` is `committed`, it means the data is not yet visible. The status must be checked using the `show transaction` statement until it becomes `visible`.

      * If `status` is `visible`, it means the data import was successful.

   * If `warnings` is greater than 0, it means some data was filtered. You can use the `show load` statement to obtain the URL and view the filtered rows.


<span id="_2-5-2-批量导入"></span>
#### Batch import

StarRocks supports multiple data import methods. For details, refer to the data import documentation. Here, we use Stream\-Load and Broker\-Load imports as examples.


* **Stream\-Load**


For more detailed syntax and best practices for using Stream\-Load, refer to the [Stream-Load](https://docs.starrocks.io/zh-cn/latest/loading/StreamLoad) manual.

Stream\-Load transfers data to StarRocks via the HTTP protocol, allowing direct import of local data without relying on other systems or components. For detailed syntax help, refer to `HELP STREAM LOAD;`.

Example 1: Use "table1_20170707" as the Label and import the local file table1_data into the table1 table.

```shell
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


Example 2: Use "table2_20170707" as the Label and import the local file table2_data into the table2 table.

```shell
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



1. <div data-tips="true" data-tips-type="warning">It is recommended to limit the file size for streaming import to within 10GB. Excessively large files will increase the cost of failure retries.</div>


2. <div data-tips="true" data-tips-type="warning">Each batch of imported data requires a Label. Ideally, the Label should be a string related to the batch of data, making it easier to read and manage. StarRocks uses the Label to ensure that, within a Database, each batch of data can only be imported successfully once. The Label of a failed task can be reused.</div>


3. <div data-tips="true" data-tips-type="warning">Streaming import is a synchronous command. If the command returns success, it means the data has been imported. If it returns failure, it means this batch of data has not been imported.</div>


* **Broker\-Load**


Broker import reads data from external storage and imports it through the deployed Broker process.

For more detailed syntax and best practices for using Broker Load, refer to the [Broker Load](https://docs.starrocks.io/zh-cn/latest/loading/BrokerLoad) manual. You can also enter `HELP BROKER LOAD` in the MySQL client command line for additional help information.

Example: Use "table1_20170708" as the Label to import files from HDFS into the table1 table.

```sql
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


Broker import is an asynchronous command. Successful execution of the above command only indicates that the task was submitted successfully. Whether the import was successful must be checked using `SHOW LOAD;`. For example:

```sql
SHOW LOAD WHERE LABEL = "table1_20170708";
```


In the returned result, if the `State` field is FINISHED, it means the import was successful.

For more information about `SHOW LOAD`, refer to `HELP SHOW LOAD;`

Asynchronous import tasks can be canceled before completion:

```sql
CANCEL LOAD WHERE LABEL = "table1_20170708";
```


<span id="_2-6-查询数据"></span>
### Query data

<span id="_2-6-1-简单查询"></span>
#### Simple query

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


<span id="_2-6-2-join-查询"></span>
#### Join query

```sql
MySQL> SELECT SUM(table1.pv) FROM table1 JOIN table2 WHERE table1.siteid = table2.siteid;
+--------------------+
| sum(`table1`.`pv`) |
+--------------------+
|                 12 |
+--------------------+
1 row in set (0.20 sec)
```


<span id="_2-6-3-子查询"></span>
#### **Subquery**

```sql
MySQL> SELECT SUM(pv) FROM table2 WHERE siteid IN (SELECT siteid FROM table1 WHERE siteid > 2);
+-----------+
| sum(`pv`) |
+-----------+
|         8 |
+-----------+
1 row in set (0.13 sec)
```
