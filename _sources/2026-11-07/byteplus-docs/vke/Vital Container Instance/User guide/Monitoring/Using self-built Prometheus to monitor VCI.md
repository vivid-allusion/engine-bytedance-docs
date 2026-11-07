---
title: "Using self-built Prometheus to monitor VCI"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Monitoring-VCI-instances-using-self-managed-Prometheus"
---

VCI supports monitoring VCIs based on a self\-built Prometheus service. This topic describes the method of configuring metric collection rules for VCI monitoring in a self\-built Prometheus service.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster to which the VCI belongs has installed the vci\-virtual\-kubelet add\-on. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.dmNpLXZpcnR1YWwta3ViZWxldC3nu4Tku7Y=).

* The VCI has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).


<span id=".6YeH6ZuG5Z-656GA5oyH5qCH"></span>
## Collecting basic metrics

VCIs provide performance metrics such as CPU, memory, and network throughput. For a detailed description of the metrics, see [Supported metrics](https://docs.byteplus.com/en/docs/vke/Getting-VCI-metrics-through-virtual-nodes#.5pSv5oyB55qE5oyH5qCH).

<span id=".5pa55rOV5LiA"></span>
### Method 1

If [Prometheus Operator](https://prometheus-operator.dev/) is deployed in the cluster, you can collect basic metrics of VCIs by modifying the Prometheus Operator configuration.

The following example demonstrates how to collect metrics based on service discovery configured by ServiceMonitor:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
  name: kubernetes-cadvisor
spec:
  selector:
    matchLabels:
      k8s-app: kubelet
  namespaceSelector:
    any: true
  endpoints:
  - port: https
    interval: 15s
    path: /metrics/cadvisor
    scheme: https
    tlsConfig:
      caFile: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      insecureSkipVerify: true
    bearerTokenFile: /var/run/secrets/kubernetes.io/serviceaccount/token
    relabelings:
    - sourceLabels: [__meta_kubernetes_node_name]
      regex: '(.+)'
      targetLabel: __metrics_path__
      replacement: /metrics/cadvisor
    - action: labelmap
      regex: '__meta_kubernetes_node_label_(.+)'
```


<span id=".5pa55rOV5LqM"></span>
### Method 2

Self\-built Prometheus obtains instance metrics by accessing virtual\-kubelet. The method of collection configuration is the same as accessing the native Kubernetes kubelet. You can collect basic metrics of VCIs by modifying the configuration file of open\-source Prometheus. The configuration file of open\-source Prometheus is usually located at `/etc/prometheus/prometheus.yml` or in your custom configuration directory.

The following example shows how to configure collection rules for the cAdvisor metric by using the standard configuration file:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  
scrape_configs:
  - job_name: 'kubernetes-cadvisor'
    scheme: https
    tls_config:
      ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      insecure_skip_verify: true
    kubernetes_sd_configs:
    - role: node
    bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
    relabel_configs:
    - source_labels: [__meta_kubernetes_node_name]
      regex: (.+)
      target_label: __metrics_path__
      replacement: /metrics/cadvisor
    - action: labelmap
      regex: __meta_kubernetes_node_label_(.+)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For configuration instructions related to the <code>scrape_configs</code> parameter, see the <a href="https://prometheus.io/docs/prometheus/latest/configuration/configuration/#scrape_config">Official Prometheus documentation</a>.</div>


<span id=".6aqM6K-B57uT5p6c"></span>
### Validating results

You can execute the command shown in the following figure on the self\-built Prometheus to verify the collection results:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e86a5150578dd8365ff5b2bfeb632da.png) </span>

<span id=".6YeH6ZuGLWdwdS3mjIfmoIc="></span>
## Collecting GPU metrics

The GPU Exporter used for VCI GPU monitoring is compatible with the monitoring metrics provided by the open\-source DCGM Exporter. For a detailed description of the metrics, see [Metrics supported by DCGM](https://docs.byteplus.com/en/docs/vke/VCI-GPU-metrics).

<span id=".5pa55rOV5LiA"></span>
### Method 1

If [Prometheus Operator](https://prometheus-operator.dev/) is deployed in the cluster, you can use the ServiceMonitor or PodMonitor of Prometheus Operator to configure service discovery for collection of VCI GPU metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before collecting metrics, you need to explicitly declare the port (<code>1025</code>) exposed by the container in the VCI pod. The following sample code snippet provides an example of declaration:</div>


<div data-tips="true" data-tips-type="tip">```yaml
...
    spec:
      containers:
        ports:
        - containerPort: 1025 # Explicitly declare the container port in the container configuration.
          name: gpu-metrics
```
</div>


The following code provides an example of collection via PodMonitor:

```yaml
apiVersion: monitoring.coreos.com/v1
kind: PodMonitor
metadata:
  name: vci-gpu
spec:
  selector:
    matchLabels:
      app: gpu # Replace the example label with the label of the target VCI pod.
  namespaceSelector:
    any: true
  podMetricsEndpoints:
  - port: gpu-metrics
    interval: 15s
    scheme: http
    relabelings:
    - action: labelmap
      regex: __meta_kubernetes_pod_label_(.+)
```


<span id=".5pa55rOV5LqM"></span>
### Method 2

You can configure self\-built Prometheus to collect GPU metrics by modifying the configuration file of open\-source Prometheus to access port `1025` of the VCI pod. The configuration file of open\-source Prometheus is usually located at `/etc/prometheus/prometheus.yml` or in your custom configuration directory.

The following sample code shows how to configure collection rules:

```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  
scrape_configs:
  - job_name: 'vci-gpu'
    scheme: http
    kubernetes_sd_configs:
    - role: pod
    relabel_configs:
    - source_labels: [__meta_kubernetes_pod_ip]
      regex: (.*)
      target_label: __address__
      replacement: $1:1025
    - action: labelmap
      regex: __meta_kubernetes_pod_label_(.+)
```


<span id=".6aqM6K-B57uT5p6c"></span>
### Validating results

You can execute the command shown in the following figure on the self\-built Prometheus to verify the collection results:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a56ec5f3c7d59a6445a937e9141b3d3.png) </span>
