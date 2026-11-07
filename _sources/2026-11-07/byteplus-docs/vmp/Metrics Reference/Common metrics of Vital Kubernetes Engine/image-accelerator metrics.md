---
title: "image-accelerator metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/image-accelerator_metrics"
---

image\-accelerator serves as a container image acceleration add\-on of the Vital Kubernetes Engine (VKE) cluster. It uses nydus to achieve image lazy loading and accelerate image pulling during pod creation. This topic describes the common query metrics of image\-accelerator.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="c0DibeBm"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|nydusd_hung_io_counts |Basic metric |
|nydusd_cumulative_read_block_bytes_sum |Basic metric |
|nydusd_cumulative_read_block_bytes_count |Basic metric |
|nydusd_cumulative_read_block_bytes_bucket |Basic metric |
|nydusd_read_errors |Basic metric |
|snapshotter_thread_counts |Basic metric |
|snapshotter_fd_counts |Basic metric |
|snapshotter_cpu_user_time_seconds |Basic metric |
|snapshotter_cpu_system_time_seconds |Basic metric |
|snapshotter_memory_usage_kilobytes |Basic metric |
|snapshotter_cpu_usage_percentage |Basic metric |
|snapshotter_snapshot_operation_elapsed_milliseconds_sum |Basic metric |
|snapshotter_snapshot_operation_elapsed_milliseconds_count |Basic metric |
|snapshotter_snapshot_operation_elapsed_milliseconds_bucket |Basic metric |
|nydusd_rss_kilobytes |Basic metric |
|nydusd_counts |Basic metric |


<span id="6mfLNyAY"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|nydusd_read_latency_microseconds_sum |Other metrics |
|nydusd_read_latency_microseconds_count |Other metrics |
|nydusd_read_latency_microseconds_bucket |Other metrics |
|nydusd_read_hits |Other metrics |
|nydusd_total_read_bytes |Other metrics |
|snapshotter_run_time_seconds |Other metrics |
|snapshotter_cache_usage_kilobytes |Other metrics |
|nydusd_lifetime_event_counts |Other metrics |
