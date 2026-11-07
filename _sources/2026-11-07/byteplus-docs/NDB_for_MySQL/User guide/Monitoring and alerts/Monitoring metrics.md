---
title: "Monitoring metrics"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Monitoring_metrics"
---

This topic introduces the monitoring items supported by NDB for MySQL and information related to the monitoring items.

## Precautions

* Cloud monitoring acquires data every 30 seconds by default, and displays the collected data after obtaining the average or maximum value according to the display granularity of the query results. For example, when querying the QPS data of a proxy node in the past 12 hours, the display granularity of the Cloud Monitoring query results is 1 minute, that is, the data displayed each time is actually the average of the past 2 query results.

* The units in the monitoring indicator table are all basic units. Please refer to the console for the specific units of each monitoring. The units displayed on the console will be flexibly adjusted according to certain conversion standards based on the monitored values, including:

   * SI: According to the SI standard, use 1000 as the prefix for unit conversion. When converting, prefixes such as K, M, and G will be added before the basic unit. For example, the basic unit of **OpenedTables** is Count. If the monitoring value of **OpenedTables** is large, the unit on the console will be adjusted to KCount, MCount, GCount, etc.

   * IEC: According to the IEC standard, 1024 is used as the prefix for unit conversion. For example, the base unit of **Storage Usage** is B. If the monitoring value of this indicator is large, the units on the console will be adjusted to KiB, MiB, GiB, etc.

## Monitoring metrics

You can call the [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData) interface to query the monitoring indicator data of the NDB for MySQL instance. When calling this interface to query, you need to obtain relevant information about the following monitoring metrics:

* **Namespace**: The product space to which the monitoring indicator to be queried belongs.

   The product space name for the instance is `VCM_veDB_MySQ`L.

* **SubNamespace**: The dimension to which the metric to query belongs.

   The instance supports viewing monitoring metrics in two dimensions: `Instance` and `Pod`.

* **MetricName**: The name of the monitoring indicator to be queried.

   The MetricName corresponding to each monitoring indicator of the instance is shown in the following table. For more details, please refer to the [cloud monitoring indicator query](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_veDB_MySQL).

### Instance monitoring metrics

NDB for MySQL provides the following monitoring data at the instance level.

|Indicator name ||MetricName |Unit |Indicator description |
|---|---|---|---|---|
|QPS ||QPS |Count/s |Counts the number of requests per second on the instance Proxy.<br><br>Data is collected from the sum of the `Questions` metric in the query result of the `show global status` command on all compute nodes. |
|TPS ||TPS |Count/s |Counts the number of transactions per second on the instance Proxy.<br><br>Data is collected from the sum of the `Com_commit` and `Com_rollback` indicators in the `show global status` command query result from all compute nodes. |
|UsedStorage |UsedStorage |UsedStorage |B |The total storage usage of the instance, including data space usage, log (Redolog, Binlog, Undolog) space usage, temporary space usage, and system space usage. |
||DataUsedStorage |DataUsedStorage |B |Stats instance data space usage. |
|Prepaid storage space usage rate ||PrepaidStorageUtil |% |Calculates the usage rate of the instance's prepaid storage space. |
|Storage space usage after compression<br><br> |Storage space usage after compression |CompressedUsedStorage |B |The total compressed storage usage of the instance, including data space usage, log (Redolog, Binlog, Undolog) space usage, temporary space usage, and system space usage.<br><br> |
||UsedColdStorage |UsedColdStorage |B |Stats instance cold data storage usage. |
||Compressed data space usage |CompressedDataUsedStorage |B |Counts the instance's compressed data storage space usage. |
|Log Storage Usage |RedoUsedStorage |RedoUsedStorage |B |Statistics instance Redolog space usage. |
||BinlogUsedStorage |BinlogUsedStorage |B |Statistical instance Binlog space usage. |
||UndoUsedStorage |UndoUsedStorage |B |Statistics instance Undolog space usage. |
||TmpUsedStorage |TmpUsedStorage |B |Stats instance temporary file space usage. |
||SysUsedStorage |SysUsedStorage |B |Statistics instance system file space usage. |
|CpuUtil |CpuUtil |CpuUtil |% |Stats the average CPU usage of all nodes in the instance. |
||MaxCpuUtil |MaxCpuUtil |% |Stats the maximum CPU usage for all nodes in the instance. |
|Memory Usage Ratio |Memory Usage Ratio |MemUtil |% |Average memory usage of all nodes in the instance. |
||memory maximum usage |MaxMemUtil |% |Stats the maximum memory usage for all nodes in the instance. |
|Network |NetworkTrafficOutput |NetSendBps |B/s |Counts the sum of the output traffic per second for all nodes in the instance. |
||NetRecvBps |NetRecvBps |B/s |Counts the sum of the input traffic per second for all nodes in the instance. |
|MPS ||MPS |Count/s |Counts the sum of operations per second for all nodes in the instance.<br><br>Derived from the `Com_insert`, `Com_insert_select`, `Com_update`, `Com_update_multi`, `Com_delete`, `Com_delete_multi`, `Com_replace`, and `Com_replace_select` indicators in the `show global status` command query results. |
|ReplicaLatency ||ReplicaLatency |μs |Statistics on the replication delay time of master\-slave redo. |
|Current Active Connections ||CurActiveConnection |Count |The current total number of connections for the instance, including the number of active connections and the number of connections created and opened. |
|RedoLogWritten ||RedoLogWritten |B/s |The amount of Redo log written per second by the primary node of the instance. |

### Node monitoring metrics

NDB for MySQL provides the following monitoring data at the node level.

|Indicator name ||MetricName |Unit |Indicator description |Collection Source |
|---|---|---|---|---|---|
|CPU Usage Ratio ||PodCpuUtil |% |Count the CPU usage of the selected node. ||
|Memory Usage Ratio ||PodMemUtil |% |Statistics the memory usage of the selected node. ||
|InnoDBBufferPool |UsedInnodbBufferPoolUtil |UsedInnodbBufferPoolUtil |% |Counts the ratio of free pages on the selected node to the total number of buffer pool pages in the InnoDB cache. |Derived from the `Innodb_buffer_pool_pages_dirty`, `Innodb_buffer_pool_pages_total`, `Innodb_buffer_pool_reads`, `Innodb_buffer_pool_read_requests` and other indicators in the `show global status` command query results. |
||InnodbBufferPoolHitUtil |InnodbBufferPoolHitUtil |% |Count the ratio of read hits to read requests on the selected node. ||
||InnodbBufferPoolDirtyUtil |InnodbBufferPoolDirtyUtil |% |Counts the ratio of dirty data in the selected node's InnoDB cache to pages used in the InnoDB cache. ||
|connection usage ||ConnectionUtil |% |Stats the connection usage for the selected node. ||
|Number of open connections ||ThreadsConnected |Count |Counts the number of open thread connections for the selected node. |Derived from the statistical information in the query results of the `show processlist` command. |
|total number of threads in the thread pool ||ThreadpoolThreads |Count |Counts the total number of threads in the thread pool for the selected node. ||
|active connections ||ThreadsRunning |Count |Counts the number of active threads currently running on the selected node. |Derived from the statistical information in the query results of the `show processlist` command. |
|ThreadsCreated ||ThreadsCreated |Count |Counts the number of threads created by the selected node. ||
|QPS ||QPS |Count/s |Counts the number of requests per second for the selected node. |Derived from the `Questions` indicator in the `show global status` command query result. |
|TPS ||TPS |Count/s |Counts the number of transactions per second for the selected node. |Derived from the `Com_rollback` and `Com_rollback` indicator in the `show global status` command query result. |
|MPS ||MPS |Count/s |Counts the number of data operations per second for the selected node. |Derived from the aggregation of `Com_insert`, `Com_insert_select`, `Com_update`, `Com_update_multi`, `Com_delete`, `Com_delete_multi`, `Com_replace`, and `Com_replace_select` indicators in the `show global status` command query results. |
|ReadIOPS |ReadIOPS |ReadIOPS |Count/s |Count the real\-time value of IOPS read by the selected node. ||
||ReadIOPSLimit |ReadIOPSLimit |Count/s |Statistics the maximum value of read IOPS for the selected node. ||
|WriteIOPS |WriteIOPS |WriteIOPS |Count/s |The real\-time value of IOPS written by the selected node is counted. ||
||WriteIOPSLimit |WriteIOPSLimit |Count/s |The maximum value of IOPS written to the selected node is counted. ||
|I/O Throughput |ReadIOThroughput |ReadIOThroughput |B/s |Counts the read I/O throughput of the selected node. ||
||WriteIOThroughput |WriteIOThroughput |B/s |Counts the write I/O throughput of the selected node. ||
|Network |NetRecvBps |NetworkTrafficInput |B/s |Count the input traffic of the selected node per second. |Derived from the `Bytes_received` indicator in the `show global status` command query result. |
||NetworkTrafficOutput |NetworkTrafficOutput |B/s |Count the output traffic of the selected node per second. |Derived from the `Bytes_sent` indicator in the `show global statu`s command query result. |
|Operation |OperationDelete |OperationDelete |Count/s |Counts the number of deletions per second for the selected node. |Derived from the `Com_delete` indicator in the `show global status` command query result. |
||OperationUpdate |OperationUpdate |Count/s |Count the number of updates per second for the selected node |Derived from the `Com_update` indicator in the `show global status` command query result. |
||OperationInsert |OperationInsert |Count/s |Counts the number of inserts per second for the selected node. |Derived from the `Com_insert` indicator in the `show global status` command query result. |
||OperationReplace |OperationReplace |Count/s |Counts the number of covered rows per second for the selected node. |Derived from the `Com_replace` indicator in the `show global status` command query result. |
||OperationCommit |OperationCommit |Count/s |Counts the number of transactions committed per second for the selected node. |Derived from the `Com_commit` indicator in the `show global status` command query result. |
||OperationRollback |OperationRollback |Count/s |Counts the number of transaction rollbacks per second for the selected node. |Derived from the `Com_rollback` indicator in the `show global status` command query result. |
|Slow query QPS ||SlowQueries |Count/s |Stats the QPS of slow query SQL on the selected node. ||
|ComStmt |ComStmtExecute |ComStmtExecute |Count/s |Statistical Com_stmt_execute cumulative number of executions. |Derived from the `Com_stmt_execute` indicator in the `show global status` command query result. |
||ComStmtReprepare |ComStmtReprepare |Count/s |Statistical Com_stmt_reprepare cumulative number of executions. |Derived from the `Com_stmt_reprepare` indicator in the `show global status` command query result. |
||ComStmtSendLongData |ComStmtSendLongData |Count/s |Statistical Com_stmt_send_long_data cumulative number of executions. |Derived from the `Com_stmt_send_long_data` indicator in the `show global status` command query result. |
||ComStmtReset |ComStmtReset |Count/s |Statistical Com_stmt_reset cumulative number of executions. |Derived from the `Com_stmt_reset` indicator in the `show global status` command query result. |
||ComStmtPrepare |ComStmtPrepare |Count/s |Statistical Com_stmt_prepare cumulative number of executions. |Derived from the `Com_stmt_prepare` indicator in the `show global status` command query result. |
||ComStmtFetch |ComStmtFetch |Count/s |Statistical Com_stmt_fetch cumulative number of executions. |Derived from the `Com_fetch` indicator in the `show global status` command query result. |
||ComStmtClose |ComStmtClose |Count/s |Statistical Com_stmt_close cumulative number of executions. |Derived from the `Com_close` indicator in the `show global status` command query result. |
|SelectScan ||SelectScan |Count/s |Counts the number of full table scans per second for the selected node. ||
|InnodbRows |InnodbRowsDeleted |InnodbRowsDeleted |Count/s |Counts the number of deleted rows per second for the selected node. |Derived from the `Innodb_rows_deleted` indicator in the `show global status` command query results. |
||InnodbRowsUpdated |InnodbRowsUpdated |Count/s |Counts the number of updated rows per second for the selected node. |Derived from the `Innodb_rows_updated` indicator in the `show global status` command query results. |
||InnodbRowsInserted |InnodbRowsInserted |Count/s |Counts the number of rows inserted per second for the selected node. |Derived from the `Innodb_rows_inserted` indicator in the `show global status` command query results. |
||InnodbRowsRead |InnodbRowsRead |Count/s |Counts the number of rows read per second by the selected node. |Derived from the `Innodb_rows_read` indicator in the `show global status` command query results. |
|InnoDBBufferData |InnodbBufferDataReads |InnodbBufferDataReads |B/s |Counts the amount of data read from the storage engine per second by the selected node. |Derived from the `Innodb_data_read` indicator in the show global status command query results. |
||InnodbBufferDataWritten |InnodbBufferDataWritten |B/s |Counts the amount of data written to the storage engine per second by the selected node. |Derived from the `Innodb_data_written` indicator in the show global status command query results. |
|InnoDBLogWritten |InnoDBLogWritten |InnodbLogWriteRequests |Count/s |Counts the number of write requests per second for the selected node log. |Derived from the `Innodb_log_write_requests` indicator in the `show global status` command query result. |
||InnodbLogFsyncs |InnodbLogFsyncs |Count/s |Counts the number of times the selected node synchronizes data to disk per second. |Derived from the `Innodb_os_log_fsyncs` indicator in the `show global status` command query result. |
|InnodbNumOpenFiles ||InnodbNumOpenFiles |Count |Counts the number of tables currently open for the selected node. ||
|OpenedTables ||OpenedTables |Count |Counts the number of open tables for the selected node. ||
|Temporary Tables Created per Second ||CreateTempTableUtil |Count/s |Counts the rate at which the selected node creates temporary tables per second. ||
|CreatedTmpDiskTables ||CreatedTmpDiskTables |Count/s |Counts the number of temporary tables created per second on disk by the selected node. ||
|CreatedTmpFiles ||CreatedTmpFiles |Count/s |Counts the number of temporary files created per second by the selected node. ||
|active transaction maximum execution time ||TrxExecuteTimeMax |s |Counts the maximum execution time of active transactions on the selected node that have been running for more than 10 seconds. ||
|row lock wait time per second for all transactions ||InnodbRowLockWaitTimeAvg |ms |Calculates the row lock wait time per second for all transactions on the selected node (total wait time / sampling period). ||
|InnodbRowLockWaits ||InnodbRowLockWaits |Count/s |Counts the number of times the selected node InnoDB waits for a row lock per second. ||
|InnodbRowsLockTimeAvg ||InnodbRowsLockTimeAvg |ms |Stats the average time for the selected node InnoDB to acquire a row lock. ||
|InnoDB File Read Frequency ||InnodbOsDataReads |Count/s |Counts the average number of times the selected node Innodb reads from the file per second. ||
|InnoDB File Write Frequency ||InnodbOsDataWrites |Count/s |Counts the average number of writes per second to the file by the selected node Innodb. ||
|InnoDB Log Physical Write Frequency ||InnodbLogWrites |Count/s |Counts the average number of physical writes per second to the log file by the selected node. ||
|HandlerCommit ||HandlerCommit |Count/s |Counts the number of intra\-InnoDB transaction commits per second for the selected node. |Derived from the `handler_commit` indicator in the `show global status` command query result. |
|HandlerRollback ||HandlerRollback |Count/s |Counts the number of internal InnoDB transaction rollbacks per second for the selected node. |Derived from the `handler_rollback` indicator in the `show global status` command query result. |
|HandlerReadRndNext ||HandlerReadRndNext |Count/s |Counts the number of read requests per second for the selected node. ||
|InnodbBufferPoolPagesFree ||InnodbBufferPoolPagesFree |Count |Counts the number of empty pages in InnoDB for the selected node. ||
|TotalInnodbBufferPoolPages ||TotalInnodbBufferPoolPages |Count |Counts the total number of pages in InnoDB for the selected node. ||
|InnodbBufferPoolRequests |InnodbBufferPoolReadRequests |InnodbBufferPoolReadRequests |Count/s |Counts the number of reads per second from the selected node's buffer pool. |Derived from the `Innodb_buffer_pool_read_requests` indicator in the `show global status` command query result. |
||InnodbBufferPoolWriteRequests |InnodbBufferPoolWriteRequests |Count/s |Counts the number of writes per second to the selected node's buffer pool. |Derived from the `Innodb_buffer_pool_write_requests` indicator in the `show global status` command query result. |
|InnodbBufferPoolReads ||InnodbBufferPoolReads |Count/s |Counts the number of physical reads per second for the selected node InnoDB. ||
|TrxHistoryLen ||TrxHistoryLen |Count |Counts the length of the historical transaction list for the selected node. ||
|IOPS usage |write IOPS usage |WriteIOPSUtil |% |Stats the write IOPS usage for the selected node. ||
||read IOPS usage |ReadIOPSUtil |% |Calculates the read IOPS usage rate for the selected node. ||
|InnoDB Monitor Number of Waits for Row Locks in Cycle ||InnodbRowLockWaitCounts |Count |Counts the number of times the selected node waits for an InnoDB row lock during the monitoring period. ||
|Number of internal rollbacks during the monitoring cycle ||HandlerRollbackCurrentCount |Count |Counts the number of internal rollbacks for the selected node during the monitoring period. ||
