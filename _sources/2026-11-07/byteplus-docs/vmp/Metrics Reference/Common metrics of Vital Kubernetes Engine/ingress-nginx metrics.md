---
title: "ingress-nginx metrics"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/ingress-nginx_metrics"
---

ingress\-nginx serves as an Ingress controller of the Vital Kubernetes Engine (VKE) cluster. It uses NGINX as a reverse proxy and load balancer. This topic describes the common query metrics of ingress\-nginx.

Vital Managed Service for Prometheus (VMP) classifies the metrics reported by VKE clusters into the following types: **basic metrics**, **other metrics**, and **custom metrics**. Billing methods vary based on different metric types. 

<span id="GHxpllTb"></span>
## Basic metrics


|Metric name |Metric type |
|---|---|
|nginx_ingress_controller_success |Basic metric |
|nginx_ingress_controller_ssl_expire_time_seconds |Basic metric |
|nginx_ingress_controller_response_size_sum |Basic metric |
|nginx_ingress_controller_response_size_count |Basic metric |
|nginx_ingress_controller_response_size_bucket |Basic metric |
|nginx_ingress_controller_response_duration_seconds_sum |Basic metric |
|nginx_ingress_controller_response_duration_seconds_count |Basic metric |
|nginx_ingress_controller_response_duration_seconds_bucket |Basic metric |
|nginx_ingress_controller_requests |Basic metric |
|nginx_ingress_controller_request_size_sum |Basic metric |
|nginx_ingress_controller_request_size_count |Basic metric |
|nginx_ingress_controller_request_size_bucket |Basic metric |
|nginx_ingress_controller_request_duration_seconds_sum |Basic metric |
|nginx_ingress_controller_request_duration_seconds_count |Basic metric |
|nginx_ingress_controller_request_duration_seconds_bucket |Basic metric |
|nginx_ingress_controller_nginx_process_write_bytes_total |Basic metric |
|nginx_ingress_controller_nginx_process_virtual_memory_bytes |Basic metric |
|nginx_ingress_controller_nginx_process_resident_memory_bytes |Basic metric |
|nginx_ingress_controller_nginx_process_requests_total |Basic metric |
|nginx_ingress_controller_nginx_process_read_bytes_total |Basic metric |
|nginx_ingress_controller_nginx_process_oldest_start_time_seconds |Basic metric |
|nginx_ingress_controller_nginx_process_num_procs |Basic metric |
|nginx_ingress_controller_nginx_process_cpu_seconds_total |Basic metric |
|nginx_ingress_controller_nginx_process_connections_total |Basic metric |
|nginx_ingress_controller_nginx_process_connections |Basic metric |
|nginx_ingress_controller_leader_election_status |Basic metric |
|nginx_ingress_controller_ingress_upstream_latency_seconds_sum |Basic metric |
|nginx_ingress_controller_ingress_upstream_latency_seconds_count |Basic metric |
|nginx_ingress_controller_ingress_upstream_latency_seconds_bucket |Basic metric |
|nginx_ingress_controller_ingress_upstream_latency_seconds |Basic metric |
|nginx_ingress_controller_ingress_upstream_header_seconds_sum |Basic metric |
|nginx_ingress_controller_ingress_upstream_header_seconds_count |Basic metric |
|nginx_ingress_controller_ingress_upstream_header_seconds_bucket |Basic metric |
|nginx_ingress_controller_ingress_upstream_header_seconds |Basic metric |
|nginx_ingress_controller_config_last_reload_successful_timestamp_seconds |Basic metric |
|nginx_ingress_controller_config_last_reload_successful |Basic metric |
|nginx_ingress_controller_config_hash |Basic metric |
|nginx_ingress_controller_bytes_sent_sum |Basic metric |
|nginx_ingress_controller_bytes_sent_count |Basic metric |
|nginx_ingress_controller_bytes_sent_bucket |Basic metric |
|nginx_ingress_controller_build_info |Basic metric |
|nginx_ingress_controller_admission_roundtrip_duration |Basic metric |
|nginx_ingress_controller_connect_duration_seconds_bucket |Basic metric |
|nginx_ingress_controller_connect_duration_seconds_count |Basic metric |
|nginx_ingress_controller_connect_duration_seconds_sum |Basic metric |
|nginx_ingress_controller_header_duration_seconds_bucket |Basic metric |
|nginx_ingress_controller_header_duration_seconds_count |Basic metric |
|nginx_ingress_controller_header_duration_seconds_sum |Basic metric |


<span id="5W4hJm48"></span>
## Other metrics


|Metric name |Metric type |
|---|---|
|nginx_ingress_controller_ssl_certificate_info |Other metrics |
|nginx_ingress_controller_check_success |Other metrics |
|nginx_ingress_controller_admission_tested_ingresses |Other metrics |
|nginx_ingress_controller_admission_tested_duration |Other metrics |
|nginx_ingress_controller_admission_render_ingresses |Other metrics |
|nginx_ingress_controller_admission_render_duration |Other metrics |
|nginx_ingress_controller_admission_config_size |Other metrics |
|nginx_ingress_controller_errors |Other metrics |
|nginx_ingress_controller_check_errors |Other metrics |
|nginx_ingress_controller_orphan_ingress |Other metrics |
