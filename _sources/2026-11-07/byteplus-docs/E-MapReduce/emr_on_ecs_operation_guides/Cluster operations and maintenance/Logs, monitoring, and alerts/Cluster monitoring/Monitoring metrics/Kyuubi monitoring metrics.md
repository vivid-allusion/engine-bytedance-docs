---
title: "Kyuubi monitoring metrics"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-kyuubi_monitoring_metrics"
---

This document provides detailed information about Kyuubi metrics.


|**Title** |**metric name** |**Unit** |
|---|---|---|
|GC status |Kyuubi Young GC count |count |
||Kyuubi Young GC count |count |
||Kyuubi Young GC count |s |
||Kyuubi Young GC count |s |
|Memory region utilization |Kyuubi Survivor Space memory utilization |% |
||Kyuubi Eden Space memory utilization |% |
||Kyuubi Compressed Class Space memory utilization |% |
||Kyuubi Old Gen memory utilization |% |
||Kyuubi Metaspace memory utilization |% |
|Heap and non\-heap memory status |Kyuubi Heap used memory |MB |
||Kyuubi Heap committed |MB |
||Kyuubi Heap maximum |MB |
||Kyuubi Heap initial |MB |
||Kyuubi Heap memory usage |MB |
||Kyuubi Non Heap initial |MB |
||Kyuubi Non Heap committed |MB |
||Kyuubi Non Heap used memory |MB |
|Thread count |Number of Kyuubi Daemon Threads |count |
||Number of Kyuubi Peak Threads |count |
||Number of Kyuubi Deadlock Threads |count |
||Number of Kyuubi Runnable Threads |count |
||Number of Kyuubi Blocked Threads |count |
||Number of Kyuubi Waiting Threads |count |
||Number of Kyuubi Terminated Threads |count |
|Operation State Ops |Kyuubi event frequency for entering Running operation state |count/s |
||Kyuubi event frequency for entering Pending operation state |count/s |
||Kyuubi event frequency for entering Initialized operation state |count/s |
||Kyuubi event frequency for entering Finished operation state |count/s |
||Kyuubi event frequency for entering Closed operation state |count/s |
|Fetch operation frequency |Kyuubi FetchResultRows method invocation frequency |count/s |
||Kyuubi FetchLogRows method invocation frequency |count/s |
|GetResultSetMetadata duration |Kyuubi GetResultSetMetadata P50 invocation duration |ms |
||Kyuubi GetResultSetMetadata P75 invocation duration ||
||Kyuubi GetResultSetMetadata P95 invocation duration ||
||Kyuubi GetResultSetMetadata P99 invocation duration ||
||Kyuubi GetResultSetMetadata P999 invocation duration ||
|CloseOperation duration |Kyuubi CloseOperation P50 invocation duration |ms |
||Kyuubi CloseOperation P75 invocation duration ||
||Kyuubi CloseOperation P95 invocation duration ||
||Kyuubi CloseOperation P99 invocation duration ||
||Kyuubi CloseOperation P999 invocation duration ||
|GetOperationStatus duration |Kyuubi GetOperationStatus P50 invocation duration |ms |
||Kyuubi GetOperationStatus P75 invocation duration ||
||Kyuubi GetOperationStatus P95 invocation duration ||
||Kyuubi GetOperationStatus P99 invocation duration ||
||Kyuubi GetOperationStatus P999 invocation duration ||
|GetInfo duration |Kyuubi GetInfo P50 invocation duration |ms |
||Kyuubi GetInfo P75 invocation duration ||
||Kyuubi GetInfo P95 invocation duration ||
||Kyuubi GetInfo P99 invocation duration ||
||Kyuubi GetInfo P999 invocation duration ||
|FetchResults duration |Kyuubi FetchResults P50 invocation duration |ms |
||Kyuubi FetchResults P75 invocation duration ||
||Kyuubi FetchResults P95 invocation duration ||
||Kyuubi FetchResults P99 invocation duration ||
||Kyuubi FetchResults P999 invocation duration ||
|ExecuteStatement duration |Kyuubi ExecuteStatement P50 invocation duration |ms |
||Kyuubi ExecuteStatement P75 invocation duration ||
||Kyuubi ExecuteStatement P95 invocation duration ||
||Kyuubi ExecuteStatement P99 invocation duration ||
||Kyuubi ExecuteStatement P999 invocation duration ||
|CloseSession duration |Kyuubi CloseSession P50 invocation duration |ms |
||Kyuubi CloseSession P75 invocation duration ||
||Kyuubi CloseSession P95 invocation duration ||
||Kyuubi CloseSession P99 invocation duration ||
||Kyuubi CloseSession P999 invocation duration ||
|OpenSession duration |Kyuubi OpenSession P50 invocation duration |ms |
||Kyuubi OpenSession P75 invocation duration ||
||Kyuubi OpenSession P95 invocation duration ||
||Kyuubi OpenSession P99 invocation duration ||
||Kyuubi OpenSession P999 invocation duration ||
|LaunchEngine Operation |Total number of Kyuubi LaunchEngine Operations |count |
||Number of Kyuubi LaunchEngine Operations Opened |count |
||Number of Kyuubi LaunchEngine Operations Initialized |count |
||Number of Kyuubi LaunchEngine Operations Running |count |
||Number of Kyuubi LaunchEngine Operations Pending |count |
||Number of Kyuubi LaunchEngine Operations Finished |count |
||Number of Kyuubi LaunchEngine Operations Closed |count |
|ExecuteStatement Operation |Total number of Kyuubi ExecuteStatement Operations |count |
||Number of Kyuubi ExecuteStatement Operations Opened |count |
||Number of Kyuubi ExecuteStatement Operations Initialized |count |
||Number of Kyuubi ExecuteStatement Operations Running |count |
||Number of Kyuubi ExecuteStatement Operations Pending |count |
||Number of Kyuubi ExecuteStatement Operations Finished |count |
||Number of Kyuubi ExecuteStatement Operations Closed |count |
|Total operations |Total number of Kyuubi Operations |count |
