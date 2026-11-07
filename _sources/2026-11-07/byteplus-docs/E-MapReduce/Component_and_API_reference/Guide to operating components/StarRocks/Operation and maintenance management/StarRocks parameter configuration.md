---
title: "StarRocks parameter configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/StarRocks_parameter_configuration"
---

This article introduces some configuration items and modification methods for StarRocks FE, BE, Broker, and system parameters.

<span id="_1-背景信息"></span>
## **Context**

StarRocks configuration items are divided into dynamic parameters and static parameters:


* Dynamic parameters mainly refer to some dynamic configurations of FE, which support online modification.

* Static parameters are configuration items that require a service restart to take effect, including static parameters of FE and all configuration items of BE.


<span id="_1-1-动态参数"></span>
### Dynamic parameters

Dynamic parameters are parameters that do not require a service restart. They can be modified dynamically using the following commands or through the web interface.

```plain
ADMIN SET FRONTEND CONFIG ("key" = "value");
```


<span id="_1-2-静态参数"></span>
### Static parameters

Static parameters must be modified through the web interface, and a service restart is required for the changes to take effect.


1. Go to the cluster interface's **Service List** \> **StarRocks Service** \> **Service Parameters** page.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_840bb3b5c40b186b1b122a5ae84871f5.png) </span>


2. In the search box at the top left, search for the corresponding configuration item. If you find the parameter, you can modify its value in the parameter value input box below. After modification, EMR will detect the parameter change and immediately prompt you to Save the parameter change.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eafd4d52b86c65b54be17c0b96b86434.png) </span>


3. If the corresponding parameter cannot be found in the search box, you can click the **Add Custom Parameter** button above the search box to add a custom parameter. In **Configuration File** , select FE or BE. For **Scope** , generally select **Component Scope**. In **Component**, select the corresponding component name. Finally, enter the parameter in **Parameter Name** and fill in the parameter value in **Parameter Value**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_87ad32a0a97771a7c3fd9d44c900239e.png) </span>


4. Whether modifying an existing parameter or adding a new parameter, only the parameter record is changed and it does not take effect immediately. A cluster node restart is required for the changes to take effect. Simply follow the cluster prompt to restart the corresponding main node.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e2c721725f4ffc131b8a86afed30f0ee.png) </span>

<span id="_2-fe动态参数"></span>
## **FE dynamic parameters**

<span id="_2-1-log相关配置"></span>
### **LOG\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|qe_slow_log_ms |5000 |Duration for identifying a slow query, Unit: ms. |


<span id="_2-2-元数据与集群管理相关配置"></span>
### **Metadata and cluster management\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|catalog_try_lock_timeout_ms |5000 |Timeout duration for acquiring Catalog Lock, Unit: ms. |
|edit_log_roll_num |50000 |Split size for Image log. |
|ignore_unknown_log_id |FALSE |Whether to ignore unknown logID:<br><br><br>* TRUE: FE will ignore these unknown logIDs.<br><br>* FALSE: For unknown logIDs, FE will exit the process. When FE rolls back to a lower version, there may be logIDs that the lower version BE cannot recognize. |
|ignore_meta_check |FALSE |Whether to ignore cases where metadata is lagging:<br><br><br>* FALSE: Ignore.<br><br>* TRUE: Do not ignore. |
|max_backend_down_time_second |3600 |After BE and FE lose connection, the maximum time FE can tolerate for BE to rejoin, Unit: s. |
|drop_backend_after_decommission |TRUE |Whether to delete the BE after it is taken down:<br><br><br>* TRUE: Delete the BE.<br><br>* FALSE: Do not delete the BE. |


<span id="_2-3-查询引擎相关配置"></span>
### **Query engine\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|max_create_table_timeout_second |60 |Maximum timeout for creating a table, Unit: s. |
|max_running_rollup_job_num_per_table |1 |Maximum concurrency for Rollup tasks per table. |
|max_planner_scalar_rewrite_num |10_0000 |Maximum number of times the optimizer can rewrite ScalarOperator. |
|statistics_manager_sleep_time_sec |60\*10 |Cycle for automatically creating statistics tables, Unit: s. |
|statistic_collect_interval_sec |120\*60 |Execution cycle for statistics functionality, Unit: s. |
|statistic_update_interval_sec |24 *60* 60 |Default collection interval for statistics jobs, Unit: s. |
|statistic_sample_collect_rows |200000 |Default sample row count for sampled statistics jobs, default is 200,000 rows. |
|enable_statistic_collect |TRUE |Statistics collection feature switch:<br><br><br>* TRUE: Enable statistics collection feature.<br><br>* FALSE: Disable statistics collection feature. |
|enable_local_replica_selection |FALSE |Whether the optimizer prioritizes selecting tablets on BE nodes with the same IP as FE:<br><br><br>* TRUE: Yes.<br><br>* FALSE: No. |
|max_distribution_pruner_recursion_depth |100 |Maximum recursion depth allowed for partition pruning. |


<span id="_2-4-导入和导出相关配置"></span>
### **Import and export\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|max_running_txn_num_per_db |100 |Number of concurrent import tasks. |
|max_load_timeout_second |259200 |Applies to all imports, Unit: s. |
|min_load_timeout_second |1 |Applies to all imports, Unit: s. |
|load_parallel_instance_num |1 |Number of concurrent instances on a single BE, default is 1. |
|db_used_data_quota_update_interval_secs |300 |Time cycle for updating database usage quota, Unit: s. |
|history_job_keep_max_second |604800 |Maximum retention time for historical tasks, Unit: s. |
|label_keep_max_num |1000 |Maximum number of import tasks retained within a certain period. Retention time is set in label_keep_max_second. |
|label_keep_max_second |259200 |Label retention time, Unit: s. |
|period_of_auto_resume_min |5 |Interval for automatically resuming Routine Load. |
|stream_load_default_timeout_second |600 |StreamLoad timeout, Unit: s. |
|max_stream_load_timeout_second |259200 |The maximum allowed value for the Stream import timeout, unit: s. |
|insert_load_default_timeout_second |3600 |The timeout for the Insert Into statement, unit: s. |
|broker_load_default_timeout_second |14400 |The timeout for Broker Load, unit: s. |
|export_max_bytes_per_be_per_task |268435456 |The maximum amount of data exported by a single export task on a single BE, default is 256 MB. |
|export_running_job_num_limit |5 |The maximum number of running export jobs. |
|export_task_default_timeout_second |7200 |The export job timeout duration, unit: s, default is 2 hours. |


<span id="_2-5-存储相关配置"></span>
### **Storage\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|capacity_used_percent_high_water |0.75 |The metric for disk usage capacity on the backend. If the value exceeds 0.75, avoid sending table creation and clone tasks to the tablet until it returns to normal. |
|storage_high_watermark_usage_percent |85 |The maximum space usage in the BE storage directory. |
|storage_min_left_capacity_bytes |2 *1024* 1024\*1024 |The minimum remaining space in the BE storage directory, default is 2 GB. |
|storage_flood_stage_left_capacity_bytes |100 *1024* 1024\*1024 |The remaining space in the BE storage directory. If the remaining space is less than this value, Load and Restore jobs will be rejected. Default is 1 GB. |
|storage_flood_stage_usage_percent |95 |The space usage in the BE storage directory. If the space usage exceeds this value, Load and Restore jobs will be rejected. |
|catalog_trash_expire_second |86400 |The duration for which metadata is retained in the recycle bin after a table or database is deleted, unit: s, default is 1 day. If this duration is exceeded, the data cannot be recovered. |
|alter_table_timeout_second |86400 |The timeout for schema change, unit: s, default is 1 day. |
|balance_load_disk_safe_threshold |0.5 |Only effective for the disk_and_tablet policy. If the disk usage of all BEs is below 50%, disk usage is considered balanced. |
|balance_load_score_threshold |0.1 |For the be_load_score policy, a BE with a load 10% lower than the average is considered underloaded, and a BE with a load 10% higher than the average is considered overloaded. For the disk_and_tablet policy, if the difference between the maximum and minimum BE disk usage exceeds 10%, disk usage is considered unbalanced and tablet rebalancing will be triggered. |
|disable_balance |FALSE |Whether to disable tablet scheduling:<br><br><br>* FALSE: Disabled.<br><br>* TRUE: Not disabled. |
|max_scheduling_tablets |2000 |The number of tablets being scheduled. If the number of tablets being scheduled exceeds this value, tablet balance checks are skipped. |
|max_balancing_tablets |100 |The number of tablets being balanced. If the number of tablets being balanced exceeds this value, tablet rebalancing is skipped. |
|disable_colocate_balance |FALSE |Whether to disable replica balancing for Colocate Table:<br><br><br>* TRUE: Disabled.<br><br>* FALSE: Not disabled. |
|recover_with_empty_tablet |FALSE |Whether to use an empty tablet as a replacement when a tablet replica is lost or damaged:<br><br><br>* TRUE: Use an empty tablet as a replacement.<br><br>* FALSE: Do not use an empty tablet as a replacement.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using an empty tablet as a substitute ensures that queries can still be executed when tablet replicas are lost or damaged (however, due to missing data, the results may be incorrect).</div><br> |
|min_clone_task_timeout_sec |3\*60 |The minimum timeout for cloning a tablet, unit: s, default is 3 minutes. |
|max_clone_task_timeout_sec |2 *60* 60 |The maximum timeout for cloning a tablet, unit: s, default is 2 hours. |
|tablet_create_timeout_second |1 |Table creation timeout duration, Unit: s. |
|tablet_delete_timeout_second |2 |Table deletion timeout duration, Unit: s. |
|tablet_repair_delay_factor_second |60 |Interval for FE to control replica repair, Unit: s. |
|consistency_check_start_time |23 |Start time for FE to initiate replica consistency check. The default is 23:00. |
|consistency_check_end_time |4 |End time for FE to initiate replica consistency check. The default is 4:00. |
|check_consistency_default_timeout_second |600 |Replica consistency check timeout duration, Unit: s. |


<span id="_2-6-其他配置"></span>
### **Other configuration**


|Configuration item |Default value |Description |
|---|---|---|
|plugin_enable |TRUE |Whether the plugin feature is enabled:<br><br><br>* TRUE: The plugin feature is enabled.<br><br>* FALSE: The plugin feature is not enabled. Note: Plugins can only be installed or uninstalled on the primary node. |
|max_small_file_number |100 |Maximum number of small files allowed for storage. |
|max_small_file_size_bytes |1024\*1024 |Maximum file size for storage. The default is 1 MB. |
|backup_job_default_timeout_ms |86400\*1000 |Backup job timeout duration, Unit: s. The default is 1 day. |
|report_queue_size |100 |Waiting queue length for Disk, Task, or Tablet reports. |


<span id="_3-fe静态参数"></span>
## **FE static parameters**

<span id="_3-1-log相关配置"></span>
### **LOG\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|log_roll_size_mb |1024 |Log split size. Each log is split every 1 GB. |
|sys_log_dir |StarRocksFe.STARROCKS_HOME_DIR/log |Directory for log retention. |
|sys_log_level |INFO |Log level. Configurable levels, from least to most strict, are INFO, WARNING, ERROR, and FATAL. |
|sys_log_verbose_modules |Empty string |Modules for log printing. For example, if set to org.apache.starrocks.catalog, only logs under the catalog module are printed. |
|sys_log_roll_interval |DAY |Time interval for log splitting. |
|sys_log_delete_age |7d |Interval for log deletion. |
|sys_log_roll_num |10 |Number of log files retained for each sys_log_roll_interval. |
|audit_log_dir |starrocksFe.STARROCKS_HOME_DIR/log |Directory for audit log retention. |
|audit_log_roll_num |90 |Number of audit logs retained. |
|audit_log_modules |"slow_query", "query" |Modules for audit log printing. By default, slow_query and query are retained. |
|audit_log_roll_interval |DAY |Time interval for audit log splitting. The values can be DAY or HOUR. |
|audit_log_delete_age |30d |Interval for audit log deletion. |
|dump_log_dir |STARROCKS_HOME_DIR/log |Directory for Dump logs. |
|dump_log_modules |"query" |Modules for Dump log printing. By default, query is retained. |
|dump_log_roll_interval |DAY |Time interval for Dump log splitting. Log file suffix is yyyyMMdd (DAY) or yyyyMMddHH (HOUR). |
|dump_log_roll_num |90 |Number of Dump log files retained for each dump_log_roll_interval. |
|dump_log_delete_age |30d |Retention duration for Dump logs. |


<span id="_3-2-server进程相关配置"></span>
### **Server process\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|frontend_address |0.0.0.0 |FE IP address. |
|priority_networks |Empty string |Specify BE IP address in CIDR format, such as 10.10. **.** /24. This is suitable for machines with multiple IPs and allows specifying the preferred network. |
|http_port |8030 |Http Server port. |
|http_backlog_num |1024 |Backlog queue length for HTTP Server. |
|cluster_name |StarRocks Cluster |Cluster name displayed in the Title on the web page. |
|rpc_port |9020 |Thrift Server port on FE. |
|thrift_backlog_num |1024 |Backlog queue length for Thrift Server. |
|thrift_server_type |THREAD_POOL |Service model used by FE's Thrift service. For example, SIMPLE, THREADED, and THREAD_POOL. |
|thrift_server_max_worker_threads |4096 |Maximum number of worker threads for Thrift Server. |
|thrift_client_timeout_ms |0 |Client timeout duration. The default value is 0, which means it will never time out. |
|brpc_idle_wait_max_time |10000 |Idle wait time for BRPC, Unit: milliseconds, default is 10 seconds. |
|query_port |9030 |MySQL Server port on FE. |
|mysql_service_nio_enabled |TRUE |Whether to enable NIO for FE connection service:<br><br><br>* TRUE: Enabled.<br><br>* FALSE: Not enabled. |
|mysql_service_io_threads_num |4 |Number of threads for FE connection service. |
|mysql_nio_backlog_num |1024 |Backlog queue length for MySQL Server. |
|max_mysql_service_task_threads_num |4096 |Maximum number of threads for MySQL Server task processing. |
|max_connection_scheduler_threads_num |4096 |Maximum number of threads in the connection timer thread pool. |
|qe_max_connection |1024 |Maximum number of connections accepted on FE, applicable to all users. |
|check_java_version |TRUE |Whether to check compatibility between the runtime and compiled Java versions:<br><br><br>* TRUE: Check.<br><br>* FALSE: Do not check. |


<span id="_3-3-元数据与集群管理相关配置"></span>
### **Metadata and cluster management\-related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|meta_dir |StarRocksFe.STARROCKS_HOME_DIR/meta |Metadata retention directory. |
|heartbeat_mgr_threads_num |8 |Number of threads for sending heartbeat tasks in HeartbeatMgr. |
|heartbeat_mgr_blocking_queue_size |1024 |Queue length of the thread pool for sending heartbeat tasks in HeartbeatMgr. |
|metadata_failure_recovery |FALSE |Force reset FE metadata. Note: Please use this parameter with caution. |
|edit_log_port |9010 |Port used for communication among FE Group (Master, Follower, Observer). |
|edit_log_type |BDB |Type of Edit log, must be BDB. |
|bdbje_heartbeat_timeout_second |30 |Heartbeat timeout interval for BDBJE, Unit: seconds. |
|bdbje_lock_timeout_second |1 |Lock timeout interval for BDBJE, Unit: seconds. |
|max_bdbje_clock_delta_ms |5000 |Maximum tolerated clock offset between Master and Non\-master, Unit: milliseconds. |
|txn_rollback_limit |100 |Transaction rollback limit. |
|bdbje_replica_ack_timeout_second |10 |Maximum time for BDBJE Master to wait for enough FOLLOWER ACKs. |
|master_sync_policy |SYNC |Log flush policy for Master, default is SYNC. |
|replica_sync_policy |SYNC |Log flush policy for Follower, default is SYNC. |
|meta_delay_toleration_second |300 |Maximum metadata lag tolerated by non\-Master nodes, Unit: seconds. |
|cluster_id |\-1 |FE or BE nodes with the same cluster_id belong to the same cluster. Default value \-1 means a cluster_id is randomly generated when Master FE starts for the first time. |


<span id="_3-4-查询引擎相关配置"></span>
### **Query engine related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|disable_colocate_join |FALSE |Whether to enable Colocate Join:<br><br><br>* FALSE: Colocate Join is not enabled.<br><br>* TRUE: Colocate Join is enabled. |
|enable_udf |FALSE |Whether to enable UDF:<br><br><br>* FALSE: UDF is not enabled.<br><br>* TRUE: UDF is enabled. |
|publish_version_interval_ms |10 |Interval for sending version activation tasks. |
|statistic_cache_columns |10_0000 |Number of rows in the statistics information table cache. |


<span id="_3-5-导入和导出相关配置"></span>
### **Import and export related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|async_load_task_pool_size |10 |Thread pool size for executing import tasks. |
|load_checker_interval_second |5 |Polling interval for import, Unit: seconds. |
|transaction_clean_interval_second |30 |Cycle for cleaning finished transactions, Unit: seconds. |
|label_clean_interval_second |14400 |Interval for label cleaning, Unit: seconds. |
|export_checker_interval_second |5 |Polling interval for export threads, Unit: seconds. |
|export_task_pool_size |5 |Thread pool size for export tasks. |
|export_checker_interval_second |5 |Scheduling cycle for export job scheduler, Unit: seconds. |


<span id="_3-6-存储相关配置"></span>
### **Storage related configuration**


|Configuration item |Default value |Description |
|---|---|---|
|storage_cooldown_second |2592000 |Time for storage medium migration, Unit: seconds, default is 30 days. |
|default_storage_medium |HDD |Default storage medium. Possible values: HDD and SSD. If no storage medium is specified when creating a table or partition, this value will be used. |
|schedule_slot_num_per_path |2 |The number of tablet\-related tasks that a BE storage directory can execute simultaneously. |
|tablet_balancer_strategy |disk_and_tablet |Tablet balancing strategy. The value can be disk_and_tablet or be_load_score. |
|tablet_stat_update_interval_second |300 |The interval at which the FE requests each BE to collect tablet information, in seconds. The default is 5 minutes. |


<span id="_4-be配置项"></span>
## **BE configuration items**

All BE configuration items are static parameters.

<span id="_4-1-日志相关"></span>
### Log related


|Configuration item |Default value |Description |
|---|---|---|
|sys_log_dir |${DORIS_HOME}/log |Directory for storing logs. Log levels include INFO, WARNING, ERROR, and FATAL. |
|sys_log_level |INFO |Log level. The configurable levels, from least to most strict, are INFO, WARNING, ERROR, and FATAL. |
|sys_log_roll_mode |SIZE\-MB\-1024 |Log split size. Logs are split every 1 GB. |
|sys_log_roll_num |10 |Number of logs to retain. |
|sys_log_verbose_modules |Empty string |Log output modules. If olap is specified, only logs under the olap module are printed. |
|sys_log_verbose_level |10 |Log display level, used to control the output of logs that start with VLOG in the code. |
|log_buffer_level |Empty string |Log flushing policy. By default, logs are kept in memory. |


<span id="_4-2-合并相关"></span>
### Merge related


|Configuration item |Default value |Description |
|---|---|---|
|base_compaction_check_interval_seconds |60 |Polling interval for BaseCompaction threads, in seconds. |
|base_compaction_num_threads_per_disk |1 |Number of BaseCompaction threads per disk. |
|base_cumulative_delta_ratio |0.3 |One of the BaseCompaction trigger conditions: the ratio of cumulative file size to base file size. |
|base_compaction_interval_seconds_since_last_operation |86400 |One of the BaseCompaction trigger conditions: the interval since the last BaseCompaction. |
|cumulative_compaction_check_interval_seconds |1 |Polling interval for CumulativeCompaction threads, in seconds. |
|min_cumulative_compaction_num_singleton_deltas |5 |One of the CumulativeCompaction trigger conditions: the minimum number of singleton files required. |
|max_cumulative_compaction_num_singleton_deltas |1000 |One of the CumulativeCompaction trigger conditions: the maximum number of singleton files required. |
|cumulative_compaction_num_threads_per_disk |1 |Number of CumulativeCompaction threads per disk. |
|min_compaction_failure_interval_sec |120 |Interval before a Tablet Compaction is rescheduled after failure, in seconds. |
|max_compaction_concurrency |\-1 |Maximum concurrency for BaseCompaction plus CumulativeCompaction. The default value of \-1 means no limit. |


<span id="_4-3-线程相关"></span>
### Thread related


|Configuration item |Default value |Description |
|---|---|---|
|heartbeat_service_thread_count |1 |Number of heartbeat threads. |
|create_tablet_worker_count |3 |Number of threads for creating tablets. |
|drop_tablet_worker_count |3 |Number of threads for deleting tablets. |
|push_worker_count_normal_priority |3 |Number of import threads for handling NORMAL priority tasks. |
|push_worker_count_high_priority |3 |Number of import threads for handling HIGH priority tasks. |
|publish_version_worker_count |2 |Number of threads for publishing versions. |
|clear_transaction_task_worker_count |1 |Number of threads for clearing transactions. |
|alter_tablet_worker_count |3 |Number of threads for performing schema changes. |
|clone_worker_count |3 |Number of threads for cloning. |
|storage_medium_migrate_count |1 |Number of threads for storage medium migration. For example, the number of threads for migrating hot data from SSD to SATA disks. |
|check_consistency_worker_count |1 |Calculate the checksum of tablets. |
|num_threads_per_core |3 |Number of threads started per CPU core. |
|doris_scanner_thread_pool_thread_num |48 |Number of threads for the storage engine to concurrently scan disks, managed uniformly in the thread pool. |
|doris_scanner_thread_pool_queue_size |102400 |Maximum number of tasks accepted by the storage engine. |
|webserver_num_workers |48 |Number of Http Server threads. |
|fragment_pool_thread_num |64 |Query thread count. By default, 64 threads are started, and subsequent query requests dynamically create threads. |
|fragment_pool_queue_size |2048 |Maximum number of query requests that can be processed on a single node. |


<span id="_4-4-服务相关"></span>
### Service related


|Configuration item |Default value |Description |
|---|---|---|
|be_port |9060 |Port of the Thrift Server on BE, used to receive requests from FE. |
|brpc_port |8060 |BRPC port, can be used to view some network statistics of BRPC. |
|brpc_num_threads |\-1 |Number of bthreads in BRPC. The default value \-1 means it is equal to the number of CPU cores. |
|priority_networks |Empty string |Specify the BE IP address in CIDR format, such as 10.10. **.** /24. Applicable when the machine has multiple IPs and a preferred network needs to be specified. |
|heartbeat_service_port |9050 |Heartbeat service port (Thrift), receives heartbeats from FE. |
|user_function_dir |${DORIS_HOME}/lib/udf |Directory for storing UDF programs. |
|storage_root_path |Empty string |Directory for storing data. |
|webserver_port |8040 |Http Server port. |


<span id="_4-5-其他配置"></span>
### Other configuration


|Configuration item |Default value |Description |
|---|---|---|
|report_task_interval_seconds |10 |Interval for reporting a single task. Unit: s. Creating tables, deleting tables, importing, and Schema Change can all be considered tasks. |
|report_disk_state_interval_seconds |60 |Interval for reporting disk status. Unit: s. Reports the status, data volume, and more of each disk. |
|report_tablet_interval_seconds |60 |Interval for reporting tablets. Unit: s. Reports the latest version of all tablets. |
|alter_tablet_timeout_seconds |86400 |Schema Change timeout. Unit: s. |
|compress_rowbatches |TRUE |Whether to compress RowBatch during RPC communication between BEs, used for data transfer between query layers. |
|serialize_batch |FALSE |Whether to serialize RowBatch during RPC communication between BEs, used for data transfer between query layers. |
|status_report_interval |5 |Interval for reporting query profiles. Unit: s. Used by FE to collect query statistics. |
|memory_limitation_per_thread_for_schema_change |2 |Maximum memory allowed for a single Schema Change task. |
|file_descriptor_cache_clean_interval |3600 |Interval for cleaning file descriptor cache. Unit: s. Used to clean file descriptors that have not been used for a long time. |
|disk_stat_monitor_interval |5 |Interval for disk status monitoring. Unit: s. |
|unused_rowset_monitor_interval |30 |Interval for cleaning expired Rowsets. Unit: s. |
|max_tablet_num_per_shard |1024 |Number of tablets per shard, used to partition tablets and prevent too many tablet subdirectories under a single directory. |
|pending_data_expire_time_sec |1800 |Maximum duration for which the storage engine retains uncommitted data. Unit: s. |
|inc_rowset_expired_sec |1800 |In incremental clone scenarios, the duration for which imported data is retained in the storage engine. Unit: s. |
|max_garbage_sweep_interval |3600 |Maximum interval for disk garbage cleaning. Unit: s. |
|min_garbage_sweep_interval |180 |Minimum interval for disk garbage cleaning. Unit: s. |
|snapshot_expire_time_sec |172800 |Interval for cleaning snapshot files. Unit: s. Default is 48 hours. |
|trash_file_expire_time_sec |259200 |The interval for recycle bin cleanup, Unit: s. Default is 72 hours. |
|file_descriptor_cache_capacity |16384 |The capacity of the file descriptor cache. |
|min_file_descriptor_number |60000 |The minimum required limit for file descriptors in the BE process. |
|index_stream_cache_capacity |10737418240 |The capacity of the cache for statistical information such as BloomFilter, Min, or Max. |
|storage_page_cache_limit |0 |The capacity of the PageCache. |
|disable_storage_page_cache |TRUE |Whether to disable Page Cache. TRUE: Page Cache is disabled. FALSE: Page Cache is not disabled. |
|periodic_counter_update_period_ms |500 |The interval for updating Counter statistics, Unit: ms. |
|load_data_reserve_hours |4 |The retention time for files generated by small batch imports, Unit: h. |
|load_error_log_reserve_hours |48 |The retention duration for imported data information, Unit: h. |
|number_tablet_writer_threads |16 |The number of threads for streaming imports. |
|streaming_load_max_mb |10240 |The maximum size for a single file in streaming imports. |
|streaming_load_rpc_max_alive_time_sec |1200 |The timeout duration for streaming import RPC. |
|enable_partitioned_aggregation |TRUE |Whether to use PartitionAggregation: TRUE: PartitionAggregation is used. FALSE: PartitionAggregation is not used. |
|enable_token_check |TRUE |Whether to enable Token verification: TRUE: Token verification is enabled. FALSE: Token verification is not enabled. |
|load_process_max_memory_limit_bytes |107374182400 |The maximum memory limit occupied by all import threads on a single node. Default is 100 GB. |
|load_process_max_memory_limit_percent |30 |The maximum memory usage ratio for all import threads on a single node. |
|sync_tablet_meta |FALSE |Whether the storage engine enables sync to persist to disk. |
|thrift_rpc_timeout_ms |5000 |The timeout duration for Thrift, Unit: ms. |
|txn_commit_rpc_timeout_ms |10000 |The timeout duration for Txn, Unit: ms. |
|routine_load_thread_pool_size |10 |The number of thread pools for routine imports. |
|tablet_meta_checkpoint_min_new_rowsets_num |10 |The minimum number of Rowsets for TabletMeta Checkpoint. |
|tablet_meta_checkpoint_min_interval_secs |600 |The polling interval for TabletMeta Checkpoint threads, Unit: s. |
|brpc_max_body_size |209715200 |The maximum package size for BRPC. Default is 200 MB. |
|max_runnings_transactions |2000 |The maximum number of transactions supported by the storage engine. |
|tablet_map_shard_size |32 |The number of Tablet groups. |
|enable_bitmap_union_disk_format_with_set |FALSE |The new Bitmap storage format, which can optimize bitmap_union performance. |
