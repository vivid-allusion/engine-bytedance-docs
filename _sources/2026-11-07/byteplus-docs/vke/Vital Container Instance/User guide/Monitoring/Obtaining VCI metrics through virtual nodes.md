---
title: "Obtaining VCI metrics through virtual nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Getting-VCI-metrics-through-virtual-nodes"
---

This topic describes how to use virtual nodes to obtain performance metrics supported by VCI (such as CPU, memory, and network throughput metrics).

<span id=".5oyH5qCH6K-05piO"></span>
## Metrics

VCI performance metrics (such as CPU, memory, and network throughput metrics) are provided based on BytePlus VMP. For more information about metrics, see [Basic VKE metrics](https://docs.byteplus.com/en/docs/vmp/API_server_metrics) and [Common cAdvisor metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-cAdvisor).

<span id=".5oyH5qCH6I635Y-W5pa55byP"></span>
## Metric querying

You can query VCI metrics by using the following command:

```bash
kubectl --kubeconfig=<kubeconfig_path> get --raw "/api/v1/nodes/<virtualnode_name>/proxy<endpoint>"
```


The variable descriptions are as follows:


* `<kubeconfig_path>`: The address of the KubeConfig file for the cluster where the VCI is located, for example, `.kube/config`.

* `<virtualnode_name>`: The name of the target virtual node to which the VCI is scheduled, for example, `vci-node1-cn-beijing-a`.

* `<endpoint>`: The endpoint corresponding to the metric, for example, `/metrics/resource`. For a list of endpoints, see the **Endpoint** column in the tables below.


A complete command example is as follows:

```bash
kubectl --kubeconfig=.kube/config get --raw "/api/v1/nodes/vci-node1-cn-beijing-a/proxy/metrics/resource"
```


<span id=".5pSv5oyB55qE5oyH5qCH"></span>
## Supported metrics

<span id="cpu"></span>
### CPU


|Metric name |Metric type |Endpoint |Unit |Metric meaning |
|---|---|---|---|---|
|container_cpu_load_average_10s |gauge |/metrics/cadvisor |N/A |Container CPU load average over the last 10 seconds. |
|container_cpu_usage_seconds_total |Counter |/metrics/resource |Seconds |Total CPU time consumed. |


<span id=".5YaF5a2Y"></span>
### Memory


|Metric name |Metric type |Endpoint |Unit |Metric meaning |
|---|---|---|---|---|
|container_memory_working_set_bytes |Gauge |/metrics/resource |Bytes |Physical memory usage of the container. |


<span id=".572R57uc"></span>
### Network


|Metric name |Metric type |Endpoint |Unit |Metric meaning |
|---|---|---|---|---|
|container_network_receive_bytes_total |Counter |/metrics/cadvisor |Bytes |Total data received. |
|container_network_receive_packets_total |Counter |/metrics/cadvisor |Packet |Total number of packets received. |
|container_network_transmit_bytes_total |Counter |/metrics/cadvisor |Bytes |Total amount of data transmitted. |
|container_network_transmit_packets_total |Counter |/metrics/cadvisor |Packet |Total number of packets transmitted. |
|container_network_receive_errors_total |Counter |/metrics/cadvisor |Count |Total number of errors encountered while receiving. |
|container_network_transmit_errors_total |Counter |/metrics/cadvisor |Count |Total number of errors encountered while transmitting. |
|container_network_receive_packets_dropped_total |Counter |/metrics/cadvisor |Packet |Total number of packets dropped while receiving. |
|container_network_transmit_packets_dropped_total |Counter |/metrics/cadvisor |Packet |Total number of packets dropped while transmitting. |


<span id=".5a2Y5YKo5Y23"></span>
### PVs


|Metric name |Metric type |Endpoint |Unit |Metric meaning |
|---|---|---|---|---|
|kubelet_volume_stats_available_bytes |Gauge |/metrics |Bytes |Available capacity in the volume. |
|kubelet_volume_stats_capacity_bytes |Gauge |/metrics |Bytes |Total capacity of the volume. |
|kubelet_volume_stats_inodes |Gauge |/metrics |Count |Maximum number of inodes (index nodes) in the volume. |
|kubelet_volume_stats_inodes_free |Gauge |/metrics |Count |Number of free inodes in the volume. |
|kubelet_volume_stats_inodes_used |Gauge |/metrics |Count |Number of used inodes in the volume. |
|kubelet_volume_stats_used_bytes |Gauge |/metrics |Bytes |Used capacity in the volume. |


<span id=".5a655Zmo57uE"></span>
### Pods


|Metric name |Metric type |Endpoint |Unit |Metric meaning |
|---|---|---|---|---|
|pod_cpu_usage_seconds_total |Counter |/metrics/resource |Seconds |Total CPU time consumed by the pod in seconds. |
|pod_memory_working_set_bytes |Gauge |/metrics/resource |Bytes |Physical memory usage of the pod in bytes. |
