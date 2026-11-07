---
title: "List of modifiable parameters in MySQL 8.0"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_modifiable_parameters_in_mysql_8_0"
---

This topic introduces the modifiable parameters for instances compatible with MySQL 8.0, their default values, value ranges, and whether a restart is required after modification.

## Parameter list

|Name |Default value |Value range |Need restart? |
|---|---|---|---|
|auto_increment_increment |1 |[1\-65535] |No |
|auto_increment_offset |1 |[1\-65535] |No |
|automatic_sp_privileges |ON |[ON\|OFF] |No |
|back_log |3000 |[0\-65535] |Yes |
|character_set_filesystem |binary |[utf8\|latin1\|gbk\|binary] |No |
|character_set_server |utf8mb4 |[utf8mb4] |Yes |
|collation_server |utf8mb4_general_ci |[armscii8_general_ci\|armscii8_bin\|ascii_general_ci\|ascii_bin\|big5_chinese_ci\|big5_bin\|binary\|cp1250_general_ci\|cp1250_czech_cs\|cp1250_croatian_ci\|cp1250_bin\|cp1250_polish_ci\|cp1251_bulgarian_ci\|cp1251_ukrainian_ci\|cp1251_bin\|cp1251_general_ci\|cp1251_general_cs\|cp1256_general_ci\|cp1256_bin\|cp1257_lithuanian_ci\|cp1257_bin\|cp1257_general_ci\|cp850_general_ci\|cp850_bin\|cp852_general_ci\|cp852_bin\|cp866_general_ci\|cp866_bin\|cp932_japanese_ci\|cp932_bin\|dec8_swedish_ci\|dec8_bin\|eucjpms_japanese_ci\|eucjpms_bin\|euckr_korean_ci\|euckr_bin\|gb18030_chinese_ci\|gb18030_bin\|gb18030_unicode_520_ci\|gb2312_chinese_ci\|gb2312_bin\|gbk_chinese_ci\|gbk_bin\|geostd8_general_ci\|geostd8_bin\|greek_general_ci\|greek_bin\|hebrew_general_ci\|hebrew_bin\|hp8_english_ci\|hp8_bin\|keybcs2_general_ci\|keybcs2_bin\|koi8r_general_ci\|koi8r_bin\|koi8u_general_ci\|koi8u_bin\|latin1_german1_ci\|latin1_swedish_ci\|latin1_danish_ci\|latin1_german2_ci\|latin1_bin\|latin1_general_ci\|latin1_general_cs\|latin1_spanish_ci\|latin2_czech_cs\|latin2_general_ci\|latin2_hungarian_ci\|latin2_croatian_ci\|latin2_bin\|latin5_turkish_ci\|latin5_bin\|latin7_estonian_cs\|latin7_general_ci\|latin7_general_cs\|latin7_bin\|macce_general_ci\|macce_bin\|macroman_general_ci\|macroman_bin\|sjis_japanese_ci\|sjis_bin\|swe7_swedish_ci\|swe7_bin\|tis620_thai_ci\|tis620_bin\|ucs2_general_ci\|ucs2_bin\|ucs2_unicode_ci\|ucs2_icelandic_ci\|ucs2_latvian_ci\|ucs2_romanian_ci\|ucs2_slovenian_ci\|ucs2_polish_ci\|ucs2_estonian_ci\|ucs2_spanish_ci\|ucs2_swedish_ci\|ucs2_turkish_ci\|ucs2_czech_ci\|ucs2_danish_ci\|ucs2_lithuanian_ci\|ucs2_slovak_ci\|ucs2_spanish2_ci\|ucs2_roman_ci\|ucs2_persian_ci\|ucs2_esperanto_ci\|ucs2_hungarian_ci\|ucs2_sinhala_ci\|ucs2_german2_ci\|ucs2_croatian_ci\|ucs2_unicode_520_ci\|ucs2_vietnamese_ci\|ucs2_general_mysql500_ci\|ujis_japanese_ci\|ujis_bin\|utf16_general_ci\|utf16_bin\|utf16_unicode_ci\|utf16_icelandic_ci\|utf16_latvian_ci\|utf16_romanian_ci\|utf16_slovenian_ci\|utf16_polish_ci\|utf16_estonian_ci\|utf16_spanish_ci\|utf16_swedish_ci\|utf16_turkish_ci\|utf16_czech_ci\|utf16_danish_ci\|utf16_lithuanian_ci\|utf16_slovak_ci\|utf16_spanish2_ci\|utf16_roman_ci\|utf16_persian_ci\|utf16_esperanto_ci\|utf16_hungarian_ci\|utf16_sinhala_ci\|utf16_german2_ci\|utf16_croatian_ci\|utf16_unicode_520_ci\|utf16_vietnamese_ci\|utf16le_general_ci\|utf16le_bin\|utf32_general_ci\|utf32_bin\|utf32_unicode_ci\|utf32_icelandic_ci\|utf32_latvian_ci\|utf32_romanian_ci\|utf32_slovenian_ci\|utf32_polish_ci\|utf32_estonian_ci\|utf32_spanish_ci\|utf32_swedish_ci\|utf32_turkish_ci\|utf32_czech_ci\|utf32_danish_ci\|utf32_lithuanian_ci\|utf32_slovak_ci\|utf32_spanish2_ci\|utf32_roman_ci\|utf32_persian_ci\|utf32_esperanto_ci\|utf32_hungarian_ci\|utf32_sinhala_ci\|utf32_german2_ci\|utf32_croatian_ci\|utf32_unicode_520_ci\|utf32_vietnamese_ci\|utf8_general_ci\|utf8_tolower_ci\|utf8_bin\|utf8_unicode_ci\|utf8_icelandic_ci\|utf8_latvian_ci\|utf8_romanian_ci\|utf8_slovenian_ci\|utf8_polish_ci\|utf8_estonian_ci\|utf8_spanish_ci\|utf8_swedish_ci\|utf8_turkish_ci\|utf8_czech_ci\|utf8_danish_ci\|utf8_lithuanian_ci\|utf8_slovak_ci\|utf8_spanish2_ci\|utf8_roman_ci\|utf8_persian_ci\|utf8_esperanto_ci\|utf8_hungarian_ci\|utf8_sinhala_ci\|utf8_german2_ci\|utf8_croatian_ci\|utf8_unicode_520_ci\|utf8_vietnamese_ci\|utf8_general_mysql500_ci\|utf8mb4_general_ci\|utf8mb4_bin\|utf8mb4_unicode_ci\|utf8mb4_icelandic_ci\|utf8mb4_latvian_ci\|utf8mb4_romanian_ci\|utf8mb4_slovenian_ci\|utf8mb4_polish_ci\|utf8mb4_estonian_ci\|utf8mb4_spanish_ci\|utf8mb4_swedish_ci\|utf8mb4_turkish_ci\|utf8mb4_czech_ci\|utf8mb4_danish_ci\|utf8mb4_lithuanian_ci\|utf8mb4_slovak_ci\|utf8mb4_spanish2_ci\|utf8mb4_roman_ci\|utf8mb4_persian_ci\|utf8mb4_esperanto_ci\|utf8mb4_hungarian_ci\|utf8mb4_sinhala_ci\|utf8mb4_german2_ci\|utf8mb4_croatian_ci\|utf8mb4_unicode_520_ci\|utf8mb4_vietnamese_ci\|utf8mb4_0900_ai_ci\|utf8mb4_de_pb_0900_ai_ci\|utf8mb4_is_0900_ai_ci\|utf8mb4_lv_0900_ai_ci\|utf8mb4_ro_0900_ai_ci\|utf8mb4_sl_0900_ai_ci\|utf8mb4_pl_0900_ai_ci\|utf8mb4_et_0900_ai_ci\|utf8mb4_es_0900_ai_ci\|utf8mb4_sv_0900_ai_ci\|utf8mb4_tr_0900_ai_ci\|utf8mb4_cs_0900_ai_ci\|utf8mb4_da_0900_ai_ci\|utf8mb4_lt_0900_ai_ci\|utf8mb4_sk_0900_ai_ci\|utf8mb4_es_trad_0900_ai_ci\|utf8mb4_la_0900_ai_ci\|utf8mb4_eo_0900_ai_ci\|utf8mb4_hu_0900_ai_ci\|utf8mb4_hr_0900_ai_ci\|utf8mb4_vi_0900_ai_ci\|utf8mb4_0900_as_cs\|utf8mb4_de_pb_0900_as_cs\|utf8mb4_is_0900_as_cs\|utf8mb4_lv_0900_as_cs\|utf8mb4_ro_0900_as_cs\|utf8mb4_sl_0900_as_cs\|utf8mb4_pl_0900_as_cs\|utf8mb4_et_0900_as_cs\|utf8mb4_es_0900_as_cs\|utf8mb4_sv_0900_as_cs\|utf8mb4_tr_0900_as_cs\|utf8mb4_cs_0900_as_cs\|utf8mb4_da_0900_as_cs\|utf8mb4_lt_0900_as_cs\|utf8mb4_sk_0900_as_cs\|utf8mb4_es_trad_0900_as_cs\|utf8mb4_la_0900_as_cs\|utf8mb4_eo_0900_as_cs\|utf8mb4_hu_0900_as_cs\|utf8mb4_hr_0900_as_cs\|utf8mb4_vi_0900_as_cs\|utf8mb4_ja_0900_as_cs\|utf8mb4_ja_0900_as_cs_ks\|utf8mb4_0900_as_ci\|utf8mb4_ru_0900_ai_ci\|utf8mb4_ru_0900_as_cs\|utf8mb4_zh_0900_as_cs\|utf8mb4_0900_bin] |No |
|connect_timeout |10 |[2\-31536000] |No |
|default_collation_for_utf8mb4 |utf8mb4_0900_ai_ci |[utf8mb4_0900_ai_ci\|utf8mb4_general_ci] |No |
|default_week_format |0 |[0\-7] |No |
|delay_key_write |ON |[OFF\|ON\|ALL] |No |
|disable_parallel_count_star |OFF |[ON\|OFF] |No |
|disconnect_on_expired_password |ON |[ON\|OFF] |Yes |
|div_precision_increment |4 |[0\-30] |No |
|enable_nonblock_ddl |OFF |[ON\|OFF] |No |
|end_markers_in_json |OFF |[ON\|OFF] |No |
|eq_range_index_dive_limit |200 |[0\-4294967295] |No |
|explicit_defaults_for_timestamp |ON |[ON\|OFF] |No |
|flush_time |0 |[0\-31536000] |No |
|ft_max_word_len |84 |[10\-84] |Yes |
|ft_min_word_len |4 |[1\-84] |Yes |
|ft_query_expansion_limit |20 |[0\-1000] |Yes |
|group_concat_max_len |1024 |[4\-18446744073709551615] |No |
|information_schema_stats_expiry |86400 |[0\-31536000] |No |
|innodb_adaptive_flushing |ON |[ON\|OFF] |No |
|innodb_adaptive_flushing_lwm |10 |[0\-70] |No |
|innodb_adaptive_hash_index |OFF |[ON\|OFF] |No |
|innodb_adaptive_max_sleep_delay |150000 |[0\-1000000] |No |
|innodb_autoextend_increment |64 |[1\-1000] |No |
|innodb_autoinc_lock_mode |2 |[0\-2] |Yes |
|innodb_buffer_pool_dump_at_shutdown |OFF<br><br>> **tip**<br><br><br>> The parameter default value has been adjusted, causing an inconsistency between the default value and the running value for instances of older versions. You need to manually modify the running value to the new default value.<br> |[ON\|OFF] |No |
|innodb_buffer_pool_load_at_startup |OFF<br><br>> **tip**<br><br><br>> The parameter default value has been adjusted, causing an inconsistency between the default value and the running value for instances of older versions. You need to manually modify the running value to the new default value.<br> |[ON\|OFF] |Yes |
|innodb_buffer_pool_size |{DBNodeClassMemory\*3/4} |[{DBNodeClassMemory\*1/16}\-{DBNodeClassMemory\*4/5}] |No |
|innodb_change_buffer_max_size |25 |[0\-50] |No |
|innodb_cmp_per_index_enabled |OFF |[ON\|OFF] |No |
|innodb_concurrency_tickets |5000 |[1\-4294967295] |No |
|innodb_deadlock_detect |ON |[ON\|OFF] |No |
|innodb_disable_sort_file_cache |OFF |[ON\|OFF] |No |
|innodb_fill_factor |100 |[10\-100] |No |
|innodb_flashback_query |OFF |[ON\|OFF] |No |
|innodb_flashback_query_window |900 |[0\-604800] |No |
|innodb_flush_neighbors |0 |[0\-2] |No |
|innodb_flush_sync |ON |[ON\|OFF] |No |
|innodb_ft_cache_size |8000000 |[1600000\-80000000] |Yes |
|innodb_ft_enable_diag_print |OFF |[ON\|OFF] |No |
|innodb_ft_enable_stopword |ON |[ON\|OFF] |No |
|innodb_ft_max_token_size |84 |[10\-84] |Yes |
|innodb_ft_min_token_size |3 |[0\-16] |Yes |
|innodb_ft_num_word_optimize |2000 |[1000\-10000] |No |
|innodb_ft_result_cache_limit |2000000000 |[1000000\-4294967295] |No |
|innodb_ft_sort_pll_degree |2 |[1\-16] |Yes |
|innodb_ft_total_cache_size |640000000 |[32000000\-1600000000] |Yes |
|innodb_io_capacity |25000 |[100\-4294967295] |No |
|innodb_io_capacity_max |50000 |[100\-4294967295] |No |
|innodb_lock_wait_timeout |50 |[1\-1073741824] |No |
|innodb_log_checksums |ON |[ON\|OFF] |No |
|innodb_log_compressed_pages |ON |[ON\|OFF] |No |
|innodb_max_dirty_pages_pct |90 |[0.000000\-99.999000] |No |
|innodb_max_purge_lag |0 |[0\-4294967295] |No |
|innodb_max_purge_lag_delay |0 |[0\-10000000] |No |
|innodb_max_undo_log_size |1073741824 |[10485760\-18446744073709551615] |No |
|innodb_old_blocks_pct |37 |[5\-95] |No |
|innodb_old_blocks_time |1000 |[0\-4294967295] |No |
|innodb_online_alter_log_max_size |4398046511104 |[65536\-18446744073709551615] |No |
|innodb_optimize_fulltext_only |OFF |[ON\|OFF] |No |
|innodb_open_files<br><br> |{MIN(MAX(DBNodeClassMemory/1048576,8192),1048576) }<br><br>> **tip**<br><br><br>> For instances purchased before the release of this parameter, the default running value is displayed as an expression only. You must restart the instance for the system to recalculate the actual running value based on the expression.  For more information about expressions, see [Expression parameter](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter).<br> |[10,2147483647]<br><br> |Yes |
|innodb_parallel_read_threads |2 |[1\-256] |No |
|innodb_print_all_deadlocks |OFF |[ON\|OFF] |No |
|innodb_purge_batch_size |MIN(MAX({DBNodeClassCPU \* 100}, 300), 5000)<br><br>> **tip**<br><br><br>> The Parameter default value is adjusted to an expression, causing the default value of instances of older versions to be inconsistent with the running value. You need to restart the instance, and the System will recalculate the actual running value based on the expression.  For more information about expressions, see [Expression parameter](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Expression_parameter).<br> |[1\-5000] |No |
|innodb_purge_rseg_truncate_frequency |16 |[1\-128] |No |
|innodb_purge_threads |{MIN(MAX(DBNodeClassCPU,4),32)} |[1\-32] |Yes |
|innodb_random_read_ahead |OFF |[ON\|OFF] |No |
|innodb_read_ahead_threshold |56 |[0\-64] |No |
|innodb_rollback_on_timeout |OFF |[ON\|OFF] |Yes |
|innodb_sort_buffer_size |1048576<br><br>> **tip**<br><br><br>> The parameter default value has been adjusted, causing an inconsistency between the default value and the running value for instances of older versions. You need to manually modify the running value to the new default value.<br> |[65536\-67108864] |Yes |
|innodb_spin_wait_delay |6 |[0\-1000] |No |
|innodb_stats_auto_recalc |ON |[ON\|OFF] |No |
|innodb_stats_method |nulls_equal |[nulls_equal\|nulls_unequal\|nulls_ignored] |No |
|innodb_stats_on_metadata |OFF |[ON\|OFF] |No |
|innodb_stats_persistent |ON |[ON\|OFF] |No |
|innodb_stats_persistent_sample_pages |20 |[1\-18446744073709551615] |No |
|innodb_stats_transient_sample_pages |8 |[1\-18446744073709551615] |No |
|innodb_strict_mode |ON |[ON\|OFF] |No |
|innodb_sync_array_size |1 |[1\-1024] |Yes |
|innodb_sync_spin_loops |30 |[0\-4294967295] |No |
|innodb_table_locks |ON |[ON\|OFF] |No |
|innodb_thread_concurrency |0 |[0\-1000] |No |
|innodb_undo_log_truncate |ON |[ON\|OFF] |No |
|interactive_timeout |28800 |[1\-31536000] |No |
|internal_tmp_mem_storage_engine |TempTable |[MEMORY\|TempTable] |No |
|join_buffer_size |{MIN(DBNodeClassMemory/1048576\*128,262144)} |[128\-67108864] |No |
|key_cache_age_threshold |300 |[100\-18446744073709551600] |No |
|key_cache_block_size |1024 |[512\-16384] |No |
|key_cache_division_limit |100 |[1\-100] |No |
|lc_time_names |en_US |[ja_JP\|pt_BR\|en_US] |No |
|local_infile |OFF |[ON\|OFF] |No |
|lock_wait_timeout |31536000 |[1\-31536000] |No |
|log_queries_not_using_indexes |OFF |[ON\|OFF] |No |
|log_throttle_queries_not_using_indexes |0 |[0\-18446744073709551615] |No |
|long_query_time |1 |[0\-4719230590769954816] |No |
|master_verify_checksum |OFF |[ON\|OFF] |No |
|max_allowed_packet |268435456<br><br>> **tip**<br><br><br>> The parameter default value has been adjusted, causing an inconsistency between the default value and the running value for instances of older versions. You need to manually modify the running value to the new default value.<br> |[1024\-1073741824] |No |
|max_connect_errors |0 |[0\-18446744073709551615] |No |
|max_digest_length |1024 |[0\-1048576] |Yes |
|max_error_count |1024 |[0\-65535] |No |
|max_heap_table_size |16777216 |[16384\-18446744073709550592] |No |
|max_join_size |18446744073709551615 |[1\-18446744073709551615] |No |
|max_length_for_sort_data |4096 |[4\-8388608] |No |
|max_points_in_geometry |65536 |[3\-1048576] |No |
|max_prepared_stmt_count |16382 |[0\-4194304] |No |
|max_seeks_for_key |18446744073709551615 |[1\-18446744073709551615] |No |
|max_sort_length |1024 |[4\-8388608] |No |
|max_sp_recursion_depth |0 |[0\-255] |No |
|max_write_lock_count |18446744073709551615 |[1\-18446744073709551615] |No |
|min_examined_row_limit |0 |[0\-18446744073709551615] |No |
|mysql_native_password_proxy_users |OFF |[ON\|OFF] |No |
|net_read_timeout |30 |[1\-31536000] |No |
|net_retry_count |10 |[1\-18446744073709551615] |No |
|net_write_timeout |60 |[1\-31536000] |No |
|ngram_token_size |2 |[1\-10] |Yes |
|nonblock_ddl_lock_wait_timeout |1 |[1\-31536000] |No |
|nonblock_ddl_retry_interval |6 |[1\-31536000] |No |
|nonblock_ddl_retry_times |0 |[0\-31536000] |No |
|optimizer_prune_level |1 |[0\-1] |No |
|optimizer_search_depth |62 |[0\-62] |No |
|optimizer_switch |index_merge=on,index_merge_union=on,index_merge_sort_union=on,index_merge_intersection=on,engine_condition_pushdown=on,index_condition_pushdown=on,mrr=on,mrr_cost_based=on,block_nested_loop=on,batched_key_access=off,materialization=on,semijoin=on,loosescan=on,firstmatch=on,duplicateweedout=on,subquery_materialization_cost_based=on,use_index_extensions=on,condition_fanout_filter=on,derived_merge=on,use_invisible_indexes=off,skip_scan=on,hash_join=on,subquery_to_derived=off,prefer_ordering_index=on,hypergraph_optimizer=off,derived_condition_pushdown=on,favor_range_scan=off |\*[index_merge=on\|index_merge=off\|index_merge_union=on\|index_merge_union=off\|index_merge_sort_union=on\|index_merge_sort_union=off\|index_merge_intersection=on\|index_merge_intersection=off\|engine_condition_pushdown=on\|engine_condition_pushdown=off\|index_condition_pushdown=on\|index_condition_pushdown=off\|mrr=on\|mrr=off\|mrr_cost_based=on\|mrr_cost_based=off\|block_nested_loop=on\|block_nested_loop=off\|batched_key_access=on\|batched_key_access=off\|materialization=on\|materialization=off\|semijoin=on\|semijoin=off\|loosescan=on\|loosescan=off\|firstmatch=on\|firstmatch=off\|duplicateweedout=on\|duplicateweedout=off\|subquery_materialization_cost_based=on\|subquery_materialization_cost_based=off\|use_index_extensions=on\|use_index_extensions=off\|condition_fanout_filter=on\|condition_fanout_filter=off\|derived_merge=on\|derived_merge=off\|use_invisible_indexes=on\|use_invisible_indexes=off\|skip_scan=on\|skip_scan=off\|hash_join=on\|hash_join=off\|subquery_to_derived=on\|subquery_to_derived=off\|prefer_ordering_index=on\|prefer_ordering_index=off\|hypergraph_optimizer=on\|hypergraph_optimizer=off\|derived_condition_pushdown=on\|derived_condition_pushdown=off\|favor_range_scan=on\|favor_range_scan=off\|default=on\|default=off] |No |
|optimizer_trace |enabled=off,one_line=off |\*[enabled=on\|enabled=off\|one_line=on\|one_line=off\|default=on\|default=off] |No |
|optimizer_trace_features |greedy_search=on,range_optimizer=on,dynamic_range=on,repeated_subselect=on |\* [greedy_search=on\|greedy_search=off\|range_optimizer=on\|range_optimizer=off\|dynamic_range=on\|dynamic_range=off\|repeated_subselect=on\|repeated_subselect=off\|default=on\|default=off] |No |
|optimizer_trace_limit |1 |[0\-9223372036854775807] |No |
|optimizer_trace_max_mem_size |1048576 |[0\-18446744073709551615] |No |
|optimizer_trace_offset |\-1 |[\-9223372036854775808\-9223372036854775807] |No |
|open_files_limit |1048576 |[1\-4294967295] |Yes |
|performance_schema |OFF |[ON\|OFF] |Yes |
|preload_buffer_size |32768 |[1024\-1073741824] |No |
|query_alloc_block_size |8192 |[1024\-4294966272] |No |
|query_prealloc_size |8192 |[8192\-18446744073709550592] |No |
|range_alloc_block_size |4096 |[4096\-4294966272] |No |
|range_optimizer_max_mem_size |8388608 |[0\-18446744073709551615] |No |
|range_optimizer_max_mem_size |8388608 |[0\-18446744073709551615] |No |
|regexp_stack_limit |8000000 |[0\-2147483647] |No |
|regexp_time_limit |32 |[0\-2147483647] |No |
|schema_definition_cache |256 |[256\-524288] |No |
|session_track_gtids |OFF |[OFF\|OWN_GTID\|ALL_GTIDS] |No |
|session_track_schema |ON |[ON\|OFF] |No |
|sha256_password_proxy_users |OFF |[ON\|OFF] |No |
|show_old_temporals |OFF |[ON\|OFF] |No |
|skip_name_resolve |OFF |[ON\|OFF] |Yes |
|slow_launch_time |2 |[0\-31536000] |No |
|slow_query_log |ON |[ON\|OFF] |No |
|sort_buffer_size |1048576<br><br>> **tip**<br><br><br>> The parameter default value has been adjusted, causing an inconsistency between the default value and the running value for instances of older versions. You need to manually modify the running value to the new default value.<br> |[32768\-18446744073709551615] |No |
|sql_mode |ONLY_FULL_GROUP_BY,STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION |\*[REAL_AS_FLOAT\|PIPES_AS_CONCAT\|ANSI_QUOTES\|IGNORE_SPACE\|ONLY_FULL_GROUP_BY\|NO_UNSIGNED_SUBTRACTION\|NO_DIR_IN_CREATE\|ANSI\|NO_AUTO_VALUE_ON_ZERO\|NO_BACKSLASH_ESCAPES\|STRICT_TRANS_TABLES\|STRICT_ALL_TABLES\|NO_ZERO_IN_DATE\|NO_ZERO_DATE\|ALLOW_INVALID_DATES\|ERROR_FOR_DIVISION_BY_ZERO\|TRADITIONAL\|HIGH_NOT_PRECEDENCE\|NO_ENGINE_SUBSTITUTION\|PAD_CHAR_TO_FULL_LENGTH\|] |No |
|stored_program_cache |256 |[16\-524288] |No |
|table_definition_cache |16384 |[400\-524288] |No |
|table_open_cache |{MAX(DBNodeClassMemory/1073741824\*256,2048)} |[1\-524288] |No |
|table_open_cache_instances |{MAX(DBNodeClassCPU,32)} |[1\-64] |Yes |
|temptable_max_mmap |1073741824 |[0\-18446744073709551615] |No |
|temptable_max_ram |1073741824 |[2097152\-18446744073709551615] |No |
|temptable_use_mmap |OFF |[ON\|OFF] |No |
|thread_pool_idle_timeout |60 |[1\-4294967295] |No |
|thread_pool_oversubscribe |8 |[1\-1000] |No |
|thread_pool_size |{DBNodeClassCPU\*4} |[{DBNodeClassCPU\*1}\-{DBNodeClassCPU\*10}] |No |
|thread_pool_stall_limit |10 |[10\-4294967295] |No |
|thread_stack |1048576 |[131072\-1073741824] |Yes |
|time_zone |+8:00 |[SYSTEM\|\-12:00\|\-11:00\|\-10:00\|\-9:00\|\-8:00\|\-7:00\|\-6:00\|\-5:00\|\-4:00\|\-3:00\|\-2:00\|\-1:00\|+0:00\|+1:00\|+2:00\|+3:00\|+4:00\|+5:00\|+5:30\|+6:00\|+6:30\|+7:00\|+8:0\|+9:00\|+10:00\|+11:00\|+12:00\|+13:00] |No |
|tmp_table_size |16777216 |[1024\-18446744073709551615] |No |
|transaction_alloc_block_size |8192 |[1024\-131072] |No |
|transaction_isolation |READ\-COMMITTED |[READ\-UNCOMMITTED\|READ\-COMMITTED\|REPEATABLE\-READ\|SERIALIZABLE] |No |
|transaction_prealloc_size |4096 |[1024\-131072] |No |
|updatable_views_with_limit |YES \| [NO\|YES] |No | |
|vedb_binlog_expire_logs_seconds |432000 |[0\-4294967295] |No |
|wait_timeout |28800 |[1\-31536000] |No |
|max_connections |he default maximum number of connections varies based on the instance specifications. For details, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |[100\-100000] |No |
|max_user_connections |0 |[0\-4294967295] |No |
|max_execution_time |0 |[0\-4294967295] |No |
|innodb_lru_scan_depth |{MIN(DBInstanceClassMemory/1048576/8, 8192)} |[100\-1099511627776]<br><br> |No |
|init_connect |'' |[''\|'set names utf8mb4'\|'set names utf8'\|'set default_collation_for_utf8mb4=utf8mb4_general_ci'\|'set default_collation_for_utf8mb4=utf8mb4_general_ci;set names utf8mb4'\|'set names utf8mb4 collate utf8mb4_general_ci'\|'set names utf8mb4 COLLATE utf8mb4_bin'\|'set names utf8mb4 collate utf8mb4_unicode_ci'] |No |
|innodb_compression_pad_pct_max |50 |[0\-70] |No |
|binlog_expire_logs_seconds |1209600 |[0\-4294967295] |No |
|max_binlog_stmt_cache_size |18446744073709500000 |[4096\-18446744073709547520] |No |
|read_rnd_buffer_size |262144 |[1\-2147483647] |No |
|innodb_status_output |OFF |[ON\|OFF] |No |
|binlog_stmt_cache_size |32768 |[4096\-16777216] |No |
|innodb_monitor_disable | |all |No |
|performance_schema_max_metadata_locks |160000 |[\-1\-1048576] |Yes |
|innodb_flush_log_at_trx_commit |1 |[0\|1\|2] |No |
|host_cache_size |128 |[0\-65535] |No |
|innodb_monitor_enable | |all |No |
|ssl |0 |[0\|1] |Yes |
|innodb_compression_level |6 |[0\-9] |No |
|innodb_compression_failure_threshold_pct |5 |[0\-100] |No |
|performance_schema_max_thread_instances |8000 |[\-1\-65536] |Yes |
|log_bin_use_v1_row_events |ON |[ON\|OFF] |No |
|innodb_ft_server_stopword_table | |.\*/.\* |No |
|innodb_status_output_locks |OFF |[ON\|OFF] |No |
|default_tmp_storage_engine |InnoDB |[InnoDB\|MyISAM\|MEMORY] |No |
|slave_parallel_type |"LOGICAL_CLOCK" |["DATABASE"\|"LOGICAL_CLOCK"] |No |
|tls_version |TLSv1,TLSv1.1,TLSv1.2 |[TLSv1,TLSv1.1,TLSv1.2\|TLSv1.2\|TLSv1.1\|TLSv1\|TLSv1,TLSv1.1\|TLSv1,TLSv1.2\|TLSv1.1,TLSv1.2] |No |
|block_encryption_mode |"aes\-128\-ecb" |["aes\-128\-ecb"\|"aes\-192\-ecb"\|"aes\-256\-ecb"\|"aes\-128\-cbc"\|"aes\-192\-cbc"\|"aes\-256\-cbc"] |No |
|innodb_thread_sleep_delay |10000 |[1\-1000000] |No |
|autocommit |ON |[ON\|OFF] |No |

## How to query the values of non\-modifiable parameters?

Log in to the [console](https://console.byteplus.com/db/vedb-mysql) and search for the parameter on the **Parameters** page of the instance. If the parameter is not found, log on to [Database Workshop](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'Parameter name'` to check the value.
