---
title: "Best practices for optimizing the performance of the Agent mode of open-source Prometheus"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Best_practices_for_optimizing_the_performance_of_the_Agent_mode_of_open-source_Prometheus"
---

In VKE or self‑managed Kubernetes clusters, you can select an appropriate metric collection method based on cluster scale, data write pipeline, and operational complexity. This topic describes how to improve the performance of the Agent mode when you use open\-source Prometheus to collect metrics and write them to VMP. The performance is optimized from three aspects: parameter configuration, labeling and metric data filtering before writing, and pressure relief and buffering.

<span id="NsOqx2PA"></span>
## Optimize parameter configuration

You can optimize the `remote_write` configuration of the Prometheus Agent as described in this section. The parameters and descriptions are as follows:


|**Parameters** |**Purpose and description** |**Adjustment guidance** |
|---|---|---|
|capacity |The memory queue capacity per shard. Default value: 10000. |We recommend setting the value to 3 to 10 times `max_samples_per_send`. A low value may cause queue backlog, and a high value increases memory consumption. |
|min_shards |The minimum number of shards used at startup. Default value: 1. |For scenarios with stable traffic, you can increase this value to avoid initial performance ramp‑up and potential data backlog. |
|max_shards |The maximum allowed number of shards. Default value: 1000. |This is a key throughput control parameter. If the remote storage has high capacity, keep the default value or increase the value appropriately. If the remote storage encounters rate limiting or insufficient performance, reduce this value to lower concurrency pressure. |
|max_samples_per_send |The maximum number of samples per send request. Default value: 2000.<br><br> |It is related to the compatibility of the remote storage API. A higher value reduces the number of requests and improves efficiency, but may increase per‑request latency and memory usage. |
|batch_send_deadline |The maximum waiting time when the queue is not full. Default value: 5s. |For environments with small data volumes, you can increase this value appropriately to aggregate more samples into a single request and improve network transmission efficiency. |
|min_backoff |The minimum waiting time before a retry. Default value: 30ms. |When the remote service is recovering, increasing this value spreads out retry requests and prevents the thundering herd effect. |
|max_backoff |The maximum waiting time before a retry. Default value: 5s. |The maximum retry interval. During frequent network jitters, you can increase this value to reserve longer recovery time for the remote service. |
|remote_timeout |Sets the timeout to send a request, which is located at the top level of `remote_write`. Default value: 30s. |We recommend setting it to an appropriate value greater than the network latency and remote storage processing time. Increase it if the remote storage responds slowly. |


Select the initial configuration based on the collection scale

Select the corresponding initial `queue_config` configuration based on the number of samples per second (sps). This configuration matches the sending concurrency, queue capacity, and batch size with the current collection scale. You can further adjust it based on the running status.



<Tabs>
<Tab zoneid="uCLWeZ2d" title="Small scale: ≤ 1k sps">
<TabTitle>Small scale: ≤ 1k sps</TabTitle>

When the collection scale does not exceed 1k sps, use the following configurations as the initial values to reduce memory usage and send concurrency. With the default values (capacity: 10000, max_samples_per_send: 2000), the memory usage per shard is typically less than 2 MB. The total peak memory can be approximated by the formula: max_shards × memory_per_shard.

Sample configuration:

```YAML
# queue_config for small scale
capacity: 5000
min_shards: 1
max_shards: 10
max_samples_per_send: 1000
batch_send_deadline: 10s
min_backoff: 100ms
max_backoff: 10s
```


Adjustment guidance:


* Reduce `capacity` and `max_shards` to save memory.

* Increase `batch_send_deadline` to aggregate more samples and improve send efficiency.


</Tab>
<Tab zoneid="TarG7xPw" title="Medium scale: 5k–20k sps">
<TabTitle>Medium scale: 5k–20k sps</TabTitle>

If the collection scale is 5k to 20k sps, you can first use configurations close to the default values and monitor the number of shards and sample backlog. These observation results help determine whether the send concurrency is approaching the upper limit or whether the remote storage has insufficient capacity.

Sample configuration:

```YAML
# queue_config for medium scale (close to default)
capacity: 10000
min_shards: 1
max_shards: 100   # You can lower the value appropriately based on backend capacity.
max_samples_per_send: 2000
batch_send_deadline: 5s
min_backoff: 30ms
max_backoff: 5s
```


Adjustment guidance:


* Focus on monitoring the `prometheus_remote_storage_shards` metric.

* If the number of shards continuously approaches `max_shards` and `samples_pending` keeps increasing, it likely indicates the remote storage encounters rate limiting or insufficient performance. In this case, you need to decrease `max_shards` to reduce concurrency pressure.


</Tab>
<Tab zoneid="kvNqMHJJ" title="Large scale: ≥ 50k sps">
<TabTitle>Large scale: ≥ 50k sps</TabTitle>

When the collection scale reaches or exceeds 50k sps, we recommend increasing the queue capacity, minimum number of shards, and number of samples sent each time, and ensuring the remote storage can handle the corresponding concurrency.

Sample configuration:

```YAML
# queue_config for large scale
capacity: 20000
min_shards: 5
max_shards: 500   # Make sure that the remote storage can handle this concurrency.
max_samples_per_send: 2500
batch_send_deadline: 2s
min_backoff: 30ms
max_backoff: 2s
```


Adjustment guidance:


* Increase `capacity` and `max_samples_per_send` to match high throughput.

* Increase `min_shards` for quick start.

* Decrease `batch_send_deadline` and `max_backoff` to accelerate data sending and recovery.


</Tab>
</Tabs>



<span id="mjW0GQ3z"></span>
## Identify and filter metric data before writing


* Use `external_labels` to identify data sources

   Under the global block, use `external_labels` to attach fixed labels to all time series sent from this Agent, such as the cluster name, region, and environment. When data from multiple clusters, regions, or environments is written to the same remote storage, these labels help distinguish metric sources.

   ```YAML
   global:
     external_labels:
       cluster: 'xxxxx'
       prometheus: 'prometheus-agent'
   ```
   

* Use `write_relabel_configs` to filter metrics

   `write_relabel_configs` is a configuration under `remote_write` that allows you to filter, reshape, and modify time series data based on labels before they are sent. This can be used to retain key metrics or discard low‑value ones, controlling the data scope written to remote storage.

   ```YAML
   write_relabel_configs:
     # Only retain metrics starting with up or app_.
     - source_labels: [__name__]
       regex: 'up|app_.*'
       action: keep
     # Discard all metrics from the debug namespace.
     - source_labels: [kubernetes_namespace]
       regex: 'debug'
       action: drop
   ```
   

* Modify or rename labels

   Use `labelmap` or `replace` to unify label names or fix non‑standard label values. This reduces the number of inconsistent labels that are written to remote storage.

   ```YAML
   write_relabel_configs:
     # Replace all labels starting with __meta_kubernetes_pod_label_ with those starting with pod_.
     - regex: __meta_kubernetes_pod_label_(.+)
       replacement: 'pod_$1'
       action: labelmap
   ```
   

* Remove high\-cardinality labels

   We recommend not using labels that have infinite or extremely large possible values, such as id, uuid, email, and session. Such labels increase the number of time series, which may raise remote storage costs and query complexity. In `write_relabel_configs`, you can use `action: labeldrop` or `action: drop` to remove high‑cardinality labels.


<span id="XYtb6xZA"></span>
## Pressure relief and buffering


* Handle remote rate limiting or overload

   When the remote storage returns HTTP 429 (rate limiting) or HTTP 5xx (overload), we recommend adjusting the following parameters:

   * Reduce `max_shards`: Decrease the number of concurrent requests and reduce write pressure on the remote storage.

   * Increase `batch_send_deadline`: Extend the local waiting time to aggregate more samples before sending. This reduces request frequency.

   * Increase `min_backoff / max_backoff`: Extend the retry interval to reserve more time for remote recovery.

* Prevent data loss when the remote storage remains unavailable

   The Prometheus Agent caches data to be sent in the write\-ahead logging (WAL), which typically holds about 2 hours of data. If the remote storage remains unavailable for more than 2 hours, the oldest data will be discarded, resulting in permanent loss. To avoid data loss, we recommend taking the following measures in advance:

   * HA deployment: Deploy at least two Agent instances (replicas) scraping the same targets.

   * PV: Ensure the Agent uses a PV to prevent WAL loss on accidental Pod restarts.

   * Multi\-write: Configure multiple `remote_write` endpoints to write data simultaneously to two or more independent remote storage systems. This achieves a higher level of data redundancy.


<span id="yRlgjI9i"></span>
## Common faults and troubleshooting

After configuring `remote_write`, we recommend monitoring the `prometheus_remote_storage_*` metrics to observe the write status and identify issues such as sample backlog, send failures, shard count approaching the upper limit, increased send latency, or excessive retries. The following table covers key metrics of `prometheus_remote_storage_*` and their meanings to help you quickly locate exceptions in the write pipeline.


|Metric |Meaning |Typical alert threshold example |
|---|---|---|
|prometheus_remote_storage_samples_pending |The total number of samples to be sent to the remote storage. This is the core metric for measuring backlog. |\> 100000 for more than 5 minutes. You need to adjust the threshold based on the actual collection scale. |
|rate(prometheus_remote_storage_failed_samples_total[5m]) |The rate of samples that failed to send over the last 5 minutes. |\> 0 for more than 5 minutes. Any persistent send failure must be investigated immediately. |
|prometheus_remote_storage_shards |The current number of active shards. |\>= max_shards \* 0.9 for more than 15 minutes. The concurrency is approaching the upper limit, which indicates a risk of data backlog. |
|histogram_quantile(0.99, rate(prometheus_remote_storage_sent_batch_duration_seconds_bucket[5m])) |The P99 batch send latency. |\> remote_timeout \* 0.8. It indicates that per‑batch send time is close to the timeout threshold, which may cause a large number of retries. |
|rate(prometheus_remote_storage_retried_samples_total[5m]) |The rate of retried samples. |\> rate(prometheus_remote_storage_succeeded_samples_total[5m]) \* 0.1. It indicates that the retry frequency is too high. |
|time() \- prometheus_remote_storage_queue_highest_sent_timestamp_seconds |The current metric write latency. |\> 4\*scrape_interval. It indicates that the written data is far behind the current timestamp, which means that multiple rounds of data backlog have occurred. |


**Detect and resolve queue backlog (when pending samples continue to grow):** 


1. Check whether `prometheus_remote_storage_shards` has reached `max_shards`.

2. Check whether `sent_batch_duration` is too high and then determine whether the issue is network latency or slow remote\-side processing.

3. Check Agent logs for a large number of `HTTP 429`, `HTTP 5xx`, or `context deadline exceeded` errors.

4. If it is a backend issue, adjust `queue_config` based on the pressure relief policy.


**Detect and resolve high memory usage:** 


1. Check whether it is caused by too many shards. Especially during data backlog, `shards` automatically scale out to `max_shards`.

2. Check `prometheus_tsdb_head_series` to confirm whether it is caused by high\-cardinality targets.

3. Reduce `max_shards` to quickly control high memory usage.


**Detect and resolve certificate or authentication issues:** 


1. Check Agent logs. They typically contain clear TLS/Auth errors such as `certificate signed by unknown authority` or `authorization failed`.

2. Check whether the configurations of `tls_config` and `authorization` (such as `bearer_token_file`) are correct.

3. Check whether the certificate exists and has the correct permissions.
