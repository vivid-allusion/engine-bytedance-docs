---
title: "Node resource reservation policies"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies"
---

As an important part of clusters, nodes need Kubernetes system components and resources to work properly. To satisfy those requirements, VKE itself consumes a certain amount of node resources to ensure business stability. Therefore, the total resources for your nodes are not equal to those available in the cluster. A node with higher specifications runs more pods, and in turn requires more resources reserved.

<span id="eI4nCeD7"></span>
## Policy description

To ensure node stability, VKE reserves memory, CPU, and process ID (PID) resources for nodes based on the corresponding ECS instance type. These resources are reserved through the kubelet parameters `kube-reserved` and `system-reserved` and are used to run Kubernetes\-related components such as kubelet, kube\-proxy, and containerd. For the specific quantities of reserved resources, see **CPU reservation policies for nodes**, **Memory reservation policies for nodes**, and **PID reservation policies for nodes**.

<span id=".6IqC54K5LWNwdS3pooTnlZnnrZbnlaU="></span>
## CPU reservation policies for nodes

The system provides the following reservation policies:


|Policy No. |Total CPU cores |Default reservation |
|---|---|---|
|1 |Total CPU cores <= 4 |100 millicores = 0.1 cores |
|2 |4 cores < total CPU cores <= 64 cores |0.1 cores + (total CPU cores – 4) \* 2.5% cores |
|3 |64 cores < total CPU cores <= 128 cores |0.1 cores + (64 \- 4) cores × 2.5% + (total CPU cores \- 64) × 1.25% |
|4 |Total CPU cores \> 128 |0.1 cores + (64 \- 4) cores \* 2.5% + (128 \- 64) cores \* 1.25% + (total CPU cores \- 128) cores \* 0.5% |


For example, for a node of the ecs.g2i.28xlarge specification, it has 112 CPU cores and the matching CPU reservation policy is the No.3 CPU reservation policy above. The reserved amount of CPU cores is `0.1 + (64-4) × 2.5% + (112-64) × 1.25% = 2.2 Cores`. This reserved resource amount will be equally divided between the `kube-reserved` and `system-reserved` parameters, meaning that the reserved CPU values in the `kube-reserved` and `system-reserved` parameters will each be 1.1 cores.

<span id=".6IqC54K55YaF5a2Y6aKE55WZ562W55Wl"></span>
## Memory reservation policies for nodes 


|Policy No. |Total memory |Default reservation |
|---|---|---|
|1 |Total memory <= 4 GiB |Total memory \* 25% |
|2 |4 GiB < total memory <= 8 GiB |4 GiB × 25% + (total memory − 4) GiB × 20% |
|3 |8 GiB < total memory <= 16 GiB |4 GiB × 25% + (8 − 4) GiB × 20% + (total memory − 8) GiB × 10% |
|4 |16 GiB < total memory <= 128 GiB. |4 GiB × 25% + (8 − 4) GiB × 20% + (16 − 8) GiB × 10% + (total memory − 16) GiB × 6% |
|5 |Total memory \> 128 GiB |4 GiB \* 25% + (8 \- 4) GiB \* 20% + (16 \- 8) GiB \* 10% + (128 \- 16) GiB \* 6% + (total memory \- 128) GiB \* 2% |


For example, for a node of the ecs.g2i.28xlarge specification, it has 448 GiB of memory and the matching memory policy is the No.5 memory reservation policy above. The reserved size of memory is `4 × 25% + (8-4) × 20% + (16-8) × 10% + (128-16) × 6% + (448-128) × 2% = 15.72 GiB`. This reserved resource will be equally divided between the `kube-reserved` and `system-reserved` parameters, meaning that the reserved memory value of the `kube-reserved` and `system-reserved` parameters will each be 7.86 GiB.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">The actual available memory for pods on a node is calculated by subtracting not only the memory reserved in the <code>kube-reserved</code> and <code>system-reserved</code> parameters, but also the memory value specified by the <code>eviction-hard</code> parameter. By default, the <code>eviction-hard</code> parameter triggers pod eviction on the node when available memory drops below 300 MiB, which means 300 MiB of memory on the node is unavailable for pods by default. You can change the memory value specified by the <code>eviction-hard</code> parameter. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring node kubelet parameters</a>.</div>


<div data-tips="true" data-tips-type="warning">Taking the node of ecs.g2i.28xlarge specification as an example: this node has 448 GiB of memory, with a total reserved memory of 15.72 GiB allocated to <code>kube-reserved</code> and <code>system-reserved</code>. If you have not specified a custom value for the <code>eviction-hard</code> parameter (which reserves 300 MiB of memory by default), the actual memory that can be allocated to pods on the ecs.g2i.28xlarge node is <code>431.98 GiB</code> (<code>448 GiB - 15.72 GiB - 300 MiB</code>).</div>


<span id=".6IqC54K5LXBpZC3pooTnlZnnrZbnlaU="></span>
## PID reservation policies for nodes


|Reserved resource |Reserved quantity |
|---|---|
|kube\-reserved |1000 |
|system\-reserved |1000 |


<span id="SmzM0cBW"></span>
## Considerations


* If you specify custom CPU or memory reservation values through the VKE custom kubelet parameter feature in `kube-reserved` and `system-reserved`, VKE reserves resources according to your custom values. For detailed operations, see [Specifying node kubelet parameters](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

* Node resource reservation policies take effect automatically for new nodes after a scale\-out. You do not need to separately configure resource reservation for such new nodes.

* The calculation method of node resource reservation policies may reduce nodes' allocable resources. It may trigger node\-pressure eviction for nodes with high resource utilization. Therefore, for stability reasons, node resource reservation policies will not take effect automatically for existing nodes. To apply changes to existing nodes, manual configuration is required. For details, see [Applying the new configurations to existing nodes](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool#.5a2Y6YeP6IqC54K55Y-C5pWw5ZCM5q2l).
