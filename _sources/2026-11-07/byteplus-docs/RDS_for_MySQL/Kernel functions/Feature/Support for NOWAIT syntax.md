---
title: "Support for NOWAIT syntax"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Support_for_NOWAIT_syntax"
---

This topic describes the NOWAIT syntax provided by RDS for MySQL.

<span id="R43oi3dT"></span>
## Background

DDL supports the "NO_WAIT" and "WAIT N" syntax, which reports an error immediately or after waiting N seconds when an MDL lock on a table cannot be obtained. In production environments, DDL statements often block business operations. For example, if a long\-running transaction prevents a DDL statement from obtaining an MDL lock, subsequent operations are continuously blocked because DDL locks have a higher priority.

Locking read SQL supports the "NOWAIT" and "SKIP LOCKED" syntax. It reports an error immediately or skips the current record if it fails to obtain a lock, which prevents worker threads from being blocked and avoids wasting thread pool resources. When the "SKIP LOCKED" syntax is executed, the skipped rows do not appear in the result set.

For historical reasons, DDL uses the "NO_WAIT" keyword, while locking read uses the "NOWAIT" keyword. This requires special attention.

<span id="nOK8ARhZ"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20250615 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20250615 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="VzWeRc5C"></span>
## Use cases


* Long\-running transactions may exist in production services. If you do not want DDL to block business SQL for a long time, try using the NO_WAIT/WAIT N syntax for DDL.

* In scenarios such as flash sales and rush buying, some rows may have a large number of concurrent modifications or locks, which leads to the blocking of many transaction threads. In this case, you can use the NOWAIT/SKIP LOCKED syntax for locking reads.


<span id="ZgfmUTJK"></span>
## Precautions


* Use the NO_WAIT syntax of DDL with caution. If read transactions continuously access a table on the replica, it will cause persistent playback failures on the replica, which in turn causes primary\-replica latency. Use the WAIT N syntax as much as possible, and evaluate the value of N based on the business traffic.

* The NO_WAIT syntax for DDL is a new, non\-community syntax. Be mindful of whether downstream versions can consume the binlog. The NOWAIT syntax for locking reads is a migration from MySQL 8.0 to MySQL 5.7. Note the binlog type and confirm whether it can be consumed.


<span id="MTAdetyy"></span>
## Instructions


* The format for the DDL NO_WAIT/WAIT N syntax is as follows:


```SQL
ALTER TABLE `table` [NO_WAIT | WAIT [n]] `command`;
DROP TABLE `table` [NO_WAIT | WAIT [n]];
TRUNCATE TABLE `table` [NO_WAIT | WAIT [n]];
OPTIMIZE TABLE `table` [NO_WAIT | WAIT [n]];
RENAME TABLE `table_src` [NO_WAIT | WAIT [n]] TO `table_dst`;
CREATE INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
CREATE FULLTEXT INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
CREATE SPATIAL INDEX `index` ON `table.columns` [NO_WAIT | WAIT [n]];
DROP INDEX `index` ON `table` [NO_WAIT | WAIT [n]];
```



* The format for the locking read NOWAIT/SKIP LOCKED syntax is as follows:


```SQL
SELECT ... [FOR UPDATE [OF table] [NOWAIT | SKIP LOCKED]];
SELECT ... [FOR SHARE [OF table] [NOWAIT | SKIP LOCKED]];
```


<span id="XdeiOfvE"></span>
## Examples

The example for the locking read NOWAIT/SKIP LOCKED syntax is as follows:

```SQL
// session 1
MySQL [t]> begin;
Query OK, 0 rows affected (0.000 sec)

MySQL [t]> select count(1) from t for update;
+----------+
| count(1) |
+----------+
|        6 |
+----------+
1 row in set (0.001 sec)

MySQL [t]>

// session 2
MySQL [t]> select count(1) from t for update nowait;
ERROR 3282 (HY000): Do not wait for lock.
MySQL [t]> select count(1) from t for update skip locked;
+----------+
| count(1) |
+----------+
|        0 |
+----------+
1 row in set (0.001 sec)
```
