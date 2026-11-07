---
title: "kubelet metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/kubelet_metrics"
---

kubelet serves as an agent component running on the worker nodes of a Vital Kubernetes Engine (VKE) cluster. It regularly receives new or modified Pod specifications from the kube\-apiserver component and ensures that Pods and their containers run as expected based on the related rules. In addition, as the monitoring component of the worker nodes, kubelet reports the running status of the node hosts to kube\-apiserver. This topic describes the common metrics of metrics\-server in the VKE cluster.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="M87qgLAw"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|kubelet_cpu_manager_pinning_errors_total |Basic metric |
|volume_operation_total_seconds_count |Basic metric |
|volume_operation_total_seconds_sum |Basic metric |
|volume_operation_total_seconds_bucket |Basic metric |
|rest_client_response_size_bytes_count |Basic metric |
|rest_client_response_size_bytes_sum |Basic metric |
|rest_client_response_size_bytes_bucket |Basic metric |
|process_open_fds |Basic metric |
|process_max_fds |Basic metric |
|kubelet_started_pods_errors_total |Basic metric |
|kubelet_started_containers_errors_total |Basic metric |
|get_token_fail_count |Basic metric |
|apiserver_storage_data_key_generation_failures_total |Basic metric |
|apiserver_audit_requests_rejected_total |Basic metric |
|apiserver_audit_event_total |Basic metric |
|workqueue_queue_duration_seconds_bucket |Basic metric |
|workqueue_queue_duration_seconds_count |Basic metric |
|workqueue_queue_duration_seconds_sum |Basic metric |
|workqueue_depth |Basic metric |
|workqueue_adds_total |Basic metric |
|rest_client_requests_total |Basic metric |
|rest_client_request_duration_seconds_sum |Basic metric |
|rest_client_request_duration_seconds_count |Basic metric |
|rest_client_request_duration_seconds_bucket |Basic metric |
|kubernetes_build_info |Basic metric |
|storage_operation_duration_seconds_bucket |Basic metric |
|storage_operation_duration_seconds_sum |Basic metric |
|storage_operation_duration_seconds_count |Basic metric |
|kubelet_volume_stats_used_bytes |Basic metric |
|kubelet_volume_stats_inodes_used |Basic metric |
|kubelet_volume_stats_inodes_free |Basic metric |
|kubelet_volume_stats_inodes |Basic metric |
|kubelet_volume_stats_capacity_bytes |Basic metric |
|kubelet_volume_stats_available_bytes |Basic metric |
|kubelet_runtime_operations_total |Basic metric |
|kubelet_runtime_operations_errors_total |Basic metric |
|kubelet_runtime_operations_duration_seconds_sum |Basic metric |
|kubelet_runtime_operations_duration_seconds_count |Basic metric |
|kubelet_runtime_operations_duration_seconds_bucket |Basic metric |
|kubelet_running_pods |Basic metric |
|kubelet_running_containers |Basic metric |
|kubelet_run_podsandbox_errors_total |Basic metric |
|kubelet_run_podsandbox_duration_seconds_bucket |Basic metric |
|kubelet_run_podsandbox_duration_seconds_sum |Basic metric |
|kubelet_run_podsandbox_duration_seconds_count |Basic metric |
|kubelet_pod_worker_start_duration_seconds_bucket |Basic metric |
|kubelet_pod_worker_start_duration_seconds_sum |Basic metric |
|kubelet_pod_worker_start_duration_seconds_count |Basic metric |
|kubelet_pod_worker_duration_seconds_sum |Basic metric |
|kubelet_pod_worker_duration_seconds_count |Basic metric |
|kubelet_pod_worker_duration_seconds_bucket |Basic metric |
|kubelet_pod_start_duration_seconds_sum |Basic metric |
|kubelet_pod_start_duration_seconds_count |Basic metric |
|kubelet_pod_start_duration_seconds_bucket |Basic metric |
|kubelet_pleg_relist_interval_seconds_sum |Basic metric |
|kubelet_pleg_relist_interval_seconds_count |Basic metric |
|kubelet_pleg_relist_interval_seconds_bucket |Basic metric |
|kubelet_pleg_relist_duration_seconds_sum |Basic metric |
|kubelet_pleg_relist_duration_seconds_count |Basic metric |
|kubelet_pleg_relist_duration_seconds_bucket |Basic metric |
|kubelet_pleg_last_seen_seconds |Basic metric |
|kubelet_pleg_discard_events |Basic metric |
|kubelet_node_name |Basic metric |
|kubelet_node_config_error |Basic metric |
|kubelet_http_requests_total |Basic metric |
|kubelet_http_requests_duration_seconds_sum |Basic metric |
|kubelet_http_requests_duration_seconds_count |Basic metric |
|kubelet_http_requests_duration_seconds_bucket |Basic metric |
|kubelet_http_inflight_requests |Basic metric |
|kubelet_container_log_filesystem_used_bytes |Basic metric |
|kubelet_cgroup_manager_duration_seconds_sum |Basic metric |
|kubelet_cgroup_manager_duration_seconds_count |Basic metric |
|kubelet_cgroup_manager_duration_seconds_bucket |Basic metric |
|kubelet_certificate_manager_client_ttl_seconds |Basic metric |
|kubelet_certificate_manager_client_expiration_renew_errors |Basic metric |
|volume_manager_total_volumes |Basic metric |
|kubernetes_feature_enabled |Basic metric |
|pod_cpu_usage_seconds_total |Basic metric |
|pod_memory_working_set_bytes |Basic metric |
|process_cpu_seconds_total |Basic metric |
|process_resident_memory_bytes |Basic metric |
|csi_operations_seconds_count |Basic metric |
|csi_operations_seconds_sum |Basic metric |
|csi_operations_seconds_bucket |Basic metric |


<span id="4qVcdao0"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|workqueue_work_duration_seconds_count |Other metrics |
|workqueue_work_duration_seconds_sum |Other metrics |
|workqueue_work_duration_seconds_bucket |Other metrics |
|workqueue_unfinished_work_seconds |Other metrics |
|workqueue_retries_total |Other metrics |
|workqueue_longest_running_processor_seconds |Other metrics |
|rest_client_request_size_bytes_count |Other metrics |
|rest_client_request_size_bytes_sum |Other metrics |
|rest_client_request_size_bytes_bucket |Other metrics |
|rest_client_rate_limiter_duration_seconds_count |Other metrics |
|rest_client_rate_limiter_duration_seconds_sum |Other metrics |
|rest_client_rate_limiter_duration_seconds_bucket |Other metrics |
|rest_client_exec_plugin_ttl_seconds |Other metrics |
|rest_client_exec_plugin_certificate_rotation_age_count |Other metrics |
|rest_client_exec_plugin_certificate_rotation_age_sum |Other metrics |
|rest_client_exec_plugin_certificate_rotation_age_bucket |Other metrics |
|process_virtual_memory_max_bytes |Other metrics |
|process_virtual_memory_bytes |Other metrics |
|process_start_time_seconds |Other metrics |
|plugin_manager_total_plugins |Other metrics |
|kubelet_started_pods_total |Other metrics |
|kubelet_started_containers_total |Other metrics |
|kubelet_managed_ephemeral_containers |Other metrics |
|kubelet_graceful_shutdown_start_time_seconds |Other metrics |
|kubelet_graceful_shutdown_end_time_seconds |Other metrics |
|go_sched_latencies_seconds |Other metrics |
|go_sched_goroutines_goroutines |Other metrics |
|go_sched_gomaxprocs_threads |Other metrics |
|go_memory_classes_total_bytes |Other metrics |
|go_memory_classes_profiling_buckets_bytes |Other metrics |
|go_memory_classes_other_bytes |Other metrics |
|go_memory_classes_os_stacks_bytes |Other metrics |
|go_memory_classes_metadata_other_bytes |Other metrics |
|go_memory_classes_metadata_mspan_inuse_bytes |Other metrics |
|go_memory_classes_metadata_mspan_free_bytes |Other metrics |
|go_memory_classes_metadata_mcache_inuse_bytes |Other metrics |
|go_memory_classes_metadata_mcache_free_bytes |Other metrics |
|go_memory_classes_heap_unused_bytes |Other metrics |
|go_memory_classes_heap_stacks_bytes |Other metrics |
|go_memory_classes_heap_released_bytes |Other metrics |
|go_memory_classes_heap_objects_bytes |Other metrics |
|go_memory_classes_heap_free_bytes |Other metrics |
|go_gc_stack_starting_size_bytes |Other metrics |
|go_gc_pauses_seconds_count |Other metrics |
|go_gc_pauses_seconds_sum |Other metrics |
|go_gc_pauses_seconds_bucket |Other metrics |
|go_gc_limiter_last_enabled_gc_cycle |Other metrics |
|go_gc_heap_tiny_allocs_objects_total |Other metrics |
|go_gc_heap_objects_objects |Other metrics |
|go_gc_heap_goal_bytes |Other metrics |
|go_gc_heap_frees_objects_total |Other metrics |
|go_gc_heap_frees_bytes_total |Other metrics |
|go_gc_heap_allocs_objects_total |Other metrics |
|go_gc_heap_allocs_bytes_total |Other metrics |
|go_gc_cycles_total_gc_cycles_total |Other metrics |
|go_gc_cycles_forced_gc_cycles_total |Other metrics |
|go_gc_cycles_automatic_gc_cycles_total |Other metrics |
|go_cgo_go_to_c_calls_calls_total |Other metrics |
|get_token_count |Other metrics |
|authentication_token_cache_request_total |Other metrics |
|authentication_token_cache_request_duration_seconds_count |Other metrics |
|authentication_token_cache_request_duration_seconds_sum |Other metrics |
|authentication_token_cache_request_duration_seconds_bucket |Other metrics |
|authentication_token_cache_fetch_total |Other metrics |
|authentication_token_cache_active_fetch_count |Other metrics |
|apiserver_webhooks_x509_missing_san_total |Other metrics |
|apiserver_webhooks_x509_insecure_sha1_total |Other metrics |
|apiserver_storage_envelope_transformation_cache_misses_total |Other metrics |
|apiserver_storage_data_key_generation_duration_seconds_count |Other metrics |
|apiserver_storage_data_key_generation_duration_seconds_sum |Other metrics |
|apiserver_storage_data_key_generation_duration_seconds_bucket |Other metrics |
|apiserver_envelope_encryption_dek_cache_fill_percent |Other metrics |
|apiserver_delegated_authz_request_total |Other metrics |
|apiserver_delegated_authz_request_duration_seconds_count |Other metrics |
|apiserver_delegated_authz_request_duration_seconds_sum |Other metrics |
|apiserver_delegated_authz_request_duration_seconds_bucket |Other metrics |
|apiserver_delegated_authn_request_total |Other metrics |
|apiserver_delegated_authn_request_duration_seconds_count |Other metrics |
|apiserver_delegated_authn_request_duration_seconds_sum |Other metrics |
|apiserver_delegated_authn_request_duration_seconds_bucket |Other metrics |
|apiserver_client_certificate_expiration_seconds_count |Other metrics |
|apiserver_client_certificate_expiration_seconds_sum |Other metrics |
|apiserver_client_certificate_expiration_seconds_bucket |Other metrics |
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
|storage_operation_errors_total |Other metrics |
|kubelet_volume_metric_collection_duration_seconds_sum |Other metrics |
|kubelet_volume_metric_collection_duration_seconds_count |Other metrics |
|kubelet_volume_metric_collection_duration_seconds_bucket |Other metrics |
|kubelet_containers_per_pod_count_sum |Other metrics |
|kubelet_containers_per_pod_count_count |Other metrics |
|kubelet_containers_per_pod_count_bucket |Other metrics |
|kubelet_cpu_manager_pinning_requests_total |Other metrics |
|kubelet_lifecycle_handler_http_fallbacks_total |Other metrics |
|kubelet_pod_start_sli_duration_seconds_bucket |Other metrics |
|kubelet_pod_start_sli_duration_seconds_count |Other metrics |
|kubelet_pod_start_sli_duration_seconds_sum |Other metrics |
|kubelet_pod_status_sync_duration_seconds_bucket |Other metrics |
|kubelet_pod_status_sync_duration_seconds_count |Other metrics |
|kubelet_pod_status_sync_duration_seconds_sum |Other metrics |
|registered_metric_total |Other metrics |
|disabled_metric_total |Other metrics |
|go_gc_heap_allocs_by_size_bytes_bucket |Other metrics |
|go_gc_heap_allocs_by_size_bytes_count |Other metrics |
|go_gc_heap_allocs_by_size_bytes_sum |Other metrics |
|go_gc_heap_frees_by_size_bytes_bucket |Other metrics |
|go_gc_heap_frees_by_size_bytes_count |Other metrics |
|go_gc_heap_frees_by_size_bytes_sum |Other metrics |
|go_sched_latencies_seconds_bucket |Other metrics |
|go_sched_latencies_seconds_count |Other metrics |
|go_sched_latencies_seconds_sum |Other metrics |
|hidden_metric_total |Other metrics |
