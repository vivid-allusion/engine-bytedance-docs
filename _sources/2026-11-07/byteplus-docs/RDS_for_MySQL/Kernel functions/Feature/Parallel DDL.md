---
title: "Parallel DDL"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parallel_DDL"
---

This topic describes the parallel DDL feature of RDS for MySQL.

<span id="bHwN2g1U"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20251015 and above.

* MySQL 8.0 version, all kernel minor versions are supported.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<span id="qC5rMPJ9"></span>
## Background

In community MySQL 5.7, creating an index involves the scan, sort, insert, and flush stages. This process runs on a single thread and is time\-consuming.

When a user executes a DDL statement to rebuild a table or create an index during database operations, the inplace algorithm allows DML statements to proceed without being blocked. However, this process requires writing additional row logs and consumes I/O, which affects SQL latency. Moreover, if the execution takes too long, an excessive number of row logs may accumulate and reach the maximum limit of the `innodb_online_alter_log_max_size` parameter, causing the DDL execution to fail. Therefore, it is essential to find a method for executing DDLs quickly.

<span id="le8Mn7qG"></span>
## Feature description

The parallel DDL feature in RDS for MySQL allows multiple threads to perform sort, insert, and flush operations in parallel at the index level when executing DDL statements that rebuild tables. When creating a single index, multiple threads can be initiated to scan the primary key index in parallel. The sorting phase also supports parallel sorting to fully leverage the benefits of multiple cores.

Additionally, the sorting algorithm and insert phase are further optimized. In single\-concurrency scenarios, its performance is comparable to the native MySQL 5.7 algorithm. In multi\-concurrency scenarios with equal memory resources for each thread, you can achieve a performance speedup of up to 2.3 times.

<span id="LFgzcRkD"></span>
## Instructions

<span id="irO74BNu"></span>
### Parameter description

RDS for MySQL provides multiple modifiable parameters for MySQL 5.7 to configure the parallel DDL feature. In MySQL 8.0 and MySQL 8.4, the parallel DDL feature is enabled by default and can be used without modifying parameters.


|**Parameter name** |**Type** |**Default value** |**Does it need instance restart to take effect?**  |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_innodb_parallel_ddl |bool |OFF |No |[ON/OFF] |GLOBAL |Enable parallel DDL |
|loose_innodb_parallel_read_threads |int |4 |No |[1, 256] |GLOBAL/SESSION |The number of threads for reading the primary key index in parallel in a parallel DDL. |
|loose_innodb_ddl_buffer_size |int |1048576 |No |[65536, 4294967295] |GLOBAL/SESSION |The maximum number of memory bytes used in parallel DDL |
|loose_innodb_ddl_threads<br><br> |int |4 |No |[1, 64] |GLOBAL/SESSION |The maximum number of threads for processing the task queue in parallel DDL. The maximum number of threads for processing indexes in parallel when a table is rebuilt. The maximum number of threads for parallel sorting when an index is created. |


<span id="C6YgQhHs"></span>
### Examples

This topic describes how to use the parallel DDL feature in MySQL 5.7. The usage of parallel DDL in MySQL 8.0 and MySQL 8.4 is the same as in the community version. For more information, refer to the [MySQL official document](https://dev.mysql.com/doc/refman/8.0/en/online-ddl-parallel-thread-configuration.html).


1. Modify the loose_innodb_parallel_ddl parameter to ON.

2. Use parallel DDL to create an index.

   * Set DDL\-related parameters.


```SQL
SET SESSION loose_innodb_parallel_read_threads = 4;
SET SESSION loose_innodb_ddl_buffer_size = 4*1048576;
SET SESSION loose_innodb_ddl_threads = 4;
```



   * Create an index.


```SQL
CREATE INDEX <index_name> ON <table_name>(<column_name>);
```



3. Use parallel DDL to rebuild a table.

   * Set DDL\-related parameters.


```SQL
SET SESSION loose_innodb_ddl_buffer_size = 4*1048576;
SET SESSION loose_innodb_ddl_threads = 4;
```



   * Creating index


```SQL
ALTER TABLE <table_name> ADD COLUMN <column_name> <column_type>, ALGORITHM=INPLACE;
```


<span id="ulITLyYE"></span>
### Precautions

The precautions for using the parallel DDL feature in MySQL 5.7 and MySQL 8.0 are the same as those for the community version. For more information, refer to the [MySQL official document](https://dev.mysql.com/doc/refman/8.0/en/online-ddl-parallel-thread-configuration.html).

<span id="YLvIe5OL"></span>
## Performance data

<span id="FGkT0bQE"></span>
### Test Environment

An instance with 32C64G specifications, 8 GiB of Sysbench data, and a 4 MiB DDL buffer configured for each thread.

<span id="tYaVUUyr"></span>
### The test results are as follows.


* The following table shows the elapsed time for creating indexes with different numbers of concurrent connections in Community Edition MySQL 5.7 and RDS for MySQL 5.7. The elapsed time for DDL execution compared with the native MySQL 5.7 version is as follows.



| |MySQL Community Edition 5.7 |RDS for MySQL 5.7 ||||||
|---|---|---|---|---|---|---|---|
||No concurrency |1 concurrency |2 concurrent |4 concurrent |8 concurrency |16 concurrency |32 concurrent |
|Index creation time (Second) |50.71 |51.80 |31.12 |25.08 |23.39 |21.85 |22.31 |



* The comparison of index creation performance between Community Edition MySQL 5.7 and RDS for MySQL 5.7 is as follows.


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d0ad4f3a4d4bfac6ac458efdab3368f.png" width="1063px" /></div>


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f807f198d52f3fe4fd5a138eb94d3ba.png" width="1060px" /></div>
