---
title: "Best practices for ECS instance selection"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ECS-selection-best-practices"
---

This topic describes how to select proper ECS types for use in VKE clusters and considerations for ECS selection.

<span id=".6ZuG576k5b2i5oCB"></span>
## Cluster architecture

The control components of a VKE cluster are managed and deployed by the cloud platform. You do not need to worry about the selection or operation and maintenance of Kubernetes master nodes. You only need to create worker nodes. This form allows you to focus more on your applications and offers benefits such as ease of use, low cost, and high availability.

<span id=".d29ya2VyLeiKgueCueinhOagvOmAieaLqQ=="></span>
## Selecting worker node specifications

<span id=".5a6e5L6L6KeE5qC8"></span>
### Instance specification

ECS provides multiple instance families, and each instance family includes various instance types. By performance characteristics, these instance families can be classified into general\-purpose, compute\-optimized, memory\-optimized, and other types.

An instance specification may be added or removed from the list of available instance specifications. Instances with a certain specification can also be sold out.  We recommend that you check available instance specifications on the **Create node pool** page before you create a node for a cluster in the [VKE console](https://console.byteplus.com/vke).

For detailed descriptions of instance families and the naming format of instance specifications, see [Instance selection best practices](https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice).

<span id=".6IqC54K56KeE5YiS"></span>
### Node planning

Typically, a Kubernetes cluster can be regarded as a super node abstracted over a group of standalone nodes. The total computing resources of this super node equal the sum of the resources of all its constituent nodes. However, due to factors like scheduling policies and node management overhead, the node utilization rate can vary significantly when services run on different node specifications. Therefore, choosing the right node type to run services is especially critical.

<span id=".6YCJ5oup5bCR6YeP5aSn6KeE5qC86IqC54K56L-Q6KGM5Lia5Yqh"></span>
#### Running workloads on a small number of large\-specification nodes

When the total resources are the same, you can choose a small number of large\-specification ECS instances as worker nodes to run workloads. The advantages and disadvantages of this node selection strategy are shown in the following table.


|Advantages and disadvantages |Description |
|---|---|
|Advantages |* Lower management costs. Managing a small number of machines is obviously easier than managing a large number of machines.<br><br>* Lower resource costs. Fewer nodes reduce additional overhead of the operating system.<br><br>* Support for resource\-intensive applications. For example, a machine learning app requiring 8 GB of memory can’t run on a cluster with nodes that have 1 GB of memory. However, it can run on a cluster with nodes that have 10 GB of memory. |
|Disadvantages |* More containers run on a single node, so node failures disrupt more workloads.<br><br>* Higher container deployment density increases the risk of node instability.<br><br>* Fewer nodes make it difficult to deploy applications with anti\-affinity (for high availability), indirectly reducing overall system reliability.<br><br>* Cluster autoscaling can easily lead to resource waste. |


<span id=".6YCJ5oup5aSn6YeP5bCP6KeE5qC86IqC54K56L-Q6KGM5Lia5Yqh"></span>
#### Running workloads on a large number of small\-specification nodes

When the total resources are the same, you can choose a large number of small\-specification ECS instances as worker nodes to run workloads. The advantages and disadvantages of this node selection strategy are shown in the table below:


|Advantages and disadvantages |Description |
|---|---|
|Advantages |* Node failures cause a smaller impact.<br><br>* This strategy facilitates anti\-affinity deployment of applications, improving application reliability.<br><br>* Resource waste is less in autoscaling scenarios, although frequent scaling may cause service fluctuations.<br><br>* Lower container deployment density improves node stability. |
|Disadvantages |* Increasing the number of nodes brings greater management pressure and higher management costs.<br><br>* More nodes lead to increased basic consumption in aspects such as kubelet, docker, cAdvisor, and log collection clients.<br><br>* Overall resource utilization decreases due to node resource fragmentation. |


<span id=".5bu66K6u5LqL6aG5"></span>
### Recommendations

There is no universally applicable method for selecting the appropriate node type. To select a node type that best fits your scenario, consider your business characteristics. Evaluate the pros and cons of high\-spec and low\-spec large instances.

Common best practices are as follows:


* Determine the total number of cores required by the cluster under normal conditions and the redundancy needed to ensure availability.

   For example, if your business peak load does not exceed 144 cores and you need to retain 10% redundancy, the total core requirement is 160 cores (144 / 90%). In this case, you can choose 10 ECS instances with 16 cores each. If one ECS instance fails, the remaining ECS instances can still support normal service availability. Alternatively, you can ensure availability through auto\-scaling. For details, see [Autoscaling](https://docs.byteplus.com/en/docs/vke/Autoscaling).

* Classify nodes based on your requirements for computing, storage, networking, and programming languages: Node types include compute\-optimized (CPU\-to\-memory ratio approximately 1:2), memory\-optimized (CPU\-to\-memory ratio 1:8), general\-purpose (CPU\-to\-memory ratio 1:4), and more. You can also categorize your workloads as compute\-intensive, IO\-intensive, and so on based on their resource needs. For example, Java applications typically have high memory usage, so we recommend using memory\-optimized instances with a CPU\-to\-memory ratio of 1:8.


<span id=".dnBjLWNuaS3pm4bnvqTkuIvpgInlnovms6jmhI_kuovpobk="></span>
## Considerations for selecting instance specifications in VPC\-CNI clusters

You need to pay special attention to the following considerations for selecting nodes for a cluster that uses the VPC\-CNI networking model.

<span id=".5Zy65pmv6K-05piO"></span>
### Scenario description

The VPC\-CNI networking solution is a container networking capability in VKE based on CNI and elastic network interfaces (ENIs) of VPCs. It allocates native ENIs to pods to enable pod networking. In this network mode, the container network and node network are on the same network plane. The container IP is a secondary ENI IP allocated by the IPAMD add\-on. This solution is applicable to scenarios with high latency sensitivity.

<span id=".5rOo5oSP5LqL6aG5"></span>
### Considerations


* Each ECS instance can have multiple ENIs, and each ENI can have multiple IP addresses.

* ECS instances of different specifications support different numbers of ENIs and different numbers of secondary IPs per ENI.

*  Each pod requires an available secondary IP address. The number of pods per node is limited by the number of ENIs that can be bound to the node and the number of secondary IPs that can be bound to a single ENI. By default, the maximum number of pods per node is calculated using this formula:  **(maximum number of secondary ENIs that can be bound × number of secondary IPs per ENI) + 1** (the "1" is reserved for the CNI pod by the system).

* For the maximum number of ENIs per ECS instance and the number of secondary IPs per ENI, see [Instance specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).


<span id=".6IqC54K5LXBvZC3mlbDph4_pmZDliLY="></span>
### Pod count limit per node

The table below lists the specifications for the general\-purpose g1ie instance family. For more information about specifications, see [Instance specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

The ecs.g1ie.large instance has 2 ENIs (including 1 primary ENI), so the maximum number of secondary ENIs that can be bound is 1. Each ENI supports 6 private IPs. Thus, if you use an ecs.g1ie.large instance as a node, the maximum number of pods per node is: **1 (secondary ENIs) × 6 (secondary IPs per ENI) + 1 (system\-reserved pod) = 7**.


|<div style="text-align: center"><br>Instance specification</div><br> |<div style="text-align: center"><br>vCPU</div><br> |<div style="text-align: center"><br>Memory (GiB)</div><br> |<div style="text-align: center"><br>ENI IP count (including a primary ENI)</div><br> |<div style="text-align: center"><br>Private IP count per ENI</div><br> |
|---|---|---|---|---|
|<div style="text-align: center"><br>ecs.g1ie.large</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>2</div><br> |<div style="text-align: center"><br>6</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.xlarge</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>10</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.2xlarge</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>4</div><br> |<div style="text-align: center"><br>10</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.4xlarge</div><br> |<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>20</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.6xlarge</div><br> |<div style="text-align: center"><br>24</div><br> |<div style="text-align: center"><br>96</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>20</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.8xlarge</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>20</div><br> |
|<div style="text-align: center"><br>ecs.g1ie.14xlarge</div><br> |<div style="text-align: center"><br>58</div><br> |<div style="text-align: center"><br>224</div><br> |<div style="text-align: center"><br>8</div><br> |<div style="text-align: center"><br>20</div><br> |
