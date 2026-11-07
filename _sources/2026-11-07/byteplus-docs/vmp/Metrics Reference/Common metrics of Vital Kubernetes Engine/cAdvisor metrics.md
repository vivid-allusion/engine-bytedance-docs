---
title: "cAdvisor metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-cAdvisor"
---

Provided by Google, cAdvisor is an open source tool used for monitoring and performance analysis of container resources. Tailored for containers, cAdvisor is integrated into Kubelet in Kubernetes. When Kubelet is started, cAdvisor is automatically started. A cAdvisor instance can monitor only one node. cAdvisor performs real\-time monitoring and performance data collection on resources and containers on nodes, including CPU, memory, network throughput, and file system. This topic describes the common metrics of cAdvisor.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and custom metrics. Billing methods vary based on different metric types. [Billing items](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go)

<span id="iZhZQgfD"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|machine_memory_bytes |Basic metric |
|machine_cpu_cores |Basic metric |
|container_threads_max |Basic metric |
|container_threads |Basic metric |
|container_tasks_state |Basic metric |
|container_start_time_seconds |Basic metric |
|container_sockets |Basic metric |
|container_processes |Basic metric |
|container_network_transmit_packets_total |Basic metric |
|container_network_transmit_packets_dropped_total |Basic metric |
|container_network_transmit_errors_total |Basic metric |
|container_network_transmit_bytes_total |Basic metric |
|container_network_receive_packets_total |Basic metric |
|container_network_receive_packets_dropped_total |Basic metric |
|container_network_receive_errors_total |Basic metric |
|container_network_receive_bytes_total |Basic metric |
|container_memory_working_set_bytes |Basic metric |
|container_memory_usage_bytes |Basic metric |
|container_memory_swap |Basic metric |
|container_memory_rss |Basic metric |
|container_memory_max_usage_bytes |Basic metric |
|container_memory_failures_total |Basic metric |
|container_memory_failcnt |Basic metric |
|container_memory_cache |Basic metric |
|container_fs_writes_bytes_total |Basic metric |
|container_fs_write_seconds_total |Basic metric |
|container_fs_usage_bytes |Basic metric |
|container_fs_reads_total |Basic metric |
|container_fs_reads_bytes_total |Basic metric |
|container_fs_read_seconds_total |Basic metric |
|container_fs_limit_bytes |Basic metric |
|container_fs_io_time_weighted_seconds_total |Basic metric |
|container_fs_io_time_seconds_total |Basic metric |
|container_fs_io_current |Basic metric |
|container_fs_inodes_total |Basic metric |
|container_fs_inodes_free |Basic metric |
|container_cpu_usage_seconds_total |Basic metric |
|container_cpu_cfs_throttled_periods_total |Basic metric |
|container_cpu_cfs_periods_total |Basic metric |
|cadvisor_version_info |Basic metric |
|machine_scrape_error |Basic metric |
|machine_cpu_sockets |Basic metric |
|container_spec_memory_swap_limit_bytes |Basic metric |
|container_spec_memory_reservation_limit_bytes |Basic metric |
|container_spec_memory_limit_bytes |Basic metric |
|container_spec_cpu_quota |Basic metric |
|container_spec_cpu_period |Basic metric |
|container_file_descriptors |Basic metric |
|container_cpu_user_seconds_total |Basic metric |
|container_cpu_system_seconds_total |Basic metric |
|container_cpu_load_average_10s |Basic metric |
|container_cpu_load_average_1min |Basic metric |
|container_cpu_cfs_throttled_seconds_total |Basic metric |
|machine_cpu_physical_cores |Basic metric |
|container_oom_events_total |Basic metric |
|container_blkio_device_usage_total |Basic metric |
|pod_cpu_usage_seconds_total |Basic metrics |
|pod_memory_working_set_bytes |Basic metric |
|vci_pod_cpu_resource |Basic metric |
|vci_pod_memory_resource |Basic metric |
|vci_pod_gpu_resource |Basic metric |


<span id="xCByglq6"></span>
## Other metrics


|Metric name |metric type |
|---|---|
|machine_nvm_capacity |Other metrics |
|machine_nvm_avg_power_budget_watts |Other metrics |
|container_ulimits_soft |Other metrics |
|container_spec_cpu_shares |Other metrics |
|container_scrape_error |Other metrics |
|container_memory_mapped_file |Other metrics |
|container_last_seen |Other metrics |
|container_fs_writes_total |Other metrics |
|container_fs_writes_merged_total |Other metrics |
|container_fs_sector_writes_total |Other metrics |
|container_fs_sector_reads_total |Other metrics |
|container_fs_reads_merged_total |Other metrics |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details about other metrics, see the <a href="https://github.com/google/cadvisor/blob/master/docs/storage/prometheus.md">official documentation</a>.</div>
