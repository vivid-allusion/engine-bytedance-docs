---
title: "List of modifiable parameters in MySQL 8.4"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_4"
---

This topic describes the modifiable parameters that RDS for MySQL provides for MySQL 8.4 instances, their default values, value ranges, and whether a restart is required after modification.

|Parameter |Default value |Need restart? |Value range |
|---|---|---|---|
|auto_increment_increment |1 |No |[1\-65535] |
|auto_increment_offset |1 |No |[1\-65535] |
|automatic_sp_privileges |ON |No |[ON\|OFF] |
|back_log |3000 |Yes |[1\-65535] |
|binlog_cache_size |2097152 |No |[4096\-16777216] |
|binlog_checksum |CRC32 |Yes |[CRC32\|NONE] |
|binlog_order_commits |ON |No |[ON\|OFF] |
|binlog_row_image |full |No |[full\|minimal] |
|binlog_rows_query_log_events |OFF |No |[ON\|OFF] |
|binlog_stmt_cache_size |32768 |No |[4096\-16777216] |
|block_encryption_mode |aes\-128\-ecb |No |[aes\-128\-ecb\|aes\-192\-ecb\|aes\-256\-ecb\|aes\-128\-cbc\|aes\-192\-cbc\|aes\-256\-cbc] |
|bulk_insert_buffer_size |4194304 |No |[0\-4294967295] |
|character_set_filesystem |binary |No |[utf8\|latin1\|gbk\|binary] |
|character_set_server |utf8mb3 |Yes |[utf8mb3\|latin1\|gbk\|gb18030\|utf8mb4] |
|collation_server |utf8_general_ci |Yes |[utf8mb4_0900_ai_ci\|utf8mb4_0900_as_ci\|utf8mb4_0900_as_cs\|utf8mb4_bin\|utf8mb4_croatian_ci\|utf8mb4_cs_0900_ai_ci\|utf8mb4_cs_0900_as_cs\|utf8mb4_czech_ci\|utf8mb4_danish_ci\|utf8mb4_da_0900_ai_ci\|utf8mb4_da_0900_as_cs\|utf8mb4_de_pb_0900_ai_ci\|utf8mb4_de_pb_0900_as_cs\|utf8mb4_eo_0900_ai_ci\|utf8mb4_eo_0900_as_cs\|utf8mb4_esperanto_ci\|utf8mb4_estonian_ci\|utf8mb4_es_0900_ai_ci\|utf8mb4_es_0900_as_cs\|utf8mb4_es_trad_0900_ai_ci\|utf8mb4_es_trad_0900_as_cs\|utf8mb4_et_0900_ai_ci\|utf8mb4_et_0900_as_cs\|utf8mb4_general_ci\|utf8mb4_german2_ci\|utf8mb4_hr_0900_ai_ci\|utf8mb4_hr_0900_as_cs\|utf8mb4_hungarian_ci\|utf8mb4_hu_0900_ai_ci\|utf8mb4_hu_0900_as_cs\|utf8mb4_icelandic_ci\|utf8mb4_is_0900_ai_ci\|utf8mb4_is_0900_as_cs\|utf8mb4_ja_0900_as_cs\|utf8mb4_ja_0900_as_cs_ks\|utf8mb4_latvian_ci\|utf8mb4_la_0900_ai_ci\|utf8mb4_la_0900_as_cs\|utf8mb4_lithuanian_ci\|utf8mb4_lt_0900_ai_ci\|utf8mb4_lt_0900_as_cs\|utf8mb4_lv_0900_ai_ci\|utf8mb4_lv_0900_as_cs\|utf8mb4_persian_ci\|utf8mb4_pl_0900_ai_ci\|utf8mb4_pl_0900_as_cs\|utf8mb4_polish_ci\|utf8mb4_romanian_ci\|utf8mb4_roman_ci\|utf8mb4_ro_0900_ai_ci\|utf8mb4_ro_0900_as_cs\|utf8mb4_ru_0900_ai_ci\|utf8mb4_ru_0900_as_cs\|utf8mb4_sinhala_ci\|utf8mb4_sk_0900_ai_ci\|utf8mb4_sk_0900_as_cs\|utf8mb4_slovak_ci\|utf8mb4_slovenian_ci\|utf8mb4_sl_0900_ai_ci\|utf8mb4_sl_0900_as_cs\|utf8mb4_spanish2_ci\|utf8mb4_spanish_ci\|utf8mb4_sv_0900_ai_ci\|utf8mb4_sv_0900_as_cs\|utf8mb4_swedish_ci\|utf8mb4_tr_0900_ai_ci\|utf8mb4_tr_0900_as_cs\|utf8mb4_turkish_ci\|utf8mb4_unicode_520_ci\|utf8mb4_unicode_ci\|utf8mb4_vietnamese_ci\|utf8mb4_vi_0900_ai_ci\|utf8mb4_vi_0900_as_cs\|utf8mb4_zh_0900_as_cs\|utf8_general_ci\|utf8_bin\|utf8_unicode_ci\|utf8_icelandic_ci\|utf8_latvian_ci\|utf8_romanian_ci\|utf8_slovenian_ci\|utf8_polish_ci\|utf8_estonian_ci\|utf8_spanish_ci\|utf8_swedish_ci\|utf8_turkish_ci\|utf8_czech_ci\|utf8_danish_ci\|utf8_lithuanian_ci\|utf8_slovak_ci\|utf8_spanish2_ci\|utf8_roman_ci\|utf8_persian_ci\|utf8_esperanto_ci\|utf8_hungarian_ci\|utf8_sinhala_ci\|latin1_bin\|latin1_danish_ci\|latin1_general_ci\|latin1_general_cs\|latin1_german1_ci\|latin1_german2_ci\|latin1_spanish_ci\|latin1_swedish_ci\|gbk_bin\|gbk_chinese_ci\|gb18030_bin\|gb18030_chinese_ci\|gb18030_unicode_520_ci] |
|concurrent_insert |AUTO |No |[NEVER\|AUTO\|ALWAYS] |
|connect_timeout |10 |No |[2\-3600] |
|default_authentication_plugin |\- |Yes |[Empty\|mysql_native_password\|caching_sha2_password] |
|default_time_zone |+08:00 |Yes |[SYSTEM\|\-12:00\|\-11:00\|\-10:00\|\-09:00\|\-08:00\|\-07:00\|\-06:00\|\-05:00\|\-04:00\|\-03:00\|\-02:00\|\-01:00\|+00:00\|+01:00\|+02:00\|+03:00\|+04:00\|+05:00\|+05:30\|+05:45\|+06:00\|+06:30\|+07:00\|+08:00\|+09:00\|+10:00\|+11:00\|+12:00\|+13:00] |
|default_week_format |0 |No |[0\-7] |
|delay_key_write |ON |No |[ON\|OFF\|ALL] |
|delayed_insert_limit |100 |No |[1\-4294967295] |
|delayed_insert_timeout |300 |No |[1\-3600] |
|delayed_queue_size |1000 |No |[1\-4294967295] |
|disconnect_on_expired_password |ON |Yes |[ON\|OFF] |
|div_precision_increment |4 |No |[0\-30] |
|end_markers_in_json |OFF |No |[ON\|OFF] |
|eq_range_index_dive_limit |100 |No |[0\-4294967295] |
|event_scheduler |OFF |No |[ON\|OFF] |
|explicit_defaults_for_timestamp |OFF |No |[ON\|OFF] |
|flush_time |0 |No |[0\-31536000] |
|ft_max_word_len |84 |Yes |[10\-84] |
|ft_min_word_len |4 |Yes |[1\-84] |
|ft_query_expansion_limit |20 |Yes |[0\-1000] |
|general_log |OFF |No |[OFF] |
|group_concat_max_len |1024 |No |[4\-1844674407370954752] |
|host_cache_size |644 |No |[0\-65535] |
|init_connect |\- |No |[Empty\|set names utf8mb4\|set names utf8\|set names utf8mb4 collate utf8mb4_general_ci\|set default_collation_for_utf8mb4=utf8mb4_general_ci\|set default_collation_for_utf8mb4=utf8mb4_general_ci;set names utf8mb4\|set @@collation_connection = IF(@@collation_connection = 'utf8mb4_0900_ai_ci', 'utf8mb4_general_ci', @@collation_connection)] |
|innodb_adaptive_flushing |ON |No |[ON\|OFF] |
|innodb_adaptive_flushing_lwm |10 |No |[0\-70] |
|innodb_adaptive_hash_index |OFF |No |[ON\|OFF] |
|innodb_adaptive_max_sleep_delay |150000 |No |[1\-1000000] |
|innodb_autoextend_increment |64 |No |[1\-1000] |
|innodb_autoinc_lock_mode |2 |Yes |[0\|1\|2] |
|innodb_buffer_pool_dump_at_shutdown |ON |No |[ON\|OFF] |
|innodb_buffer_pool_dump_pct |25 |No |[1\-100] |
|innodb_buffer_pool_instances |{LEAST(DBInstanceMemory/1073741824, 8)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |Yes |[1\-64] |
|innodb_buffer_pool_load_at_startup |ON |Yes |[ON\|OFF] |
|innodb_buffer_pool_size |{DBInstanceMemory\*3/4}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[134217728\-1099511627776] |
|innodb_change_buffer_max_size |25 |No |[0\-50] |
|innodb_change_buffering |none |No |[none\|inserts\|deletes\|changes\|purges\|all] |
|innodb_cmp_per_index_enabled |OFF |No |[ON\|OFF] |
|innodb_commit_concurrency |0 |Yes |[0\-1000] |
|innodb_compression_failure_threshold_pct |5 |No |[0\-100] |
|innodb_compression_level |6 |No |[0\-9] |
|innodb_compression_pad_pct_max |50 |No |[0\-70] |
|innodb_concurrency_tickets |5000 |No |[1\-4294967295] |
|innodb_deadlock_detect |ON |No |[ON\|OFF] |
|innodb_disable_sort_file_cache |OFF |No |[ON\|OFF] |
|innodb_flush_log_at_trx_commit |1 |No |[0\|1\|2] |
|innodb_flush_method |O_DIRECT |Yes |[fsync\|O_DSYNC\|littlesync\|nosync\|O_DIRECT\|O_DIRECT_NO_FSYNC] |
|innodb_flush_neighbors |0 |No |[0\|1\|2] |
|innodb_flush_sync |ON |No |[ON\|OFF] |
|innodb_ft_cache_size |8000000 |Yes |[1600000\-80000000] |
|innodb_ft_enable_diag_print |OFF |No |[ON\|OFF] |
|innodb_ft_enable_stopword |ON |No |[ON\|OFF] |
|innodb_ft_max_token_size |84 |Yes |[10\-84] |
|innodb_ft_min_token_size |3 |Yes |[0\-16] |
|innodb_ft_num_word_optimize |2000 |No |[1000\-10000] |
|innodb_ft_result_cache_limit |2000000000 |No |[1000000\-4294967295] |
|innodb_ft_sort_pll_degree |2 |Yes |[1\-16] |
|innodb_ft_total_cache_size |640000000 |Yes |[32000000\-1600000000] |
|innodb_io_capacity |20000 |No |[100\-18446744073709551615] |
|innodb_io_capacity_max |40000 |No |[100\-18446744073709551615] |
|innodb_lock_wait_timeout |50 |No |[1\-1073741824] |
|innodb_log_checksums |ON |No |[ON\|OFF] |
|innodb_log_compressed_pages |OFF |No |[ON\|OFF] |
|innodb_log_writer_threads |* For instances with kernel version MySQL 8.4.7_20260815 and above, the default value is OFF.<br><br>* For instances with kernel versions earlier than MySQL 8.4.7_20260815, the default value is ON. |No |[ON\|OFF] |
|innodb_lru_scan_depth |{BY_STORAGE_TYPE(1024, 100)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[100\-18446744073709551615] |
|innodb_max_dirty_pages_pct |75 |No |[0\-99] |
|innodb_max_dirty_pages_pct_lwm |10 |No |[0\-99] |
|innodb_max_purge_lag |0 |No |[0\-4294967295] |
|innodb_max_purge_lag_delay |0 |No |[0\-10000000] |
|innodb_max_undo_log_size |1073741824 |No |[10485760\-18446744073709551615] |
|innodb_monitor_enable |all |No |[all] |
|innodb_old_blocks_pct |37 |No |[5\-95] |
|innodb_old_blocks_time |1000 |No |[0\-1024] |
|innodb_online_alter_log_max_size |134217728 |No |[134217728\-2147483647] |
|innodb_open_files |3000 |Yes |[1\-8192] |
|innodb_optimize_fulltext_only |OFF |No |[ON\|OFF] |
|innodb_page_cleaners |{LEAST(DBInstanceMemory/1073741824, 8)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |Yes |[1\-64] |
|innodb_print_all_deadlocks |ON |No |[ON\|OFF] |
|innodb_purge_batch_size |300 |Yes |[1\-5000] |
|innodb_purge_rseg_truncate_frequency |128 |No |[1\-128] |
|innodb_purge_threads |1 |Yes |[1\-32] |
|innodb_random_read_ahead |OFF |No |[ON\|OFF] |
|innodb_read_ahead_threshold |56 |No |[0\-64] |
|innodb_read_io_threads |1 |Yes |[1\-64] |
|innodb_rollback_on_timeout |OFF |Yes |[ON\|OFF] |
|innodb_rollback_segments |128 |No |[1\-128] |
|innodb_sort_buffer_size |1048576 |Yes |[65536\-67108864] |
|innodb_spin_wait_delay |6 |No |[0\-1000] |
|innodb_stats_auto_recalc |ON |No |[ON\|OFF] |
|innodb_stats_method |nulls_equal |No |[nulls_equal\|nulls_unequal\|nulls_ignored] |
|innodb_stats_on_metadata |OFF |No |[ON\|OFF] |
|innodb_stats_persistent |ON |No |[ON\|OFF] |
|innodb_stats_persistent_sample_pages |20 |No |[1\-4294967295] |
|innodb_stats_transient_sample_pages |8 |No |[1\-4294967295] |
|innodb_status_output |OFF |No |[ON\|OFF] |
|innodb_status_output_locks |OFF |No |[ON\|OFF] |
|innodb_strict_mode |OFF |No |[ON\|OFF] |
|innodb_sync_array_size |512 |Yes |[1\-1024] |
|innodb_sync_spin_loops |30 |No |[0\-4294967295] |
|innodb_table_locks |ON |No |[ON\|OFF] |
|innodb_temp_data_file_path |ibtmp1:50M:autoextend:max:30G |Yes |\- |
|innodb_thread_concurrency |0 |No |[0\-1000] |
|innodb_thread_sleep_delay |10000 |No |[0\-1000000] |
|innodb_write_io_threads |1 |Yes |[1\-64] |
|interactive_timeout |7200 |No |[10\-86400] |
|join_buffer_size |{LEAST(DBInstanceMemory/1048576\*128, 262144)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[128\-4294967295] |
|key_cache_age_threshold |300 |No |[100\-4294967295] |
|key_cache_block_size |1024 |No |[512\-16384] |
|key_cache_division_limit |100 |No |[1\-100] |
|kill_idle_transaction |0 |No |[0\-31536000] |
|lc_time_names |en_US |No |[ja_JP\|pt_BR\|en_US] |
|local_infile |ON |No |[ON\|OFF] |
|lock_wait_timeout |31536000 |No |[1\-31536000] |
|log_error_verbosity |2 |No |[1\-3] |
|log_queries_not_using_indexes |OFF |No |[ON\|OFF] |
|log_slow_admin_statements |ON |No |[ON\|OFF] |
|log_throttle_queries_not_using_indexes |0 |No |[0\-4294967295] |
|long_query_time |1 |No |[0.1\-31536000] |
|loose_binlog_large_trans_threshold |268435456 |No |[20971520\-18446744073709551615] |
|loose_binlog_lock_striping |OFF |Yes |[ON\|OFF] |
|loose_binlog_parallel_flush |OFF |Yes |[ON\|OFF] |
|loose_buffered_scan |OFF |No |[ON\|OFF] |
|loose_buffered_scan_threshold |1000 |No |[0\-18446744073709551615] |
|loose_convert_disabled_engines_to_innodb |ON |No |[ON\|OFF] |
|loose_default_vector_distance |euclidean |No |[euclidean\|l2\|cosine] |
|loose_default_vector_index_algorithm |hnsw |No |[hnsw] |
|loose_enable_binlog_large_trans_opt |OFF |No |[ON\|OFF] |
|loose_enable_binlog_preallocate |OFF |Yes |[ON\|OFF] |
|loose_enable_blob_prefetch |OFF |No |[ON\|OFF] |
|loose_enable_in_list_optimization |OFF |No |[ON\|OFF\|AUTO] |
|loose_enable_logical_prefetch_page |OFF |No |[ON\|OFF] |
|loose_enable_track_index_io |OFF |No |[ON\|OFF] |
|loose_extend_varchar_enhance |OFF |No |[ON\|OFF] |
|loose_hnsw_default_ef_construction |10 |No |[0\-10000] |
|loose_hnsw_default_m |16 |No |[0\-10000] |
|loose_hnsw_ef_search |20 |No |[0\-10000] |
|loose_hnsw_max_cache_size |1073741824 |No |[0\-18446744073709551615] |
|loose_in_list_optimization_threshold |32768 |No |[1\-4294967295] |
|loose_innodb_data_file_logic_drop |OFF |No |[ON\|OFF] |
|loose_innodb_data_file_logic_drop_max_size |1024 |No |[128\-2048] |
|loose_innodb_default_index_merge_threshold |{BY_STORAGE_TYPE(50, 25)}<br><br>> **tip**<br><br><br>> This parameter is an expression parameter. For details about the value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[1\-50] |
|loose_innodb_inplace_ddl_optimize |OFF |No |[ON\|OFF] |
|loose_limit_offset_pushdown_threshold |\-1 |No |[\-1\-9223372036854775807] |
|loose_logical_prefetch_rows_threshold |10240 |No |[0\-4294967295] |
|loose_prefer_user_defined_function |ON |No |[ON\|OFF] |
|loose_rds_flashback_query |OFF |No |[ON\|OFF] |
|loose_rds_flashback_query_window |900 |No |[1\-604800] |
|loose_rds_performance_schema |ON |Yes |[ON\|OFF] |
|loose_recycle_bin |OFF |No |[ON\|OFF] |
|loose_recycle_bin_retention |604800 |No |[1\-31536000] |
|loose_recycle_scheduler |OFF |No |[ON\|OFF] |
|loose_recycle_scheduler_interval |30 |No |[1\-60] |
|loose_thread_pool_enabled |ON |Yes |[ON\|OFF] |
|loose_thread_pool_oversubscribe |16 |No |[2\-128] |
|loose_thread_pool_size |{MAX(DBInstanceCpu, 2)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[1\-64] |
|loose_vector_index_enabled |ON |No |[ON\|OFF] |
|low_priority_updates |OFF |No |[ON\|OFF] |
|max_allowed_packet |1073741824 |No |[16384\-1073741824] |
|max_binlog_cache_size |18400000000000000000 |No |[4096\-18446744073709547520] |
|max_binlog_stmt_cache_size |18400000000000000000 |No |[4096\-18446744073709547520] |
|max_connect_errors |100 |No |[1\-4294967295] |
|max_connections |{MAP(DBInstanceCpu, DBInstanceMemory)}<br><br>Description<br><br>This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically). |No |[100\-200000] |
|max_error_count |64 |No |[0\-65535] |
|max_execution_time |0 |No |[0\-4294967295] |
|max_heap_table_size |67108864 |No |[16384\-1844674407370954752] |
|max_join_size |18446744073709551615 |No |[1\-18446744073709551615] |
|max_length_for_sort_data |1024 |No |[4\-8388608] |
|max_points_in_geometry |65536 |No |[3\-1048576] |
|max_prepared_stmt_count |16382 |No |[0\-1048576] |
|max_seeks_for_key |18400000000000000000 |No |[1\-18446744073709551615] |
|max_sort_length |1024 |No |[4\-8388608] |
|max_sp_recursion_depth |0 |No |[0\-255] |
|max_user_connections |0 |No |[0\|100\-200000] |
|max_write_lock_count |102400 |No |[1\-102400] |
|min_examined_row_limit |0 |No |[0\-4294967295] |
|myisam_sort_buffer_size |262144 |No |[262144\-16777216] |
|mysql_native_password_proxy_users |OFF |No |[ON\|OFF] |
|net_buffer_length |16384 |No |[1024\-1048576] |
|net_read_timeout |30 |No |[1\-31536000] |
|net_retry_count |10 |No |[1\-4294967295] |
|net_write_timeout |60 |No |[1\-31536000] |
|ngram_token_size |2 |Yes |[1\-10] |
|open_files_limit |1048576 |Yes |[1\-18446744073709551615] |
|optimizer_prune_level |1 |No |[0\|1] |
|optimizer_search_depth |62 |No |[0\-62] |
|optimizer_switch |batched_key_access=off,block_nested_loop=on,condition_fanout_filter=on,derived_condition_pushdown=on,derived_merge=on,duplicateweedout=on,engine_condition_pushdown=on,firstmatch=on,hash_join=on,index_condition_pushdown=on,index_merge=on,index_merge_intersection=on,index_merge_sort_union=on,index_merge_union=on,loosescan=on,materialization=on,mrr=on,mrr_cost_based=on,prefer_ordering_index=on,semijoin=on,skip_scan=on,subquery_materialization_cost_based=on,subquery_to_derived=off,use_index_extensions=on,use_invisible_indexes=off |No |\- |
|optimizer_trace_limit |1 |No |[0\-4294967295] |
|optimizer_trace_max_mem_size |16384 |No |[0\-4294967295] |
|optimizer_trace_offset |\-1 |No |[\-2147483648\-2147483647] |
|performance_schema |OFF |Yes |[ON\|OFF] |
|performance_schema_max_thread_instances |\-1 |Yes |[\-1\-1048576] |
|preload_buffer_size |32768 |No |[1024\-1073741824] |
|query_alloc_block_size |8192 |No |[1024\-16384] |
|query_prealloc_size |8192 |No |[8192\-1048576] |
|range_alloc_block_size |4096 |No |[4096\-18446744073709550592] |
|range_optimizer_max_mem_size |8388608 |Yes |[0\-18446744073709551615] |
|read_buffer_size |{LEAST(DBInstanceMemory/1048576\*128, 262144)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[8192\-2147479552] |
|relay_log_recovery |ON |Yes |[ON\|OFF] |
|replica_net_timeout |60 |No |[1\-31536000] |
|replica_type_conversions |\- |No |[\*Empty\|ALL_LOSSY\|ALL_NON_LOSSY\|ALL_SIGNED\|ALL_UNSIGNED] |
|session_track_gtids |OFF |No |[OFF\|OWN_GTID\|ALL_GTIDS] |
|sha256_password_proxy_users |OFF |No |[ON\|OFF] |
|slow_launch_time |2 |No |[1\-1024] |
|slow_query_log |ON |No |[ON\|OFF] |
|sort_buffer_size |262144 |No |[32768\-4294967295] |
|source_verify_checksum |OFF |No |[ON\|OFF] |
|sql_mode |ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION |No |[\*ALLOW_INVALID_DATES\|ANSI_QUOTES\|ERROR_FOR_DIVISION_BY_ZERO\|HIGH_NOT_PRECEDENCE\|IGNORE_SPACE\|NO_AUTO_VALUE_ON_ZERO\|NO_BACKSLASH_ESCAPES\|NO_DIR_IN_CREATE\|NO_ENGINE_SUBSTITUTION\|NO_UNSIGNED_SUBTRACTION\|NO_ZERO_DATE\|NO_ZERO_IN_DATE\|ONLY_FULL_GROUP_BY\|PAD_CHAR_TO_FULL_LENGTH\|PIPES_AS_CONCAT\|REAL_AS_FLOAT\|STRICT_ALL_TABLES\|STRICT_TRANS_TABLES\|TIME_TRUNCATE_FRACTIONAL] |
|sql_safe_updates |OFF |No |[ON\|OFF] |
|stored_program_cache |256 |No |[16\-524288] |
|sync_binlog |1 |No |[0\-4294967295] |
|sync_relay_log_info |10000 |No |[0\-4294967295] |
|sync_source_info |10000 |No |[0\-4294967295] |
|table_definition_cache |{LEAST(DBInstanceMemory/1073741824\*512, 2048)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[400\-524288] |
|table_open_cache |{LEAST(DBInstanceMemory/1073741824\*256, 2048)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[1\-524288] |
|table_open_cache_instances |{LEAST(DBInstanceMemory/1073741824, 16)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |Yes |[1\-64] |
|thread_cache_size |{LEAST(DBInstanceMemory/1073741824\*512, 2048)}<br><br>> **tip**<br><br><br>> This is an expression parameter. For details about value rules, refer to [Expression parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/configuring_parameter_dynamically).<br> |No |[0\-16384] |
|thread_stack |1048576 |Yes |[131072\-2147482624] |
|tls_version |TLSv1.2 |Yes |[TLSv1.2] |
|tmp_table_size |2097152 |No |[262144\-1073741824] |
|transaction_alloc_block_size |8192 |No |[1024\-131072] |
|transaction_isolation |READ\-COMMITTED |No |[READ\-UNCOMMITTED\|READ\-COMMITTED\|REPEATABLE\-READ\|SERIALIZABLE] |
|transaction_prealloc_size |4096 |No |[1024\-131072] |
|updatable_views_with_limit |YES |No |[YES\|NO] |
|wait_timeout |86400 |No |[1\-31536000] |
