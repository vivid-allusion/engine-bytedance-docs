---
title: "Monitoring metrics"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics"
---

This topic describes the monitoring items supported by RDS for MySQL and related information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For easier viewing, the RDS for MySQL monitoring dashboard automatically adjusts the unit of measurement based on the data volume. The actual unit displayed on the dashboard prevails. For example, when the InnoDB read volume is high, the unit changes from Byte/s to KB/s. If the read volume increases further, the unit changes to MB/s.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query each monitoring indicator data and alarm information. When calling the query interface, you need to obtain the Namespace of the product, the SubNamespace to which the index to be queried belongs, and the MetricName of the index to be queried. The Namespace for RDS for MySQL is <code>VCM_RDS_MySQL</code>. The MetricName and SubNamespace for each metric are provided in the list of monitoring items below.</div>


* <div data-tips="true" data-tips-type="tip">You can also obtain details about each monitoring indicator in <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_RDS_MySQL">Querying monitoring indicators for RDS for MySQL</a>.</div>



<span id=".55uR5o6n6aG55YiX6KGo"></span>
## List of monitoring items

RDS for MySQL provides new monitoring items that allow you to view monitoring information at the instance and node levels under the resource monitoring, deployment monitoring, and engine monitoring categories. To use it, refer to [List of monitoring items that support multi-dimensional viewing](https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics#.5a6e5L6LLeiKgueCueWPjOe7tOW6puebkeaOp-mhueWIl-ihqA==). The original monitoring items, which only support instance\-level monitoring, are still available. Refer to [List of monitoring items that only support the instance dimension](https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics#xTqFWMdY) for related information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If your instance does not support viewing monitoring information from node dimensions for resource monitoring, deployment monitoring, and engine monitoring, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to apply for an upgrade of your instance version.</div>


* <div data-tips="true" data-tips-type="tip">The new monitoring items provide all the information that the old items do. As support for the old items will be gradually discontinued, you should use the new monitoring items and migrate any business logic that relies on the old ones.</div>


* <div data-tips="true" data-tips-type="tip">For instances of MySQL 8.4.7_20260415, MySQL 8.0.43_20251015,  MySQL 5.7.44_20251015, and later versions, RDS for MySQL provides 5\-second monitoring for some monitoring items. For a list of supported items, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/monitoring_metrics#.5a6e5L6LLeiKgueCueWPjOe7tOW6puebkeaOp-mhueWIl-ihqA==">List of monitoring items that support multi\-dimensional viewing</a>. This feature is currently in beta testing by invitation only. To use it for free, apply by <a href="https://console.byteplus.com/workorder/create/">submitting a ticket</a>. If this capability is charged in the future, RDS for MySQL will announce the billing details one month in advance.</div>



<span id=".5a6e5L6LLeiKgueCueWPjOe7tOW6puebkeaOp-mhueWIl-ihqA=="></span>
### List of monitoring items that support multi\-dimensional viewing


|Monitoring Metrics |Name |MetricName |Subnamespace |Unit |Description of indicators |Supported viewing dimensions |Whether to support a 5\-second aggregation cycle |
|---|---|---|---|---|---|---|---|
|CPU utilization |CPU utilization |CpuUtil |resource_monitor_new |Percent |CPU utilization. |Instance & Node |Yes<br><br> |
|Memory utilization |Memory utilization |MemUtil |resource_monitor_new |Percent |Memory utilization. |Instance & Node |Yes<br><br> |
|Disk utilization |Disk utilization |DiskUtil |resource_monitor_new |Percent |Disk space used/Purchased instance space first. |Instance & Node |No |
|network input traffic |network input traffic |NetworkReceiveThroughput |resource_monitor_new |Byte/s |Number of bytes received per second first. |Instance & Node |Yes |
|Network output traffic |Network output traffic |NetworkTransmitThroughput |resource_monitor_new |Byte/s |Number of bytes sent per second. |Instance & Node |No |
|IOPS usage rate |IOPS usage rate |IOPS |resource_monitor_new |Count/s |IOPS utilization. |Instance & Node |No |
|Total disk usage |\- |DiskUsageBytes |resource_monitor_new |Bytes |Total disk usage.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports creating alarm strategies and does not provide a dashboard display.</div><br> |None. |No |
|Total disk usage |Total disk usage |TotalDiskUsageBytes |resource_monitor_new |Bytes |Total disk usage. |Instance & Node |No |
|Slow log usage |Slow log usage |ErrLogUsageBytes |resource_monitor_new |Bytes |Disk usage of the slow log. |Instance & Node |No |
|Error log usage |Error log usage |ErrLogUsageBytes |resource_monitor_new |Bytes |Disk usage of the error log. |Instance & Node |No |
|Binlog usage |Binlog usage |BinlogUsageBytes |resource_monitor_new |Bytes |Binlog disk usage |Instance & Node |No |
|Redo log usage |Redo log usage |RedoLogUsageBytes |resource_monitor_new |Bytes |Disk usage of the redo log. |Instance & Node |No |
|Undo log usage |Undo log usage |UndoLogUsageBytes |resource_monitor_new |Bytes |Disk usage of the undo log first. |Instance & Node |No |
|Relay log usage |Relay log usage |RelayLogUsageBytes |resource_monitor_new |Bytes |Relay log disk usage |Instance & Node |No |
|System data usage |System data usage |SystemDataUsageBytes |resource_monitor_new |Bytes |Disk usage of system data. |Instance & Node |No |
|User data usage |User data usage |UserDataUsageBytes |resource_monitor_new |Bytes |Disk usage of user data |Instance & Node |No |
|Audit log usage |Audit log usage |AuditLogUsageBytes |resource_monitor_new |Bytes |Disk usage of the audit log. |Instance & Node |No |
|Temporary file usage |Temporary file usage |TempFileUsageBytes |resource_monitor_new |Bytes |Temporary file disk usage. |Instance & Node |No |
|Other log usage |Other log usage |OtherUsageBytes |resource_monitor_new |Bytes |Disk usage of other logs. |Instance & Node |No |
|ReplacationDelay |Slave replication latency |ReplicationDelay |deploy_monitor_new |Second |Primary\-secondary delay time. |Instance & Node |Yes |
|TPS |TPS |ProxyTPS |proxy_monitor |Count |The number of transactions received by the database proxy service of the instance per second. Transactions include successfully committed transactions, failed rolled\-back transactions, and single requests without explicit transactions. |Instance |No |
|QPS |QPS |ProxyQPS |proxy_monitor |Count |The number of requests that the database proxy of the instance receives per second. |Instance |No |
|Connections |Connections |ProxyConnection |proxy_monitor |Count |The number of connections for the database proxy service of the proxy instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After MySQL reaches its max connections, the number of proxy connections is greater than the number of MySQL connections, with the proxy's max connections being twice that of MySQL.</div><br> |Instance |No |
|CPU utilization |CPU utilization |ProxyCpuUtil |proxy_monitor |Percent |CPU usage rate of the database proxy service of the instance first. |Instance |No |
|Memory utilization |Memory utilization |ProxyMemUtil |proxy_monitor |Percent |Memory usage rate of the instance database proxy service. |Instance |No |
|Connection rate |Connection rate |ProxyNewConnections |proxy_monitor |Count/Second |Connection rate for the instance Database proxy. |Instance |No |
|Inbound traffic |Inbound traffic |ProxyFlowInBytes |proxy_monitor |Count |Total inbound traffic received by the database proxy service of the instance. |Instance |No |
|Outbound traffic |Outbound traffic |ProxyFlowOutBytes |proxy_monitor |Count |The outbound traffic of the database proxy service for the instance. |Instance |No |
|Total number of requests |Total requests |ProxyRequestNum |proxy_monitor |Count/Second |Total number of requests for the instance database proxy service. |Instance |No |
|Number of read requests |Number of read requests |ProxyReadReqestNum |proxy_monitor |Count/Second |Number of read requests for the instance Database proxy service first. |Instance |No |
|Write requests |Write requests |ProxyWriteRequestNum |proxy_monitor |Count/Second |Number of write requests for the instance database proxy service. |Instance |No |
|Connection utilization |\- |ProxyConnectionUsage |proxy_monitor |Percent |Proxy connection usage rate.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports creating alarm strategies and does not provide a dashboard display.</div><br> |None. |No |
|Connection utilization |Database proxy connection utilization |ProxyEndpointUsedConnRatio |proxy_monitor |Percent |Connection usage rate of the proxy endpoint. |Endpoint |No |
|Endpoint connections |Connections |ProxyEndpointConnection |proxy_monitor |Count |Proxy endpoint connections. |Endpoint |No |
|Endpoint TPS |TPS |ProxyEndpointTPS |proxy_monitor |Count |Number of transactions received per second by the proxy endpoint. |Endpoint |No |
|Endpoint QPS |QPS |ProxyEndpointQPS |proxy_monitor |Count |Number of requests received per second by the proxy endpoint. |Endpoint |No |
|Endpoint connection rate |Connection rate |ProxyEndpointNewConnections |proxy_monitor |Count/Second |Connection rate of the proxy endpoint. |Endpoint |No |
|Total endpoint request count |Total requests |ProxyEndpointRequestNum |proxy_monitor |Count/Second |Total number of requests for the proxy endpoint |Endpoint |No |
|Endpoint read requests |Number of read requests |ProxyEndpointReadReqNum |proxy_monitor |Count/Second |Number of read requests for the proxy endpoint. |Endpoint |No |
|Endpoint write requests |Write requests |ProxyEndpointWriteReqNum |proxy_monitor |Count/Second |Number of write requests for the Proxy endpoint. |Endpoint |No |
|Endpoint inbound traffic |Inbound traffic |ProxyEndpointFlowInBytes |proxy_monitor |Byte/Second |Inbound traffic of the proxy endpoint. |Endpoint |No |
|Endpoint egress traffic |Outbound traffic |ProxyEndpointFlowOutBytes |proxy_monitor |Byte/Second |Outbound traffic of the proxy endpoint. |Endpoint |No |
|Slow queries |Slow queries |SlowQueries |engine_monitor_new |Count/Second |Number of queries exceeding long_query_time Second |Instance & Node |No |
|Number of full table scans |Number of full table scans |SelectScan |engine_monitor_new |Count/Second |The number of queries that performed a full table Search |Instance & Node |Yes |
|Query Count |Query Count |OperationSelect |engine_monitor_new |Count/Second |QPS |Instance & Node |Yes |
|Updates |Updates |OperationUpdate |engine_monitor_new |Count/Second |Updates per second. |Instance & Node |No |
|Deleted count |Deleted count |OperationDelete |engine_monitor_new |Count/Second |Deletions per second. |Instance & Node |Yes |
|Insert count |Insert count |OperationInsert |engine_monitor_new |Count/Second |Number of INSERT requests per Second. |Instance & Node |Yes |
|Coverage count |Coverage count |OperationReplace |engine_monitor_new |Count/Second |Overwrites Per Second. |Instance & Node |No |
|Submit count |Submit count |OperationCommit |engine_monitor_new |Count/Second |Number of submits per second. |Instance & Node |Yes |
|Rollback count |Rollback count |OperationRollback |engine_monitor_new |Count/Second |Rollbacks per second first. |Instance & Node |Yes |
|Requests per second |Number of MySQL requests per second |QPS |engine_monitor_new |Count/Second |The quantity of queries sent by the MySQL client to MySQL per second, including queries within stored procedures. This metric counts COM_STMT_PREPARE, COM_STMT_CLOSE, and COM_STMT_RESET. |Instance & Node |Yes |
|TPS |TPS |TPS |engine_monitor_new |Count/Second |TPS (including succeeded transactions and failed rollback transactions). |Instance & Node |Yes |
|Number of Insert_Select |Insert select executions per Second |InsertSelect |engine_monitor_new |Count/Second |The average number of Insert_Select statements executed per second. |Instance & Node |No |
|Current number of open connections |Current number of open connections |ThreadsConnected |engine_monitor_new |Count |The number of currently open connections. |Instance & Node |Yes |
|Number of created threads |Number of created threads |ThreadsCreated |engine_monitor_new |Count |Number of threads created to handle connections. |Instance & Node |Yes |
|Running thread count |Running thread count |ThreadsRunning |engine_monitor_new |Count |The count of threads that are active and not in sleep state. |Instance & Node |No |
|Connection utilization percentage |MySQL connection usage rate |ConnUsage |engine_monitor_new |Percent |MySQL connection utilization ratio. |Instance & Node |Yes |
|Number of abnormally closed client connections |Number of abnormally closed client connections |AbortedClients |engine_monitor_new |Count |Number of connections aborted because the client terminated without closing the connection properly |Instance & Node |Yes |
|Number of failed connections |Number of failed connections |AbortedConnects |engine_monitor_new |Count |The number of failed attempts to connect to the MySQL server. |Instance & Node |Yes |
|Connections blocked by MDL lock |Connections waiting for an MDL lock |waitMDLConns |engine_monitor_new |Count |Connections blocked by MDL lock |Instance & Node |No |
|Number of transactions not submitted for more than 30 seconds |Number of transactions not submitted for more than 30 seconds |TrxOver30sAndSleep |engine_monitor_new |Count |Number of transactions in a sleep state that have been open for over 30 seconds first. |Instance & Node |No |
|Number of transactions that timed out after 1 minute and were not submitted |Number of transactions that timed out after 1 minute and were not submitted |TrxOver1mAndSleep |engine_monitor_new |Count |Number of transactions in a sleep state for over 1 minute and not closed first. |Instance & Node |Yes |
|Quantity of uncommitted transactions with a timeout of over 30 minutes |Quantity of uncommitted transactions with a timeout of over 30 minutes |TrxOver30mAndSleep |engine_monitor_new |Count |Number of transactions in a sleep State that have not been closed for more than 30 minutes. |Instance & Node |No |
|Quantity of large transactions with an execution time of more than 30 minutes |Quantity of large transactions with an execution time of more than 30 minutes |TrxOver30m |engine_monitor_new |Count |The number of large transactions with an execution time of more than 30 minutes. |Instance & Node |No |
|Quantity of large transactions with an execution time exceeding 1 hour |Quantity of large transactions with an execution time exceeding 1 hour |TrxOver1h |engine_monitor_new |Count |Quantity of large transactions with an execution time exceeding 1 hour. |Instance & Node |No |
|Quantity of large transactions exceeding 24 hours |Quantity of large transactions exceeding 24 hours |TrxOver24h |engine_monitor_new |Count |Number of large transactions with an execution time of more than 24 hours. |Instance & Node |No |
|Temporary table quantity |Temporary table quantity |CreatedTmpTables |engine_monitor_new |Count/Second |Quantity of temporary tables created |Instance & Node |No |
|Number of table lock waits |Number of table lock waits |TableLocksWaited |engine_monitor_new |Count/Second |The number of times that table locks could not be obtained Now |Instance & Node |Yes |
|Open tables |Number of open tables |OpenedTables |engine_monitor_new |Count |Number of open tables. |Instance & Node |No |
|Number of open files |Open file count |OpenFiles |engine_monitor_new |Count |Number of open files. |Instance & Node |Yes |
|Innodb cache hit rate |Innodb cache hit rate |InnodbCacheHitRate |engine_monitor_new |Percent |The cache hit rate of the InnoDB Engine. |Instance & Node |Yes |
|Innodb cache usage rate |Innodb cache usage rate |InnodbCacheUtil |engine_monitor_new |Percent |InnoDB Engine cache usage rate first. |Instance & Node |Yes |
|Innodb read volume |Innodb read volume |InnodbDataRead |engine_monitor_new |Byte/s |The number of bytes of data read by the InnoDB Engine per second |Instance & Node |No |
|Innodb write volume |Innodb write volume |InnodbDataWritten |engine_monitor_new |Byte/s |The number of bytes of data written by the InnoDB engine per second. |Instance & Node |Yes |
|Innodb reads |Innodb reads |InnodbDataReadCounts |engine_monitor_new |Count/Second |Number of data reads completed by the InnoDB Engine per second. |Instance & Node |Yes |
|Number of Innodb writes |Innodb writes |InnodbDataWriteCounts |engine_monitor_new |Count/Second |The number of writes completed by the InnoDB Engine per second. |Instance & Node |No |
|Number of InnoDB tables currently open |Number of InnoDB tables currently open |InnodbNumOpenFiles |engine_monitor_new |Count |Current number of open tables in the InnoDB engine. |Instance & Node |Yes |
|Number of Innodb rows read |Number of Innodb rows read |InnodbDataReadBytes |engine_monitor_new |Count/Second |Number of rows read by the InnoDB Engine per second. |Instance & Node |Yes |
|Innodb rows deleted |Innodb rows deleted |InnodbRowsDeleted |engine_monitor_new |Count/Second |The number of rows deleted per second by the InnoDB engine. |Instance & Node |No |
|Innodb row insert quantity |Innodb row insert quantity |InnodbRowsInserted |engine_monitor_new |Count/Second |The number of rows inserted by the InnoDB engine per second. |Instance & Node |Yes |
|Innodb rows updated |Innodb rows updated |InnodbRowsUpdated |engine_monitor_new |Count/Second |Number of rows updated by the InnoDB engine per second. |Instance & Node |Yes |
|Average Innodb row lock obtain time |Innodb average row lock wait time |InnodbRowsLockTimeAvg |engine_monitor_new |Millisecond |Average duration of InnoDB Engine row locks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This metric is the average wait time for row locks since MySQL started. It is calculated by dividing the total wait time for row locks by the total number of row lock waits. It is not a real\-time Value and is updated only when a new row lock wait occurs. After MySQL restarts, this metric is cleared and recounted, which causes the Value to change abruptly.</div><br> |Instance & Node |No |
|Number of InnoDB row lock waits |Innodb row lock wait count |InnodbRowLockWaits |engine_monitor_new |Count/Second |The number of times the InnoDB Engine waits for row locks per second. |Instance & Node |Yes |
|InnoDB table maximum row lock wait time |InnoDB table maximum row lock wait time |InnodbRowLockTimeMax |engine_monitor_new |Millisecond |Maximum InnoDB wait time for row locks. |Instance & Node |Yes |
|Average number of physical writes to the InnoDB redo log file per second |Average number of physical writes to the InnoDB redo log file per second |InnodbLogWrites |engine_monitor_new |Count/Second |Average number of physical writes to the Redo Log File per second by InnoDB. |Instance & Node |No |
|Average number of fsync writes completed to the log file per second |Average number of fsync writes completed to the log file per second |InnodbOsLogFsyncs |engine_monitor_new |Count/Second |The average number of fsync() writes completed to the Log file per second. |Instance & Node |No |
|Average Number of Completed Fsync Writes to Data Files Per Second |InnoDB average fsync operations per second |InnodbDataFsyncs |engine_monitor_new |Count/Second |The average number of fsync() writes completed to data files per second. |Instance & Node |No |
|Redo log usage |Redo log usage |RedologSize |engine_monitor_new |MByte |Disk usage of Redo log. |Instance & Node |No |
|Slow log usage |Slow log usage |SlowLogSize |engine_monitor_new |MByte |The disk usage of the slow log. |Instance & Node |No |
|Number of temporary files |Number of temporary files |CreatedTmpFiles |engine_monitor_new |Count/Second |Number of temporary files created per second. |Instance & Node |No |
|Quantity of temporary disk tables |Quantity of temporary disk tables |CreatedTmpDiskTables |engine_monitor_new |Count/Second |The number of temporary tables created on disk per second. |Instance & Node |No |
|Number of requests to read the next row |Number of requests to read the next row |HandlerReadRndNext |engine_monitor_new |Count/Second |Number of requests to read the next row per second. |Instance & Node |No |
|Internal rollback count |Internal rollback count |HandlerRollback |engine_monitor_new |Count/Second |The number of times transactions are rolled back per second. |Instance & Node |Yes |
|Internal submit count |Internal submit count |HandlerCommit |engine_monitor_new |Count/Second |Number of transaction submits per second. |Instance & Node |No |
|Quantity of empty Innodb pages |Quantity of empty Innodb pages |InnodbBufferPoolPagesFree |engine_monitor_new |Count |Number of empty pages in the InnoDB Engine memory. |Instance & Node |Yes |
|Total Innodb pages |Total Innodb pages |TotalInnodbBufferPoolPages |engine_monitor_new |Count |Total number of memory pages occupied by the InnoDB engine. |Instance & Node |Yes |
|Innodb logical reads |Innodb logical reads |InnodbBufferPoolReadRequests |engine_monitor_new |Count/Second |The number of logical read requests that the InnoDB Engine has Completed per second. |Instance & Node |No |
|Innodb physical read |Innodb physical read |InnodbBufferPoolReads |engine_monitor_new |Count/Second |The number of physical read requests completed by the InnoDB engine per second. |Instance & Node |Yes |
|InnoDB buffer pool dirty page ratio |InnoDB buffer pool dirty page ratio |InnodbBpDirtyPct |engine_monitor_new |Percent |The ratio of dirty pages in the InnoDB buffer pool, calculated by the formula: InnoDB_buffer_pool_pages_dirty/InnoDB_buffer_pool_pages_data\* 100%. |Instance & Node |Yes |
|InnoDB Buffer Pool page flush request quantity |InnoDB Buffer Pool page flush request quantity |InnodbBufferPoolPagesFlushed |engine_monitor_new |Count/Second |Number of InnoDB Buffer Pool page flush requests. |Instance & Node |No |
|RocksDB read data volume |RocksDB disk reads<br><br> |RocksDBBytesRead |engine_monitor_new |Byte/Second |Bytes read from disk per second by the RocksDB Engine.<br><br> |Instance & Node |No |
|RocksDB write data volume |RocksDB Disk Write Volume |RocksDBBytesWritten |engine_monitor_new |Byte/Second |The number of bytes written to disk per second by the RocksDB engine.<br><br> |Instance & Node |No |
|RocksDB read cache amount |RocksDB read cache amount |RocksDBBlockCacheBytesRead |engine_monitor_new |Byte/Second |Data volume read from Cache by the RocksDB engine. |Instance & Node |No |
|RocksDB write cache amount |RocksDB write cache amount |RocksDBBlockCacheBytesWrite |engine_monitor_new |Byte/Second |Data volume written to the cache by the RocksDB engine. |Instance & Node |No |
|RocksDB WAL write volume |RocksDB WAL log write size |RocksDBWalLogCapacity |engine_monitor_new |Byte/Second |Data volume written to the WAL log by the RocksDB engine<br><br> |Instance & Node |No |


<span id="xTqFWMdY"></span>
### List of monitoring items that only support the instance dimension


|Monitoring Metrics |Name |**MetricName** |**Subnamespace** |**Unit** |**Description of indicators** |
|---|---|---|---|---|---|
|CPU utilization |CPU utilization |CpuUtil |resource_monitor |Percent |CPU utilization. |
|Memory utilization |Memory utilization |MemUtil |resource_monitor |Percent |Memory utilization. |
|Disk utilization |Disk utilization |DiskUtil |resource_monitor |Percent |Disk space used/Purchased instance space first. |
|network input traffic |network input traffic |NetworkReceiveThroughput |resource_monitor |Byte/s |Number of bytes received per second first. |
|Network output traffic |Network output traffic |NetworkTransmitThroughput |resource_monitor |Byte/s |Number of bytes sent per second. |
|IOPS |IOPS |IOPS |resource_monitor |Count/s |IOPS。 |
|Disk usage |Disk usage |DiskUsageBytes |resource_monitor |Bytes |Disk usage. |
|ReplacationDelay |Slave replication latency |ReplicationDelay |deploy_monitor |Second |Primary\-secondary delay time. |
|TPS |TPS |ProxyTPS |proxy_monitor |Count |The number of transactions the Proxy receives per Second. Transactions include successfully committed transactions, failed rolled\-back transactions, and single requests without explicit transactions. |
|QPS |QPS |ProxyQPS |proxy_monitor |Count |Number of requests received by the proxy per second. |
|Connections |Connections |ProxyConnection |proxy_monitor |Count |Proxy connection count.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After MySQL reaches its max connections, the number of proxy connections is greater than the number of MySQL connections, with the proxy's max connections being twice that of MySQL.</div><br> |
|CPU utilization |CPU utilization |ProxyCpuUtil |proxy_monitor |Percent |The CPU usage rate of the database proxy. |
|Memory utilization |Memory utilization |ProxyMemUtil |proxy_monitor |Percent |Proxy memory usage rate |
|Connection utilization |Database proxy connection utilization |ProxyConnectionUsage |proxy_monitor |Percent |Proxy connection usage rate. |
|Slow queries |Slow queries |SlowQueries |engine_monitor |Count/Second |Number of queries exceeding `long_query_time` Second |
|Number of full table scans |Number of full table scans |SelectScan |engine_monitor |Count/Second |The number of queries that performed a full table Search |
|Updates |Updates |OperationUpdate |engine_monitor |Count/Second |Updates per second. |
|Deleted count |Deleted count |OperationDelete |engine_monitor |Count/Second |Deletions per second. |
|Insert count |Insert count |OperationInsert |engine_monitor |Count/Second |Number of `INSERT` requests per Second. |
|Coverage count |Coverage count |OperationReplace |engine_monitor |Count/Second |Overwrites Per Second. |
|Submit count |Submit count |OperationCommit |engine_monitor |Count/Second |Number of submits per second. |
|Rollback count |Rollback count |OperationRollback |engine_monitor |Count/Second |Rollbacks per second first. |
|Requests per second |Number of MySQL requests per second |QPS |engine_monitor |Count/Second |The quantity of queries sent by the MySQL client to MySQL per second, including queries within stored procedures. This metric counts `COM_STMT_PREPARE`, `COM_STMT_CLOSE`, and `COM_STMT_RESET`. |
|TPS |TPS |TPS |engine_monitor |Count/Second |TPS (including succeeded transactions and failed rollback transactions). |
|Insert_Selects per second |Average number of insert select executions per second |InsertSelect |engine_monitor |Count/Second |The average number of `Insert_Select` statements executed per second. |
|Current number of open connections |Current number of open connections |ThreadsConnected |engine_monitor |Count |The number of currently open connections. |
|Number of created threads |Number of created threads |ThreadsCreated |engine_monitor |Count |Number of threads created to handle connections. |
|Running thread count |Running thread count |ThreadsRunning |engine_monitor |Count |The count of threads that are active and not in sleep state. |
|Connection utilization percentage |MySQL connection usage rate |ConnUsage |engine_monitor |Percent |MySQL connection utilization ratio. |
|Temporary table quantity |Temporary table quantity |CreatedTmpTables |engine_monitor |Count/Second |Quantity of temporary tables created |
|Number of table lock waits |Number of table lock waits |TableLocksWaited |engine_monitor |Count/Second |The number of times that table locks could not be obtained Now |
|Open tables |Number of open tables |OpenedTables |engine_monitor |Count |Number of opened tables. |
|Number of open files |Open file count |OpenFiles |engine_monitor |Count |Number of open files. |
|Innodb cache hit rate |Innodb cache hit rate |InnodbCacheHitRate |engine_monitor |Percent |The cache hit rate of the InnoDB Engine. |
|Innodb cache usage rate |Innodb cache usage rate |InnodbCacheUtil |engine_monitor |Percent |InnoDB Engine cache usage rate first. |
|Innodb read volume |Innodb read volume |InnodbDataRead |engine_monitor |Byte/s |The number of bytes of data read by the InnoDB Engine per second |
|Innodb write volume |Innodb write volume |InnodbDataWritten |engine_monitor |Byte/s |The number of bytes of data written by the InnoDB engine per second. |
|Innodb reads |Innodb reads |InnodbDataReadCounts |engine_monitor |Count/Second |Number of data reads completed by the InnoDB Engine per second. |
|Number of Innodb writes |Innodb writes |InnodbDataWriteCounts |engine_monitor |Count/Second |The number of writes completed by the InnoDB Engine per second. |
|Number of InnoDB tables currently open |Number of InnoDB tables currently open |InnodbNumOpenFiles |engine_monitor |Count |Current number of open tables in the InnoDB engine. |
|Number of Innodb rows read |Number of Innodb rows read |InnodbDataReadBytes |engine_monitor |Count/Second |Number of rows read by the InnoDB Engine per second. |
|Innodb rows deleted |Innodb rows deleted |InnodbRowsDeleted |engine_monitor |Count/Second |The number of rows deleted per second by the InnoDB engine. |
|Innodb row insert quantity |Innodb row insert quantity |InnodbRowsInserted |engine_monitor |Count/Second |The number of rows inserted by the InnoDB engine per second. |
|Innodb rows updated |Innodb rows updated |InnodbRowsUpdated |engine_monitor |Count/Second |Number of rows updated by the InnoDB engine per second. |
|Average Innodb row lock obtain time |Innodb average row lock wait time |InnodbRowsLockTimeAvg |engine_monitor |Millisecond |Average duration of InnoDB Engine row locks.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This metric is the average wait time for row locks since MySQL started. It is calculated by dividing the total wait time for row locks by the total number of row lock waits. It is not a real\-time Value and is updated only when a new row lock wait occurs. After MySQL restarts, this metric is cleared and recounted, which causes the Value to change abruptly.</div><br> |
|Number of InnoDB row lock waits |Innodb row lock wait count |InnodbRowLockWaits |engine_monitor |Count/Second |The number of times the InnoDB Engine waits for row locks per second. |
|InnoDB table maximum row lock wait time |InnoDB table maximum row lock wait time |InnodbRowLockTimeMax |engine_monitor |Millisecond |Maximum InnoDB wait time for row locks. |
|Average number of physical writes to the InnoDB redo log file per second |Average number of physical writes to the InnoDB redo log file per second |InnodbLogWrites |engine_monitor |Count/Second |Average number of physical writes to the Redo Log File per second by InnoDB. |
|Average number of fsync writes completed to the log file per second |Average number of fsync writes completed to the log file per second |InnodbOsLogFsyncs |engine_monitor |Count/Second |The average number of `fsync()` writes completed to the Log file per second. |
|Average Number of Completed Fsync Writes to Data Files Per Second |InnoDB average fsync operations per second |InnodbDataFsyncs |engine_monitor |Count/Second |The average number of `fsync()` writes completed to data files per second. |
|Redo log usage |Redo log usage |RedologSize |engine_monitor |MByte |Disk usage of Redo log. |
|Slow log usage |Slow log usage |SlowLogSize |engine_monitor |MByte |The disk usage of the slow log. |
|Number of temporary files |Number of temporary files |CreatedTmpFiles |engine_monitor |Count/Second |Number of temporary files created per second. |
|Quantity of temporary disk tables |Quantity of temporary disk tables |CreatedTmpDiskTables |engine_monitor |Count/Second |The number of temporary tables created on disk per second. |
|Number of requests to read the next row |Number of requests to read the next row |HandlerReadRndNext |engine_monitor |Count/Second |Number of requests to read the next row per second. |
|Internal rollback count |Internal rollback count |HandlerRollback |engine_monitor |Count/Second |The number of times transactions are rolled back per second. |
|Internal submit count |Internal submit count |HandlerCommit |engine_monitor |Count/Second |Number of transaction submits per second. |
|Quantity of empty Innodb pages |Quantity of empty Innodb pages |InnodbBufferPoolPagesFree |engine_monitor |Count |Number of empty pages in the InnoDB Engine memory. |
|Total Innodb pages |Total Innodb pages |TotalInnodbBufferPoolPages |engine_monitor |Count |Total number of memory pages occupied by the InnoDB engine. |
|Innodb logical reads |Innodb logical reads |InnodbBufferPoolReadRequests |engine_monitor |Count/Second |The number of logical read requests that the InnoDB Engine has Completed per second. |
|Innodb physical read |Innodb physical read |InnodbBufferPoolReads |engine_monitor |Count/Second |The number of physical read requests completed by the InnoDB engine per second. |
|InnoDB buffer pool dirty page ratio |InnoDB buffer pool dirty page ratio |InnodbBpDirtyPct |engine_monitor |Percent |The ratio of dirty pages in the InnoDB buffer pool, calculated by the formula: `InnoDB_buffer_pool_pages_dirty/InnoDB_buffer_pool_pages_data* 100%`. |
|InnoDB Buffer Pool page flush request quantity |InnoDB Buffer Pool page flush request quantity |InnodbBufferPoolPagesFlushed |engine_monitor |Count/Second |Number of InnoDB Buffer Pool page flush requests. |


<span id="s7mZdEYF"></span>
## Alert policy configuration recommendations

We recommend that you configure trigger conditions for the following resource\-level monitoring items in your alert policy as shown in the table below.


|MetricName |Subnamespace |**Number of continuous cycles** |**Statistical method** |**Recommended threshold** |
|---|---|---|---|---|
|CPU utilization |CpuUtil |3 |Average value |\> 80% |
|System data usage |SystemDataUsageBytes |3 |Average value |\> 80% |
|User data usage |UserDataUsageBytes |3 |Average value |\> 80% |
|Memory utilization |MemUtil |3 |Average value |\> 90% |
