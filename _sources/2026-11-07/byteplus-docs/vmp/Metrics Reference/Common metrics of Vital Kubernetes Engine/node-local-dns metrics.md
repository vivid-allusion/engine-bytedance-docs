---
title: "node-local-dns metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/node-local-dns_metrics"
---

node\-local\-dns serves as a local Domain Name System (DNS) caching add\-on of the Vital Kubernetes Engine (VKE) cluster. The add\-on provides a DNS caching proxy to improve the performance and stability of DNS service discovery in the cluster. This topic describes the common query metrics of node\-local\-dns.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types.

<span id="6PfzDk05"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|coredns_reload_failed_total |Basic metric |
|coredns_local_localhost_requests_total |Basic metric |
|coredns_health_request_duration_seconds_sum |Basic metric |
|coredns_health_request_duration_seconds_count |Basic metric |
|coredns_health_request_duration_seconds_bucket |Basic metric |
|coredns_forward_responses_total |Basic metric |
|coredns_forward_requests_total |Basic metric |
|coredns_forward_request_duration_seconds_sum |Basic metric |
|coredns_forward_request_duration_seconds_count |Basic metric |
|coredns_forward_request_duration_seconds_bucket |Basic metric |
|coredns_forward_max_concurrent_rejects_total |Basic metric |
|coredns_forward_healthcheck_broken_total |Basic metric |
|coredns_forward_conn_cache_misses_total |Basic metric |
|coredns_forward_conn_cache_hits_total |Basic metric |
|coredns_dns_responses_total |Basic metric |
|coredns_dns_response_size_bytes_sum |Basic metric |
|coredns_dns_response_size_bytes_count |Basic metric |
|coredns_dns_response_size_bytes_bucket |Basic metric |
|coredns_dns_requests_total |Basic metric |
|coredns_dns_request_size_bytes_sum |Basic metric |
|coredns_dns_request_size_bytes_count |Basic metric |
|coredns_dns_request_size_bytes_bucket |Basic metric |
|coredns_dns_request_duration_seconds_sum |Basic metric |
|coredns_dns_request_duration_seconds_count |Basic metric |
|coredns_dns_request_duration_seconds_bucket |Basic metric |
|coredns_cache_misses_total |Basic metric |
|coredns_cache_hits_total |Basic metric |
|coredns_cache_entries |Basic metric |
|coredns_build_info |Basic metric |
|coredns_panics_total |Basic metric |
|coredns_kubernetes_dns_programming_duration_seconds_sum |Basic metric |
|coredns_kubernetes_dns_programming_duration_seconds_bucket |Basic metric |
|coredns_kubernetes_dns_programming_duration_seconds_count |Basic metric |
|coredns_dns_do_requests_total |Basic metric |
|coredns_cache_requests_total |Basic metric |
|controller_runtime_webhook_requests_total |Basic metric |
|controller_runtime_webhook_latency_seconds_bucket |Basic metric |
|controller_runtime_webhook_latency_seconds_sum |Basic metric |
|controller_runtime_webhook_latency_seconds_count |Basic metric |
|rest_client_request_duration_seconds_bucket |Basic metric |
|rest_client_request_duration_seconds_count |Basic metric |
|rest_client_request_duration_seconds_sum |Basic metric |
|controller_runtime_webhook_requests_in_flight |Basic metric |


<span id="GJNJXfwO"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|coredns_plugin_enabled |Other metrics |
|coredns_hosts_reload_timestamp_seconds |Other metrics |
|coredns_health_request_failures_total |Other metrics |
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
|coredns_dns_quic_responses_total |Other metrics |
|coredns_dns_https_responses_total |Other metrics |
|process_cpu_seconds_total |Other metrics |
|process_max_fds |Other metrics |
|process_resident_memory_bytes |Other metrics |
|process_start_time_seconds |Other metrics |
|process_virtual_memory_bytes |Other metrics |
|process_virtual_memory_max_bytes |Other metrics |
