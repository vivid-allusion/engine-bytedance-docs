---
title: "Test methods"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/test_methods"
---

This topic describes the environments, tools, steps, and metrics used for RDS for PostgreSQL performance testing.

<span id=".5rWL6K-V546v5aKD"></span>
## Test Environment


* **Region**: cn\-beijing\-autodriving, with S20 models in the node pool

* **Availability zone**: Availability zone B

* **ECS of client**: Computation type c3i 32 vCPU 64 GiB, Specification code: ecs.c3i.8xlarge

* **OS mirror image**: CentOS 8.3 64\-bit version


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because you must install additional compilation tools for the stress test tools, we recommend you bind the ECS instance to an EIP.</div>


<span id=".5rWL6K-V5bel5YW3"></span>
## Test tool

SysBench is a modular benchmarking test tool that supports multiple platforms and multiple threads. It evaluates the performance of core parameters when the system runs a high\-load database to gain quick insights into the database system performance.

<span id=".5LiL6L295a6J6KOF5rWL6K-V5bel5YW3"></span>
### Downloading and installing the testing tool

```bash
wget -c https://github.com/akopytov/sysbench/archive/1.0.12.zip
yum install make automake libtool pkgconfig libaio-devel postgresql-devel
unzip 1.0.12.zip
cd sysbench-1.0.12
# SysBench supports MySQL by default. Please add PostgreSQL to the supported list here.
./autogen.sh
./configure --with-pgsql --without-mysql
make
make install
```


<span id=".5rWL6K-V5q2l6aqk"></span>
## Test steps

Replace the database, username, password, port, host domain, and other information in the command correctly as needed. The duration of this performance test is 180 seconds.

<span id=".MS7liJ3lp4vljJbmtYvor5XmlbDmja4="></span>
### 1. Initializing test data

Use the sysbench tool to load test data.The command is as follows:

```bash
sysbench ./tests/include/oltp_legacy/oltp.lua \
--db-driver=pgsql \
--pgsql-db=sbtest \
--pgsql-user=<username> \
--pgsql-password=<password> \
--pgsql-port=5432 \
--pgsql-host=<host> \
--oltp-tables-count=32 \
--oltp-table-size=10000000 \
--time=180 \
--max-requests=0 \
--threads=20 \
--report-interval=5 \
--forced-shutdown=1 \
prepare
```


<span id=".Mi7lkK_liqjmtYvor5U="></span>
### 2. Starting test

Execute the following command to test the performance. During the testing process, the `threads` parameter will be adjusted to find the optimal number of `threads` that achieve the best performance and record the results.

```bash
sysbench ./tests/include/oltp_legacy/oltp.lua \
 --db-driver=pgsql \
 --pgsql-db=sbtest \
 --pgsql-user=<username> \
 --pgsql-password=<password> \
 --pgsql-port=5432 \
 --pgsql-host=<host> \
 --oltp-tables-count=32 \
 --oltp-table-size=10000000 \
 --time=180 \ 
 --max-requests=0 \
 --threads=64 \
 --report-interval=5 \
 --forced-shutdown=1 \
 run
```


<span id=".My7muIXnkIbmtYvor5XmlbDmja4="></span>
### 3. Clearing test data

After the performance test is completed, clear the test data with the following command.

```bash
sysbench ./tests/include/oltp_legacy/oltp.lua \
 --db-driver=pgsql \
 --pgsql-db=sbtest \
 --pgsql-user=<username> \
 --pgsql-password=<password> \
 --pgsql-port=5432 \
 --pgsql-host=<host> \
--oltp-tables-count=32 \
 --oltp-table-size=10000000 \
 --time=180 \
 --max-requests=0 \
 --threads=200 \
 --report-interval=5 \
 --forced-shutdown=1 \
 cleanup
```


<span id=".5rWL6K-V5oyH5qCH"></span>
## Test metrics


* **TPS**

   Transactions Per Second: the number of transactions executed per second by the database.

* **QPS**

   Queries Per Second: the number of SQL queries executed per second by the database. It contains Read, Write, and Other query types.


<span id=".5rWL6K-V57uT5p6c"></span>
## The test results are as follows.

For details about test results, refer to [Performance test results](https://docs.byteplus.com/en/docs/RDS_for_PG/performance_test_result).
