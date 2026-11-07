---
title: "Idle transaction cleanup"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Idle_transaction_cleanup"
---

RDS for MySQL provides the ability to automatically clean up long\-idle transactions. This topic describes how to use this feature.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20241215 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20230615 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation

Instances in the RDS for MySQL 8.0.26 version series do not currently support this feature.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Users can use the following parameter to configure the time threshold for clearing idle transactions.


|Parameter name |Type |Need to restart |Description |
|---|---|---|---|
|kill_idle_transaction |integer |No |Controls the timeout for idle transactions in seconds. The default is 0 (disabled). |


<span id=".5L2_55So56S65L6L"></span>
## **Examples**


1. Set `kill_idle_transaction` to 5.

2. Start a transaction and write a record.

   ```cpp
   mysql> begin;
   Query OK, 0 rows affected (0.00 sec)
   
   mysql> insert into t1 values (1,1,1);
   Query OK, 1 row affected (0.00 sec)
   
   mysql> select * from t1;
   +---+---+------+
   | a | b | c    |
   +---+---+------+
   | 1 | 1 |    1 |
   +---+---+------+
   1 row in set (0.00 sec)
   ```
   

3. Wait for more than 5 seconds. When you query again, you will find that the transaction has been rolled back.

   ```cpp
   mysql> select * from t1;
   ERROR 2006 (HY000): MySQL server has gone away
   No connection. Trying to reconnect...
   Connection id:    11
   Current database: test
   
   Empty set (0.01 sec)
   ```
