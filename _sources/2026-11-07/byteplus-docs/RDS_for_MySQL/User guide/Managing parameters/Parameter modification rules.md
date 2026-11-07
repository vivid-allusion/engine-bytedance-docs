---
title: "Parameter modification rules"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parameter_modification_rules"
---

This topic explains the parameter modification rules for RDS for MySQL.

<span id=".5Lul5LiL5Y-C5pWw5LuF5pSv5oyB5Zyo5pyA5paw54mI5pys55qE5a6e5L6L5Lit5L-u5pS5"></span>
## The following parameters can be modified only in the latest instance version.

If these parameters are included in a batch modification, the changes only take effect on new version instances, while older version instances will ignore the modifications.


|Parameter name |Instance version |Parameter default value |Need to restart |
|---|---|---|---|
|loose_innodb_data_file_logic_drop |MySQL 8.0, MySQL 8.4 |OFF |No |
|loose_innodb_data_file_logic_drop_max_size |MySQL 8.0, MySQL 8.4 |1024 |No |
|loose_thread_pool_enabled |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ON |* MySQL 5.7:<br><br>   * For **MySQL 5.7.44_20260415 and later** instances: When the value of the `loose_thread_handling_switch_mode` parameter is `handling_switch_new` or `handling_switch_all`, modifying this parameter does not require an instance restart; otherwise, an instance restart is required.<br><br>   * For instances with kernel versions **earlier than MySQL 5.7.44_20260415**, modifying this parameter requires an instance restart.<br><br>* MySQL 8.0:<br><br>   * For **MySQL 8.0.32_20260415 and later** instances: When the value of the `loose_thread_handling_switch_mode` parameter is `handling_switch_new` or `handling_switch_all`, modifying this parameter does not require an instance restart; otherwise, an instance restart is required.<br><br>   * For instances with kernel versions **earlier than MySQL 8.0.32_20260415**, modifying this parameter requires an instance restart.<br><br>* MySQL 8.4: Modifying this parameter requires an instance restart. |
|loose_thread_pool_oversubscribe |MySQL 5.7, MySQL 8.0, MySQL 8.4 |16 |No |
|loose_thread_pool_size |MySQL 5.7, MySQL 8.0, MySQL 8.4 | |No |
|loose_kill_idle_transaction |MySQL 8.0, MySQL 8.4 |0 |No |
|loose_rds_performance_schema |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ON |Yes |


<span id="9CKi9hv1"></span>
## The following parameters must have the same value set for all nodes in an instance.

By default, the effective scope is all nodes, and modifying them only on read\-only nodes is not supported.


|Parameter name |Instance version |Parameter default value |Need to restart |
|---|---|---|---|
|auto_increment_increment |MySQL 5.7, MySQL 8.0, MySQL 8.4 |1 |No |
|auto_increment_offset |MySQL 5.7, MySQL 8.0, MySQL 8.4 |1 |No |
|collation_server |MySQL 5.7, MySQL 8.0, MySQL 8.4 |utf8_general_ci |Yes |
|lower_case_table_names |MySQL 5.7 |1 |Yes |
|max_execution_time |MySQL 5.7, MySQL 8.0, MySQL 8.4 |0 |No |
|replica_net_timeout |MySQL 8.0, MySQL 8.4 |60 |No |
|replica_type_conversions |MySQL 8.0, MySQL 8.4 |\- |No |
|relay_log_recovery |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ON |Yes |
|source_verify_checksum |MySQL 8.0, MySQL 8.4 |OFF |No |
|sql_safe_updates |MySQL 5.7, MySQL 8.0, MySQL 8.4 |OFF |No |
|sync_source_info |MySQL 8.0, MySQL 8.4 |10000 |No |
|tls_version |MySQL 5.7 |TLSv1,TLSv1.1,TLSv1.2 |Yes |
|innodb_large_prefix |MySQL 5.7 |ON |No |
|default_time_zone |MySQL 5.7, MySQL 8.0, MySQL 8.4 |+08:00 |Yes |
|sql_mode |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |No |


<span id=".5Lul5LiL5Y-C5pWw55qE5YC85b-F6aG76K6-5a6a5Li6LWJsb2NrLXNpemUt55qE5YCN5pWw"></span>
## The value for the following parameters must be a multiple of `block_size`.

For some system variables, if the set value is not an integer multiple of the specified block size (`block_size`), the server rounds it down to the next smaller multiple of the block size before storing it, that is, [FLOOR(value)](https://dev.mysql.com/doc/refman/8.0/en/mathematical-functions.html#function_floor)\* block_size. For example, assume a given variable has a block size of 4096, and its value is set to 100,000 (assuming that the maximum value of the variable is greater than this number). Since 100,000 / 4096 = 24.4140625, the server automatically reduces the value to 98,304 (24 \* 4096) before storage.

In some cases, the specified maximum value for a variable is the maximum value allowed by the MySQL parser, but it is not an exact multiple of the block size. In this case, the effective maximum value is the next smaller multiple of the block size. For example, the maximum value for the system variable is displayed as 4294967295 (2^32 \- 1), and its block size is 1024. 4294967295 / 1024 = 4194303.9990234375. Therefore, if this variable is set to its specified maximum value, the actual stored value is 4194303 \* 1024 = 4294966272.

For more details about `block_size`, refer to [MySQL server system variables](https://dev.mysql.com/doc/refman/8.0/en/server-system-variables.html).


* `block_size` is 1024

   
   |Parameter name |Instance version |Parameter default value |Need to restart |
   |---|---|---|---|
   |TRANSACTION_ALLOC_BLOCK_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |8192 |No |
   |THREAD_STACK |MySQL 5.7, MySQL 8.0, MySQL 8.4 |1048576 |Yes |
   |INNODB_BUFFER_POOL_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 | |No |
   |TRANSACTION_PREALLOC_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |4096 |No |
   |MAX_ALLOWED_PACKET |MySQL 5.7, MySQL 8.0, MySQL 8.4 |1073741824 |No |
   |QUERY_ALLOC_BLOCK_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |8192 |No |
   |MAX_HEAP_TABLE_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |67108864 |No |
   |NET_BUFFER_LENGTH |MySQL 5.7, MySQL 8.0, MySQL 8.4 |16384 |No |
   |QUERY_PREALLOC_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |8192 |No |
   |RANGE_ALLOC_BLOCK_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |4096 |No |
   |QUERY_CACHE_SIZE |MySQL 5.7 |0 |No |
   

* `block_size` is 128

   
   |Parameter name |Instance version |Parameter default value |Need to restart |
   |---|---|---|---|
   |JOIN_BUFFER_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 | |No |
   

* `block_size` is 100

   
   |Parameter name |Instance version |Parameter default value |Need to restart |
   |---|---|---|---|
   |KEY_CACHE_AGE_THRESHOLD |MySQL 5.7, MySQL 8.0, MySQL 8.4 |300 |No |
   

* `block_size` is 512

   
   |Parameter name |Instance version |Parameter default value |Need to restart |
   |---|---|---|---|
   |KEY_CACHE_BLOCK_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |1024 |No |
   

* `block_size` is 4096

   
   |Parameter name |Instance version |Parameter default value |Need to restart |
   |---|---|---|---|
   |READ_BUFFER_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 | |No |
   |BINLOG_CACHE_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |2097152 |No |
   |BINLOG_STMT_CACHE_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |32768 |No |
   |MAX_BINLOG_CACHE_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |18446744073709547520 |No |
   |MAX_BINLOG_STMT_CACHE_SIZE |MySQL 5.7, MySQL 8.0, MySQL 8.4 |18400000000000000000 |No |
   


&nbsp;

<span id=".aW5ub2RiLXRlbXAtZGF0YS1maWxlLXBhdGgt5Y-C5pWw55qE6K6-5a6a6ZmQ5Yi2"></span>
## Restrictions on setting the `innodb_temp_data_file_path` Parameter


|Parameter name |Instance version |Parameter default value |Need to restart |
|---|---|---|---|
|innodb_temp_data_file_path |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ibtmp1:50M:autoextend:max:30G |Yes |


The value of `innodb_temp_data_file_path` can be set to `ibtmp1:LM:autoextend` or `ibtmp1:LM:autoextend:max:NG`. L and N are positive integers, where L is greater than or equal to 12 and N is greater than or equal to 1.

&nbsp;

<span id=".5Lul5LiL5Y-C5pWw5LiN5YWB6K646K6-572u5Li656m6"></span>
## The following parameters cannot be set to empty


|Parameter name |Instance version |Parameter default value |Need to restart |
|---|---|---|---|
|slave_type_conversions |MySQL 5.7 |\- |No |
|init_connect |MySQL 5.7, MySQL 8.0, MySQL 8.4 |\- |No |
|sql_mode |MySQL 5.7, MySQL 8.0, MySQL 8.4 |ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |No |


<span id=".5a2Y5Zyo5L6d6LWW5YWz57O755qE5Y-C5pWw"></span>
## Dependent parameters

The following parameters have dependencies. When modifying them, ensure that their values comply with the dependency rules.


|Parameter |Rules |
|---|---|
|innodb_buffer_pool_instances and innodb_page_cleaners |innodb_page_cleaners cannot be greater than innodb_buffer_pool_instances. |
|innodb_io_capacity and innodb_io_capacity_max |Innodb_io_capacity cannot be greater than innodb_io_capacity_max. |
|innodb_max_dirty_pages_pct_lwm and innodb_max_dirty_pages_pct |innodb_max_dirty_pages_pct_lwm cannot be greater than innodb_max_dirty_pages_pct. |
|innodb_temp_data_file_path |The value of this parameter must be configured according to the formula ibtmp1:50M:autoextend:max:30G, where the size of L must be no less than 12 and the size of N must be no less than 1. |
|performance_schema_max_thread_instances |This parameter must be used with loose_rds_performance_schema and takes effect only when loose_rds_performance_schema is set to ON. |


<span id=".5YW25LuW6KeE5YiZ"></span>
## Other rules


|Parameter |**Instance version** |Validation rules |**Need to restart** |
|---|---|---|---|
|character_set_server collation_server |MySQL 5.7, MySQL 8.0, MySQL 8.4 |Checks whether the character set and collation for instance creation are valid. If valid, the converted value is returned. |Yes |
|innodb_io_capacity<br><br>innodb_io_capacity_max |MySQL 5.7, MySQL 8.0, MySQL 8.4 |`Innodb_io_capacity` cannot be greater than `innodb_io_capacity_max`. |No |
|innodb_page_cleaners<br><br>innodb_buffer_pool_instances |MySQL 5.7, MySQL 8.0, MySQL 8.4 |`innodb_page_cleaners` cannot be greater than `innodb_buffer_pool_instances`. |Yes |
|innodb_max_dirty_pages_pct_lwm<br><br>innodb_max_dirty_pages_pct |MySQL 5.7, MySQL 8.0, MySQL 8.4 |`innodb_max_dirty_pages_pct_lwm` cannot be greater than `innodb_max_dirty_pages_pct`. |No |
|innodb_buffer_pool_size<br><br>&nbsp;<br><br> |MySQL 5.7, MySQL 8.0, MySQL 8.4<br><br> |* When innodb_buffer_pool_size is less than 1 GiB, the system will forcibly override innodb_buffer_pool_instances to 1 regardless of the configured value.<br><br>* When innodb_buffer_pool_size is greater than or equal to 1 GiB, you can customize the innodb_buffer_pool_instances configuration, with a maximum value of 64 for this parameter. |No |
|innodb_buffer_pool_instances |||Yes |


&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If some parameters in the table above are not found in the Parameter list, it may be because your instance is not the latest Version. You can <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support.</div>
