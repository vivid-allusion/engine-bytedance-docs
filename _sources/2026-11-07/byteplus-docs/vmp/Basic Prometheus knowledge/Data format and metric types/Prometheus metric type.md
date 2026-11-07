---
title: "Prometheus metric type"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Prometheus-metric-types"
---

From the perspective of storage, all metrics in Prometheus are the same. However, subtle differences exist among these metrics in different scenarios. For example, in the samples returned by the node exporter,


* the metric node_load1 indicates the current system load status. The sample data returned by this metric changes continuously over time.

* The sample data obtained by the metric node_cpu_seconds_total is different. The value continuously increases because it indicates the cumulative usage duration of the node CPU. Therefore, theoretically, the value will continue to increase if the node is not stopped. To help users distinguish the metrics, Prometheus defines four different metric types, including counter, gauge, histogram, and summary.



|Metric Type |Descriptions |Common Metrics |
|---|---|---|
|Counter |The value of a counter can only increase or be reset to zero on system restart. Common metrics, such as `http_requests_total` and `node_cpu_seconds_total`, are all counters. The name of the counter is often suffixed with `_total`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A counter is a simple but useful metric. However, the cumulative value of a metric cannot directly help users understand the system status. Therefore, a counter is often used with the rate or increase function and a <strong>range vector</strong>.</div><br> |CPU usage duration, network traffic, and request count |
|Gauge |Different from a counter, a gauge indicates the current state of the system. Therefore, the sample data of this type of metric can increase or decrease. For example, `node_memory_MemFree_bytes` (the current free memory size on the host) and `container_memory_usage_bytes` (the current memory size of the container) are both gauges. |Memory usage, disk space, and service running status |
|Histogram |However, a counter can only be calculated as a mean value. The mean value is not enough for data such as **API request latency**. You also need to view the distribution of the data and even calculate quantiles. For this type of data, Prometheus provides two types of metrics: histogram and summary. A histogram pre\-defines multiple buckets for grouping all possible samples. When a new sample is collected, it falls into a specific bucket. When you use a histogram, you can calculate quantiles by using the distribution of samples across various buckets. Heatmaps are especially suitable for displaying histograms. |Various latency and duration metrics |
|Summary |Similar to a histogram, a summary can also be used to view the distribution of data. However, the difference lies in that a summary returns calculated data, which is the specific value of the median. Therefore, compared with a histogram, a summary omits computing consumption during queries, which also results in the loss of the original sample data. ||
