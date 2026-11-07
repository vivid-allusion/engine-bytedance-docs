---
title: "vpc-cni metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/vpc-cni_metrics"
---

vpc\-cni serves as a network component in VKE clusters and supports the VPC\-CNI network mode. This topic describes the common metrics of vpc\-cni in the VKE cluster.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="lmOUv5QX"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|resource_pool_total |Basic metric |
|resource_pool_target_min |Basic metric |
|resource_pool_target |Basic metric |
|resource_pool_max_cap |Basic metric |
|metadata_error_count |Basic metric |
|metadata_latency_ms_sum |Basic metric |
|metadata_latency_ms_count |Basic metric |
|metadata_latency_ms_bucket |Basic metric |
|openapi_error_count |Basic metric |
|openapi_latency_ms_sum |Basic metric |
|openapi_latency_ms_count |Basic metric |
|openapi_latency_ms_bucket |Basic metric |
|resource_manager_error_count |Basic metric |
|resource_pool_available |Basic metric |
|rpc_latency_ms_sum |Basic metric |
|rpc_latency_ms_count |Basic metric |
|rpc_latency_ms_bucket |Basic metric |
|cello_acl_watcher_event_process_latency_bucket |Other metrics |
|sub_sys_error_count |Basic metric |
|metadata_statistic |Basic metric |
|openapi_statistic |Basic metric |


<span id="Jy5Y3nfz"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|promhttp_metric_handler_requests_total |Other metrics |
|promhttp_metric_handler_requests_in_flight |Other metrics |
|process_virtual_memory_max_bytes |Other metrics |
|process_virtual_memory_bytes |Other metrics |
|process_start_time_seconds |Other metrics |
|process_resident_memory_bytes |Other metrics |
|process_open_fds |Other metrics |
|process_max_fds |Other metrics |
|process_cpu_seconds_total |Other metrics |
|go_threads |Other metrics |
|go_memstats_sys_bytes |Other metrics |
|go_memstats_stack_sys_bytes |Other metrics |
|go_memstats_stack_inuse_bytes |Other metrics |
|go_memstats_other_sys_bytes |Other metrics |
|go_memstats_next_gc_bytes |Other metrics |
|go_memstats_mspan_sys_bytes |Other metrics |
|go_memstats_mspan_inuse_bytes |Other metrics |
|go_memstats_mcache_sys_bytes |Other metrics |
|go_memstats_mcache_inuse_bytes |Other metrics |
|go_memstats_mallocs_total |Other metrics |
|go_memstats_lookups_total |Other metrics |
|go_memstats_last_gc_time_seconds |Other metrics |
|go_memstats_heap_sys_bytes |Other metrics |
|go_memstats_heap_released_bytes |Other metrics |
|go_memstats_heap_objects |Other metrics |
|go_memstats_heap_inuse_bytes |Other metrics |
|go_memstats_heap_idle_bytes |Other metrics |
|go_memstats_heap_alloc_bytes |Other metrics |
|go_memstats_gc_sys_bytes |Other metrics |
|go_memstats_gc_cpu_fraction |Other metrics |
|go_memstats_frees_total |Other metrics |
|go_memstats_buck_hash_sys_bytes |Other metrics |
|go_memstats_alloc_bytes_total |Other metrics |
|go_memstats_alloc_bytes |Other metrics |
|go_info |Other metrics |
|go_goroutines |Other metrics |
|go_gc_duration_seconds_sum |Other metrics |
|go_gc_duration_seconds_count |Other metrics |
|go_gc_duration_seconds |Other metrics |
|cilium_agent_api_process_time_seconds_sum |Other metrics |
|cilium_agent_api_process_time_seconds_count |Other metrics |
|cilium_agent_api_process_time_seconds_bucket |Other metrics |
|cilium_agent_bootstrap_seconds_sum |Other metrics |
|cilium_agent_bootstrap_seconds_count |Other metrics |
|cilium_agent_bootstrap_seconds_bucket |Other metrics |
|cilium_api_limiter_adjustment_factor |Other metrics |
|cilium_api_limiter_processed_requests_total |Other metrics |
|cilium_api_limiter_processing_duration_seconds |Other metrics |
|cilium_api_limiter_rate_limit |Other metrics |
|cilium_api_limiter_requests_in_flight |Other metrics |
|cilium_api_limiter_wait_duration_seconds |Other metrics |
|cilium_api_limiter_wait_history_duration_seconds_sum |Other metrics |
|cilium_api_limiter_wait_history_duration_seconds_count |Other metrics |
|cilium_api_limiter_wait_history_duration_seconds_bucket |Other metrics |
|cilium_bpf_map_ops_total |Other metrics |
|cilium_endpoint |Other metrics |
|cilium_endpoint_regeneration_time_stats_seconds_sum |Other metrics |
|cilium_endpoint_regeneration_time_stats_seconds_count |Other metrics |
|cilium_endpoint_regeneration_time_stats_seconds_bucket |Other metrics |
|cilium_endpoint_regenerations_total |Other metrics |
|cilium_endpoint_state |Other metrics |
|cilium_errors_warnings_total |Other metrics |
|cilium_event_ts |Other metrics |
|cilium_identity |Other metrics |
|cilium_k8s_client_api_calls_total |Other metrics |
|cilium_k8s_client_api_latency_time_seconds_sum |Other metrics |
|cilium_k8s_client_api_latency_time_seconds_count |Other metrics |
|cilium_k8s_client_api_latency_time_seconds_bucket |Other metrics |
|cilium_k8s_event_lag_seconds |Other metrics |
|cilium_kubernetes_events_received_total |Other metrics |
|cilium_kubernetes_events_total |Other metrics |
|cilium_policy |Other metrics |
|cilium_policy_endpoint_enforcement_status |Other metrics |
|cilium_policy_import_errors_total |Other metrics |
|cilium_policy_max_revision |Other metrics |
|cilium_policy_regeneration_time_stats_seconds_sum |Other metrics |
|cilium_policy_regeneration_time_stats_seconds_count |Other metrics |
|cilium_policy_regeneration_time_stats_seconds_bucket |Other metrics |
|cilium_policy_regeneration_total |Other metrics |
|cilium_triggers_policy_update_call_duration_seconds_sum |Other metrics |
|cilium_triggers_policy_update_call_duration_seconds_count |Other metrics |
|cilium_triggers_policy_update_call_duration_seconds_bucket |Other metrics |
|cilium_triggers_policy_update_folds |Other metrics |
|cilium_triggers_policy_update_total |Other metrics |
|cilium_version |Other metrics |
|cilium_policy_implementation_delay_sum |Other metrics |
|cilium_policy_implementation_delay_count |Other metrics |
|cilium_policy_implementation_delay_bucket |Other metrics |
|cilium_services_events_total |Other metrics |
|cilium_k8s_cnp_status_completion_seconds_sum |Other metrics |
|cilium_k8s_cnp_status_completion_seconds_count |Other metrics |
|cilium_k8s_cnp_status_completion_seconds_bucket |Other metrics |
|cilium_bpf_syscall_duration_seconds_sum |Other metrics |
|cilium_bpf_syscall_duration_seconds_count |Other metrics |
|cilium_bpf_syscall_duration_seconds_bucket |Other metrics |
|cilium_bpf_maps_virtual_memory_max_bytes |Other metrics |
|cilium_bpf_progs_virtual_memory_max_bytes |Other metrics |
|cilium_controllers_failing |Other metrics |
|cilium_controllers_runs_duration_seconds_sum |Other metrics |
|cilium_controllers_runs_duration_seconds_count |Other metrics |
|cilium_controllers_runs_duration_seconds_bucket |Other metrics |
|cilium_controllers_runs_total |Other metrics |
|cilium_datapath_conntrack_dump_resets_total |Other metrics |
|cilium_datapath_conntrack_gc_duration_seconds_sum |Other metrics |
|cilium_datapath_conntrack_gc_duration_seconds_count |Other metrics |
|cilium_datapath_conntrack_gc_duration_seconds_bucket |Other metrics |
|cilium_datapath_conntrack_gc_entries |Other metrics |
|cilium_datapath_conntrack_gc_key_fallbacks_total |Other metrics |
|cilium_datapath_conntrack_gc_runs_total |Other metrics |
|cilium_datapath_nat_gc_entries |Other metrics |
|cilium_datapath_signals_handled_total |Other metrics |
|cilium_drop_bytes_total |Other metrics |
|cilium_forward_bytes_total |Other metrics |
|cilium_forward_count_total |Other metrics |
|cilium_ip_addresses |Other metrics |
|cilium_nodes_all_datapath_validations_total |Other metrics |
|cilium_nodes_all_events_received_total |Other metrics |
|cilium_nodes_all_num |Other metrics |
|cilium_process_cpu_seconds_total |Other metrics |
|cilium_process_max_fds |Other metrics |
|cilium_process_open_fds |Other metrics |
|cilium_process_resident_memory_bytes |Other metrics |
|cilium_process_start_time_seconds |Other metrics |
|cilium_process_virtual_memory_bytes |Other metrics |
|cilium_process_virtual_memory_max_bytes |Other metrics |
|cilium_unreachable_health_endpoints |Other metrics |
|cilium_unreachable_nodes |Other metrics |
|cilium_drop_count_total |Other metrics |
|cilium_subprocess_start_total |Other metrics |
|cello_k8s_client_api_latency_time_seconds_sum |Other metrics |
|cello_k8s_client_api_latency_time_seconds_count |Other metrics |
|cello_k8s_client_api_latency_time_seconds_bucket |Other metrics |
|cello_k8s_client_api_calls_total |Other metrics |
|cello_acl_recalculate_time_status_second_sum |Other metrics |
|cello_acl_recalculate_time_status_second_count |Other metrics |
|cello_acl_recalculate_time_status_second_bucket |Other metrics |
|cello_acl_cr_total_count |Other metrics |
|cello_acl_rules_total_count |Other metrics |
|cello_bpf_map_ops_total |Other metrics |
|cello_acl_watcher_event_process_latency_sum |Other metrics |
|cello_acl_watcher_event_process_latency_count |Other metrics |
|cello_acl_watcher_event_process_latency_bucket |Other metrics |
