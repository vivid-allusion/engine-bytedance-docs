---
title: "Monitoring service observability"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring_service_observability"
---

Monitoring service observability allows you to monitor key metrics of the prometheus\-adapter add\-on, including request load, error rate, cache refresh, process resources, and more. This helps you quickly locate add\-on anomalies and assess the operational health status. This topic describes how to enable monitoring service observability, configure collection rules, and view the preset observability dashboard for prometheus\-adapter.

## Prerequisites

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The VKE observability feature has been enabled. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

* The prometheus\-adapter add\-on has been installed. For details, see [prometheus-adapter](https://docs.byteplus.com/en/docs/vke/prometheus-adapter-add-on?lang=en).

## Procedure

### Step 1: Enable observability

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Find the target cluster and click its name.

3. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

4. On the **Monitoring services** card, click **Enable** to enable monitoring service observability for the cluster.

5. The system automatically checks the necessary conditions for enabling observability, These conditions include workspace configuration, add\-on status, and more.

6. Click **To enable it first** to enable monitoring service observability.

### Step 2: Configure collection rules

After monitoring service observability is enabled, you can configure collection rules to specify the target add\-ons, specific metrics, and time intervals for metric collection. You can discard unnecessary metrics as needed.

1. In the left navigation pane of the cluster management page, click **Observability settings**, and select the **Basic observability** tab.

2. On the **Monitoring services** card, click **Edit settings**. Select the **Metric** tab to configure collection rules that specify the target metrics to collect.

   * In the **Actions** column of the add\-on list, click the switch to enable or disable the collection rules for the target add\-on. After you disable the collection rules, the system stops collecting metrics for that component.

   * In the **Actions** column of the add\-on list, click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f33c825f87fff5f5ec3e0ffd80c56234.png) icon to add or remove specific metrics or configure the metric collection interval and metric relabeling for the add\-on.

      * For **Collection interval**, select a collection interval for the metrics of the add\-on. The supported collection intervals vary for different add\-ons.

      * In the **metric list**, select a metric to collect. To stop collecting a metric, uncheck it. Click the **All**, **Basic metrics**, or **Other metrics** tab to filter metrics by type.

         > **tip**

         * > The impact of adjusting the metric collection interval is as follows. Adjust the interval as needed:

            * > Reducing the collection interval: This increases the number of metrics reported per unit time and improves monitoring accuracy. However, the cost of standard VMP workspaces increases.

            * > Increasing the collection interval: This decreases the number of metrics reported per unit time and lowers the cost of standard VMP workspaces. However, this decreases monitoring accuracy.

         * > Cloud service metrics are categorized into **Basic metrics** and **Other metrics**. The billing method varies based on different types of metrics. For details, see [VMP billing](https://docs.byteplus.com/en/docs/vmp/pay-as-you-go).

      * In the **metricRelabelings** section, click **Add rule** to configure metric relabeling rules. This allows you to rewrite the labels of each metric after collection and before writing to storage. Common use cases include modifying label values, adding new labels, and renaming labels to standardize label naming for queries. For details, see [Metric relabeling](https://docs.byteplus.com/en/docs/vmp/Metric_relabel?lang=en).

         |No. |Feature |Replacement value |Description |
         |---|---|---|---|
         |① |Action type |`action` |The action to apply to the metrics. Currently, only **replace** is supported. The logic is as follows:<br><br><br>* If the values of `target_label` and `source_labels` are the same, the value of `source_label` is overwritten.<br><br>* If the key specified by `target_label` does not exist, a new label is created by default. |
         |② |Source labels |`sourceLabels` |Specify one or more source labels, separated by `\|` if multiple labels are provided. The system reads the values of these labels for matching or extraction. |
         |③ |Regular expression |`regex` |The regular expression pattern used to match source label values.<br><br><br>* The default is `(.*)`, which matches any value.<br><br>* You can use capture groups such as `(.+)` to extract partial content. |
         |④ |Replacement value |`replacement` |The value written to the target label after a successful match.<br><br><br>* The default is `$1`, which refers to the content of the first capture group in the regular expression.<br><br>* A fixed string is also supported. |
         |⑤ |Target label |`targetLabel` |The name of the target label to which the processing result is written.<br><br><br>* If the target label already exists, its existing value is overwritten.<br><br>* If the target label does not exist, a new label is created. |

3. Click **Confirm** to finish.

### Step 3: Configure alerting

Monitoring service observability currently does not support alert rule templates. To configure alert rules, see [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules).

## Observability dashboards

> **tip**

> The built\-in dashboards provide features such as period\-over\-period comparisons of monitoring data and the ability to copy dashboard queries. For details, see [Usage of dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

You can view the built\-in monitoring dashboard in the VKE console. This dashboard provides information such as API service quality, metric discovery cache, and process resources.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Monitoring services** \> **Prometheus Adapter monitoring** to view the monitoring dashboard.

   The following table describes the charts on the prometheus\-adapter dashboard in detail.

   > Description

   > For the method of obtaining the PromQL statements that correspond to the charts, see [Using dashboards](https://docs.byteplus.com/en/docs/vke/Using_dashboard).

   |Chart name |Unit |Chart description |
   |---|---|---|
   |**Overview/One Screen Overview** |||
   |API QPS |req/s | The total request rate across all API traffic (calculated based on data from the past 5 minutes), including requests to /healthz, /apis, and the metrics API. This information reflects the request load of the add\-on.<br><br><br>* Under normal circumstances, this value should fluctuate periodically and steadily in line with the collection interval of the HPA controller.<br><br>* If there is a sustained increase or spike, it usually indicates that a large number of HPA objects are frequently pulling custom metrics. We recommend checking whether any HPA has a configuration with an excessively short collection interval or whether there are abnormal metric query requests. |
   |5xx Error Ratio |% |The proportion of 5xx error requests to total requests (calculated based on data from the past 5 minutes), reflecting the add\-on's request error rate.<br><br><br>* Under normal circumstances, the error rate should be close to 0%, and occasional brief fluctuations are within an acceptable range.<br><br>* If the error rate remains above 0% or rises significantly, it typically indicates that the add\-on is encountering errors when processing custom metric queries. Check the add\-on logs and verify whether the backend Prometheus is reachable. |
   |API P99 Latency |Milliseconds |The P99 latency of API requests (calculated based on data from the past 5 minutes), reflecting the tail latency of request processing by the adapter.<br><br><br>* Under normal circumstances, the P99 latency should remain low, fluctuating with request volume but remaining overall stable.<br><br>* If the P99 latency increases significantly or remains persistently high, it usually indicates that the add\-on's response is slowing down, which may impact the timeliness of HPA scaling that depends on custom metrics. Check the add\-on's resource usage and the performance of backend Prometheus queries. |
   |Panics (1h) |Count |The cumulative number of panics (calculated based on data from the past 1 hour), reflecting the stability of the add\-on process.<br><br><br>* Under normal circumstances, this value should always be 0.<br><br>* If a value greater than 0 is observed, it indicates that the add\-on process has crashed and restarted. Investigate the add\-on logs immediately to identify the cause of the panic and resolve the issue... |
   |Cache Refreshes (10m) |Count |The cumulative number of cache refresh triggers (calculated based on data from the past 10 minutes), reflecting the update frequency of the add\-on's metric cache.<br><br><br>* Under normal circumstances, this value should increase periodically at a fixed cycle, consistent with the cache refresh interval specified in the add\-on configuration.<br><br>* If this value remains at 0 for an extended period, it indicates that the cache is not refreshed and custom metric data may have stopped updating. In this case, check whether the add\-on is running normally. If the refresh count is high, there may be frequent restarts or a configuration anomaly. |
   |Process Uptime |Automatic conversion (seconds / minutes / hours) |The continuous execution time of the prometheus\-adapter process (current time minus process start time), reflecting the stability of the Adapter instance.<br><br><br>* Under normal circumstances, this value should keep increasing monotonically, indicating that the add\-on process is running stably without a restart.<br><br>* If this value drops sharply (resets to zero and starts growing again), it indicates that the add\-on process has restarted. The Reason for restart should be investigated by correlating the Panics metric and Addon log. |
   |**API Service/API Quality of Service** |||
   |API Request Rate by Subresource / Code |req/s |The average API request rate by subresource and status code (calculated based on data from the past 5 minutes), reflecting the request volume and response distribution for different subresources.<br><br><br>* Under normal circumstances, the request rate varies with the query frequency of clients such as HPA, and success status codes should account for the majority.<br><br>* If the 4xx or 5xx request rate for a certain subresource continues to rise, we recommend troubleshooting request failures by correlating the corresponding status code, add\-on logs, and Prometheus backend status. |
   |5xx Error Ratio |% |The proportion of 5xx error requests to total requests (calculated based on data from the past 5 minutes), reflecting server\-side errors encountered by the add\-on when processing API requests.<br><br><br>* Under normal circumstances, this proportion should be close to 0%.<br><br>* If this proportion continues to rise, it usually indicates that an abnormal condition occurred when the add\-on processed custom metric queries. Check the add\-on logs, resource usage, and whether the backend Prometheus is reachable. |
   |API Request Latency |Milliseconds (ms) |The P50, P95, and P99 latency of API requests (calculated based on data from the past 5 minutes), reflecting the overall latency and tail latency of API requests.<br><br><br>* Under normal conditions, all percentile values should remain stable, with P95 and P99 higher than P50.<br><br>* If P95 or P99 continues to rise, it indicates that some requests are becoming slower, which may affect the timeliness of HPA retrieving custom metrics. Check the component resource usage and the query performance of the backend Prometheus. |
   |Inflight Requests |Count |The number of API requests being processed by prometheus\-adapter at the current time, shown by request type. This information reflects the add\-on's real\-time concurrent request pressure.<br><br><br>* Under normal circumstances, this value fluctuates as requests arrive and are processed.<br><br>* If this value remains high or continues to increase, it indicates that requests may be accumulating. Troubleshoot process bottlenecks using API request Latency, CPU usage, and add\-on logs. |
   |API Request Rate by Verb / Subresource |req/s |The average API request rate calculated by request method and subresource (based on data from the past 5 minutes), reflecting the access frequency of different types of custom metric queries.<br><br><br>* Under normal circumstances, the request rate changes with the query frequency of clients such as HPA.<br><br>* When the request rate of a certain type increases abnormally, we recommend checking whether there are a large number of HPAs performing high\-frequency queries on the same subresource or whether the client is configured with an excessively short query interval. |
   |TLS Handshake Errors |Count |The cumulative number of TLS handshake errors for prometheus\-adapter (calculated based on data from the past 5 minutes), reflecting anomalies encountered when clients establish encrypted connections to the add\-on.<br><br><br>* Under normal circumstances, this value should be 0.<br><br>* If this value is greater than 0 or continues to increase, check whether the aggregation API certificates are valid, whether the TLS configurations of the client and the add\-on are consistent, and review the handshake error messages in the add\-on logs. |
   |**Metric Discovery/Metric Discovery Cache** |||
   |Cache Refresh Rate |ops/s |The average cache refresh rate by refresh type (calculated based on data from the past 5 minutes), reflecting the update frequency of the metric discovery cache.<br><br><br>* Under normal circumstances, this value should change regularly according to the cache refresh cycle specified in the add\-on configuration.<br><br>* If this value remains at 0 for an extended period, it may indicate that the cache is not being refreshed properly. If the value is significantly higher than expected, check whether the add\-on is restarting frequently or whether the cache refresh configuration is abnormal. |
   |Cache Refresh Latency |Milliseconds (ms) |Cache refresh latency (calculated based on data from the past 5 minutes), showing the average, P95, and P99 values broken down by refresh type. This information reflects the refresh efficiency and tail latency of the metric discovery cache.<br><br><br>* Under normal conditions, all latency values should remain stable, with P95 and P99 higher than the average.<br><br>* If P95 or P99 continues to rise, it indicates that some cache refreshes are slowing down, which may cause new metrics or metric changes not to be discovered in time. Check backend Prometheus query performance, rule quantity, and add\-on resource usage. |
   |Cache Refresh Attempts (10m) |Count |The number of cache refresh attempts counted by refresh type (calculated based on data from the past 10 minutes), reflecting the refresh frequency of the metric discovery cache.<br><br><br>* Under normal circumstances, this value should match the cache refresh cycle specified in the add\-on configuration.<br><br>* If this value remains at 0 for a long time, it may indicate that cache refresh is not being executed. If it is significantly higher than expected, we recommend checking whether the add\-on is frequently restarted or if the cache refresh configuration is abnormal. |
   |Refreshes over 10s (15m) |Count |The number of cache refreshes that took longer than 10 seconds, broken down by refresh type (calculated based on data from the past 15 minutes). This information reflects the occurrence of slow cache refresh requests.<br><br><br>* Under normal circumstances, this value should be 0 or remain low.<br><br>* If this value continues to increase, it indicates that cache refreshes are frequently taking longer than 10 seconds, which may cause delays in updating metric discovery results. Check the query performance of the backend Prometheus, the number of rules, and the resource usage of the component. |
   |**Runtime/Process Resources** |||
   |CPU Usage |cores |Average CPU usage of each prometheus\-adapter instance (calculated based on data from the past 5 minutes). The value represents the number of CPU cores used, reflecting the add\-on's computational resource consumption.<br><br><br>* Under normal conditions, this value should vary with API request volume and cache refresh task count and remain within the CPU limit of the instance.<br><br>* If this Value continues to rise OR approaches the CPU limit, requests and cache refreshes may slow down. Troubleshoot the issue by combining API request latency, cache refresh latency, and instance resource configuration. |
   |Resident Memory |byte |The resident memory size used by each prometheus\-adapter instance at the current moment, reflecting the amount of data actually resident in physical memory for the add\-on.<br><br><br>* Under normal circumstances, this value fluctuates with cache size and request load, but should remain generally stable.<br><br>* If this value continues to grow or approaches the memory limit, it may indicate an excessively large cache size or abnormal memory growth. Combine the instance memory limit, restart records, and add\-on logs to troubleshoot the issue. |
   |File Descriptor Utilization |% |The proportion of open file descriptors to the maximum allowed by the system across all prometheus\-adapter instances at the current moment, reflecting the usage of file descriptor resources.<br><br><br>* Under normal circumstances, this proportion should remain low and stable.<br><br>* If this proportion continues to rise or approaches 100%, the add\-on may not be able to establish new network connections or open files. Check whether connections are properly released and examine the maximum process file descriptor limit. |
   |Goroutines |Count |The current Goroutine quantity for individual prometheus\-adapter instances. This information reflects the scale of concurrent tasks within the add\-on.<br><br><br>* Under normal circumstances, this value fluctuates slightly with request volume and cache refresh tasks and remains relatively stable.<br><br>* If this value continues to increase and does not decrease, request blocking or abnormal Goroutine exits may have occurred. Troubleshoot the issue using the add\-on logs, request latency, and resource usage. |

## View metrics

* You can use the Explore feature of VMP to quickly query and display metric data. For details, see [Querying metrics](https://docs.byteplus.com/en/docs/vmp/explore-metrics).
