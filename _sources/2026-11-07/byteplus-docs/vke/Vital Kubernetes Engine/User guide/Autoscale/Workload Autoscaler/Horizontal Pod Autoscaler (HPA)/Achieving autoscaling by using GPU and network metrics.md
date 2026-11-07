---
title: "Achieving autoscaling by using GPU and network metrics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling"
---

In addition to the built\-in CPU and memory metrics supported by Kubernetes, Vital Kubernetes Engine(VKE) also provides pre\-configured rules for GPU and network metrics. This allows autoscaling to be triggered based on GPU usage or network traffic of containers. This topic describes how to configure an autoscaler based on the GPU or network metric.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5Z-65pys5qaC5b-1"></span>
### Description

By default, a Horizontal Pod Autoscaler (HPA) supports automatic scaling only based on CPU and memory usage. It cannot meet scaling requirements in complex scenarios. For example, production environments often expect scaling based on GPU usage or network traffic of pods.

VKE provides the prometheus\-adapter add\-on to address this issue. It exposes native Prometheus metrics in the Custom Metrics API format and comes pre\-configured with conversion rules for GPU and network metrics. After you enable [cloud native observability](https://docs.byteplus.com/en/docs/vke/Monitoring-overview) for a cluster, you can configure automatic workload scaling for greater stability and cost\-efficiency based on collected GPU and network metric data. 

Autoscaling based on GPU usage and network involves the following major steps:


1. Install the prometheus\-adapter add\-on in the cluster.

2. Enable cloud native observability in the cluster and collect relevant metrics. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and [Basic observability](https://docs.byteplus.com/en/docs/vke/Monitoring-overview).

3. Configure an HPA to implement workload autoscaling based on GPU usage or network traffic.


<span id=".5oyH5qCH6K-05piO"></span>
### Metrics

VKE supports autoscaling based on GPU and network metrics of workloads. The following table describes the preset metrics.


|Metric description |Metric name |Unit |
|---|---|---|
|GPU usage |`k8s_pod_rate_gpu_used` |% |
|GPU memory usage |`k8s_pod_rate_gpu_memory_used` |% |
|GPU memory used |`k8s_pod_gpu_memory_used` |MiB |
|Network receive throughput |`k8s_pod_network_receive_throughput` |% |
|Network transmit throughput |`k8s_pod_network_transmit_throughput` |% |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the <code>kube-system</code> namespace, you can check <code>prometheus-adapter-config</code> to verify preset metric names and the corresponding Prometheus metrics.</div>


* <div data-tips="true" data-tips-type="tip">In addition to the preset GPU and network metrics, you can also configure autoscaling based on custom metrics. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling">Achieving autoscaling based on custom metrics</a>.</div>



<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* If multiple metrics are specified in an HPA, the calculation is done for each metric, and then the largest of the desired replica counts is chosen.

* An HPA applies only to Deployments, Statefulsets and CustomResourceDefinitions (CRDs).

* HPAs for GPU\-based autoscaling support only GPU pods, not mGPU pods.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Cloud native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* The target cluster has been connected by using kubectl. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* The nvidia\-device\-plugin add\-on has been installed with the **Install dcgm\-exporter** option selected for **Deploy addons**. For details, see [nvidia-device-plugin](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.bnZpZGlhLWRldmljZS1wbHVnaW4t57uE5Lu2).

* The prometheus\-agent add\-on has been installed with the **Install node\-exporter** option selected for **Deploy addons**. For details, see [prometheus-agent](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.cHJvbWV0aGV1cy1hZ2VudC3nu4Tku7Y=).

* The prometheus\-adapter add\-on has been installed. For details, see [prometheus-adapter](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.cHJvbWV0aGV1cy1hZGFwdGVyLee7hOS7tg==).


<span id=".6YCa6L-H5o6n5Yi25Y-w6YWN572u"></span>
## Creating through the console


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the target cluster.

4. In the left navigation bar on the cluster management page, click **Autoscaling** \> **HPA**. On the page that appears, click **Create HorizontalPodAutoscaler** and configure parameters as needed.

   * **Basic information**

      
      |**Parameters** |**Description** |
      |---|---|
      |Name |Enter a name that complies with the displayed naming rules. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the autoscaler belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Label |Add Kubernetes labels to specify identifying attributes of the autoscaler. Click **Add new** and then enter a key\-value pair that complies with the on\-screen requirements. |
      |Annotation |Create Kubernetes annotations to attach non\-identifying metadata to this autoscaler for efficient metadata retrieval. Annotations can contain characters that are not permitted in labels. Click **Add annotation** and then enter a key\-value pair that complies with the on\-screen requirements. |
      

   * **Scaling policy**

      
      |**Parameters** |**Description** |
      |---|---|
      |Scaling object |Specify the object for autoscaling. You can specify a **Deployment**, **StatefulSet**, or **Custom resource** object. After specifying the type of the object for autoscaling, select a specific object from the drop\-down list. |
      |Monitoring metrics |Configure the metrics based on which scaling is performed. The GPU and network metrics supported in VKE include:<br><br><br>* **GPU usage** \- the `average GPU usage of all pod replicas for the workload`. When the GPU usage reaches this specified value, scaling is triggered.<br><br>* **GPU memory usage** \- the percentage of `the total usage of GPU video memory shared by all pods to the total GPU video memory requests shared by all pods`. When the GPU video memory usage reaches this specified value, scaling is triggered.<br><br>* **GPU memory** \- `the shared GPU video memory used by all pods`. When the GPU video memory size reaches this specified value, scaling is triggered.<br><br>* **Network receive throughput** \- `the sum of inbound bandwidth for all containers in all pods for the workload`. When the network receive throughput reaches this specified value, scaling is triggered.<br><br>* **Network transmit throughput** \- `the sum of outbound bandwidth for all containers in all pods for the workload`. When the network transmit throughput reaches this specified value, scaling is triggered.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">An HPA configuration cannot contain  duplicate scaling metrics in the same category.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, a maximum of two metrics can be included.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For information about how to configure autoscaling based on CPU and memory usage, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler">Creating HPA</a>.</div><br> |
      |Minimum number of instances |Configure the minimum and maximum replica counts for scaling. When the policy is triggered, workload instances will scale within this range. |
      |Maximum number of instances ||
      

   * **Scaling rule**

      
      |Parameter |Description |
      |---|---|
      |Scaling policy |Select **Scale\-out policy** and **Scale\-in policy** to configure the workload scale\-in and scale\-out behavior. |
      |Silence time |Specify the cooldown period for the scale\-out or scale\-in policy. The value is an integer in seconds.<br><br>After the system completes scaling, the scaling policy will not be executed again during the quiet time. This prevents frequent changes in the number of workload replicas that lead to system instability. |
      |Policy type |Specify the policy type. Valid values:<br><br><br>* **Maximum value**: executes the policy that has the most impact on pod count.<br><br>* **Minimum value**: executes the policy that has the least impact on pod count.<br><br>* **Disable**: disables the scale\-out policy or scale\-in policy. |
      |Policy |Configure the scaling policy content, including the following items:<br><br><br>* **Type**: specifies the type of scaling policy behavior.<br><br>   * **Pod**: performs scaling based on the number of pods.<br><br>   * **Percentage**: performs scaling based on the percentage of pods.<br><br>* **Threshold**: specifies the threshold for scaling. This parameter needs to be used together with **Type**. For example, if you set the **Type** parameter to **Pod** and set the threshold to 10, it indicates that 10 replicas will be scaled out or scaled in within the time interval.<br><br>* **Time interval**: Specify the interval at which scaling is performed. The value is an integer. Valid values: 1 to 1800. Unit: seconds. |
      

5. Click **Confirm**.


<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM6YWN572u"></span>
## Use kubectl

Use the following code example to create an HPA associated with the object for autoscaling based on GPU utilization.

```YAML
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: gpu-hpa  # The HPA name.
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment # The type of the object for autoscaling. Supported types include Deployment, StatefulSet, and CustomResourceDefinition.
    name: deployment-demo # The object instance for autoscaling.
  minReplicas: 1 # The minimum number of replicas.
  maxReplicas: 10 # The maximum number of replicas.
  metrics:
  - type: Pods
    pods:
      metric:
        name: k8s_pod_rate_gpu_used  # The metric that triggers the HPA. In this example, it is pod GPU utilization.
      target:
        averageValue: 20  # When GPU utilization exceeds 20%, a scale-out is triggered.
        type: AverageValue
```


<span id="KIx6dSDa"></span>
## Validating results

<span id="pt3Q9xea"></span>
### Viewing configuration

In the left navigation bar, click **Autoscaling** \> **HPA** to view the configured HPA.

<span id="iM48oj2h"></span>
### Validating scaling results


1. When pod GPU usage increases, a scale\-out will be triggered. You can view HPA information by using the following command:

   ```Bash
   kubectl get hpa
   ```
   

   The expected outcome is an increase in the Deployment replicas to 2, as demonstrated below:

   ```Bash
   NAME      REFERENCE                         TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
   gpu-hpa   Deployment/example-gpu-workload   23/20      1         10        2          62s   
   ```
   

2. When the GPU usage of pods drops below the specified value, a scale\-in is triggered. You can use the following command to view HPA information:

   ```Bash
   kubectl get hpa
   ```
   

   The expected outcome is a decrease in the Deployment replicas to 1, as demonstrated below:

   ```Bash
   NAME      REFERENCE                         TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
   gpu-hpa   Deployment/example-gpu-workload   0/20      1         10        1          15m
   ```
   


<span id=".5Y-C6ICD5L-h5oGv"></span>
## References

Different versions of HPA resources provide varied levels of granular control over scaling behavior. For details, see [Kubernetes documentation](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/).

When you configure workload autoscaling to meet your business requirements, consider the Kubernetes version that you are using.
