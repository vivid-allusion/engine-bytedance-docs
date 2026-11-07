---
title: "Amplifying nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Amplifying_nodes"
---

VKE provides the node amplification feature to virtually inflate the allocatable resources of nodes by using the Katalyst framework. It increases node deployment density without modifying workload declarations. This topic describes how to enable and use the node amplification feature for a cluster.

<span id="ZmWUpF5u"></span>
## Feature introduction

Node amplification virtually inflates the capacity and allocatable resources of a node. It makes the scheduler perceive a larger available capacity and schedules more Pods onto the node. This fully uses idle physical resources and achieves Pod‑density improvement with zero intrusion on the Pods.

This capability is implemented through three independent policy groups: the amplification policy, scheduling watermark, and pressure eviction. Each is managed by its own CRD. You can combine them as needed:


|**CRD** |**Responsibility** |**Configuration content** |
|---|---|---|
|NodeOvercommitConfig (NOC) |Amplification policy |Select node pools, set amplification ratios (static/dynamic), and set load watermarks. |
|NodeSchedulingConfig |Scheduling watermark |Configure the load‑aware scheduling threshold (stop line) per node pool. |
|AdminQoSConfiguration (AQC) |Pressure eviction |Tiered pressure eviction: Label‑based fine‑grained eviction and system‑pressure QoS‑aware fallback eviction. |


<span id="FexnI04z"></span>
## Prerequisites


* The katalyst add\-on has been installed in the target cluster, and the **node amplification** feature is enabled on the Addon parameter configuration page. For details, see [katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).

* Dynamic amplification and prediction rely on VMP to provide historical metric queries. Dynamic prediction estimates load based on the use\-defined amplification ratio. Cloud\-native observability has been enabled in VKE. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability). For the names of related core metrics, see the [Appendix](https://docs.byteplus.com/en/docs/vke/Amplifying_nodes#bOMJcfTK) section of this topic.


<span id="VZD7Rcb7"></span>
## Considerations

Before you enable the node amplification feature, confirm the following limitations to prevent business interruption or resource contention.


|**Limitation item** |**Description** |
|---|---|
|Mutual exclusivity with Cluster Autoscaler (CA) |You cannot enable both **node amplification** and **autoscaling** for the same node pool. Amplified allocatable resources may mislead CA about actual node capacity. This will cause incorrect scale\-in decisions or delayed scale‑up. Amplified node pools and CA node pools must be separated. |
|Hard upper limit on amplification ratio |Default limits: CPU ≤ 3.0 and Memory ≤ 2.0. Any configuration exceeding these limits will be rejected by the system and will not take effect. We recommended setting the initial value of CPU to 1.5 to 2.0 and memory to 1.2 to 1.5. Then, gradually increase the value after observation. |
|GPU resource amplification not supported |Only CPU and memory can be amplified. GPU, NPU, and other accelerator resources cannot be amplified. |
|Nodes with cpuManagerPolicy: static (exclusive‑core nodes) |On nodes with `cpuManagerPolicy: static` enabled, only the shared CPU pool is amplified. CPU and memory resources of exclusive‑core Pods are excluded from amplification calculation. |
|Kubelet restart risk |When katalyst is uninstalled or the amplification ratio is lowered, scheduled Pods are unaffected. However, if kubelet restarts, Pod eviction may occur because the sum of Pod requests may exceed the current node capacity. |
|One NOC per node pool |When multiple NOCs match the same node pool, only the most recently created NOC takes effect. |


<span id="ALtHoHBk"></span>
## Procedure

<span id="IMzSkIlC"></span>
### Step 1: Add an amplification label to the target node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the left navigation bar, select **Cluster**, and click the name of the target cluster.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. On the **Node pool** page, find the target node pool and click **Edit** in the **Actions** column.

5. On the **Edit node pool** page, configure two **node labels** and select **Enable auto renew for node labels and taints** in the **Advanced configurations** section in the **Node pool configuration** step.

   * Label 1:

      * Label key: `katalyst.kubewharf.io/overcommit_node_pool`

      * Label value: the node pool identifier, such as the node pool name or ID. You can specify a custom value.

   * Label 2:

      * Label key: `vke.node.katalyst.deploy`

      * Label value: `true`

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc8a4d5059a9eb7d3b6cd22e042f78e8.png) </span>


<span id="5VJkqwRE"></span>
### Step 2: Issue an NOC to set the amplification ratio


1. Connect to the cluster through kubectl. For details, see [Connecting to a cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Define an amplification policy for the node pool by issuing an NOC. The following YAML file `nodeovercommit-test.yaml` of NOC functions as an example.

   ```YAML
   apiVersion: overcommit.katalyst.kubewharf.io/v1alpha1
   kind: NodeOvercommitConfig
   metadata:
     name: nodeovercommit-test # The custom amplification policy name.
     labels:
       vke.node.katalyst.deploy: "true" # This field has a fixed value.
   spec:
     nodeOvercommitSelectorVal: "test-pool"  # The name of the node pool. It matches the value of katalyst.kubewharf.io/overcommit_node_pool on the node.
     resourceOvercommitRatio:  # The amplification factor settings.
       cpu: "2"
       memory: "1.5"
     #
     overcommitStrategyType: dynamic # Whether to dynamically adjust the amplification ratio. Valid values: dynamic (adjusts based on real-time and historical load to compute a recommended value) and static (uses the fixed amplification ratio configured above). To dynamically adjust the ratio, targetLoadThreshold must be set. The final effective amplification ratio is min(dynamic, static).
     targetLoadThreshold:  # The target load watermark for amplified nodes. When dynamic adjustment is enabled, idle resources are amplified based on this watermark to make the actual load on the node closer to the target.
       cpu: 80
       memory: 90
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The resource calculation methods differ between static and dynamic adjustment of the amplification ratio. For details, see the <a href="https://docs.byteplus.com/en/docs/vke/Amplifying_nodes#bOMJcfTK">Appendix</a> section of this topic.   </div>
   

3. Run the following command to create and issue the NOC.

   ```Bash
   kubectl apply -f nodeovercommit-test.yaml
   ```
   


<span id="7LSfzOqP"></span>
### Step 3: (Optional) Enable the load\-aware scheduling policy

To address the scheduling priority issue between non‑amplified and amplified nodes within the same node pool, you can combine [load‑aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling) with NodeSchedulingConfig objects.


* When a node does not match any NodeSchedulingConfig, the global configuration is used. If a matching custom resource exists, its configuration takes precedence.

* When a node matches multiple NodeSchedulingConfigs, the most recently created one takes effect.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If load‑aware scheduling is not enabled, node utilization cannot be effectively controlled. This poses risks to business operations. By default, VKE schedules Pods only based on Pod <code>request</code> values. When actual resource usage exceeds the amplified allocatable resources, OOM failures may occur. Therefore, we strongly recommend enabling load‑aware scheduling.</div>



1. On the configuration page of the load‑aware scheduling add\-on (scheduler‑plugin add\-on), configure the global node resource utilization threshold. For more details, see [Load‑aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_257ac8869b388731e949e77290e2b474.png) </span>

2. Specify a custom resource utilization threshold for the corresponding node pool by applying a NodeSchedulingConfig. The following YAML file `nodeschedulingconfig-test.yaml` functions as an example.

   ```YAML
   apiVersion: scheduling.vke.volcengine.com/v1beta1
   kind: NodeSchedulingConfig
   metadata:
     name: nodeschedulingconfig-test   # The custom NodeSchedulingConfig name.
   spec:
     nodeSelector:
       matchLabels:
         katalyst.kubewharf.io/overcommit_node_pool: test-pool  # The node selector. It defines the scope for the resource utilization threshold. For example, the scope can be the corresponding amplified node pool.
     targetLoadThreshold:
       cpu: 70  # The CPU resource utilization threshold. Unit:  percentage.
       memory: 70  # The memory resource utilization threshold. Unit:  percentage.
   ```
   

3. Run the following command to issue the NodeSchedulingConfig.

   ```Bash
   kubectl apply -f nodeschedulingconfig-test.yaml
   ```
   


<span id="vFwc5zGC"></span>
### Step 4: (Optional) Enable node pressure awareness and eviction policy

When a node is amplified, it can host workloads that exceed its capacity. If the amplification ratio is too high or the actual container load exceeds expectations, the node may become overloaded. This affects overall service performance. We recommend configuring pressure awareness and eviction policies on the node via an AQC and also creating a KatalystCustomConfig (KCC) to add the labels of the node to an allowlist.


1. Create an AQC and configure pressure awareness and eviction. The following YAML file `adminqosconfiguration-test.yaml` functions as an example.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: AdminQoSConfiguration
   metadata:
     name: katalyst-config # The name of the KatalystCustomConfig object. This field has a fixed value.
     namespace: katalyst-system
     labels:
       vke.node.katalyst.deploy: "true"  # This field has a fixed value.
   spec:
     # The amplified node pool selector. It matches the value of the label katalyst.kubewharf.io/overcommit_node_pool on the node.
     nodeLabelSelector: "katalyst.kubewharf.io/overcommit_node_pool=test-pool" 
     priority: 10 # It must correspond to the nodeLabelSelectorAllowedKeyList defined in the KatalystCustomConfig.
     config:
       evictionConfig: 
         cpuSystemPressureEvictionConfig: 
           enableCPUSystemPressureEviction: true # Enable system CPU pressure awareness and eviction policy.
           usageUpperBoundRatio: 0.8 # The node CPU utilization threshold. 1 indicates 100%.
           evictionWorkloadScope: declaredEvictable # When it is enabled, only Pods with the katalyst.kubewharf.io/evictable=true annotation can be evicted.
         memoryPressureEvictionConfig:
           evictionWorkloadScope: declaredEvictable # When it is enabled, only Pods with the katalyst.kubewharf.io/evictable=true annotation can be evicted.
           enableNumaLevelEviction: true # Enable per‑NUMA memory pressure awareness and eviction policy.
   ```
   

2. Run the following command to create an AQC.

   ```Bash
   kubectl apply -f adminqosconfiguration-test.yaml
   ```
   

3. Create a KCC object to define the Group, Version, and Resource (GVR) information as well as the management behavior of the AQC. The following YAML file `katalystcustomconfig-test.yaml` functions as an example.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: KatalystCustomConfig
   metadata:
     name: katalyst-config  # The name of the KatalystCustomConfig object. This field has a fixed value.
     namespace: katalyst-system  # The namespace of the KatalystCustomConfig object. This field has a fixed value.
     labels:
       vke.node.katalyst.deploy: "true"  # The label related to the fine-grained resource management feature of node pool configuration. This field has a fixed value.
   spec:
     nodeLabelSelectorAllowedKeyList: # Enable AdminQoSConfiguration to add node labels to allowlists via nodeLabelSelector.
       - priority: 10 # Define the priority of the following label keys when multiple adminqosconfigurations match a single node. A higher value indicates higher priority.
         keyList: # Define the list of supported label keys with the corresponding priority.
           - katalyst.kubewharf.io/overcommit_node_pool
     targetType:  # The description of the GVR information for the AdminQosConfiguration. This field has a fixed value.
       group: config.katalyst.kubewharf.io
       resource: adminqosconfigurations
       version: v1alpha1
   ```
   

4. Run the following command to create a KCC.

   ```Bash
   kubectl apply -f katalystcustomconfig-test.yaml
   ```
   

   After the preceding configuration is complete, the system performs pressure awareness and eviction as follows:

   * CPU pressure awareness and eviction policy:

      * CPU pressure is detected every 5 seconds. If CPU usage reaches usageUpperBoundRatio (0.8 in the example) within at least 8 out of the last 10 detection cycles, an eviction is triggered.

      * The cooldown period between two Pod evictions is 300 seconds. After an eviction is triggered, no other evictions will occur within 300 seconds.

      * When an eviction occurs, the node is tainted with `node.katalyst.kubewharf.io/SystemCPU` to prevent Pods from being scheduled onto the node.

      * DaemonSet Pods will not be evicted.

   * Memory pressure awareness and eviction policy per NUMA:

      * Reads NUMA memory watermark values (`free`, `low`, `min`) from `/proc/zoneinfo`.

      * If `min` < `free` < `low` is detected for 12 consecutive cycles (5 seconds for each cycle), a memory eviction is triggered.

      * When `free` < `min` is detected, the cumulative cycles are quickly increased to 11 cycles. That means that if `free` < `low` is detected in the next cycle, eviction will be triggered.

      * DaemonSet Pods will not be evicted.


<span id="wSfengtQ"></span>
## Validate results


1. Check the `status` field of the NOC to verify the matching relationship between the node and the NOC.

   ```Bash
   kubectl get noc nodeovercommit-test -o jsonpath='{.status.matchedNodeList}'
   ```
   

   The expected output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e77a19b47eaff5e79ebf658f7fe03b33.png) </span>

2. If CPU and memory amplification ratios are specified for the node, view the annotations related to amplification on the corresponding node.

   ```Bash
   kubectl get node ${NODE_NAME} -o jsonpath='{.metadata.annotations}'
   ```
   

   The expected output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8f8bf15fdf14f547f19004f97aefa92.png) </span>

3. Verify whether the capacity and allocatable resources of the node have been amplified.

   ```Bash
   # View the actual resource capacity of the node
   kubectl get node ${NODE_NAME} -o jsonpath='{.status.capacity}' 
   kubectl get node ${NODE_NAME} -o jsonpath='{.status.allocatable}'
   ```
   

   The expected output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fc29165931d298340ad10573147626b2.png) </span>


<span id="bOMJcfTK"></span>
## Appendix

<span id="WbZtc6se"></span>
### Core metrics

The following table describes core metrics related to dynamic amplification and prediction capabilities.


<Tabs>
<Tab zoneid="zfFysPtHhy" title="Controller metrics">
<TabTitle>Controller metrics</TabTitle>

The following table describes controller metric names and their meanings.


|**Metric name** |**Type** |**Tag** |**Meaning and measurement method** |
|---|---|---|---|
|noc_matched_nodes |Gauge |config_name |The number of nodes matched by each NodeOvercommitConfig. |
|noc_realtime_cpu_overcommit_ratio |Gauge |node |The real\-time CPU amplification ratio. |
|noc_realtime_memory_overcommit_ratio |Gauge |node |The real‑time memory amplification ratio. |
|noc_predict_cpu_overcommit_ratio |Gauge |node |The predicted CPU amplification ratio. |
|noc_predict_memory_overcommit_ratio |Gauge |node |The predicted memory amplification ratio. |



</Tab>
<Tab zoneid="mbxkgJyaXc" title="Webhook metrics">
<TabTitle>Webhook metrics</TabTitle>

The following table describes webhook metric names and their meanings.


|**Metric name** |**Type** |**Tag** |**Meaning and measurement method** |
|---|---|---|---|
|node_mutator_request_total |Counter |type=nodeAllocatableMutator |Total webhook requests (successful and failed requests). |
|node_mutator_request_fail |Counter |type=nodeAllocatableMutator |The number of failed mutate operations. |
|node_mutator_latency |Counter |type=nodeAllocatableMutator |The mutate latency, which is a cumulative counter. You can use the irate function to calculate the latency. |



</Tab>
<Tab zoneid="u8bFkVnaCI" title="Agent metrics">
<TabTitle>Agent metrics</TabTitle>

The following table describes agent metric names and their meanings.


|**Metric name** |**Type** |**Tag** |**Meaning and measurement method** |
|---|---|---|---|
|realtime_overcommit_advisor_update_fail |Counter |node |The number of failed real‑time amplification ratio updates. |
|realtime_overcommit_advisor_update_total |Counter |node |The total number of real‑time amplification ratio updates. |



</Tab>
</Tabs>


<span id="7SZJlPZ7"></span>
### Amplified resource calculation


|<div style="text-align: center"><br><strong>Symbol</strong></div><br> |<div style="text-align: center"><br><strong>Meaning</strong></div><br> |<div style="text-align: center"><br><strong>Calculation method description</strong></div><br> |
|---|---|---|
|A<sub>0</sub> |Allocatable resources before node amplification |A<sub>0</sub> = Node specification \- System reserved resources<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For a description of system\-reserved resources, see <a href="https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies">Policy for node reserved resources</a>.</div><br> |
|A |Allocatable resources after node amplification |A =  (A<sub>0</sub> \- O) × R |
|R |Amplification ratio |* Static amplification ratio:<br><br>   R<sub>static</sub> = User\-defined value of `resourceOvercommitRatio` configured in the NOC.<br><br>* Dynamic amplification ratio:<br><br>   R<sub>dynamic</sub> = [ Q + ( A<sub>0</sub> × T − U ) / L ] / A<sub>0</sub><br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The dynamic amplification ratio will not exceed the static amplification ratio.</div><br> |
|O |Exclusive resource<br><br> |Only the resources of Pods with exclusive cores are counted. This means that the kubelet parameter of the node has been configured with `cpu-manager-policy=static`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For a description of the node kubelet parameter <code>cpu-manager-policy</code>, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring Kubelet parameters for node pools</a>.</div><br> |
|Q |Allocated requests on the node |The sum of CPU or memory requests of all Pods on the node (excluding resources of exclusive\-core Pods). |
|L |Pod average load ratio |L = U ÷ Q<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">To prevent the amplification factor from being too aggressive, VKE sets the following lower limits when calculating the average load ratio of Pods on a node:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Memory: 1/2</div><br><br><br>* <div data-tips="true" data-tips-type="default">CPU: 1/3</div><br> |
|T |Target load watermark |The user\-defined value of `targetLoadThreshold` in NOC. |
|U |The actual resource usage of all Pods on the node. |Resources can be calculated through the following two methods:<br><br><br>* **Real‑time collection**: Collects the real‑time resource usage of all Pods on the node (excluding exclusive‑core Pod resources).<br><br>* **Historical prediction**: Queries the cloud‑native observability platform for historical resource usage metrics of the workloads corresponding to Pods on the node. The default query window is 7 days. At least 1 day of metrics is required. When metrics are insufficient, the usage is estimated through (1/R<sub>static</sub> × Q). |
