---
title: "Hive monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs_Hive_monitoring_metrics"
---

This document provides detailed information about Hive metrics.

Hive metrics include the following sections:


* [Hive-overview](https://docs.byteplus.com/docs/E-MapReduce/105451#hive-%E6%A6%82%E8%A7%88)

* [Hive-HivemetaStore](https://docs.byteplus.com/docs/E-MapReduce/105451#hive-hivemetastore)

* [Hive-HiveSever2](https://docs.byteplus.com/docs/E-MapReduce/105451#hive-hivesever2)


<span id="hive-概览"></span>
## Hive\-overview


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|Node information |Total number of healthy HiveServer2 nodes |Number of operations |
||Total number of healthy HiveMetastore nodes |Number of operations |


<span id="hive-hivemetastore"></span>
## Hive\-HivemetaStore


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|GC count |Hive MetaStore YGC count |Number of requests |
||Hive MetaStore FGC count |Number of requests |
|GC duration |Hive MetaStore YGC duration |s |
||Hive MetaStore FGC duration |s |
||Total Hive MetaStore GC duration |s |
||Hive MetaStore extra sleep time |ms |
|Memory region usage ratio |Hive MetaStore survivor space usage |% |
||Hive MetaStore Eden space usage |% |
||Hive MetaStore CompressedClassSpace usage |% |
||Hive MetaStore OldSpace usage |% |
||Hive MetaStore Metaspace usage |% |
|Memory usage |Hive MetaStore heap memory usage |MB |
||Hive MetaStore heap memory committed |MB |
||Hive MetaStore heap memory initial value |MB |
||Hive MetaStore heap memory maximum value |MB |
||Hive MetaStore non\-heap memory usage |MB |
||Hive MetaStore non\-heap memory committed |MB |
||Hive MetaStore non\-heap memory initial value |MB |
|Heap memory usage ratio |Hive MetaStore heap memory usage ratio |% |
|File descriptor count |Hive MetaStore open file descriptor count |Number of operations |
||Hive MetaStore maximum file descriptor count |Number of operations |
|CPU load |Hive MetaStore CPU usage |% |
||Hive MetaStore system CPU usage |% |
||Hive MetaStore process CPU usage time |h |
|Worker thread count |Hive MetaStore daemon thread count |Number of operations |
||Total Hive MetaStore thread count |Number of operations |
|Average request duration |Hive MetaStore AlterTable average duration |ms |
||Hive MetaStore AlterTableWithEnvContext average duration |ms |
||Hive MetaStore CreateTable average duration |ms |
||Hive MetaStore CreateTableWithEnvContext average duration |ms |
||Hive MetaStore DropTableWithEnvContext average duration |ms |
||Hive MetaStore GetTable average duration |ms |
||Hive MetaStore GetTables average duration |ms |
||Hive MetaStore GetTableReq average duration |ms |
||Hive MetaStore GetDatabase average duration |ms |
||Hive MetaStore GetDatabases average duration |ms |
||Hive MetaStore GetAllFunctions average duration |ms |


<span id="hive-hivesever2"></span>
## Hive\-HiveSever2


|**Title** |**Metric name** |**Unit** |
|---|---|---|
|GC count |HiveServer2 YGC count |Number of requests |
||HiveServer2 FGC count |Number of requests |
|GC duration |HiveServer2 YGC duration |s |
||HiveServer2 FGC duration |s |
||Total HiveServer2 GC duration |s |
||HiveServer2 extra sleep time |ms/s |
|Memory region usage ratio |HiveServer2 survivor space usage |% |
||HiveServer2 Eden space usage |% |
||HiveServer2 CompressedClassSpace usage |% |
||HiveServer2 OldSpace usage |% |
||HiveServer2 Metaspace usage |% |
|Memory usage |HiveServer2 heap memory usage |MB |
||HiveServer2 heap memory committed |MB |
||HiveServer2 heap memory initial value |MB |
||HiveServer2 heap memory maximum value |GB |
||HiveServer2 non\-heap memory usage |MB |
||HiveServer2 non\-heap memory committed |MB |
||HiveServer2 non\-heap memory initial value |MB |
|Heap memory usage ratio |HiveServer2 heap memory usage ratio |% |
|File descriptor count |HiveServer2 open file descriptor count |Number of operations |
||HiveServer2 maximum file descriptor count |Number of operations |
|CPU load |HiveServer2 CPU usage |% |
||HiveServer2 system CPU usage |% |
||HiveServer2 process CPU usage time |h |
|Worker thread count |HiveServer2 daemon thread count |Number of operations |
||Total HiveServer2 thread count |Number of operations |
||HiveServer2 JVM threads count |Number of operations |
||HiveServer2 JVM daemon threads count |Number of operations |
||HiveServer2 JVM blocked threads count |Number of operations |
||HiveServer2 JVM deadlock threads count |Number of operations |
||HiveServer2 JVM new threads count |Number of operations |
||HiveServer2 JVM runnable threads count |Number of operations |
||HiveServer2 JVM terminated threads count |Number of operations |
||HiveServer2 JVM timed waiting threads count |Number of operations |
||HiveServer2 JVM waiting threads count |Number of operations |
|Process runtime |HiveServer2 process runtime |s |
|Driver execution latency |HiveServer2 Driver execution latency P99 |ms |
||HiveServer2 Driver average latency |ms |
|Number of open connections |Number of open connections in HiveServer2 |Number of operations |
|Asynchronous operation load |Size of the asynchronous thread pool in HiveServer2 |Number of operations |
||Size of the asynchronous operation queue in HiveServer2 |Number of operations |
||Number of SemanticAnalyze requests in HiveServer2 |Number of requests |
||Number of RunTask requests in HiveServer2 |Number of requests |
||Number of ReleaseLocks requests in HiveServer2 |Number of requests |
|SQL tasks |Average time that SQL tasks remain in the Pending state in HiveServer2 |ms |
||Average time that SQL tasks remain in the Running state in HiveServer2 |ms |
|Number of active users |Number of current active users in HiveServer2 |Number of operations |
|Query time |Average time to execute queries in HiveServer2 |ms |
||Average time to submit queries in HiveServer2 |ms |
|Number of queries |Number of successful queries in HiveServer2 |Number of operations |
||Number of failed queries in HiveServer2 |Number of operations |
|Number of engine jobs |Number of Hive on MR jobs in HiveServer2 |Number of operations |
||Number of Hive on TEZ jobs in HiveServer2 |Number of operations |
|Number of sessions |Number of active sessions in HiveServer2 |Number of operations |
||Number of open sessions in HiveServer2 |Number of operations |
|Number of active queries |Number of active queries in HiveServer2 |Number of operations |
|Operation statistics |Number of closed operations in HiveServer2 |Number of operations |
||Number of completed operations in HiveServer2 |Number of operations |
||Number of cancelled operations in HiveServer2 |Number of operations |
||Number of operations with errors in HiveServer2 |Number of operations |
