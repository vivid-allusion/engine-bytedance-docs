---
title: "query_log"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query_log"
---

The system table `system.query_log` contains information about executed queries, such as start time, processing duration, and error messages.

<span id="8a2fea6c"></span>
## Column name


|**Field name** |**Data type** |**Description of field meaning** |
|---|---|---|
|type |Enum8('QueryStart' = 1, 'QueryFinish' = 2, 'ExceptionBeforeStart' = 3, 'ExceptionWhileProcessing' = 4) |The type of event that occurred during query execution.<br><br><br>* 'QueryStart'=1: Query execution started successfully.<br><br>* 'QueryFinish'=2: Query execution finished successfully.<br><br>* 'ExceptionBeforeStart'=3: Exception occurred before query execution started.<br><br>* 'ExceptionWhileProcessing'=4: Exception occurred during query execution. |
|event_date |Date |Query start date. |
|event_time |DateTime |Query start time. |
|event_time_microseconds |DateTime64(6) |Query start time with microsecond precision. |
|query_start_time |DateTime |Start time of the query execution. |
|query_start_time_microseconds |DateTime64(6) |Start time of query execution with microsecond precision. |
|query_duration_ms |UInt64 |Duration of query execution (in milliseconds) |
|read_rows |UInt64 |Total number of rows read from all tables and table functions involved in the query. |
|read_bytes |UInt64 |Total number of bytes read from all tables and table functions involved in the query. |
|written_rows |UInt64 |For INSERT queries, this column displays the number of rows written; for other query types, the value in this column is 0. |
|written_bytes |UInt64 |For INSERT queries, this column displays the number of bytes written (uncompressed); for other query types, the value in this column is 0. |
|result_rows |UInt64 |Number of rows in the result set for SELECT queries, or the actual number of rows written for INSERT queries. |
|result_bytes |UInt64 |The number of memory bytes used to store the query result. |
|memory_usage |UInt64 |For MPP execution in the optimizer, this parameter indicates the memory usage of a single segment.<br><br>For non\-optimizer execution, this parameter indicates the memory usage of a single query. |
|query_memory_usage |UInt64 |In MPP execution mode for the optimizer, by default, `exchange_use_query_memory_tracker=1`. query_memory_usage records the peak combined memory usage of all segments on this node before the current segment exits. |
|total_cpu_seconds |Float64 |Total CPU time used by the query statement, measured in seconds. |
|io_wait_seconds |Float64 |Query statement IO wait time, in seconds. |
|current_database |String |Name of the currently connected database. |
|query |String |Original query statement. |
|normalized_query_hash |UInt64 |Query statement hash fingerprint. |
|query_kind |LowCardinality(String) |Query type. |
|databases |Array(LowCardinality(String)) |Names of databases found in the query. |
|tables |Array(LowCardinality(String)) |The names of tables present in the query. |
|columns |Array(LowCardinality(String)) |The names of columns present in the query. |
|projections |Array(LowCardinality(String)) |The names of projections used during query execution. |
|materialized_views |Array(LowCardinality(String)) |The names of views or materialized views used during query execution. |
|exception_code |Int32 |Exception code. |
|exception |String |Exception message. |
|stack_trace |String |Query stack trace information. Returns an empty string if the query completes successfully. |
|is_initial_query |UInt8 |Query initiation type. Values are as follows:<br><br><br>* 1: Query initiated by the client.<br><br>* 0: Query initiated by another query as part of distributed query execution. |
|user |String |Name of the user who initiated the current query. |
|query_id |String |Query statement ID. |
|address |IPv6 |IP address where the query originated. |
|port |UInt16 |Client port where the query originated. |
|initial_user |String |Name of the user who runs the initial query (for distributed query execution). |
|initial_query_id |String |ID of the initial query (for distributed query execution). |
|initial_address |IPv6 |IP address where the parent query is started. |
|initial_port |UInt16 |Client port where the parent query is started. |
|initial_query_start_time |DateTime |Initial query start time (used for distributed query execution). |
|initial_query_start_time_microseconds |DateTime64(6) |Initial query start time with microsecond precision (used for distributed query execution). |
|interface |UInt8 |Type of interface that initiated the query. The following values:<br><br><br>* 1：TCP<br><br>* 2：HTTP |
|os_user |String |The operating system username running the client. |
|client_hostname |String |The hostname of the computer running the ByteHouse client or other TCP client. |
|client_name |String |ByteHouse client or other TCP client name. |
|client_revision |UInt32 |Version of the ByteHouse client or other TCP client. |
|client_version_major |UInt32 |Major version of the ByteHouse client or other TCP client. |
|client_version_minor |UInt32 |Minor version of the ByteHouse client or other TCP client. |
|client_version_patch |UInt32 |Patch version for the ByteHouse client or other TCP client |
|http_method |UInt8 |The HTTP method used to start the query. The following values:<br><br><br>* 0: The query starts from the TTCP interface.<br><br>* 1: Uses the GET method.<br><br>* 2: Uses the POST method. |
|http_user_agent |String |Uses the UserAgent information from the HTTP request header. |
|http_referer |String |Uses the Referer information from the HTTP request header (including the absolute or partial address of the page where the query was made). |
|forwarded_for |String |Uses the X\-Forwarded\-For information from the HTTP request header. |
|quota_key |String |The quota key specified in the quota settings. |
|revision |UInt32 |Engine internal version number. |
|log_comment |String |Log comment. It can be set to any string not exceeding mmax_query_size. If not defined, it is an empty string. |
|thread_ids |Array(UInt64) |Thread IDs involved in query execution. |
|ProfileEvents |Map(String, UInt64) |Information about query measurement metrics. Detailed descriptions are available in the system.events table. |
|ProfileEventsTimeline |Map(String, UInt64) |Records timeline information for query\-related events. |
|Settings |Map(String, String) |Settings parameters used during query execution. |
|Graphviz |Map(String, String) |When print_graph=1 is set, stores the optimizer link query plan as a Graphviz DOT string. |
|used_aggregate_functions |Array(String) |Names of aggregate functions used during query execution. |
|used_aggregate_function_combinators |Array(String) |The canonical name of the aggregation function combinator used during query execution. |
|used_database_engines |Array(String) |The name of the database engine used during query execution. |
|used_data_type_families |Array(String) |The name of the data type family used during query execution. |
|used_dictionaries |Array(String) |Dictionary names used during query execution. |
|used_formats |Array(String) |Format names used during query execution. |
|used_functions |Array(String) |Function names used during query execution. |
|used_storages |Array(String) |Storage names used during query execution. |
|used_table_functions |Array(String) |Use table function names during query execution. |
|partition_ids |Array(String) |When `log_queries_with_partition_ids=1` is configured, records the IDs of table partitions accessed by the current query. |
|segment_id |Int64 |In optimizer chain MPP execution mode, the current query's execution segment ID. |
|segment_parallel |Int64 |Number of segment instances. |
|segment_parallel_index |Int64 |Segment instance ID. |
|resource_group |String |Resource group name used during query execution. |
|fallback_reason |String |Reasons for optimizer pipeline MPP execution mode fallback |
|query_plan |String |Optimizer pipeline query plan in JSON format |
|segment_profile |Array(String) |During optimizer execution pipeline, records the plan and execution duration for segments when `log_segment_profiles=1` is enabled |
|session_id |String |Session ID |


<span id="98820b32"></span>
## Example

```SQL
SELECT * FROM system.query_log LIMIT 1; 
```


```SQL
Row 1:
──────
type：                                  QuerySatrt      
event_date:                             2025-06-09     
event_time:                             2025-06-09 14:05:17       
event_time_microseconds:                2025-06-09 14:05:17.230230      
query_start_time:                       2025-06-09 14:05:17       
query_start_time_microseconds:          2025-06-09 14:05:17.230230      
query_duration_ms:                      0    
read_rows:                              0        
read_bytes:                             0        
written_rows:                           0      
written_bytes:                          0       
result_rows:                            0       
result_bytes:                           0       
memory_usage:                           0        
query_memory_usage:                     0    
total_cpu_seconds:                      0    
io_wait_seconds:                        0    
current_database:                       default     
query:                                  select count(1) + 123456788     
normalized_query_hash:                  9580075159047059276   
query_kind:                             Select     
databases:                              []    
tables:                                 []       
columns:                                []        
projections:                            []       
materialized_views:                     []       
exception_code:                         0    
exception:        
stack_trace:      
is_initial_query:                       1       
user:                                   default        
query_id:                               a4789c7d-edf8-44b2-97d2-05af0eaccc03       
address:                                ::ffff:127.0.0.1       
port:                                   34956        
initial_user:                           default        
initial_query_id:                       a4789c7d-edf8-44b2-97d2-05af0eaccc03      
initial_address:                        ::ffff:127.0.0.1        
initial_port:                           34956       
initial_query_start_time:               2025-06-09 14:05:17      
initial_query_start_time_microseconds:  2025-06-09 14:05:17.230230   
interface:                              1       
os_user:        
client_hostname:                        iv-ydxo6kp1j4xjd1tibrju       
client_name:                            ClickHouse       
client_revision:                        54465        
client_version_major:                   21        
client_version_minor:                   9        
client_version_patch:                   1     
http_method:                            0        
http_user_agent:        
http_referer:       
forwarded_for:        
quota_key:        
revision:                               54454       
log_comment:        
thread_ids:                             []        
ProfileEvents:                          {}        
ProfileEventsTimeline:                  {}       
Settings:                               { "allow_strict_resize": "0", "background_pool_size": "16", "background_schedule_pool_size": "16", "connect_timeout_with_failover_ms": "1000", "distributed_aggregation_memory_efficient": "0", "distributed_product_mode": "allow", "enable_eliminate_complicated_pk_fk_join": "1", "enable_eliminate_complicated_pk_fk_join_without_top_join": "1", "enable_eliminate_join_by_fk": "1", "enable_evaluate_constant_for_nondeterministic": "0", "enable_group_by_keys_pruning": "1", "enable_merge_scheduler": "0", "enable_new_ann": "1", "enable_optimizer": "1", "enable_plan_cache": "1", "enable_sharding_optimize": "0", "enable_uncompressed_cache_shard_mode": "1", "enable_windows_parallel": "1", "enable_zero_copy_read": "1", "exchange_enable_block_compress": "1", "exchange_enable_multipath_reciever": "0", "exchange_multi_path_receiver_queue_size": "20000", "exchange_remote_receiver_queue_size": "4000", "exchange_source_pipeline_threads": "32", "exchange_unordered_output_parallel_size": "16", "force_manipulate_materialize_mysql_table": "1", "input_format_skip_unknown_fields": "1", "insert_distributed_sync": "1", "join_algorithm": "parallel_hash", "local_filesystem_read_method": "pread", "log_processors_profiles": "0", "log_queries": "1", "log_query_threads": "0", "materialize_ttl_after_modify": "0", "max_block_size": "65536", "max_execution_time": "300", "max_insert_block_size": "1048576", "max_insert_block_size_bytes": "0", "max_memory_usage": "39084202393", "max_memory_usage_for_all_queries": "39084202393", "max_memory_usage_for_user": "39084202393", "max_partitions_per_insert_block": "1000", "max_query_size": "1048576", "max_rows_to_schedule_merge": "500000000", "max_threads": "32", "merge_tree_max_bytes_to_use_cache": "13743895347", "merge_tree_max_rows_to_use_cache": "1000000000000", "parallel_join_threshold": "900000", "queue_max_wait_ms": "100000", "receive_timeout": "1000000", "rewrite_complex_predicate_by_domain": "1", "slow_query_ms": "0", "strict_rows_to_schedule_merge": "50000000", "timeout_before_checking_execution_speed": "0", "total_rows_to_schedule_merge": "0", "use_uncompressed_cache": "1" }  
Graphviz:                               {}      
used_aggregate_functions:               []       
used_aggregate_function_combinators:    []         
used_database_engines:                  []            
used_data_type_families:                []            
used_dictionaries:                      []            
used_formats:                           []            
used_functions:                         []            
used_storages:                          []            
used_table_functions:                   []            
partition_ids:                          []            
segment_id:                             0       
segment_parallel:                       1       
segment_parallel_index:                 1        
resource_group:        
fallback_reason:       
query_plan:      
segment_profiles:                       []  
session_id:  
```
