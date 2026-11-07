---
title: "Test methods"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_methods"
---

This topic describes the test scenarios and methods used to stress test RDS for MySQL.

<span id="4dX3scoP"></span>
## Test scenario

This test includes the following two scenarios:


* In\-memory: Suitable for small data volumes. All data can be loaded into the Buffer Pool, and data access primarily hits the memory cache.

* I/O\-bound: Suitable for large data volumes. Only frequently accessed data is loaded into the Buffer Pool for read and write operations. Disk read/write and Buffer Pool updates occur during pressure testing.


<span id="0jggHbEf"></span>
## Test steps


* Replace the following parameters with the actual values of your MySQL instance:

   * mysql\-db: database.

   * mysql\-host: connection address.

   * mysql\-port: database port.

   * mysql\-user: database account.

   * mysql\-password: database account password.

* Replace the following parameters with actual values based on the test scenario:

   * table_size: the number of rows in the test table.

   * tables: the number of test tables.

   * time: test time.

   * threads: the number of concurrent threads.

1. Importing data

   ```Plain Text
   nohup sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --time=XXX  --threads=XXX oltp_read_write prepare
   ```
   

2. Run test

   ```Plain Text
   nohup sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --time=XXX  --threads=XXX oltp_read_write run
   ```
   

3. Clear data

   ```Plain Text
   nohup sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=XXX --table_size=XXX --tables=XXX --time=XXX  --threads=XXX oltp_read_write cleanup
   ```
