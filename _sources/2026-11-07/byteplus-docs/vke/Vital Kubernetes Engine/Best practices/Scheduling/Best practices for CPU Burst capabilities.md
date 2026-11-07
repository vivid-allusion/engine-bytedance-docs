---
title: "Best practices for CPU Burst capabilities"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Best_practices_for_CPU_Burst_capabilities"
---

This topic describes best practices for CPU Burst capabilities.

<span id="QXL0kaPF"></span>
## Feature overview

In containerized environments, setting CPU limits for containers is a common resource isolation method. When a service experiences sudden traffic spikes, containers may suffer from CPU throttling, leading to degraded service quality, such as increased request latency and reduced throughput.

CPU Burst is an elastic CPU resource capability provided by Katalyst. It dynamically detects the CPU Throttled status of containers and adaptively adjusts their CPU parameters. When sudden load spikes occur, CPU Burst temporarily provides containers with CPU resources beyond their CPU limits, mitigating performance bottlenecks caused by CPU throttling and ensuring the service quality of latency\-sensitive applications. For more feature details, see [Using pod CPU Burst capabilities](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability).

<span id="D5rJsGSJ"></span>
## Application scenario

CPU Burst is mainly suitable for the following three typical scenarios.


<columns>
<columnsItem zoneid="ciiiaKVIdj">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="zHe3m2ME"></span>
## Millisecond\\-level short burst traffic


* **Typical manifestation**: Pod CPU is throttled by CFS Quota, with P99 latency spikes lasting for milliseconds.

* **Recommended policy**: \`cpuBurstOnly\` (enable kernel Burst) or \`auto\` (adaptively enable both cpuBurstOnly and cfsQuotaBurstOnly capabilities).

* **Expected outcome**: Borrow unused CPU quota in kernel space, significantly reducing P99 latency.

* **Applicable services**: Web services, API Gateway, microservices, and other latency\\-sensitive online services.

</card>



</columnsItem>
<columnsItem zoneid="u28nSZI3Ci">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="D3Gj6jAR"></span>
## Sustained high load lasting for seconds to minutes


* **Typical manifestation**: Kernel Burst credits are quickly exhausted, throttling is still triggered, TPS drops, lasting from seconds to minutes.

* **Recommended policy**: \`auto\`.

* **Expected outcome**: CFS Quota is dynamically increased in userspace, with both TPS and P99 improving simultaneously.

* **Applicable services**: Sustained high\\-load services such as Elasticsearch search engine, middleware services, and database proxies.

</card>



</columnsItem>
<columnsItem zoneid="zcxfJRKcZh">


<card mode="container" href="" iconSet="1" iconSize="" icon="" >

<span id="5ewIQGag"></span>
## CPU\\-intensive during application startup


* **Typical manifestation**: CPU demand greatly exceeds the steady\\-state needs during app initialization (e.g., JVM warm\\-up or class loading), leading to excessively long startup times.

* **Recommended policy**: \`cpuBurstOnly\` or \`auto\`.

* **Expected outcome**: Allow containers to temporarily use more CPU resources during startup, accelerating application readiness.

* **Applicable services**: Java applications and AI inference services requiring warm\\-up.

</card>



</columnsItem>
</columns>


<span id="JionSfMH"></span>
## Prerequisites

Before using CPU Burst capabilities, ensure that the following conditions are met:


* The katalyst add\-on of v0.5.13\-vke.14 or later has been deployed in the cluster, and CPU Burst\-related configurations have been enabled. For details, see [Katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).

* The target pod meets the relevant restrictions for using CPU Burst capabilities. For details, see [Using pod CPU Burst capabilities](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability).

* The node or node pool where the target pod resides has been added with the Label: `vke.node.katalyst.deploy=true`. For details, see [Adding labels to nodes](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability?lang=en#jMn0Nk6b).


<span id="UJKHSy55"></span>
## Recommended best configurations for features

<span id="iFDMiBKx"></span>
### Policy selection guide

The katalyst provides four CPU Burst policies. You can select the appropriate policy based on your workload characteristics.


|**Policy** |**CPU Burst** |**CFS Quota burst** |**Application scenario** |
|---|---|---|---|
|none |Disable |Disable |Disable all bursts (default). |
|cpuBurstOnly |Enable |Disable |For millisecond\-level short burst traffic scenarios. |
|cfsQuotaBurstOnly |Disable |Enable |For scenarios where throttling is caused by sustained high loads lasting for seconds to minutes, or where the node kernel does not support CPU Burst. |
|auto (recommended) |Enable |Enable |For scenarios requiring handling of both short bursts and sustained high loads. It delivers the best overall results.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For most online servers, the <code>auto</code> strategy is recommended. This strategy enables protection for both kernel Burst (for millisecond\-level bursts) and CFS Quota bursting (for minute\-level high loads).</div><br> |


<span id="TUuxuW1Q"></span>
### Recommended parameter configurations


|**Parameter** |**Default value** |**Recommended value** |**Description** |
|---|---|---|---|
|cpu_burst_percent |100 |100 |Kernel CPU Burst limit (percentage relative to CPU Limit). |
|cfs_quota_burst_percent |300 |200~300 |The maximum percentage that CFS Quota can be increased. 300 means it can be increased to 3 times the original Quota. |
|cfs_quota_burst_period_seconds |\-1 (indicates unlimited)<br><br> |Set this based on your workload characteristics. |Time limit for a container to continuously consume its maximum CPU quota. Set a positive integer to limit the duration, preventing long\-term resource occupation. |
|sharePoolThresholdPercent |50 |50~70 |Safety threshold for CPU usage of the node shared pool. Exceeding this threshold will forcibly decrease all increased quotas (configurable only at the cluster level). |


<span id="Vn6ikqXk"></span>
## Typical scenario configurations

The following provides complete configuration examples for two typical scenarios. The scenario descriptions, operation steps, and verification steps are included in these examples.


<Tabs>
<Tab zoneid="J070M5xwDU" title="Scenario 1: Online web service">
<TabTitle>Scenario 1: Online web service</TabTitle>

<span id="N3eFZrBj"></span>
### Scenario description

Suitable for most online services, such as Nginx, API gateways, and microservices. This scenario primarily involves short\-duration traffic bursts. After enabling the `auto` policy, good results can be obtained with default settings for the remaining parameters.

<span id="2AlZkOGA"></span>
### Procedure


1. Connect to the target cluster. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. In the pod's `metadata.annotations`, add the `katalysty.kubewharf.io/cpu_enhancement` annotation and enable the `auto` policy for CPU Burst.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: web-service  # Deployment name.
     namespace: default # Deployment namespace.
   spec:
     replicas: 1 # The number of replicas for the Deployment  .
     selector:
       matchLabels:
         app: demo-nginx
     template:
       metadata:
         annotations:
           katalyst.kubewharf.io/cpu_enhancement: '{"cpu_burst_policy":"auto"}'  # Enable CPU Burst and configure auto policy.
         labels:
           app: demo-nginx
       spec:
         containers:
         - name: container-1
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
           resources:
             limits:  # The maximum CPU or memory limit for the container. To enable CPU Burst, the CPU Limit must be configured.
               cpu: "2"
               memory: "2Gi"
             requests: # CPU or memory requests for the container.
               cpu: "1"
               memory: "1Gi"
   ```
   


<span id="aTWxRzkg"></span>
### Validation steps


1. On the node where the pod resides, confirm whether kernel CPU Burst is enabled. For detailed operations, see [Verifying results](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability?lang=en#.5ZyoLXBvZC3lsYLpnaLlvIDlkK8tY3B1LWJ1cnN0LeiDveWKmw==).

2. Use a monitoring platform (e.g., VMP) to observe the CPU Throttled metrics of the pod.

   Currently, VMP provides the `basic metrics container_cpu_cfs_throttled_periods_total` and `container_cpu_cfs_periods_total`, which can be queried directly via [Explore](https://docs.byteplus.com/en/docs/vmp/Explore). You can also implement more pod resource monitoring on your own via the VMP [monitoring dashboard](https://docs.byteplus.com/en/docs/vmp/Dashboards).


</Tab>
<Tab zoneid="MtW6Qex2uv" title="Scenario 2: Sustained high-load services">
<TabTitle>Scenario 2: Sustained high-load services</TabTitle>

<span id="wn0kVrEE"></span>
### Scenario description

Suitable for sustained high\-load scenarios such as Elasticsearch and middleware. We recommend limiting the duration of CFS Quota burst to avoid prolonged high\-load operation. At the same time, you can increase the CPU threshold of the node shared pool reasonably to reserve more elastic headroom for workloads.

<span id="T8bJjYle"></span>
### Procedure


1. Connect to the target cluster. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. (Optional) Adjust the CPU threshold of the node shared pool at the cluster level.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the node has a significant amount of idle resources, you can adjust the CPU threshold of the cluster\-level node shared pool as described below. Otherwise, you can leave the cluster\-level configuration unchanged.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When performing cluster\-level operations as an IAM user, ensure that you have administrator privileges. For details, see <a href="https://docs.byteplus.com/en/docs/vke/RBAC_permissions">RBAC permissions</a>.   </div>
   

   1. Adjust the CPU threshold of the node shared pool to 60%.

      ```YAML
      apiVersion: config.katalyst.kubewharf.io/v1alpha1
      kind: AdminQoSConfiguration
      metadata:
        name: katalyst-config  # This field has a fixed value: the name of the AdminQoSConfiguration object.
        namespace: katalyst-system  # This field has a fixed value: the namespace of the AdminQoSConfiguration object.
        labels:
          vke.node.katalyst.deploy: "true"  # The label related to the fine-grained resource management feature of node pool configuration. Keep the default value, meaning CPU Burst applies to nodes carrying this Label.
      spec:
        config:
          fineGrainedResourceConfig:
            cpuBurstConfig:  # Configure CPU Burst for pods at the cluster level.
              sharePoolThresholdPercent: 60 # Node CPU utilization safety threshold when CFS Quota burst is enabled.
      ```
      

   2. Create the corresponding katalystCustomConfig object to make the cluster\-level configuration take effect.

      ```YAML
      apiVersion: config.katalyst.kubewharf.io/v1alpha1
      kind: katalystCustomConfig
      metadata:
        name: katalyst-config # This field has a fixed value: the name of the KatalystCustomConfig object.
        namespace: katalyst-system  # This field has a fixed value: the namespace of the KatalystCustomConfig object.
        labels:
          vke.node.katalyst.deploy: "true"  # This field has a fixed value. The label related to the fine-grained resource management feature of node pool configuration.
      spec:
        targetType:  # This field has a fixed value. It describes the GVR information of the AdminQosConfiguration.
          group: config.katalyst.kubewharf.io
          resource: adminqosconfigurations
          version: v1alpha1
      ```
      

3. Perform pod\-level configuration by enabling the `auto` policy in the pod of your business application, and set a duration limit.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: elasticsearch  # Deployment name.
     namespace: default  # Deployment namespace.
     labels:
       run: elasticsearch
   spec:
     replicas: 1 # The number of replicas for the Deployment.
     selector:
       matchLabels:
         run: elasticsearch
     strategy: {}
     template:
       metadata:
         annotations:
           katalyst.kubewharf.io/cpu_enhancement: '{"cpu_burst_policy":"auto",cfs_quota_burst_period_seconds":"600"}' # Enable CPU Burst, configure the auto strategy, and set a duration limit.
         labels:
           run: elasticsearch
       spec:
         containers:
           image: doc-cn-beijing.cr.volces.com/vke/elasticsearch:8.19.12  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
           name: elasticsearch
           resources:
             limits:  # The maximum CPU or memory limit for the container. To enable CPU Burst, the CPU Limit must be configured.
               cpu: "4"
               memory: 10Gi
             requests:  # CPU or memory requests for the container.
               cpu: "4"
               memory: 10Gi
   ```
   


<span id="QYVoCfsy"></span>
### Validation steps


1. On the node where the pod resides, confirm whether kernel CPU Burst and CFS quota are enabled. For detailed operations, see [Verifying results](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability?lang=en#.5ZyoLXBvZC3lsYLpnaLlvIDlkK8tY3B1LWJ1cnN0LeiDveWKmw==).

2. Use a monitoring platform (e.g., VMP) to observe the CPU Throttled metrics of the pod.

   Currently, VMP provides the basic metrics `container_cpu_cfs_throttled_periods_total` and `container_cpu_cfs_periods_total`, which can be queried directly via [Explore](https://docs.byteplus.com/en/docs/vmp/Explore). You can also implement more pod resource monitoring on your own via the VMP [monitoring dashboard](https://docs.byteplus.com/en/docs/vmp/Dashboards).


</Tab>
</Tabs>


<span id="j8TgaOwZ"></span>
## FAQ


<span id="2452MZbR"></span>
## What should I do if enabling CPU Burst does not yield obvious results?


* Ensure that the pod has a CPU limit configured. You cannot enable CPU Burst capabilities for Pods without a CPU limit.

* Ensure that the pod is not in a system namespace. For the details about the namespace name, see [Using Pod CPU Burst capabilities](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability).

* Check whether the node kernel version meets the requirements.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Kernel Burst is only supported on the following node <a href="https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images">OS image</a>:   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Public veLinux images with kernel version 5.4, 5.10, or 5.15   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Public Ubuntu images with kernel version 5.15   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Custom images created based on the preceding public images built on two kernel versions   </div>
   



<span id="e4O73UVX"></span>
## How to choose among cpuBurstOnly, cfsQuotaBurstOnly, and auto?


* If traffic is mostly low but occasionally experiences millisecond\-level bursts: select `cpuBurstOnly`.

* If the service has sustained high\-load traffic lasting seconds or even minutes, or has an irregular traffic pattern: select `auto`.

* If the node kernel version does not support the CPU Burst feature: select `cfsQuotaBurstOnly`.



<span id="DZ8Ad0QM"></span>
## What is the appropriate value for sharePoolThresholdPercent?

The default value of 50% is suitable for most scenarios. If the node has a significant amount of idle resources and the application is not latency\-sensitive, you can reasonably increase it to 60%–70% to allow more room for bursting.



<span id="3fZrutcf"></span>
## How to configure cfs_quota_burst_period_seconds?


* The default value `-1` indicates no duration limit, suitable for scenarios where the duration of high\-load traffic is uncertain, or the service cannot tolerate any CPU throttling.

* Setting it to a positive integer imposes a duration limit, suitable for scenarios where the duration of high\-load traffic is relatively predictable and short\-term CPU throttling is tolerable.
