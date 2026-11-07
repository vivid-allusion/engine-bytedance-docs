---
title: "Cluster autoscaler best practices"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-Autoscaler-best-practices"
---

A cluster autoscaler (CA) automatically scales the cluster based on the scheduling status of pods and the use of node resources within the cluster. This ensures that workloads run normally in pods on the node and controls the quantity of cluster resources to reduce costs. This topic describes common CA best practices in VKE.

<span id=".57uE5Lu26YOo572y"></span>
## Add\-on deployment

In VKE clusters, a CA exists as a managed component named cluster\-autoscaler, which can be installed and configured in the VKE console. To do so, follow the steps below:


1. In the VKE console, install and configure the cluster\-autoscaler add\-on.

2. Enable autoscaling for the node pool, and set the scaling scope and priority.

3. Create a workload and set appropriate scheduling conditions so that it can be scheduled onto nodes in the node pool with autoscaler enabled.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler">Creating CAs</a>.</div>


<span id=".6IqC54K55rGg6YWN572u"></span>
## Node pool configuration

Node pools are key to improving availability and reducing costs. To achieve effective autoscaling, you need to properly configure node pools for the cluster. Recommendations for configuring node pools are as follows.


|Recommendation |Description |
|---|---|
|Uniform node specifications within a node pool |Each node in the node pool should have the same scheduling attributes, such as labels, taints, and resources. After enabling autoscaling for the node pool, do not modify the node pool or its nodes. If nodes within the same node pool have different labels and taints, CA may only consider the scheduling attributes of a single node during scaling, which causes unexpected scaling. |
|A single availability zone (AZ) for a node pool |* If pod scheduling is AZ\-dependent, configure the node pool to reside in a single AZ and use multiple node pools to cover multiple AZs.<br><br>* If a node pool spans multiple AZs, CA will assume that new nodes belong to one AZ, which does not align with actual pod scheduling requirements. This may cause unschedulable pods or failed scaling triggers. |
|Configuring labels for node pools |When node scale\-out happens in a cluster, the node pool automatically adds labels to nodes. If the pool has no nodes, CA cannot detect these labels, which prevents normal scaling if pending pods rely on these labels. We recommend configuring labels for the node pool and adding node pool affinity labels when creating workloads. This lets CA detect labels and scale the correct pool. |
|Reducing the number of node pools with autoscaling enabled |CA scans the cluster every 10 seconds to trigger scaling. Before each scan, it calculates pending pod scheduling for all autoscaling\-enabled node pools. More autoscaling\-enabled node pools means longer scanning or scaling. Therefore, disable autoscaling for node pools that no longer need autoscaling. |
|Defining priorities for autoscaling\-enabled node pools |CA supports selecting node pools by priority during the scale\-out process. You can configure priorities for multiple autoscaling\-enabled node pools to meet cluster scaling needs for specific scenarios. |
|Preventing nodes from scaling in by CA |To retain specific nodes (block CA from deleting them), add this annotation to the nodes: `kubectl annotate node <nodename> cluster-autoscaler.kubernetes.io/scale-down-disabled=true`. |


<span id=".Y2Et6YWN572u"></span>
## CA configuration

<span id=".5omp5a65562W55Wl"></span>
### Scale\-out policies

Understanding and selecting the appropriate scale\-out policy can better meet your scaling needs. When formulating policies, CA estimates how well node pools can satisfy the scheduling requirements of pending pods. Among node pools that meet the scheduling requirements, CA selects the most suitable one based on the scaling policy. CA provides the following scale\-out policies:


* **Random**: CA first filters out node pools that cannot meet the scheduling requirements of pending pods and then randomly selects one from the remaining node pools.

* **Priority**: Among node pools that meet the scheduling requirements of pending pods, CA selects the one with the highest priority. If multiple node pools have the same priority, it falls back to random selection.

* **Least waste**: For node pools satisfying scheduling requirements for pending pods, CA calculates a score for each node pool based on CPU and memory usage to represent overall resource waste after scaling. A lower score indicates less waste, and CA selects the node pool with the lowest score. If multiple node pools have the same lowest score, it falls back to random selection.

* **Most pods**: For node pools satisfying scheduling requirements for pending pods, CA calculates how many pods each can schedule after scaling, ignoring limits on the node pool scaling range.  If all pending pods come from the same workload, it falls back to random selection because the calculation results for all node pools will be identical.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For general scenarios, the random policy and priority policy are recommended</div>


<span id=".57yp5a656ZiI5YC8"></span>
### Scale\-in thresholds

CA supports configuring scale\-in thresholds for GPU nodes and non\-GPU nodes. The calculation formula is `node resource requests/total node resources`.


* If mGPU is not enabled on GPU nodes, CA uses the number of GPU cards as the metric for calculating the scale\-in threshold.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The mGPU feature is currently in the <strong>public beta</strong> stage. For details, see <a href="https://docs.byteplus.com/en/docs/vke/mGPU-overview">mGPU overview</a>.</div>



* If mGPU is enabled on GPU nodes, CA uses the number of mGPU cores, GPU memory size, number of CPU cores, and amount of memory as metrics for calculating the scale\-in threshold and compares the maximum value with the threshold.

* For CPU nodes, CA uses the number of CPU cores and amount of memory as metrics for calculating the scale\-in threshold and compares the maximum value with the threshold.


Since scale\-in usually triggers rescheduling of pods and the cost of scale\-in at the node level is relatively high, it is recommended to set conservative scale\-in thresholds. In addition, CA also supports suppressing scale\-in behavior at the pod level by marking their running nodes as non\-scalable. The supported pods include:


* Pods with local storage.

* Non\-DaemonSet pods in the `kube-system` namespace.

* Pods with the `cluster-autoscaler.kubernetes.io/safe-to-evict=false` label.


<span id=".5pu05aSa6YWN572u"></span>
### More configuration

For other CA configurations, see [Creating CAs](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler).

<span id=".5oCn6IO95ZKM5Y-v5omp5bGV5oCn"></span>
## Performance and scalability

<span id=".5oCn6IO9"></span>
### Performance

CA performance is mainly influenced by its available resources and scan intervals. A managed CA scans the cluster once every 10 seconds to make scaling decisions.

No extra limit applies to the number of scaling groups that a managed CA can manage. You can adjust the number of scaling groups according to the actual scaling records of autoscaling\-enabled node pools. This prevents the node count in a node pool from remaining consistently low or high. However, more node pools mean longer scans and decision\-making processes for CA.

<span id=".5Y-v5omp5bGV5oCn"></span>
### Scalability

CA scalability depends primarily on CA configuration parameters and node pools. Because too many pending pods will increase the time required for each CA execution and cannot accelerate the scale\-out, the upper limit for a single scale\-out operation by CA is restricted to 90 nodes. To improve CA scalability for specific scenarios, contact professional support.


* **Optimizing scalability with custom images**: When a pod transitions from Pending to Running, time is spent not only on node resource preparation but also on container image pulling. If the image is large and many pods start simultaneously, significant pressure occurs during image pulling and loading, which results in nodes being scaled out but pods failing to run normally. To resolve this, package container images into ECS system images in advance as custom images to eliminate image\-pulling latency. For more information about custom images, see [Overview of operating system (OS) images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

* **Optimizing scalability with placeholder pods**: A placeholder pod is a low\-priority pod. When a pending pod is created, it preempts resources from the low\-priority placeholder pod. This lets the pending pod be scheduled and created normally as it has resources, while the placeholder pod reverts to Pending, triggering CA scaling. This method can effectively improve the efficiency of container readiness, but it also incurs additional costs. For pod priority\-based preemption, see [How do I set pod priorities to implement preemption?](https://developer.volcengine.com/articles/7278155404318605372)


<span id=".5a656YeP6KeE5YiS"></span>
## Capacity planning

CA capacity is subject to both node pools and quotas. When autoscaling is enabled for a node pool, you need to configure the upper and lower limits on the number of nodes. Quotas affect account\-level resources.

The upper and lower limits on the number of nodes in a node pool are user\-defined and can be adjusted in real time based on business requirements. Quotas affect the count of account\-level resources, such as nodes and node pools. For information about how to increase quotas, see [How do I increase quotas?](https://docs.byteplus.com/en/docs/vke/How-do-I-increase-a-quota)

<span id=".5Y-v6KeC5rWL5oCn"></span>
## Observability

CA is a managed add\-on that does not require manual operation and maintenance. VKE observability provides a CA monitoring dashboard that displays CA metrics. For details, see [Control plane service observability](https://docs.byteplus.com/en/docs/vke/Control-plane-service-observability).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CA monitoring metrics in VKE are consistent with those of the community version. For details, see <a href="https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/proposals/metrics.md">CA monitoring metrics</a>.</div>


<span id=".6auY5Y2x5pON5L2c"></span>
## High\-risk operations

The following operations may cause CA to fail to scale as expected. Please pay extra attention during configuration:


* **Inconsistent node scheduling attributes within a node pool**


A node pool is a collection of nodes with the same scheduling attributes. However, you can also modify the scheduling attributes of node pools and nodes via the console, which may lead to unexpected scaling behavior. For example, if nodes in the same pool have different labels or taints, CA will prioritize the scheduling attributes of existing nodes in the pool when making scaling decisions and will only reference one node at most. This can cause CA to be influenced by the attributes of a single node, resulting in failed scaling.


* **Configuring multiple AZs for a node pool in AZ affinity scheduling scenarios**


In AZ affinity scheduling scenarios, if a node pool spans multiple AZs, CA will assume new nodes from scale\-out belong to only one AZ, leading to a mismatch between actual pod scheduling requirements. This potentially causes pods to remain unschedulable after scale\-out or causes failure in triggering scaling behavior. We recommend configuring multiple node pools, with each node pool corresponding to one AZ.


* **Pods with node affinity associated with an empty node pool**


Node pools automatically add labels to their nodes, for example, to mark a node as belonging to a specific node pool. If the node pool itself does not have these labels and the node pool has no nodes, CA will not detect these labels. As a result, CA will ignore the pod affinity requirements for the node pool when formulating scaling policies, leading to failed scaling.


* **Too many DaemonSet pods and static pods**


CA considers DaemonSet pods and static pods during scaling. If the remaining resources of the node template involved in the scale\-out (after deducting resources for DaemonSet/static pods) are insufficient to schedule pending pods, CA will not trigger scale\-out.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more high\-risk operations in VKE, see <a href="https://docs.byteplus.com/en/docs/vke/High-risk-operations-and-recovery-solutions">High\-risk operations and solutions</a>.</div>


<span id=".5LiOLXZjaS3nmoTlr7nmr5Q="></span>
## Comparison with VCI

CA automatically adjusts the size of the Kubernetes cluster based on workload demands. Its main advantage is the ability to dynamically scale the cluster according to actual needs, avoiding resource waste. However, the node scaling process with CA can be relatively time\-consuming. Therefore, CA is more suitable for long\-running applications that require dynamic adjustments based on workload changes. However, it has limitations in supporting short\-term, large\-scale, and bursty workloads.

For such scenarios, you can use BytePlus VCI to build clusters with rapid scaling and pay\-as\-you\-go capabilities.  VCI is a serverless, containerized computing service that provides benefits such as instance startup within seconds, high\-concurrency instance creation, and sandbox\-based container isolation. It allows you to focus on building applications, eliminating the need to purchase or manage underlying infrastructure such as cloud servers. For details, see [What is VCI?](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance)
