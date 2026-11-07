---
title: "csi-ebs metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/csi-ebs_metrics"
---

csi\-ebs is the storage service add\-on for Vital Kubernetes Engine (VKE) clusters. It provides the standard Container Storage Interface (CSI) implementation that enables the VKE cluster to use Elastic Block Storage (EBS). This topic describes the common query metrics of csi\-ebs.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, o**ther metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="AwuL6RFd"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|volc_api_throttled_requests_total |Basic metric |
|volc_api_request_errors |Basic metric |
|volc_api_request_duration_seconds |Basic metric |
|volc_api_request_duration_seconds_bucket |Basic metric |
|volc_api_request_duration_seconds_count |Basic metric |
|volc_api_request_duration_seconds_sum |Basic metric |
|process_virtual_memory_max_bytes |Basic metric |
|process_virtual_memory_bytes |Basic metric |
|process_resident_memory_bytes |Basic metric |
|process_open_fds |Basic metric |
|process_max_fds |Basic metric |
|process_cpu_seconds_total |Basic metric |
|go_threads |Basic metric |
|go_goroutines |Basic metric |


<span id="8ukuULE8"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|process_start_time_seconds |Other metrics |
|go_sched_latencies_seconds |Other metrics |
|go_sched_latencies_seconds_bucket |Other metrics |
|go_sched_latencies_seconds_count |Other metrics |
|go_sched_latencies_seconds_sum |Other metrics |
|go_sched_goroutines_goroutines |Other metrics |
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
|go_info |Other metrics |
|go_goroutines |Basic metric |
|go_gc_pauses_seconds_total |Other metrics |
|go_gc_pauses_seconds_total_bucket |Other metrics |
|go_gc_pauses_seconds_total_count |Other metrics |
|go_gc_pauses_seconds_total_sum |Other metrics |
|go_gc_heap_tiny_allocs_objects_total |Other metrics |
|go_gc_heap_objects_objects |Other metrics |
|go_gc_heap_goal_bytes |Other metrics |
|go_gc_heap_frees_objects_total |Other metrics |
|go_gc_heap_frees_bytes_total |Other metrics |
|go_gc_heap_frees_by_size_bytes_total |Other metrics |
|go_gc_heap_frees_by_size_bytes_total_bucket |Other metrics |
|go_gc_heap_frees_by_size_bytes_total_count |Other metrics |
|go_gc_heap_frees_by_size_bytes_total_sum |Other metrics |
|go_gc_heap_allocs_objects_total |Other metrics |
|go_gc_heap_allocs_bytes_total |Other metrics |
|go_gc_heap_allocs_by_size_bytes_total |Other metrics |
|go_gc_heap_allocs_by_size_bytes_total_bucket |Other metrics |
|go_gc_heap_allocs_by_size_bytes_total_count |Other metrics |
|go_gc_heap_allocs_by_size_bytes_total_sum |Other metrics |
|go_gc_duration_seconds |Other metrics |
|go_gc_duration_seconds_count |Other metrics |
|go_gc_duration_seconds_sum |Other metrics |
|go_gc_cycles_total_gc_cycles_total |Other metrics |
|go_gc_cycles_forced_gc_cycles_total |Other metrics |
|go_gc_cycles_automatic_gc_cycles_total |Other metrics |
