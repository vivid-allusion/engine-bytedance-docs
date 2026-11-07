---
title: "Monitoring metrics"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/monitoring_metrics"
---

Click the Monitoring tab to access detailed information on the Resource Monitor, Engine Monitor, Deployment Monitor, and Agent Monitor for the instance. The monitoring metrics for each type of monitoring are shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the convenience of display, the monitoring alarm chart will automatically adjust the unit level according to the amount of data, and the specific display shall prevail. For example, when the replication delay is high, the unit is adjusted from μs to ms; when the replication delay is high, the unit is adjusted from ms to s.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query each monitoring indicator data and alarm information. When calling the query interface, you need to obtain the Namespace of the product, the SubNamespace to which the index to be queried belongs, and the MetricName of the index to be queried. The RDS for PostgreSQL has <code>VCM_RDS_PostgreSQL</code> Namespace, and the MetricName and SubNamespace of each indicator are shown in the following table.</div>


* <div data-tips="true" data-tips-type="tip">You can also get the detailed information of each monitoring metric in the <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_RDS_PostgreSQL&tabKey=metric">Cloud Monitor Metrics</a>.</div>




|**Name** |**MetricName** |**SubNamespace** |**Unit** |**Description of indicators** |
|---|---|---|---|---|
|CPU utilization |CpuUtil |resource_monitor |Percent |With idle\-time overcommitment allowed, CPU utilization may exceed 100%. |
|Memory utilization |MemUtil |resource_monitor |Percent |Overuse during idle time is allowed, and memory utilization may be greater than 100%. |
|Disk utilization |DiskUtil |resource_monitor |Percent |The ratio of the used disk space to the total disk space of the instance. |
|User CPU utilization |UserCPUUtil |resource_monitor |Percent |User CPU utilization is one of the components of CPU usage. |
|System CPU utilization |SysCPUUtil |resource_monitor |Percent |System CPU utilization is one of the components of CPU utilization. |
|RSS memory usage |RSSMemUsage |resource_monitor |Bytes(SI) |The physical memory size actually occupied by the instance. |
|Cache memory usage |CacheMemUsage |resource_monitor |Bytes(SI) |Amount of memory used by the file system cache. |
|network input traffic |NetworkReceiveThroughput |resource_monitor |Bytes/Second(SI) |Input traffic counted by the PostgreSQL kernel. |
|network output traffic |NetworkTransmitThroughput |resource_monitor |Bytes/Second(SI) |Output traffic counted by the PostgreSQL kernel. |
|Disk usage |DiskUsage |resource_monitor |Bytes(SI) |The total amount of disk space used. |
|Data file disk usage |BaseDiskUsage |resource_monitor |Bytes(SI) |The disk size occupied by the data resource in the PostgreSQL instance. |
|WAL log disk usage |WalDiskUsage |resource_monitor |Bytes(SI) |The disk space occupied by the WAL logs in the PostgreSQL instance. |
|run log disk usage |LogDiskUsage |resource_monitor |Bytes(SI) |The disk size occupied by the running logs in the PostgreSQL instance, including error logs and slow logs, is used as the source of audit data. |
|Temporary file disk usage |TempFileDiskUsage |resource_monitor |Bytes(SI) |The size of the disk occupied by the pgsql_tmp directory in the PostgreSQL instance. The pgsql_tmp directory is used to store the temporary data generated during the execution of SQL. |
|Maximum WAL log accumulation in replication slots |SlotMaxWALAccumulation<br><br> |resource_monitor |Bytes(SI) |The maximum amount of WAL logs accumulated in all replication slots. |
|Disk read\-write state<br><br> |DiskReadWriteStatus |resource_monitor |Count |Current disk read\-write status, 0 means read\-write, otherwise it is not 0. |
|Database size<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only used to configure alarm strategies and does not provide dashboard display.</div><br> |DBSize |resource_monitor |Bytes(SI) |The disk space occupied by the data resources in the database. |
|Database bloat rate<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only used to configure alarm strategies and does not provide dashboard display.</div><br> |DBExpansionRate |resource_monitor |Bytes/Second(SI) |The rate at which the disk space used by data resources in the database bloats. |
|Inactive transactions<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only used to configure alarm strategies and does not provide dashboard display.</div><br> |InactiveSlotCount |resource_monitor |None |The number of replication slots that are inactive. |
|Size of the largest table in the database<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only used to configure alarm strategies and does not provide dashboard display.</div><br> |DBMaxTableSize |resource_monitor |Bytes(SI) |The size of the largest table in the database. |
|TPS |TPS |engine_monitor |Count/Second |The number of transactions processed per second in a PostgreSQL instance. |
|Connection utilization |ConnectionUsedUtil |engine_monitor |Percent |The percentage of the maximum number of connections used by all connections for the current instance. |
|Total connections |TotalConnection |engine_monitor |Count |The number of all connections to the current instance, both active and inactive. |
|Slow queries per second |SlowQueries |engine_monitor |Count/Second |The number of queries per second that take longer than the duration set by the log_min_duration_statement parameter. |
|Slow queries per 30 seconds |SlowQueriesIncrement |engine_monitor |Count |The number of queries per 30 seconds that exceeded the duration set by the log_min_duration_statement parameter. |
|Slow queries in the last n seconds |SlowQueriesCustomIncrement |engine_monitor |Count |The number of slow queries that occurred in the past n seconds. The value of n can be adjusted by modifying the running value of the parameter slow_query_custom_count_range. |
|Instantaneous slow queries |InstantaneousSlowQueries |engine_monitor |Count |The number of slow queries currently queried from the kernel that take longer than the query duration set by the log_min_duration_statement parameter. |
|Error queries per second |ErrorQueries |engine_monitor |Count/s |The number of queries with errors per second. |
|Incremental trend of error queries every 30 seconds |ErrorQueriesIncrement |engine_monitor |Count |The number of erroneous queries that occur within every 30 seconds. |
|Rows inserted per second |RowsInserted |engine_monitor |Count/Second |Number of rows inserted per second. |
|Rows deleted per second |RowsDeleted |engine_monitor |Count/Second |The number of rows deleted per second. |
|RowsUpdated |RowsUpdated |engine_monitor |Count/Second |The number of rows updated per second. |
|Current active connections |ActiveConnection |engine_monitor |Count |Total number of client processes currently executing in the database. |
|Free connections |IdleConnection |engine_monitor |Count |Total number of client side processes requested but not used in the current database. |
|Inactive transactions |IdleInTxnConnection |engine_monitor |Count |The total number of unused client threads in the current database transaction. |
|Transaction commits per second |CommitsPerSecond |engine_monitor |Count/Second |The number of times transactions are committed per second in a PostgreSQL instance. |
|Transaction rollbacks per second |RollbacksPerSecond |engine_monitor |Count/Second |The number of times transactions are rolled back per second in a PostgreSQL instance. |
|Longest transaction execution time |LongestTransactionExecTime |engine_monitor |Second |The longest statement execution time among the currently executing queries. |
|Queries with lock wait times exceeding 1 hour |LocksUngrantedCountOver1h |engine_monitor |Count |The number of queries in the PostgreSQL instance that have been waiting for locks for more than one hour. |
|2pc transactions |PreparedXactsCount |engine_monitor |Count |The number of open two\-phase commit transactions in the database. |
|Maximum duration of a 2pc transaction |OldestPreparedXactsDuration |engine_monitor |Second |The maximum duration of a two\-phase transaction. |
|Database maximum age XIDs |DbMaxAgeXids<br><br> |engine_monitor |None |The maximum age of the database in the current instance. If the value is too large, it will cause the transaction to be rolled back, and the instance cannot be written during the transaction rollback. |
|Global read\-only state<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only used to configure alarm strategies and does not provide dashboard display.</div><br> |ReadOnlyStatus |engine_monitor |None |Whether the current instance has enabled global read\-only parameters and is in a non\-writable state. |
|Locks waiting to be released<br><br> |LocksUngrantedCount |engine_monitor |Count |The number of locks waiting to be released in the database. |
|Lock holdings<br><br> |LocksGrantedCount |engine_monitor |Count |The number of locks that have been granted for the database. |
|Database deadlocks<br><br> |DeadLocksCount |engine_monitor |Count |The current number of deadlocks in the database. |
|Cache hits per second |SharedBuffersBlksHit |engine_monitor |Count/Second |The number of times a disk block was found in the buffer without a disk read, in database. |
|Cache hit rate |SharedBuffersBlksHitRate |engine_monitor |Percent |The percentage of times that disk blocks were found in the buffer. |
|Ratio of data return to scan<br><br> |DBFetchedReturnedRatio |engine_monitor |Percent |The database returns the ratio of the number of rows (tup_fetched) to the number of rows scanned (tup_returned). The larger the value, the more valid data is returned; the smaller the value, the more likely there is SQL that is not using an index. |
|Watches per second |RowsFetched |engine_monitor |Count/Second |The number of times the index matches the item. |
|Rows scanned per second |RowsReturned |engine_monitor |Count/Second |The number of rows scanned per second of the Heap table/Index table. |
|Transaction success rate |TransactionSuccessRate |engine_monitor |Percent |Transaction success rate per second. |
|Replication delay |ReplicationDelay |deploy_monitor |Second |The delay time of primary\-secondary replication. |
|The number of transaction conflicts per second. |DBConflicts |deploy_monitor |Count/Second |The number of transaction conflicts per second. |
|Primary\-Secondary writeLag<br><br> |ReplicationWriteLag |deploy_monitor |Second |The delay between when the primary server's WAL records have been flushed to disk and when the secondary server receives the WAL data but has not yet written it to its own operating system cache. |
|Primary\-Secondary flushLag<br><br> |ReplicationFlushLag |deploy_monitor |Second |The delay during which WAL on the primary has been sent to the secondary, but the standby has not yet flushed (fsynced) it to its own disk. |
|WAL files to be archived |UnarchivedWALSegmentsCount |deploy_monitor |Count |The number of WAL files that are in the ready state but have not yet been archived. |
|Proxy QPS |ProxyQPS |proxy_monitor |Count/Second |The number of SQLs executed per second by the database (including INSERT, SELECT, UPDATE, and DELETE). |
|Proxy CPU utilization |ProxyCPUUtil |proxy_monitor |Percent |The CPU utilization of the proxy node. |
|Proxy memory utilization |ProxyMemUtil |proxy_monitor |Percent |The memory utilization of the proxy node. |
|Proxy connections |ProxyConnection |proxy_monitor |Count |The number of open connections. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For setting <code>log_min_duration_statement</code> parameters, see <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_parameters">Modifying parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">If there are no monitoring indicators of <code>User mode CPU usage</code> and <code>System state CPU usage</code> in the monitoring board of your instance, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000179">submit a ticket</a> to apply for an upgrade of the instance version.</div>
