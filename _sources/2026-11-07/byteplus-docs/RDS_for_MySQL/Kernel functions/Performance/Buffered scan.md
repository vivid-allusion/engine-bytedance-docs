---
title: "Buffered scan"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Buffered_scan"
---

This topic describes the buffered scan feature of RDS for MySQL.

<span id="67w6RDA1"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20251215 and above.

* MySQL 8.0 with a kernel version of MySQL 8.0.43_20251215 or later.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="Rh8Uuets"></span>
## Background

MySQL Community Edition performs well on typical transactional workloads, such as point queries and small\-range queries, but its performance on analytical workloads, such as large\-range queries and full table scans, can be improved.

In scenarios with large\-range queries and full table scans, the storage engine scans a large number of records and processes them individually. Consequently, the processing logic for each record is executed multiple times. Analysis of performance hotspots indicates that the process InnoDB uses to handle each record contains substantial redundant logic. This logic is executed for each record, severely degrading query performance.

<span id="oepdVYSX"></span>
## Feature description

RDS for MySQL has optimized its scanning method, which is called buffered scan. When using buffered scan, the storage engine scans multiple records at once, stores them in a buffer, and then processes them together. The optimized scanning method eliminates the redundant logic that was executed for each record, significantly improving performance for large\-range queries and full table scans.

<span id="Gk3fHrVd"></span>
## Instructions

<span id="bHKKVohI"></span>
### Parameter description

RDS for MySQL provides the following modifiable parameters to configure the buffered scan feature.


|**Parameter name** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|
|loose_buffered_scan |OFF |No<br><br> |[ON\|OFF] |GLOBAL/SESSION |Enables or disables the buffered scan method. Values:<br><br><br>* `ON`: enable.<br><br>* `OFF`: disable. |
|loose_buffered_scan_threshold |1000 |No |[0, 18446744073709551615] |GLOBAL/SESSION |The lower limit on the number of scanned rows that triggers a buffered scan. A buffered scan is performed when the optimizer's estimated number of scanned rows exceeds the value of this parameter. |


<span id="3H4LMJFI"></span>
### Examples

The following code example shows the procedure for using the buffered scan method.

```Plain Text
mysql> -- 在当前 session 中允许使用 buffered scan 扫描方式
mysql> SET SESSION loose_buffered_scan = ON;
Query OK, 0 rows affected (0.00 sec)

mysql> -- 在当前 session 中调整 buffered scan 扫描方式的生效阈值
mysql> SET SESSION loose_buffered_scan_threshold = 10;
Query OK, 0 rows affected (0.00 sec)

mysql> 
mysql> -- 创建测试表
mysql> CREATE TABLE t(id BIGINT PRIMARY KEY AUTO_INCREMENT, a INT);
Query OK, 0 rows affected (0.02 sec)

mysql> -- 导入测试数据
mysql> INSERT INTO t(a) VALUES(0);
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO t(a) SELECT a + (SELECT COUNT(*) FROM t) FROM t;
Query OK, 1 row affected (0.01 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> INSERT INTO t(a) SELECT a + (SELECT COUNT(*) FROM t) FROM t;
Query OK, 2 rows affected (0.00 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> INSERT INTO t(a) SELECT a + (SELECT COUNT(*) FROM t) FROM t;
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> INSERT INTO t(a) SELECT a + (SELECT COUNT(*) FROM t) FROM t;
Query OK, 8 rows affected (0.01 sec)
Records: 8  Duplicates: 0  Warnings: 0

mysql> 
mysql> -- 使用 EXPLAIN 语句查看执行计划，Extra 列出现 Using buffered scan 说明使用了 buffered scan 扫描方式
mysql> EXPLAIN FORMAT=TRADITIONAL SELECT COUNT(a) FROM t;
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+---------------------+
| id | select_type | table | partitions | type | possible_keys | key  | key_len | ref  | rows | filtered | Extra               |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+---------------------+
|  1 | SIMPLE      | t     | NULL       | ALL  | NULL          | NULL | NULL    | NULL |   16 |   100.00 | Using buffered scan |
+----+-------------+-------+------------+------+---------------+------+---------+------+------+----------+---------------------+
1 row in set, 1 warning (0.01 sec)

mysql> -- 使用 buffered scan 扫描方式执行全表扫描
mysql> SELECT COUNT(a) FROM t;
+----------+
| COUNT(a) |
+----------+
|       16 |
+----------+
1 row in set (0.00 sec)
```


<span id="EqDx5pDW"></span>
### Precautions


* The buffered scan method supports only the InnoDB storage engine.

* The buffered scan method does not support partitioned tables.

* The buffered scan method does not support tables that contain BLOB, TEXT, or JSON fields.

* The buffered scan method does not support point lookups on primary or unique indexes. These queries return a maximum of one row and do not require optimization with a buffered scan.


<span id="fsZjp5Wh"></span>
## Performance data

<span id="xq7AGMOP"></span>
### Test Environment


* Instance specification: RDS for MySQL, general\-purpose, 8C32G

* Instance version: MySQL 8.0


<span id="K6WgVZm6"></span>
### Test steps


1. Create the lineitem table in TPC\-H and import approximately 60,000,000 rows of data.

2. Scan the lineitem table with buffered scan enabled and disabled, respectively:


```SQL
mysql> -- Close the buffered scan method in the current session.
mysql> SET SESSION loose_buffered_scan = OFF;
Query OK, 0 rows affected (0.00 sec)

mysql> 
mysql> -- Scan the lineitem table.
mysql> SELECT SUM(l_quantity) FROM lineitem;
+-----------------+
| SUM(l_quantity) |
+-----------------+
|   1529738036.00 |
+-----------------+
1 row in set (17.87 sec)

mysql> -- Enable the buffered scan mode in the current session
mysql> SET SESSION loose_buffered_scan = ON;
Query OK, 0 rows affected (0.00 sec)

mysql> 
mysql> -- Scan the lineitem table.
mysql> SELECT SUM(l_quantity) FROM lineitem;
+-----------------+
| SUM(l_quantity) |
+-----------------+
|   1529738036.00 |
+-----------------+
1 row in set (15.36 sec)
```


<span id="QKEuUo5s"></span>
### The test results are as follows.

Scanning the lineitem table takes 17.87 seconds with buffered scan disabled, and 15.36 seconds with it enabled. Using the buffered scan method improves performance by about 16.34%.
