---
title: "Analyzing the primary-replica lag issue of RDS for MySQL instances through full SQL insight"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Analyzing_the_primary-replica_lag_issue_of_RDS_for_MySQL_instances_through_full_SQL_insight"
---

When an RDS for MySQL instance encounters primary\-replica lag, you can refer to this topic to troubleshoot the database instance issues.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In RDS for MySQL, primary\-replica lag refers to the data synchronization delay between the primary database and the replica database. This lag causes the data on the replica to fall behind the data on the primary.

<span id=".6Zeu6aKY5o6S5p-l"></span>
## Problem troubleshooting

Data delay may be caused by factors such as excessively high DML QPS, DML operation tables lacking primary keys or unique keys, DDL operations, large transactions, or lock blocking. You can follow the operational guidelines below to troubleshoot and analyze the specific causes of the data delay.

<span id=".5Y-v6IO95Y6f5Zug5LiA77yaZG1sLXFwcy3ov4fpq5g="></span>
### Possible reason 1: excessively high DML QPS

Excessively high DML QPS can degrade database performance or even cause crashes, leading to data delays. To determine if your instance's DML QPS is excessively high, analyze and compare metrics in full SQL insight like DML execution times, average DML execution time, maximum DML execution time and rows affected over different timeframes. You can perform the following steps to check if excessively high DML QPS is causing the primary\-replica lag.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-left corner of the **Operation observability** page, click the drop\-down icon and select the target instance.

5. On the target instance page, click **Full** **SQL insight**.

6. On the **Full** **SQL insight** page, click **Write analysis**.

7. On the **Write analysis** tab, select query time, database and table. The maximum query time span can not exceed 24 hours.

   Check if metrics such as DML execution times, average DML execution time, and rows affected show an increasing trend over different time periods. If a rising trend is observed, you can use the Time comparison feature on the **Full** **SQL** **insight** tab to compare metric trends across periods and determine if the instance's DML QPS is too high.


<span id=".5Y-v6IO95Y6f5Zug5LqM77yaZG1sLeaTjeS9nOihqOe8uuWwkeS4u-mUruaIluWUr-S4gOmUrg=="></span>
### Possible reason 2: DML operation tables lack primary keys or unique keys

During DML operations, the absence of a primary key or unique key can lead to issues such as degraded database performance, compromised data integrity, and the inability to uniquely identify rows. These issues can subsequently contribute to primary\-replica lag. You can use the following method to determine if primary\-replica lag is caused by DML operations on tables that lack a primary key or unique key.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-left corner of the **Operation observability** page, click the drop\-down icon and select the target instance.

5. On the target instance page, click **Full** **SQL** **insight**.

6. On the **Full** **SQL** **insight** tab, locate the **SQL template lists** pane, and check whether the table corresponding to the DML statement with a long SQL execution time has a primary key or a unique key.


<span id=".5Y-v6IO95Y6f5Zug5LiJ77yaZGRsLeaTjeS9nA=="></span>
### Possible reason 3: DDL operations

DDL operations usually take a long time to execute, especially when the data volume of the table is huge. A DDL operation typically requires a similar time to apply on a read\-only node or replica as on the primary. When a DDL is executed on a large table, this leads to a notable, synchronized increase in replication time across all replicas and read\-only nodes, resulting in primary\-replica lag. You can perform the following steps to check if DDL operations are causing primary\-replica lag.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-left corner of the **Operation observability** page, click the drop\-down icon and select the target instance.

5. On the target instance page, click **Full** **SQL insight**.

6. On the **Write analysis** tab, **view** Maximum DDL **execution time**.


<span id=".5Y-v6IO95Y6f5Zug5Zub77ya5aSn5LqL5Yqh"></span>
### Possible reason 4: large transactions

In a database, a large transaction is typically defined as one that contains a massive number of data operations, such as thousands or even tens of thousands of` INSERT`, `UPDATE`, or `DELETE`, or a single SQL statement that affects a vast number of rows. Large transactions consume significant system resources and have long execution times, which can degrade database performance and concurrency.

When a large transaction executes on the primary instance, it generates a substantial volume of Binlog. Consequently, replicas or read\-only nodes require more time to fetch this Binlog and at least the same duration as the primary to apply the updates, ultimately leading to primary\-replica lag. You can perform the following steps to check if large transactions are causing the primary\-replica lag.


* Method 1: Check for large transactions causing primary\-replica lag using DBW's full SQL insight

   * Log on to the [DBW console](https://console.byteplus.com/dbw).

   * On the top menu bar, switch the region.

   * On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

   * In the upper\-left corner of the **Operation observability** page, click the drop\-down icon and select the target instance.

   * On the target instance page, click **Full** **SQL** **insight**.

   * On the **Full** **SQL** **insight** tab, locate the SQL template lists pane, view the **Average TRXCommitTime** (i.e., total transaction submit time) and **SQL time** of the SQL statement.

* Method 2: Check for large transactions causing primary\-replica lag by executing SQL commands

   Execute the following command to view whether there are long\-running transactions on the instance:

   ```sql
   SELECT 
       t.*, 
       TO_SECONDS(NOW()) - TO_SECONDS(t.trx_started) AS idle_time 
   FROM 
       INFORMATION_SCHEMA.INNODB_TRX t;
   ```
   


<span id=".5Y-v6IO95Y6f5Zug5LqU77ya6ZSB6Zi75aGe"></span>
### Possible reason 5: lock blocking

Lock blocking contributes to primary\-replica lag by delaying transaction commits on the primary, affecting Binlog generation and write, and causing lock competition during Binlog processing on the replica. You can use the following method to check if lock locking is causing primary\-replica lag.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, switch the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. In the upper\-left corner of the **Operation observability** page, click the drop\-down icon and select the target instance.

5. On the target instance page, click **Full** **SQL insight**.

6. On the **Write analysis** tab, view metrics including ** Average innodb row lock wait time for DML**, **Average MDL lock wait time for DML**, **Maximum DML execution time**, **Average innodb row lock wait time for DDL**, and **Average MDL lock wait time for DDL** to determine if lock locking is causing primary\-replica lag.


At the same time, you can also execute the following command on the instance to view whether the current database has MDL locks that cause lock blocking:

```sql
select * from  information_schema.metadata_lock_info;
```
