---
title: "cr-credential-controller metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/cr-credential-controller_metrics"
---

cr\-credential\-controller serves as a container image password\-free add\-on of the Vital Kubernetes Engine (VKE) cluster. It can pull private images from Container Registry (CR) without passwords when applications are created in container clusters. This topic describes the common query metrics of cr\-credential\-controller.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="TCwKPlUQ"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|process_resident_memory_bytes |Basic metric |
|process_open_fds |Basic metric |
|process_max_fds |Basic metric |
|process_cpu_seconds_total |Basic metric |
|go_goroutines |Basic metric |
|cr_credential_client_request_duration_seconds |Basic metric |
|cr_credential_client_request_error |Basic metric |
|cr_credential_client_request_total |Basic metric |
|cr_credential_resource_request_error |Basic metric |
|cr_credential_resource_request_total |Basic metric |


<span id="0HJoBsUh"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|workqueue_work_duration_seconds_count |Other metrics |
|workqueue_work_duration_seconds_sum |Other metrics |
|workqueue_work_duration_seconds_bucket |Other metrics |
|workqueue_unfinished_work_seconds |Other metrics |
|workqueue_retries_total |Other metrics |
|workqueue_queue_duration_seconds_bucket |Other metrics |
|workqueue_queue_duration_seconds_sum |Other metrics |
|workqueue_queue_duration_seconds_count |Other metrics |
|workqueue_longest_running_processor_seconds |Other metrics |
|workqueue_depth |Other metrics |
|workqueue_adds_total |Other metrics |
|rest_client_response_size_bytes_sum |Other metrics |
|rest_client_response_size_bytes_count |Other metrics |
|rest_client_response_size_bytes_bucket |Other metrics |
|rest_client_requests_total |Other metrics |
|rest_client_request_duration_seconds_count |Other metrics |
|rest_client_request_duration_seconds_sum |Other metrics |
|rest_client_request_duration_seconds_bucket |Other metrics |
|process_virtual_memory_max_bytes |Other metrics |
|process_virtual_memory_bytes |Other metrics |
|process_start_time_seconds |Other metrics |
|leader_election_master_status |Other metrics |
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
|go_memstats_frees_total |Other metrics |
|go_memstats_buck_hash_sys_bytes |Other metrics |
|go_memstats_alloc_bytes_total |Other metrics |
|go_memstats_alloc_bytes |Other metrics |
|go_info |Other metrics |
|go_gc_duration_seconds_count |Other metrics |
|go_gc_duration_seconds_sum |Other metrics |
|go_gc_duration_seconds |Other metrics |
|controller_runtime_webhook_requests_total |Other metrics |
|controller_runtime_webhook_requests_in_flight |Other metrics |
|controller_runtime_webhook_latency_seconds_count |Other metrics |
|controller_runtime_webhook_latency_seconds_sum |Other metrics |
|controller_runtime_webhook_latency_seconds_bucket |Other metrics |
|controller_runtime_reconcile_total |Other metrics |
|controller_runtime_reconcile_time_seconds_count |Other metrics |
|controller_runtime_reconcile_time_seconds_sum |Other metrics |
|controller_runtime_reconcile_time_seconds_bucket |Other metrics |
|controller_runtime_reconcile_errors_total |Other metrics |
|controller_runtime_max_concurrent_reconciles |Other metrics |
|controller_runtime_active_workers |Other metrics |
|certwatcher_read_certificate_total |Other metrics |
|certwatcher_read_certificate_errors_total |Other metrics |
