---
title: "Autoscaling based on custom metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling"
---

This article describes how to create a Horizontal Pod Autoscaler (HPA) by specifying custom metrics in a YAML configuration file.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5Z-65pys5qaC5b-1"></span>
### Basic knowledge

By default, a Horizontal Pod Autoscaler (HPA) supports automatic scaling only based on CPU and memory usage. It cannot meet scaling requirements in complex scenarios. By enabling cloud native observability access in the cluster, you can monitor, collect, and query various metrics for add\-ons within the cluster. By using the prometheus\-adapter add\-on, you can leverage these metrics to implement workload autoscaling, allowing workloads to scale more effectively on demand while ensuring stability and balancing costs.

Scaling on custom metrics involves three major steps:


1. Enable cloud native observability in the Vital Kubernetes Engine (VKE) cluster to collect and expose metrics. You can collect metrics as needed. For details, see [Basic observability](https://docs.byteplus.com/en/docs/vke/Basic-observability).

2. Establish mappings between original metrics and custom metrics by using prometheus\-adapter.

3. Configure an HPA on custom metrics to enable workload autoscaling.


<span id=".5oyH5qCH5pig5bCE"></span>
### Metric mapping

By default, the HPA component in a cluster cannot recognize the raw metrics collected by VMP. Therefore, you need to use the prometheus\-adapter add\-on to convert the raw metrics collected by VMP into custom metrics that the HPA component can recognize and use.

After the prometheus\-adapter add\-on is installed, a new configuration item named `prometheus-adapter-config` will be added to the `kube-system` namespace of the cluster. This configuration item is used to record the mapping relationships of preset metrics. The following content is an example of the configuration item:

```YAML
rules:
  - seriesQuery: 'container_network_receive_bytes_total'
    resources:
      overrides:
        namespace: {resource: "namespace"}
        pod: {resource: "pod"}
    name: {as: 'k8s_pod_network_receive_throughput'}
    metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>,cluster="ccmketollk1b***",pod!=""}[1m])) by (<<.GroupBy>>) / 125000.0'
```


The following table describes parameters in the above mapping configuration.


|Parameter |Description |
|---|---|
|`seriesQuery` |The original metrics in VMP. You can add labels to these metrics, as in `container_network_receive_bytes_total{cluster="ccm5pq1j5i7***"}`. |
|`resources.overrides` |Maps a Kubernetes\-native resource to a label of the metric in VMP, where:<br><br><br>* The label key is the label for the VMP metric.<br><br>* The label value is the Kubernetes\-native resource that needs to be mapped, such as `pod`, `namespace`, and `node`. When an HPA uses a custom metric, it automatically uses the native resource name of the metric as a label for the VMP metric.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can use the <code>kubectl api-resources -o wide</code> command to view the native resources of the cluster.</div><br> |
|`name` |The custom metric name, for example, `k8s_pod_network_receive_throughput`. This custom metric can be used by an HPA. |
|`metricsQuery` |The aggregation statement for VMP metrics.   <br><br><br>* `<<.Series>>` will be populated with the original metric specified in `seriesQuery`. In this example, it is `container_network_receive_bytes_total`.<br><br>* `<<.LabelMatchers>>` will be populated with two labels in key\-value pairs for the metric to be queried: `namespace` and `pod`.<br><br>* `<<.GroupBy>>` will be set to `pod`, meaning that aggregation will be performed on the `pod` dimension. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To prevent prometheus\-adapter from querying an excessive number of metrics, we recommend that you configure label filters for <code>seriesQuery</code> and <code>metricsQuery</code>. Additionally, since a VMP workspace can connect to multiple clusters, make sure that you add cluster labels when configuring labels for query.</div>


After configuring custom metrics, you can view the custom metrics by using the `kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta2/" | jq .` command.

```YAML
{
  "kind": "APIResourceList",
  "apiVersion": "v1",
  "groupVersion": "custom.metrics.k8s.io/v1beta2",
  "resources": [
    {
      "name": "pods/k8s_pod_network_receive_throughput",
      "singularName": "",
      "namespaced": true,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    },
    {
      "name": "namespaces/k8s_pod_network_receive_throughput",
      "singularName": "",
      "namespaced": false,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    }
  ]
}
```


You can use `kubectl get --raw "/apis/custom.metrics.k8s.io/v1beta2/namespaces/kube-system/pods/*/k8s_pod_network_receive_throughput" | jq .` to query the inbound bandwidth metric for all pods in the `kube-system` namespace.

```YAML
{
  "kind": "MetricValueList",
  "apiVersion": "custom.metrics.k8s.io/v1beta2",
  "metadata": {},
  "items": [
    {
      "describedObject": {
        "kind": "Pod",
        "namespace": "kube-system",
        "name": "coredns-59f55659db-s94hm",
        "apiVersion": "/v1"
      },
      "metric": {
        "name": "k8s_pod_network_receive_throughput",
        "selector": null
      },
      "timestamp": "2024-04-12T10:13:04Z",
      "value": "1m"
    },
    {
      "describedObject": {
        "kind": "Pod",
        "namespace": "kube-system",
        "name": "metrics-server-6c487585c5-fl792",
        "apiVersion": "/v1"
      },
      "metric": {
        "name": "k8s_pod_network_receive_throughput",
        "selector": null
      },
      "timestamp": "2024-04-12T10:13:04Z",
      "value": "18m"
    }
    // ...
  ]
}
```


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud\-native observability has been enabled. For details, see [Enabling cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The prometheus\-adapter add\-on has been installed. For details, see [prometheus-adapter](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.cHJvbWV0aGV1cy1hZGFwdGVyLee7hOS7tg==).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Upgrade the prometheus\-adapter add\-on to version v1.1.0 or later. If you are using an earlier version, when you install the prometheus\-adapter add\-on, specify the same VMP workspace as the one that is bound to the cluster. Otherwise, the prometheus\-adapter add\-on will not be able to convert data properly.   </div>
   

* (Optional) The target cluster has been connected by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="8nO6Y38A"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66Ieq5a6a5LmJ5oyH5qCH5bm26YWN572u5pig5bCE"></span>
### Step 1: create custom metrics and configure mappings


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation bar, click **Configurations** \> **ConfigMap**. Select `kube-system` from the namespace drop\-down list. In the namespace, find the `prometheus-adapter-config` item, and in the **Actions** column, click **Edit Yaml** to add the mappings for custom metrics. This example demonstrates how to create a custom metric named `k8s_pod_network_receive_throughput` from the `container_network_receive_bytes_total metric`.

   ```YAML
   rules:
     - seriesQuery: 'container_network_receive_bytes_total'
       resources:
         overrides:
           namespace: {resource: "namespace"}
           pod: {resource: "pod"}
       name: {as: 'k8s_pod_network_receive_throughput'}
       metricsQuery: 'sum(rate(<<.Series>>{<<.LabelMatchers>>,cluster="ccmketollk1b***",pod!=""}[1m])) by (<<.GroupBy>>) / 125000.0'
   ```
   

5. Click **Confirm**.


<span id=".5q2l6aqk5LqM77ya5L2_55So6Ieq5a6a5LmJ5oyH5qCH6YWN572uLWhwYQ=="></span>
### Step 2: configure an HPA using the custom metric


1. Create a workload. This example demonstrates how to create a Deployment.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: workload-demo
     namespace: default
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: workload-demo
     template:
       metadata:
         labels:
           app: workload-demo
       spec:
         containers:
         - name: nginx
           image: nginx:1.14.2
           ports:
           - containerPort: 80
   ```
   

2. Create an HPA associated with the workload to specify autoscaling based on custom metrics.   

   * `metrics.type` is set to `Pods`.

   * `metrics.pods.metric.name` is the custom metric name configured above (`k8s_pod_network_receive_throughput`).

   * `metrics.pods.target.type` is set to `AverageValue`.

   * `metrics.pods.target.averageValue` is the threshold for triggering the scaling action.

   ```YAML
   apiVersion: autoscaling/v2
   kind: HorizontalPodAutoscaler
   metadata:
     name: hpa-demo
   spec:
     scaleTargetRef:
       apiVersion: apps/v1
       kind: Deployment
       name: workload-demo
     minReplicas: 1
     maxReplicas: 10
     metrics:
     - type: Pods
       pods:
         metric:
           name: k8s_pod_network_receive_throughput  # Specify a name for the metric
         target:
           type: AverageValue # The target value of the AverageValue type. For Pod metric types, only the target value of the AverageValue type is supported.
           averageValue: 20  # Configure the HPA trigger threshold
   ```
   


<span id=".57uT5p6c6aqM6K-B"></span>
## Verifying results


1. When the custom metric of pods reaches the threshold, a scale\-out is triggered. You can view HPA information by using the following command:

   ```Bash
   kubectl get hpa   
   ```
   

   The expected outcome is an increase in the Deployment replicas to 2, as demonstrated below:

   ```Bash
   NAME      REFERENCE                   TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
   hpa-demo  Deployment/workload-demo    23/20m    1         10        2          62s   
   ```
   

2. When the custom metric drops below the threshold, a scale\-in is triggered. You can view HPA information by using the following command:

   ```Bash
   kubectl get hpa   
   ```
   

   The expected outcome is a decrease in the Deployment replicas to 1, as demonstrated below:

   ```Bash
   NAME       REFERENCE                  TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
   hpa-demo   Deployment/workload-demo   0/20m     1         10        1          20m
   ```
