---
title: "HPA best practices"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Container_horizontal_scaling_best_practices"
---

Horizontal Pod Autoscaler (HPA) resources are the primary method for dynamically scaling workloads. This topic provides HPA best practices that you can follow to improve HPA stability and ensure long\-term workload stability.

<span id=".5oyH5qCH6YCJ5oup5LiO6YWN572u"></span>
## Metric selection and configuration

To ensure that workloads can scale dynamically as needed, you must select suitable metrics and configure reasonable scaling thresholds.

<span id=".6YCJ5oup5ZCI6YCC55qE5oyH5qCH"></span>
### Selecting suitable metrics

In the VKE console, you can configure commonly used HPA metrics such as CPU, memory, network, and GPU. These metrics can satisfy most use cases. For details, see the following topics:


* [Achieving autoscaling by using CPU and memory metrics](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler)

* [Achieving autoscaling by using GPU and network metrics](https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling)


For specific scenarios, the timeliness and accuracy of scaling can also be improved by using [custom metric scaling](https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling).   


* For Java\-based business containers, since they rely on virtual machines, consider using `container_memory_rss` for memory metrics instead of the default `container_memory_working_set_bytes`.

* For GPU\-based business containers, prioritize the use of the GPU metric `DCGM_FI_PROF_SM_ACTIVE`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For common metrics in VKE, see <a href="https://docs.byteplus.com/en/docs/vmp/Metrics-Reference">Metric references</a>.</div>


<span id=".6YWN572u5ZCI55CG55qE5Ly457yp6ZiI5YC8"></span>
### Configuring reasonable scaling thresholds

When cloud\-native observability is enabled for the cluster, you can use PromQL to query workload resource usage and evaluate the metric thresholds configured for the HPA.

For example, the CPU metric can be used in two ways to query and observe pod resource usage:


* **Average value**: Aggregate the total resource usage of the workloads and calculate the average usage per pod. PromQL example: `avg(rate(container_cpu_usage_seconds_total{cluster="cxxx",namespace="xxx",pod=~"xxx-.*",pod!="",container!=""}[1m]))`

* **Maximum value**: Aggregate the resource usage of each pod under the workload separately and select the maximum value. PromQL example: `max(sum(rate(container_cpu_usage_seconds_total{cluster="cxxx",namespace="xxx",pod=~"xxx-.*",pod!="",container!=""}[1m])) by (pod))`


For non\-core workloads, considering the balance of resource costs, use the maximum value of pod resource usage to evaluate HPA scaling thresholds. For core workloads, prioritize stability by using the average value of pod resource usage to evaluate HPA scaling thresholds.

<span id=".6K6-572u6ZiI5YC85pe26ICD6JmR5a655beu"></span>
### Considering tolerance when setting thresholds

To avoid frequent scaling due to fluctuations in workload metrics, an HPA uses tolerance to limit scaling behavior.

HPA tolerance is defined by control plane parameters, with a default value of 10% (that is, 0.1). If the change in workload metrics does not exceed the tolerance relative to the threshold, the HPA will not trigger scaling. For example, if the CPU usage threshold is 80%, the actual scaling actions triggered by HPA are as follows:


* Scale\-out: When CPU usage exceeds `80*(1+0.1)=88`, the workload is scaled out.

* Scale\-in: When CPU usage falls below `80*(1-0.1)=72`, the workload is scaled in.


<span id=".6YWN572u5aSa5Liq5oyH5qCH"></span>
### Configuring multiple metrics

An HPA supports multiple metrics. As long as at least one metric can be collected normally, the HPA can scale the workload normally. This design improves scaling stability.

If an HPA uses multiple metrics simultaneously, the expected number of replicas is calculated independently for each metric. The HPA uses the maximum expected replica count to scale the workload, ensuring timely scaling.

<span id=".5Ly457yp6KGM5Li6566h5o6n"></span>
## Scaling behavior control

An HPA achieves autoscaling by modifying the expected number of replicas for the workload. You can configure scaling rules for an HPA to enable fine\-grained control over scaling behavior.

For details on how to configure and use scaling rules, see [Configuring metric scaling in the console](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler#.6YCa6L-H5o6n5Yi25Y-w6YWN572u).

<span id=".5pi-5byP6YWN572u6buY6K6k5Ly457yp6KeE5YiZ"></span>
### Explicitly configuring default scaling rules

If an HPA does not have explicitly configured scaling rules, it will use the default scaling rules. In this case, scale\-out and scale\-in actions share a silence time, which means that each scaling action is based on the maximum replica count calculated from workload metrics in the past 5 minutes. This implies that if the workload experiences a brief abnormal overload and the HPA has computed the desired replica count, the HPA will continuously scale out the workload to a large number of replicas for the next 5 minutes.  Although these scaled\-out replicas will later be automatically reclaimed by the HPA, the scaling process may cause two key issues:


* Rapid scale\-out of workloads within a short period can overload data plane add\-ons or even control plane add\-ons, affecting overall business stability.

* Newly created containers consume extra computing resources for initialization. This further drives up workload scaling metrics, and consequently triggers continuous scale\-out, and amplifies overload impact.


To prevent workloads from scaling out excessively due to abnormal overload, you need to explicitly configure scaling rules for all HPAs. This practice allows independent control of scale\-out and scale\-in actions. For workloads with unclear operational characteristics, you can explicitly configure default scaling rules of HPAs:

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300
    policies:
    - type: Percent
      value: 100
      periodSeconds: 15
  scaleUp:
    stabilizationWindowSeconds: 0
    policies:
    - type: Percent
      value: 100
      periodSeconds: 15
    - type: Pods
      value: 4
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5Ymv5pys5Ly457yp6YCf546H5o6n5Yi2"></span>
### Replica scaling rate control

The expected number of replicas for an HPA is calculated based on metrics, and scaling rules control the rate at which the workload transitions incrementally from its current replica count to the desired count.

<span id=".5b-r6YCf5omp5a65"></span>
#### Fast scale\-out

The workload scales out multiplicatively. For example, when metrics rise, scale\-out is triggered immediately, and the number of replicas changes in a multiplicative sequence as `1, 9, 81, 729, ...`. The corresponding configuration example is as follows:

```yaml
behavior:
  scaleUp:
    stabilizationWindowSeconds: 0
    policies:
    - type: Percent
      value: 900
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5oWi6YCf5omp5a65"></span>
#### Slow scale\-out

The workload scales out additively (by integer increment). For example, if a 300\-second observation period is required before scaling, and the replica count changes in this pattern: `1, 3, 5, 7, ...`, the corresponding configuration example is as follows:

```yaml
behavior:
  scaleUp:
    stabilizationWindowSeconds: 300
    policies:
    - type: Pods
      value: 2
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5YWI5b-r5ZCO5oWi5omp5a65"></span>
#### Fast\-then\-slow scale\-out

The workload first scales out multiplicatively, then scales out additively by integer increments. For example, the number of replicas changes in this sequence pattern: `1, 9, 81, 161, ...`. The corresponding configuration example is as follows:

```yaml
behavior:
  scaleUp:
    stabilizationWindowSeconds: 0
    policies:
    - type: Percent
      value: 900
      periodSeconds: 15
    - type: Pods
      value: 80
      periodSeconds: 15
    selectPolicy: Min
```


<span id=".5b-r6YCf57yp5a65"></span>
#### Fast scale\-in

The workload scales in by percentage. For example, if the current number of replicas is `100`, scale\-in is triggered immediately when metrics drop, and the number of replicas changes in this sequence: `100, 1`. The corresponding configuration example is as follows:

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300
    policies:
    - type: Percent
      value: 100
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5oWi6YCf57yp5a65"></span>
#### Slow scale\-in

The workload scales by integer decrement. For example, the current replica count is `7`, a 300\-second observation period is required, and the replica count changes in this sequence: `7, 5, 3, 1`. The corresponding configuration example is as follows:

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300
    policies:
    - type: Pods
      value: 2
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5YWI5b-r5ZCO5oWi57yp5a65"></span>
#### Fast\-then\-slow scale\-in

The workload first scales in by percentage, then by integer decrement. For example, the current number of replicas is `100`, the number of replicas changes in this sequence: `100, 60, 36, 21, ...`. The corresponding configuration example is as follows:

```yaml
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300
    policies:
    - type: Percent
      value: 40
      periodSeconds: 15
    - type: Pods
      value: 15
      periodSeconds: 15
    selectPolicy: Max
```


<span id=".5YW85a655oCn"></span>
## Compatibility

<span id=".aHBhLeS4ji1rdWJlcm5ldGVzLeeahOWFvOWuueaApw=="></span>
### Compatibility between HPAs and Kubernetes

HPAs primarily use two API versions: `autoscaling/v2beta2` and `autoscaling/v2`. Both versions are compatible. However, `autoscaling/v2beta2` will be deprecated in Kubernetes version 1.26 and later. Therefore, we recommend uniformly using the stable version `autoscaling/v2`.

<span id=".aHBhLeS4ji1ocGEt55qE5YW85a655oCn"></span>
### Compatibility between HPAs

A single workload can have multiple HPAs configured, but this easily leads to unforeseen behaviors or conflicts. Therefore, we recommend configuring only one HPA for a single workload for horizontal scaling.

<span id=".aHBhLeS4ji1jcm9uaHBhLeeahOWFvOWuueaApw=="></span>
### Compatibility between HPAs and CronHPAs

The CronHPA is affected by the HPA of the same workload.


* If HPA is already configured for the workload before you create a CronHPA, the CronHPA indirectly modifies the workload's replica count by adjusting the HPA's replica count. For details, see [Workload scaling principles](https://docs.byteplus.com/en/docs/vke/How-Workload-Autoscaler-works).

* If no HPA is configured for the workload before CronHPA creation, the CronHPA will directly modify the number of replicas of the workload, regardless of whether an HPA is created later.


<span id=".aHBhLeS4ji1paHBhLeeahOWFvOWuueaApw=="></span>
### Compatibility between HPAs and IHPAs

An [Intelligent Horizontal Pod Autoscaler (IHPA)](https://docs.byteplus.com/en/docs/vke/Intelligent_Horizontal_Pod_Autoscaler_overview) supports a DryRun mode. You can configure an IHPA for the workload while the HPA for the workload is working normally. When the IHPA runs stably and meets the workload scaling requirements, switch to the IHPA mode and delete the HPA.

<span id=".aHBhLeS4ji12cGEt55qE5YW85a655oCn"></span>
### Compatibility between HPAs and VPAs

An HPA is used for horizontal scaling of workloads, while a VPA is used for vertical scaling. Since their use cases differ, it is not recommended to configure both an HPA and VPA for the same workload.
