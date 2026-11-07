---
title: "Test method"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Test_method_1"
---

This topic describes the test method used to stress test NDB for MySQL.

<span id="测试步骤"></span>
## Test steps

Replace the database, connection IP, and user password according to the actual information.

<span id="_1-创建待测数据库"></span>
#### 1. Create the database to be tested

```bash
mysql -h XXX -P XXX -u XXX -p XXX -e 'create database sbtest'
```


<span id="_2-修改实例参数"></span>
#### 2. Modify instance parameters

Adjust the `max_prepared_stmt_count` to a maximum of 1048576.

<span id="_3-使用-sysbench-测试云数据库-vedb-mysql-版一主一只读节点的只读性能"></span>
#### 3. Use SysBench to test the read\-only performance of NDB for MySQL with one master and one read\-only node.

The test address is the connection address of the default end point, and the test process will last for 10 minutes.

```bash
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_read_only prepare
## Prepare the data
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --range_selects=0 --skip-trx=1 --report-interval=1 oltp_read_only run
## Running workload
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --range_selects=0 oltp_read_only cleanup
## Clean up
```


<span id="_4-使用-sysbench-测试云数据库-vedb-mysql-版一主一只读节点的写入性能"></span>
#### 4. Use SysBench to test the write performance of NDB for MySQL master\-only read\-only node

The test address is the connection address of the default end point, and the test process will last for 10 minutes.

```bash
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600  oltp_write_only prepare
## Prepare the data
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_write_only run
## Running workload
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=25000 --tables=250 --events=0 --time=600   --threads=XXX --percentile=95  oltp_write_only cleanup
## Clean up
```


<span id="_5-使用-sysbench-测试云数据库-vedb-mysql-版一主一只读节点的混合读写性能"></span>
#### 5. Use SysBench to test the mixed read and write performance of NDB for MySQL with one master and one read node

The test address is the connection address of the default end point, and the test process will last for 10 minutes.

```bash
sysbench --db-driver=mysql --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600  oltp_read_write prepare
## Prepare the data
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95 --report-interval=1 oltp_read_write run
## Running workload
sysbench --db-driver=mysql  --mysql-host=XXX --mysql-port=XXX --mysql-user=XXX --mysql-password=XXX --mysql-db=sbtest --table_size=250000 --tables=25 --events=0 --time=600   --threads=XXX --percentile=95  oltp_read_write cleanup
## Clean up
```
