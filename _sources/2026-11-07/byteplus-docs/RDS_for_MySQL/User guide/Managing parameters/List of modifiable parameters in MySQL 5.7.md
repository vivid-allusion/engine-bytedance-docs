---
title: "List of modifiable parameters in MySQL 5.7"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7"
---

This topic introduces the modifiable parameters that RDS for MySQL provides for MySQL 5.7 instances, as well as their default values, value ranges, and whether a restart is required after modification.


|Parameter name |Supported engine type |Parameter default value |Whether an instance restart is required for the change to take effect |Value range |
|---|---|---|---|---|
|auto_increment_increment |InnoDB, RocksDB |1 |No |[1\-65535] |
|auto_increment_offset |InnoDB, RocksDB |1 |No |[1\-65535] |
|automatic_sp_privileges |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|avoid_temporal_upgrade |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|back_log |InnoDB, RocksDB |3000 |Yes |[1\-65535] |
|binlog_cache_size |InnoDB, RocksDB |2097152 |No |[4096\-16777216] |
|binlog_checksum |InnoDB, RocksDB |CRC32 |Yes |[CRC32\|NONE] |
|binlog_order_commits |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|binlog_row_image |InnoDB, RocksDB |full |No |[full\|minimal] |
|binlog_rows_query_log_events |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|binlog_stmt_cache_size |InnoDB, RocksDB |32768 |No |[4096\-16777216] |
|block_encryption_mode |InnoDB, RocksDB |aes\-128\-ecb |No |[aes\-128\-ecb\|aes\-192\-ecb\|aes\-256\-ecb\|aes\-128\-cbc\|aes\-192\-cbc\|aes\-256\-cbc] |
|bulk_insert_buffer_size |InnoDB, RocksDB |4194304 |No |[0\-4294967295] |
|character_set_filesystem |InnoDB, RocksDB |binary |No |[utf8\|latin1\|gbk\|binary] |
|character_set_server |InnoDB, RocksDB |utf8 |Yes |[utf8\|latin1\|gbk\|gb18030\|utf8mb4] |
|collation_server |InnoDB, RocksDB |utf8_general_ci |Yes |[utf8_general_ci\|utf8_bin\|utf8_unicode_ci\|utf8_icelandic_ci\|utf8_latvian_ci\|utf8_romanian_ci\|utf8_slovenian_ci\|utf8_polish_ci\|utf8_estonian_ci\|utf8_spanish_ci\|utf8_swedish_ci\|utf8_turkish_ci\|utf8_czech_ci\|utf8_danish_ci\|utf8_lithuanian_ci\|utf8_slovak_ci\|utf8_spanish2_ci\|utf8_roman_ci\|utf8_persian_ci\|utf8_esperanto_ci\|utf8_hungarian_ci\|utf8_sinhala_ci\|utf8_german2_ci\|utf8_croatian_ci\|utf8_unicode_520_ci\|utf8_vietnamese_ci\|utf8_general_mysql500_ci\|latin1_bin\|latin1_danish_ci\|latin1_general_ci\|latin1_general_cs\|latin1_german1_ci\|latin1_german2_ci\|latin1_spanish_ci\|latin1_swedish_ci\|gbk_bin\|gbk_chinese_ci\|gb18030_bin\|gb18030_chinese_ci\|gb18030_unicode_520_ci\|utf8mb4_general_ci\|utf8mb4_bin\|utf8mb4_unicode_ci\|utf8mb4_icelandic_ci\|utf8mb4_latvian_ci\|utf8mb4_romanian_ci\|utf8mb4_slovenian_ci\|utf8mb4_polish_ci\|utf8mb4_estonian_ci\|utf8mb4_spanish_ci\|utf8mb4_swedish_ci\|utf8mb4_turkish_ci\|utf8mb4_czech_ci\|utf8mb4_danish_ci\|utf8mb4_lithuanian_ci\|utf8mb4_slovak_ci\|utf8mb4_spanish2_ci\|utf8mb4_roman_ci\|utf8mb4_persian_ci\|utf8mb4_esperanto_ci\|utf8mb4_hungarian_ci\|utf8mb4_sinhala_ci\|utf8mb4_german2_ci\|utf8mb4_croatian_ci\|utf8mb4_unicode_520_ci\|utf8mb4_vietnamese_ci] |
|concurrent_insert |InnoDB, RocksDB |AUTO |No |[NEVER\|AUTO\|ALWAYS] |
|connect_timeout |InnoDB, RocksDB |10 |No |[2\-3600] |
|default_time_zone |InnoDB, RocksDB |+08:00 |Yes |[SYSTEM\|\-12:00\|\-11:00\|\-10:00\|\-09:00\|\-08:00\|\-07:00\|\-06:00\|\-05:00\|\-04:00\|\-03:00\|\-02:00\|\-01:00\|+00:00\|+01:00\|+02:00\|+03:00\|+04:00\|+05:00\|+05:30\|+06:00\|+06:30\|+07:00\|+08:00\|+09:00\|+10:00\|+11:00\|+12:00\|+13:00] |
|default_week_format |InnoDB, RocksDB |0 |No |[0\-7] |
|delay_key_write |InnoDB, RocksDB |ON |No |[ON\|OFF\|ALL] |
|delayed_insert_timeout |InnoDB, RocksDB |300 |No |[1\-3600] |
|disconnect_on_expired_password |InnoDB, RocksDB |ON |Yes |[ON\|OFF] |
|div_precision_increment |InnoDB, RocksDB |4 |No |[0\-30] |
|end_markers_in_json |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|eq_range_index_dive_limit |InnoDB, RocksDB |100 |No |[0\-4294967295] |
|event_scheduler |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|explicit_defaults_for_timestamp |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|flush_time |InnoDB, RocksDB |0 |No |[0\-31536000] |
|ft_max_word_len |InnoDB, RocksDB |84 |Yes |[10\-84] |
|ft_min_word_len |InnoDB, RocksDB |4 |Yes |[1\-84] |
|ft_query_expansion_limit |InnoDB, RocksDB |20 |Yes |[0\-1000] |
|general_log |InnoDB, RocksDB |OFF |No |[OFF] |
|group_concat_max_len |InnoDB, RocksDB |1024 |No |[4\-1844674407370954752] |
|host_cache_size |InnoDB, RocksDB |644 |No |[0\-65535] |
|init_connect |InnoDB, RocksDB |\- |No |[Empty\|set names utf8mb4\|set names utf8\|set names utf8mb4 collate utf8mb4_general_ci] |
|innodb_adaptive_flushing |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_adaptive_flushing_lwm |InnoDB, RocksDB |10 |No |[0\-70] |
|innodb_adaptive_hash_index |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_adaptive_max_sleep_delay |InnoDB, RocksDB |150000 |No |[1\-1000000] |
|innodb_autoextend_increment |InnoDB, RocksDB |64 |No |[1\-1000] |
|innodb_autoinc_lock_mode |InnoDB, RocksDB |2 |Yes |[0\|1\|2] |
|innodb_buffer_pool_dump_at_shutdown |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_buffer_pool_dump_pct |InnoDB, RocksDB |25 |No |[1\-100] |
|innodb_buffer_pool_instances |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824, 8)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |Yes |[1\-64] |
|innodb_buffer_pool_load_at_startup |InnoDB, RocksDB |ON |Yes |[ON\|OFF] |
|innodb_buffer_pool_size |InnoDB |{DBInstanceMemory\*3/4}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[134217728\-1099511627776] |
|innodb_change_buffer_max_size |InnoDB, RocksDB |25 |No |[0\-50] |
|innodb_change_buffering |InnoDB, RocksDB |none |No |[none\|inserts\|deletes\|changes\|purges\|all] |
|innodb_cmp_per_index_enabled |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_commit_concurrency |InnoDB, RocksDB |0 |Yes |[0\-1000] |
|innodb_compression_failure_threshold_pct |InnoDB, RocksDB |5 |No |[0\-100] |
|innodb_compression_level |InnoDB, RocksDB |6 |No |[0\-9] |
|innodb_compression_pad_pct_max |InnoDB, RocksDB |50 |No |[0\-70] |
|innodb_concurrency_tickets |InnoDB, RocksDB |5000 |No |[1\-4294967295] |
|innodb_deadlock_detect |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_disable_sort_file_cache |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_flush_log_at_trx_commit |InnoDB, RocksDB |1 |No |[0\|1\|2] |
|innodb_flush_method |InnoDB, RocksDB |O_DIRECT |Yes |[fsync\|O_DSYNC\|O_DIRECT\|O_DIRECT_NO_FSYNC] |
|innodb_flush_neighbors |InnoDB, RocksDB |0 |No |[0\|1\|2] |
|innodb_flush_sync |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_ft_cache_size |InnoDB, RocksDB |8000000 |Yes |[1600000\-80000000] |
|innodb_ft_enable_diag_print |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_ft_enable_stopword |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_ft_max_token_size |InnoDB, RocksDB |84 |Yes |[10\-84] |
|innodb_ft_min_token_size |InnoDB, RocksDB |3 |Yes |[0\-16] |
|innodb_ft_num_word_optimize |InnoDB, RocksDB |2000 |No |[1000\-10000] |
|innodb_ft_result_cache_limit |InnoDB, RocksDB |2000000000 |No |[1000000\-4294967295] |
|innodb_ft_sort_pll_degree |InnoDB, RocksDB |2 |Yes |[1\-16] |
|innodb_ft_total_cache_size |InnoDB, RocksDB |640000000 |Yes |[32000000\-1600000000] |
|innodb_io_capacity |InnoDB, RocksDB |20000 |No |[100\-4294967295] |
|innodb_io_capacity_max |InnoDB, RocksDB |40000 |No |[100\-4294967295] |
|innodb_large_prefix |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_lock_wait_timeout |InnoDB, RocksDB |50 |No |[1\-1073741824] |
|innodb_log_checksums |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_log_compressed_pages |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_log_file_size |InnoDB, RocksDB |1073741824 |Yes |[4194304\-107374182400] |
|innodb_lru_scan_depth |InnoDB, RocksDB |{BY_STORAGE_TYPE(1024, 100)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[100\-4294967295] |
|innodb_max_dirty_pages_pct |InnoDB, RocksDB |75 |No |[0\-99] |
|innodb_max_dirty_pages_pct_lwm |InnoDB, RocksDB |10 |No |[0\-99] |
|innodb_max_purge_lag |InnoDB, RocksDB |0 |No |[0\-4294967295] |
|innodb_max_purge_lag_delay |InnoDB, RocksDB |0 |No |[0\-10000000] |
|innodb_max_undo_log_size |InnoDB, RocksDB |1073741824 |No |[10485760\-18446744073709551615] |
|innodb_monitor_enable |InnoDB, RocksDB |all |No |[all] |
|innodb_old_blocks_pct |InnoDB, RocksDB |37 |No |[5\-95] |
|innodb_old_blocks_time |InnoDB, RocksDB |1000 |No |[0\-1024] |
|innodb_online_alter_log_max_size |InnoDB, RocksDB |134217728 |No |[134217728\-2147483647] |
|innodb_open_files |InnoDB, RocksDB |3000 |Yes |[10\-8192] |
|innodb_optimize_fulltext_only |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_page_cleaners |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824, 8)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |Yes |[1\-64] |
|innodb_print_all_deadlocks |InnoDB, RocksDB |ON |No |[OFF\|ON] |
|innodb_purge_batch_size |InnoDB, RocksDB |300 |Yes |[1\-5000] |
|innodb_purge_rseg_truncate_frequency |InnoDB, RocksDB |128 |No |[1\-128] |
|innodb_purge_threads |InnoDB, RocksDB |1 |Yes |[1\-32] |
|innodb_random_read_ahead |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_read_ahead_threshold |InnoDB, RocksDB |56 |No |[0\-64] |
|innodb_read_io_threads |InnoDB, RocksDB |4 |Yes |[1\-64] |
|innodb_rollback_on_timeout |InnoDB, RocksDB |OFF |Yes |[OFF\|ON] |
|innodb_rollback_segments |InnoDB, RocksDB |128 |No |[1\-128] |
|innodb_spin_wait_delay |InnoDB, RocksDB |6 |No |[0\-1000] |
|innodb_stats_auto_recalc |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_stats_method |InnoDB, RocksDB |nulls_equal |No |[nulls_equal\|nulls_unequal\|nulls_ignored] |
|innodb_stats_on_metadata |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_stats_persistent |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_stats_persistent_sample_pages |InnoDB, RocksDB |20 |No |[1\-4294967295] |
|innodb_stats_sample_pages |InnoDB, RocksDB |8 |No |[1\-4294967296] |
|innodb_stats_transient_sample_pages |InnoDB, RocksDB |8 |No |[1\-4294967295] |
|innodb_status_output |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_status_output_locks |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_strict_mode |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|innodb_sync_array_size |InnoDB, RocksDB |1024 |Yes |[1\-1024] |
|innodb_sync_spin_loops |InnoDB, RocksDB |30 |No |[0\-4294967295] |
|innodb_table_locks |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_temp_data_file_path |InnoDB, RocksDB |ibtmp1:50M:autoextend:max:30G |Yes |\- |
|innodb_thread_concurrency |InnoDB, RocksDB |0 |No |[0\-1000] |
|innodb_thread_sleep_delay |InnoDB, RocksDB |10000 |No |[0\-1000000] |
|innodb_undo_log_truncate |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|innodb_write_io_threads |InnoDB, RocksDB |4 |Yes |[1\-64] |
|interactive_timeout |InnoDB, RocksDB |7200 |No |[10\-86400] |
|join_buffer_size |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1048576\*128, 262144)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[128\-4294967295] |
|key_cache_age_threshold |InnoDB, RocksDB |300 |No |[100\-4294967295] |
|key_cache_block_size |InnoDB, RocksDB |1024 |No |[512\-16384] |
|key_cache_division_limit |InnoDB, RocksDB |100 |No |[1\-100] |
|kill_idle_transaction |InnoDB, RocksDB |0 |No |[0\-31536000] |
|lc_time_names |InnoDB, RocksDB |en_US |No |[ja_JP\|pt_BR\|en_US] |
|local_infile |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|lock_wait_timeout |InnoDB, RocksDB |31536000 |No |[1\-31536000] |
|log_bin_use_v1_row_events |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|log_error_verbosity |InnoDB, RocksDB |2 |No |[1\-3] |
|log_queries_not_using_indexes |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|log_slow_admin_statements |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|log_throttle_queries_not_using_indexes |InnoDB, RocksDB |0 |No |[0\-4294967295] |
|long_query_time |InnoDB, RocksDB |1 |No |[0.1\-31536000] |
|loose_binlog_large_trans_threshold |InnoDB, RocksDB |268435456 |No |[20971520\-18446744073709551615] |
|loose_binlog_lock_striping |InnoDB |ON |Yes |[ON\|OFF] |
|loose_buffered_scan |InnoDB |OFF |No |[ON\|OFF] |
|loose_buffered_scan_threshold |InnoDB<br><br> |1000<br><br> |No |[0\-18446744073709551615] |
|loose_convert_disabled_engines_to_innodb |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|loose_enable_binlog_large_trans_opt |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_enable_binlog_preallocate |InnoDB |ON |Yes |[ON\|OFF] |
|loose_enable_in_list_optimization |InnoDB, RocksDB |OFF |No |[ON\|OFF\|AUTO] |
|loose_enable_logical_prefetch_page |InnoDB |OFF |No |[ON\|OFF] |
|loose_enable_plan_cache |InnoDB |OFF |No |[ON\|OFF] |
|loose_enable_track_index_io |InnoDB |OFF |No |[ON\|OFF] |
|loose_event_replica_consistent |InnoDB |ON |No |[ON\|OFF] |
|loose_extend_varchar_enhance |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_logical_prefetch_rows_threshold<br><br> |InnoDB |32768 |No |[1\-4294967295] |
|loose_in_list_optimization_threshold |InnoDB, RocksDB |32768 |No |[1\-4294967295] |
|loose_innodb_autoinc_persistent |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_innodb_autoinc_persistent_interval |InnoDB, RocksDB |1 |No<br><br> |[1, 10000] |
|loose_innodb_data_file_logic_drop |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_innodb_data_file_logic_drop_max_size |InnoDB, RocksDB |1024 |No |[128\-2048] |
|loose_innodb_ddl_buffer_size |InnoDB |1048576 |No |[65536\-4294967295] |
|loose_innodb_ddl_threads |InnoDB |4 |No |[1\-64] |
|loose_innodb_default_index_merge_threshold<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only kernel versions between <strong> </strong><strong><code>MySQL 5.7.44_20251015 ~ MySQL 5.7.44_20260216</code></strong><strong> </strong> support this parameter.</div><br> |InnoDB |{BY_STORAGE_TYPE(50, 25)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is an expression parameter. For details about the value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[1\-50] |
|loose_innodb_instant_ddl_enabled |InnoDB |OFF |No |[ON\|OFF] |
|loose_innodb_parallel_ddl |InnoDB |OFF |No |[ON\|OFF] |
|loose_innodb_parallel_read_threads |InnoDB |4 |No |[1\-256] |
|loose_innodb_use_fdatasync |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_limit_offset_pushdown_threshold |InnoDB |\-1 |No |[\-1\-9223372036854775807] |
|loose_prefer_user_defined_function |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|loose_rds_flashback_query |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_rds_flashback_query_window |InnoDB, RocksDB |900 |No |[1\-604800] |
|loose_rds_performance_schema |InnoDB, RocksDB |ON |Yes |[ON\|OFF] |
|loose_recycle_bin |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_recycle_bin_retention |InnoDB, RocksDB |604800 |No |[1\-31536000] |
|loose_recycle_scheduler |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|loose_recycle_scheduler_interval |InnoDB, RocksDB |30 |No |[1\-60] |
|loose_thread_handling_switch_mode |InnoDB, RocksDB |handling_switch_off |No |[handling_switch_off\|handling_switch_new\|handling_switch_all] |
|loose_thread_pool_enabled |InnoDB, RocksDB |ON |* For **MySQL 5.7.44_20260415 and later** instances: When the value of the `loose_thread_handling_switch_mode` parameter is `handling_switch_new` or `handling_switch_all`, modifying this parameter does not require an instance restart; otherwise, an instance restart is required.<br><br>* For instances with kernel versions **earlier than MySQL 5.7.44_20260415**, modifying this parameter requires an instance restart. |[ON\|OFF] |
|loose_thread_pool_oversubscribe |InnoDB, RocksDB |16 |No |[2\-128] |
|loose_thread_pool_size |InnoDB, RocksDB |{MAX(DBInstanceCpu, 2)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[1\-64] |
|low_priority_updates |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|lower_case_table_names |InnoDB, RocksDB |1 |Yes |[0\|1] |
|master_verify_checksum |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|max_allowed_packet |InnoDB, RocksDB |1073741824 |No |[16384\-1073741824] |
|max_binlog_cache_size |InnoDB, RocksDB |18446744073709547520 |No |[4096\-18446744073709547520] |
|max_binlog_stmt_cache_size |InnoDB, RocksDB |18400000000000000000 |No |[4096\-18446744073709547520] |
|max_connect_errors |InnoDB, RocksDB |100 |No |[1\-4294967295] |
|max_connections |InnoDB, RocksDB |{MAP(DBInstanceCpu, DBInstanceMemory)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |* For instances with MySQL 5.7.44_20260415 and earlier kernel minor versions, the value range is [100\-100000].<br><br>* For instances with MySQL 5.7.44_20260415 and above kernel minor versions, the value range is [100\-200000]. |
|max_error_count |InnoDB, RocksDB |64 |No |[0\-65535] |
|max_execution_time |InnoDB, RocksDB |0 |No |[0\-4294967295] |
|max_heap_table_size |InnoDB, RocksDB |67108864 |No |[16384\-1844674407370954752] |
|max_join_size |InnoDB, RocksDB |18446744073709551615 |No |[1\-18446744073709551615] |
|max_length_for_sort_data |InnoDB, RocksDB |1024 |No |[4\-8388608] |
|max_points_in_geometry |InnoDB, RocksDB |65536 |No |[3\-1048576] |
|max_prepared_stmt_count |InnoDB, RocksDB |16382 |No |[0\-1048576] |
|max_seeks_for_key |InnoDB, RocksDB |18400000000000000000 |No |[1\-18446744073709551615] |
|max_sort_length |InnoDB, RocksDB |1024 |No |[4\-8388608] |
|max_sp_recursion_depth |InnoDB, RocksDB |0 |No |[0\-255] |
|max_user_connections |InnoDB, RocksDB |0 |No |* For instances with MySQL 5.7.44_20260415 and earlier kernel minor versions, the value range is [0\|100\-100000].<br><br>* For instances with MySQL 5.7.44_20260415 and above kernel minor versions, the value range is [0\|100\-200000]. |
|max_write_lock_count |InnoDB, RocksDB |102400 |No |[1\-102400] |
|metadata_locks_cache_size |InnoDB, RocksDB |1024 |Yes |[1\-1048576] |
|min_examined_row_limit |InnoDB, RocksDB |0 |No |[0\-4294967295] |
|myisam_sort_buffer_size |InnoDB, RocksDB |262144 |No |[262144\-16777216] |
|mysql_native_password_proxy_users |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|net_buffer_length |InnoDB, RocksDB |16384 |No |[1024\-1048576] |
|net_read_timeout |InnoDB, RocksDB |30 |No |[1\-31536000] |
|net_retry_count |InnoDB, RocksDB |10 |No |[1\-4294967295] |
|net_write_timeout |InnoDB, RocksDB |60 |No |[1\-31536000] |
|ngram_token_size |InnoDB, RocksDB |2 |Yes |[1\-10] |
|open_files_limit |InnoDB, RocksDB |1048576 |Yes |[4000\-1073741824] |
|optimizer_prune_level |InnoDB, RocksDB |1 |No |[0\|1] |
|optimizer_search_depth |InnoDB, RocksDB |62 |No |[0\-62] |
|optimizer_switch |InnoDB, RocksDB |batched_key_access=off,block_nested_loop=on,condition_fanout_filter=on,derived_merge=on,duplicateweedout=on,engine_condition_pushdown=on,firstmatch=on,index_condition_pushdown=on,index_merge=on,index_merge_intersection=on,index_merge_sort_union=on,index_merge_union=on,loosescan=on,materialization=on,mrr=on,mrr_cost_based=on,semijoin=on,subquery_materialization_cost_based=on,use_index_extensions=on |No |\- |
|optimizer_trace_limit |InnoDB, RocksDB |1 |No |[0\-4294967295] |
|optimizer_trace_max_mem_size |InnoDB, RocksDB |16384 |No |[0\-4294967295] |
|optimizer_trace_offset |InnoDB, RocksDB |\-1 |No |[\-1\-4294967295] |
|performance_schema |InnoDB, RocksDB |OFF |Yes |[ON\|OFF] |
|performance_schema_max_thread_instances |InnoDB, RocksDB |\-1 |Yes |[\-1\-1048576] |
|preload_buffer_size |InnoDB, RocksDB |32768 |No |[1024\-1073741824] |
|query_alloc_block_size |InnoDB, RocksDB |8192 |No |[1024\-16384] |
|query_cache_limit |InnoDB, RocksDB |1048576 |No |[1\-1048576] |
|query_cache_min_res_unit |InnoDB, RocksDB |1024 |No |[512\-18446744073709551608] |
|query_cache_size |InnoDB, RocksDB |0 |No |[0\-10485760000] |
|query_cache_type |InnoDB, RocksDB |OFF |Yes |[OFF\|ON\|DEMAND] |
|query_cache_wlock_invalidate |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|query_prealloc_size |InnoDB, RocksDB |8192 |No |[8192\-1048576] |
|range_alloc_block_size |InnoDB, RocksDB |4096 |No |[4096\-18446744073709550592] |
|range_optimizer_max_mem_size |InnoDB, RocksDB |8388608 |Yes |[0\-18446744073709551615] |
|read_buffer_size |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1048576\*128, 262144)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[8192\-2147479552] |
|relay_log_recovery |InnoDB, RocksDB |ON |Yes |[ON\|OFF] |
|rocksdb_compaction_sequential_deletes |RocksDB |10 |No |[0\-2000000] |
|rocksdb_deadlock_detect |RocksDB |ON |No |[ON\|OFF] |
|rocksdb_flush_log_at_trx_commit |RocksDB |1 |No |[0\|1\|2] |
|rocksdb_large_table_drop_compact_protect_enable |RocksDB |OFF |No |[ON\|OFF] |
|rocksdb_lock_wait_timeout |RocksDB |50 |No |[1\-1073741824] |
|rocksdb_max_row_locks |RocksDB |1048576 |No |[1\-1073741824] |
|rocksdb_merge_buf_size |RocksDB |524288 |No |[100\-18446744073709551615] |
|rocksdb_merge_combine_read_size |RocksDB |8388608 |No |[100\-18446744073709551615] |
|rocksdb_track_and_verify_wals_in_manifest |RocksDB |OFF |Yes |[ON\|OFF] |
|rocksdb_write_policy |RocksDB |write_committed |Yes |[write_committed\|write_prepared\|write_unprepared] |
|session_track_gtids |InnoDB, RocksDB |OFF |No |[OFF\|OWN_GTID\|ALL_GTIDS] |
|sha256_password_proxy_users |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|show_old_temporals |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|slave_net_timeout |InnoDB, RocksDB |60 |No |[1\-31536000] |
|slave_parallel_type<br><br> |InnoDB |LOGICAL_CLOCK |Yes |DATABASE \| LOGICAL_CLOCK \| TABLE |
|slave_type_conversions |InnoDB, RocksDB |\- |Yes |[Empty\|ALL_LOSSY\|ALL_NON_LOSSY\|ALL_LOSSY,ALL_NON_LOSSY\|ALL_SIGNED\|ALL_UNSIGNED\|ALL_SIGNED,ALL_UNSIGNED] |
|slow_launch_time |InnoDB, RocksDB |2 |No |[1\-1024] |
|slow_query_log |InnoDB, RocksDB |ON |No |[ON\|OFF] |
|sort_buffer_size |InnoDB, RocksDB |262144 |No |[32768\-4294967295] |
|sql_mode |InnoDB, RocksDB |ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION |No |[\*ALLOW_INVALID_DATES\|ANSI_QUOTES\|ERROR_FOR_DIVISION_BY_ZERO\|HIGH_NOT_PRECEDENCE\|IGNORE_SPACE\|NO_AUTO_CREATE_USER\|NO_AUTO_VALUE_ON_ZERO\|NO_BACKSLASH_ESCAPES\|NO_DIR_IN_CREATE\|NO_ENGINE_SUBSTITUTION\|NO_FIELD_OPTIONS\|NO_KEY_OPTIONS\|NO_TABLE_OPTIONS\|NO_UNSIGNED_SUBTRACTION\|NO_ZERO_DATE\|NO_ZERO_IN_DATE\|ONLY_FULL_GROUP_BY\|PAD_CHAR_TO_FULL_LENGTH\|PIPES_AS_CONCAT\|REAL_AS_FLOAT\|STRICT_ALL_TABLES\|STRICT_TRANS_TABLES] |
|sql_safe_updates |InnoDB, RocksDB |OFF |No |[ON\|OFF] |
|stored_program_cache |InnoDB, RocksDB |256 |No |[16\-524288] |
|sync_binlog |InnoDB, RocksDB |1 |No |[0\-4294967295] |
|sync_master_info |InnoDB, RocksDB |10000 |No |[0\-4294967295] |
|sync_relay_log_info |InnoDB, RocksDB |10000 |No |[0\-4294967295] |
|table_definition_cache |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824\*512, 2048)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[400\-80480] |
|table_open_cache |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824\*256, 2048)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[1\-524288] |
|table_open_cache_instances |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824, 16)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |Yes |[1\-64] |
|thread_cache_size |InnoDB, RocksDB |{LEAST(DBInstanceMemory/1073741824\*512, 2048)}<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is an expression parameter. For details about value rules, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically">Expression parameters</a>.</div><br> |No |[0\-16384] |
|thread_stack |InnoDB, RocksDB |1048576 |Yes |[131072\-2147482624] |
|tls_version |InnoDB, RocksDB |TLSv1,TLSv1.1,TLSv1.2 |Yes |[TLSv1,TLSv1.1,TLSv1.2\|TLSv1.1,TLSv1.2\|TLSv1.2] |
|tmp_table_size |InnoDB, RocksDB |2097152 |No |[262144\-1073741824] |
|transaction_alloc_block_size |InnoDB, RocksDB |8192 |No |[1024\-131072] |
|transaction_isolation |InnoDB, RocksDB |READ\-COMMITTED |No |[READ\-UNCOMMITTED\|READ\-COMMITTED\|REPEATABLE\-READ\|SERIALIZABLE] |
|transaction_prealloc_size |InnoDB, RocksDB |4096 |No |[1024\-131072] |
|updatable_views_with_limit |InnoDB, RocksDB |YES |No |[YES\|NO] |
|wait_timeout |InnoDB, RocksDB |86400 |No |[1\-31536000] |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

<span id=".5aaC5L2V5p-l6K-i5LqR5pWw5o2u5bqTLW15c3FsLeeJiOS4jeaUr-aMgeS_ruaUueeahOWPguaVsOeahOiuvuWumuWAvO-8nw=="></span>
### How do I check the values of parameters that cannot be modified in RDS for MySQL?

Log on to [Database Workshop](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'Parameter name'` to check the value.
