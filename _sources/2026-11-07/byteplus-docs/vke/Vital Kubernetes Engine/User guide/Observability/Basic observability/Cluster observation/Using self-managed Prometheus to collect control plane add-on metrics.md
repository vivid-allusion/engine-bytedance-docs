---
title: "Using self-managed Prometheus to collect control plane add-on metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_self-managed_Prometheus_to_collect_control_plane_metrics"
---

VKE clusters expose metrics of control plane add\-ons. This helps you use self\-managed Prometheus to collect metrics and build a cluster control plane monitoring dashboard. As a result, the metrics are integrated with your self\-managed monitoring system. This topic describes how to enable metric collection for cluster control plane add\-ons.

<span id="GdABN4El"></span>
## Usage limits


* The Kubernetes version of the cluster must meet the following requirements: If the cluster version is outdated, upgrade it first. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

   * [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.17\-vke.44 and later

   * [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.15\-vke.34 and later

   * [Kubernetes v1.28](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28): v1.28.15\-vke.27 and later

   * [Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30): v1.30.4\-vke.12 and later

   * [Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32): v1.32.3\-vke.7 and later

   * Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE

* You can collect metrics only for the following managed add\-ons: kube\-apiserver, etcd, kube\-scheduler, kube\-controller\-manager, and cloud\-controller\-manager in the cluster control plane. You cannot collect metrics for other managed add\-ons. For related add\-on metrics, see [VKE metrics](https://docs.byteplus.com/en/docs/vmp/Common-metrics-of-Vital-Kubernetes-Engine).


<span id="GdABN4El"></span>
## Prerequisites


* Self\-managed Prometheus can be deployed either inside or outside the cluster to be monitored.

* When a self\-managed Prometheus is deployed outside the cluster to be monitored, make sure that it can access the API server of the VKE cluster and has read permissions on `/metrics`.


<span id="bcIkUwOc"></span>
## Procedure

<span id="K8st5H3X"></span>
### Step 1: Enable metric collection for control plane add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation pane, click **Cluster**. Click the name of the target cluster to enter its management page.

4. In the left navigation pane, click **Operation and maintenance configuration**. In the **Custom metric collection** configuration section, enable **Metric collection from control plane components**.


<span id="h8yvIqf4"></span>
### Step 2: Configure collection rules

Before you use self\-managed Prometheus to collect metrics from cluster control plane add\-ons, you need to configure metric collection jobs for control plane add\-ons in the Prometheus configuration file `prometheus.yaml`. The sample code is as follows:

```YAML
global:
  scrape_interval: 15s # By default, scrape targets every 15 seconds.
  # Attach these labels to any time series or alerts when communicating with
  # external systems (federation, remote storage, Alertmanager).
  external_labels:
    monitor: 'custom-prometheus-monitor'
# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: api-server-demo
     ......
     
  - job_name: etcd-demo
    ......
     
  - job_name: scheduler-demo
    ......
```


<span id="2crd8HuO"></span>
#### Cluster internal monitoring

If your self\-managed Prometheus is deployed inside the cluster to be monitored, you can collect data of control plane add\-ons based on the following sample collection rule code.


<Tabs>
<Tab zoneid="ni3C4pFJ9Q" title="APIServer">
<TabTitle>APIServer</TabTitle>

The collection rule sample code is as follows:

```YAML
- job_name: api-server-demo
  params:
    job: ["apiserver"]
  kubernetes_sd_configs:
  - role: endpoints
  relabel_configs:
  - action: keep
    regex: default;kubernetes;https
    source_labels:
    - __meta_kubernetes_namespace
    - __meta_kubernetes_service_name
    - __meta_kubernetes_endpoint_port_name
  scheme: https
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: false
```



</Tab>
<Tab zoneid="qfm7kPxnR8" title="ETCD">
<TabTitle>ETCD</TabTitle>

The collection rule sample code is as follows:

```YAML
- job_name: etcd-demo
  params:
    job: ["etcd"]
  kubernetes_sd_configs:
  - role: endpoints
  relabel_configs:
  - action: keep
    regex: default;kubernetes;https
    source_labels:
    - __meta_kubernetes_namespace
    - __meta_kubernetes_service_name
    - __meta_kubernetes_endpoint_port_name
  scheme: https
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: false
```



</Tab>
<Tab zoneid="lrojoIZvjk" title="Kube-Scheduler">
<TabTitle>Kube-Scheduler</TabTitle>

The collection rule sample code is as follows:

```YAML
- job_name: kube-scheduler-demo
  params:
    job: ["scheduler"]
  kubernetes_sd_configs:
  - role: endpoints
  relabel_configs:
  - action: keep
    regex: default;kubernetes;https
    source_labels:
    - __meta_kubernetes_namespace
    - __meta_kubernetes_service_name
    - __meta_kubernetes_endpoint_port_name
  scheme: https
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: false
```



</Tab>
<Tab zoneid="Bckl8KyOM4" title="Kube-Controller-Manager">
<TabTitle>Kube-Controller-Manager</TabTitle>

The collection rule sample code is as follows:

```YAML
- job_name: kcm-demo
  params:
    job: ["kcm"]
  kubernetes_sd_configs:
  - role: endpoints
  relabel_configs:
  - action: keep
    regex: default;kubernetes;https
    source_labels:
    - __meta_kubernetes_namespace
    - __meta_kubernetes_service_name
    - __meta_kubernetes_endpoint_port_name
  scheme: https
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: false
```



</Tab>
<Tab zoneid="wTHkok310c" title="Cloud-Controller-Manager">
<TabTitle>Cloud-Controller-Manager</TabTitle>

The collection rule sample code is as follows:

```YAML
- job_name: ccm-demo
  params:
    job: ["ccm"]
  kubernetes_sd_configs:
  - role: endpoints
  relabel_configs:
  - action: keep
    regex: default;kubernetes;https
    source_labels:
    - __meta_kubernetes_namespace
    - __meta_kubernetes_service_name
    - __meta_kubernetes_endpoint_port_name
  scheme: https
  bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
  tls_config:
    ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
    insecure_skip_verify: false
```



</Tab>
</Tabs>


<span id="3FmoDzJx"></span>
#### Cluster external monitoring

If your self\-managed Prometheus is deployed outside the cluster to be monitored, it cannot automatically mount ServiceAccount credentials or access internal Kubernetes services as it would inside the cluster. The configuration method is as follows:


1. Manually specify the API server address of the VKE cluster to connect external Prometheus to the cluster.

2. Manually provide authentication credentials, including a CA certificate and a bearer token, to pass the permission check of the Kubernetes API.

3. Perform node\-based service discovery to automatically obtain the addresses of all nodes in the cluster, and subsequently collect node\-related metrics.


The configuration sample code is as follows:

```YAML
  - job_name: 'external-cluster-monitor-job'
    scheme: https
    tls_config:
      ca_file: /etc/prometheus/kubernetes-ca.crt
    bearer_token: '<ServiceAccount bearer_token>'
    kubernetes_sd_configs:
      - api_server: 'https://<APIServer URL>'
        role: node
        tls_config:
          ca_file: /etc/prometheus/kubernetes-ca.crt
        bearer_token: '<ServiceAccount bearer_token>' 
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more configuration details, see <a href="https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config">Configuration </a>and <a href="https://github.com/prometheus/prometheus/issues/4633">Monitoring kubernetes with prometheus from outside of k8s cluster</a>.</div>


<span id="plBMrIHa"></span>
## Validate the result


1. Log in to the self\-managed Prometheus console and switch to the Graph page.

2. Enter the `up` command to view whether the specified collection task functions as expected.

   The expected result is as follows. Take the API server observability task as an example. `up{instance="xxx.xxx.xxx.xxx:6443", job="api-server-demo"} `indicates the corresponding collection task. When its value is `1`, it indicates the task is running as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8401cbe4abcd9c4a876a4edb635f51d1.png) </span>

3. Enter the following metrics to check whether the data can be displayed as expected.

   ```YAML
   apiserver_request_total{job="api-server-demo"}
   ```
   

   The expected result is similar to the following one. If metrics and data can be queried as expected, the self\-managed Prometheus can collect metrics of the core components from the cluster.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cbce67a312d9775979c040104b59feb2.png) </span>
