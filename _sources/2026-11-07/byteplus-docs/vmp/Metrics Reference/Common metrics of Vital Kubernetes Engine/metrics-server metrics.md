---
title: "metrics-server metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/metrics-server_metrics"
---

metrics\-server serves as a monitoring component for Vital Kubernetes Engine (VKE) clusters. It is mainly used to aggregate the core monitoring data of resources within the cluster. This topic describes the common metrics of metrics\-server in the VKE cluster.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="p3nwngZP"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|metrics_server_storage_points |Basic metric |
|metrics_server_manager_tick_duration_seconds_bucket |Basic metric |
|metrics_server_manager_tick_duration_seconds_sum |Basic metric |
|metrics_server_manager_tick_duration_seconds_count |Basic metric |
|metrics_server_api_metric_freshness_seconds_bucket |Basic metric |
|metrics_server_api_metric_freshness_seconds_sum |Basic metric |
|metrics_server_api_metric_freshness_seconds_count |Basic metric |
|metrics_server_kubelet_origin_extremum_value |Basic metric |


<span id="5eJRtLcH"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|metrics_server_kubelet_request_duration_seconds_bucket |Other metric |
|metrics_server_kubelet_request_duration_seconds_sum |Other metric |
|metrics_server_kubelet_request_duration_seconds_count |Other metric |
|metrics_server_kubelet_last_request_time_seconds |Other metric |
|metrics_server_kubelet_request_total |Other metric |
