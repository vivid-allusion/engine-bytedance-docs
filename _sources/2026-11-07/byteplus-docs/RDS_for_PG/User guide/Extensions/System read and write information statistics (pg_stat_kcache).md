---
title: "System read and write information statistics (pg_stat_kcache)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/statistics_on_system_read_or_write_information-pg_stat_kcache"
---

pg_stat_kcache is an extension that collects statistics on PostgreSQL's file system read/write information during operation.

<span id=".5a6e546w5Y6f55CG"></span>
## Implementation principle

pg_stat_kcache calls the Linux interface `getrusage` before and after query execution to retrieve process\-related resource information, then calculates the difference to determine the resources used by the current query.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The definitions of functions and views related to pg_stat_kcache depend on the <a href="https://www.postgresql.org/docs/11/pgstatstatements.html">pg_stat_statements</a> extension. Before use, you need to Modify the <code>shared_preload_libraries</code> parameter, adding <code>pg_stat_statements</code> and <code>pg_stat_kcache</code> to its Running value.</div>


* <div data-tips="true" data-tips-type="tip">Modifying the <code>shared_preload_libraries</code> parameter requires a Restart instance. Refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters">Modifying parameters</a> and operate with caution.</div>



<span id=".5qC45b-D5a-56LGh"></span>
### Core objects

The core objects of pg_stat_kcache are shown in the following table.


|**Type of object** |**Object name** |**Object description** |**Examples** |
|---|---|---|---|
|GUC parameter |pg_stat_kcache.linux_hz |* Integer type, minimum value \-1, maximum value INT_MAX, default value \-1.<br><br>* Compensation value for sampling error, see: linux CONFIG_HZ. |```sql```<br>```set pg_stat_kcache.linux_hz = -1;```<br> |
||pg_stat_kcache.track |Enumeration type with possible values: [none, top, all]. Default value is top, which controls which SQL statements to trace, with meanings as follows:<br><br><br>* top: trace the top\-level SQL statements, usually those sent directly by the client.<br><br>* all: trace both top\-level and nested statements, such as nested SQL statements executed within a Function.<br><br>* none: disable tracing. |```sql```<br>```set pg_stat_kcache.track = all;```<br> |
||pg_stat_kcache.track_planning |* bool type, default value is false.<br><br>* Effective in PostgreSQL 13 and later versions.<br><br>* Indicates whether to track resource usage during query optimization. |```sql```<br>```set pg_stat_kcache.track_planning = true;```<br> |
|Functions |pg_stat_kcache() |Return tracing information recorded in shared memory.<br><br>It can be called directly but is usually accessed through the pg_stat_kcache_detail view. |```sql```<br>```select * from pg_stat_kcache();```<br>```select pg_stat_kcache();```<br> |
||pg_stat_kcache_reset() |Clear recorded trace information. |```sql```<br>```select pg_stat_kcache_reset();```<br> |
|Views |pg_stat_kcache_detail |Results of join queries on pg_stat_kcache(), pg_stat_statements, pg_database, and pg_roles. |```sql```<br>```select * from pg_stat_kcache_detail;```<br> |
||pg_stat_kcache |Aggregate the pg_stat_kcache_detail view by datname dimension with sum. |```sql```<br>```Select *  from pg_stat_kcache;```<br> |


<span id=".5Ye95pWw5ZKM6KeG5Zu-5YiX5ZCN5ZCr5LmJ"></span>
### Meaning of function and view column names


|Column name |Type |Description |
|---|---|---|
|datname |name |Database name. |
|plan_user_time |double precision |pg_stat_kcache.track_planning enables and represents the user CPU time consumed for SQL query optimization, in seconds or milliseconds. Effective in PostgreSQL 13 and later versions. |
|plan_system_time |double precision |pg_stat_kcache.track_planning enables and represents the system CPU time consumed for SQL query optimization, in seconds or milliseconds. Effective for PostgreSQL version 13 and above. |
|plan_minflts |bigint |pg_stat_kcache.track_planning enabled indicates the number of soft page faults during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|plan_majflts |bigint |pg_stat_kcache.track_planning is enabled, indicating the number of hard page faults during SQL query optimization. Effective for PostgreSQL 13 and above. |
|plan_nswaps |bigint |Enabled with pg_stat_kcache.track_planning, indicating the number of swaps during SQL query optimization. Effective in PostgreSQL 13 and above. |
|plan_reads |bigint |pg_stat_kcache.track_planning enabled means the number of read bytes initiated through the file system during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|plan_reads_blks |bigint |Enabling pg_stat_kcache.track_planning tracks the number of 8K blocks read via the file system during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|plan_writes |bigint |Enabling pg_stat_kcache.track_planning means tracking the number of write bytes initiated through the file system during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|plan_writes_blks |bigint |Effective when pg_stat_kcache.track_planning is enabled, indicates the number of 8K blocks written via the file system during SQL query planning. Effective from PostgreSQL 13 and later versions. |
|plan_msgsnds |bigint |pg_stat_kcache.track_planning enable takes effect, representing the number of IPC messages sent during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|plan_msgrcvs |bigint |pg_stat_kcache.track_planning enabled means the number of IPC messages received during SQL query optimization. Effective in PostgreSQL 13 and above. |
|plan_nsignals |bigint |pg_stat_kcache.track_planning is enabled and effective, indicating the number of signals received during SQL query optimization. Effective for PostgreSQL 13 and above. |
|plan_nvcsws |bigint |Enabled with pg_stat_kcache.track_planning, indicating the number of voluntary context switches during SQL query optimization. Effective for PostgreSQL 13 and above. |
|plan_nivcsws |bigint |pg_stat_kcache.track_planning enable takes effect, representing the number of passive context switches occurring during SQL query optimization. Effective in PostgreSQL 13 and later versions. |
|exec_user_time |double precision |Indicates the user CPU time consumed during the SQL execution phase, in seconds or milliseconds. |
|exec_system_time |double precision |Indicates system CPU time consumed during the SQL execution phase, in seconds or milliseconds. |
|exec_minflts |bigint |Represents the number of soft page faults during SQL execution. |
|exec_majflts |bigint |Indicates the number of hard page faults during the SQL execution phase. |
|exec_nswaps |bigint |Represents the number of swaps during SQL execution. |
|exec_reads |bigint |Indicates the number of read bytes initiated through the file system during the SQL execution phase. |
|exec_reads_blks |bigint |Represents the SQL execution phase, indicating the number of 8K blocks read through the file system. |
|exec_writes |bigint |Indicates the number of bytes written through the file system during the SQL execution phase. |
|exec_writes_blks |bigint |Represents the SQL execution phase, indicating the number of 8K blocks written through the file system. |
|exec_msgsnds |bigint |Indicates the number of IPC messages sent during the SQL execution phase. |
|exec_msgrcvs |bigint |Represents the number of IPC messages received during SQL execution stage. |
|exec_nsignals |bigint |Indicates the number of signals received during the SQL execution phase. |
|exec_nvcsws |bigint |The number of voluntary context switches during the SQL execution phase. |
|exec_nivcsws |bigint |Represents the number of passive context switches occurring during the SQL execution phase. |


&nbsp;

<span id=".5a6J6KOF5o-S5Lu2"></span>
## Install extension

Use the following command to install the extension.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">A super account is required to create the extension.</div>


```sql
create extension pg_stat_statements ;
create extension pg_stat_kcache ;
```


<span id=".5o-S5Lu255qE5L2_55So"></span>
## Using extensions

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* GUC parameter configuration is completed.

   Added `pg_stat_statements` and `pg_stat_kcache` to the shared_preload_libraries list.

* Extension is installed.

* Data is imported.


<span id=".5L2_55So5o-S5Lu2"></span>
### Extension usage


1. Enable read/write and check resource usage.

   ```sql
   sysbench --test=./tests/include/oltp_legacy/oltp.lua --db-driver=pgsql --pgsql-db=sysbench --pgsql-user=root --pgsql-password=Bd2021_bd --pgsql-port=5432 --pgsql-host=10.249.184.214 --oltp-tables-count=10 --oltp-table-size=1000000 --max-time=120 --max-requests=0 --num-threads=50 --report-interval=3  --forced-shutdown=1 run
   ```
   

2. Check resource usage.

   ```sql
   select * from pg_stat_kcache_detail;
   select * from pg_stat_kcache;
   select pg_stat_kcache_reset();
   ```
