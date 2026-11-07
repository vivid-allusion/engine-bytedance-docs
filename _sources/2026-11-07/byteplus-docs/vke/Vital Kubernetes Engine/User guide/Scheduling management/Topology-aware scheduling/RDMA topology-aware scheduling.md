---
title: "RDMA topology-aware scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling"
---

This topic mainly introduces the methods and limits of using RDMA topology\-aware scheduling in VKE.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

In AI scenarios such as the Large Language Model (LLM) training, there are usually multiple pods executing training tasks in parallel in a Job. These pods need to frequently exchange data with each other while running, such as parameters and gradient values. To ensure network communication overhead does not constitute a performance bottleneck of training tasks, we can usually use RDMA network to directly transfer data between GPUs. However, in the data center, the number of RDMA network devices that can be connected to a switch is limited. Usually, we need to connect the S0 and S1 switches with all the servers in one miniPod. Such kind of network topology structure will lead to differences in terms of communication distances among different RDMA network interface cards. Therefore, communication performance varies based on different GPU devices.

Therefore, the VKE provides the RDMA topology\-aware scheduling capability. By being aware of the network topology information of the GPU cards and RDMA devices, the scheduler can schedule all the pods in the same Job to the nodes and RDMA network interface cards that have as close as possible topology distances in the RDMA network. In this way, we can help users to give full play to the communication capability of the RDMA network, thus enhancing the training performance of the AI Large Language Model (LLM).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


|Project |Requirement |Supplementary description |
|---|---|---|
|Cluster versions |* [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.10\-vke.13 and later versions<br><br>* [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.10\-vke.21 and later versions<br><br>* [Kubernetes v1.28](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28): v1.28.3\-vke.15 and later versions<br><br>* [Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30): v1.30.4\-vke.8 and later versions |When the cluster version does not meet the requirements, upgrade the cluster to the required version. For detailed operations, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster). |
|Cluster network |VPC\-CNI network model |If no clusters that use the VPC\-CNI network model exist, create a cluster first. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster). |
|Add\-on dependency |* katalyst add\-on (public beta)<br><br>* Scheduler\-plugin add\-on<br><br>* rdma\-device\-plugin add\-on (public beta) |For descriptions of add\-on installation and configuration, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on). |
|Functional dependency |kubelet custom configuration parameters |For more introductions to features, refer to [Configuring the kubelet custom parameters for nodes](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool). |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The clusters that meet the limits have been created. For detailed operations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

<span id=".5L2_55So5pa55rOV"></span>
## Use methods

<span id=".5q2l6aqk5LiA77ya6ZuG576k5Lit5L2_55SoLXJkbWEt6LWE5rqQ"></span>
### Step 1: Use RDMA resources in clusters

We need to prepare the nodes supporting RDMA devices (such as High\-performance Computing Optimized GPU) in the clusters. You can create nodes or use existing nodes that meet your business requirements.. In addition, you need to manually add a node label with `vke.node.rdma.mode` as the key and `shared `as the value to configure RDMA use modes for nodes. For detailed operations, see [Using RDMA resources in the VKE clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Among the three modes of RDMA, including exclusive, shared, and shared\-multi (1:N shared), only the shared mode can support the topology information reporting of RDMA.</div>


* <div data-tips="true" data-tips-type="warning">The option <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool">Enable auto renew for node labels and taints</a> allows existing nodes in the pool to automatically update labels you added in this page. Caution! Disabling this option might make the cluster unable to use existing RDMA nodes in the pool.</div>



<span id=".5q2l6aqk5LqM77ya56Gu5L-d6ZuG576k5Lit5a6J6KOF5L6d6LWW55qE57uE5Lu2"></span>
### Step 2: Ensure that dependent add\-ons are installed in the clusters

RDMA topology\-aware scheduling depends on three add\-ons, including scheduler\-plugin, rdma\-device\-plugin, and katalyst, in the clusters. You must ensure that these three add\-ons have been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


* **scheduler\-plugin**

   Install this add\-on and enable **RDMA topology\-aware scheduling**.

* **rdma\-device\-plugin**

   You can directly install this add\-on, without configuration\-related operations.

* **katalyst**

   Install this add\-on and enable the **topology\-aware scheduling** feature.


<span id=".5q2l6aqk5LiJ77ya6YWN572u6ZyA6KaB5oSf55-lLXJkbWEt5ouT5omR55qE6IqC54K5"></span>
### Step 3: Configure the nodes that need to be aware of RDMA topology

<span id=".5pu05pS56IqC54K5LWt1YmVsZXQt5Y-C5pWw"></span>
#### Modifying the kubelet parameters of nodes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">Only the clusters of the Kubernetes Version 1.24 and Version 1.26 need configuring the kubelet custom parameters. The clusters of the Kubernetes Version 1.28 and later versions need no configuration.</div>


* <div data-tips="true" data-tips-type="warning">You can configure the kubelet parameters for the newly added nodes when creating clusters, the newly added nodes when creating node pools, the newly added nodes for existing node pools, and stock nodes for existing node pools. For detailed operations, refer to <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Configuring the kubelet custom parameters for nodes</a>.</div>



Add kubelet parameters for nodes that need to be aware of RDMA topology to enable the corresponding feature gate.

The VKE supports configuring the kubelet parameters of the node pools where the nodes are located through the console. In the **Advanced configuration** of the node pools, add the kubelet custom parameters: `feature-gates: QoSResourceManager=true`.

<span id=".5Li66IqC54K55re75Yqg5oyH5a6aLWxhYmVs"></span>
#### Adding the specified label to the nodes

Configure the label that turns on the RDMA topology awareness for the nodes. Configure the key as `vke.node.katalyst.deploy` and the value as `true`.

<span id=".5q2l6aqk5Zub77ya5p-l6K-iLXJkbWEt5ouT5omR5L-h5oGv"></span>
### Step 4: Query RDMA topology information

After you complete the above three steps, the RDMA topology information will be recorded in the custom resources CustomNodeResource of the Kubernetes (KCNR for short).


1. Use kubectl to connect to the clusters. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to query the KCNR of the RDMA topology\-aware nodes in the clusters.

   Replace `<node-name>` with your node name.

   ```bash
   kubectl get kcnr <node-name> -oyaml
   ```
   

3. In the KCNR obtained, query the following annotated fields to view the RDMA topology and resource remainder information of this node.

   ```yaml
   apiVersion: node.katalyst.kubewharf.io/v1alpha1
   kind: CustomNodeResource
   metadata:
     name: 10.27.0.4  # Node Name
   # The spec describes all RDMA network interface card IDs in the node and the information about the S0 switch connected.
   spec:
     nodeResourceProperties:    # The nodeResourceProperties contains all the RDMA network interface card information in this node, including network interface card IDs and the hash of the switches connected.
     - propertyName: RDMATOR/0000:1a:00.0    # RDMA ID.
       propertyValues:
       - b6f73fb8fb523a512a30edf3c73b7ab********    # The hash of the S0 switch connected to the RDMA. This hash can label one S0 uniquely.
     - propertyName: RDMATOR/0000:3f:00.0
       propertyValues:
       - b6f73fb8fb523a512a30edf3c73b7ab********
     - propertyName: RDMATOR/0000:d1:00.0
       propertyValues:
       - 985abf31e6b7bd2aef8dfe551406912********
     - propertyName: RDMATOR/0000:e7:00.0
       propertyValues:
       - 985abf31e6b7bd2aef8dfe551406912********
   # The status describes allocatable resources for each RDMA network interface card on the node. It helps determine whether a network interface card has been occupied by pods.
   
   # Through the tree structure description of node resources, the top level is socket zone, which contains multiple numa zones. Then the numa zones contain multiple RDMA network interface cards.
   status:
     topologyPolicy: SingleNUMANodeContainerLevel
     topologyZone:
     # socket zone
     - name: "0"
       type: Socket
       resources: {}
       children:
       # numa zone
       - name: "0"
         type: Numa
         resources:
           allocatable:
             cpu: "61"
             nvidia.com/gpu: "4"
             vke.volcengine.com/rdma: "2"
           capacity:
             cpu: "64"
             nvidia.com/gpu: "4"
             vke.volcengine.com/rdma: "2"
         allocations:
         - consumer: test-rdma-metrics/test-rdma-host-57bezr9pt-76b4cbf99c-bm7k8/667e2f44-e5ec-496f-81c0-0794********
           requests:
             vke.volcengine.com/rdma: "1"
         children:
         # Information on RDMA network interface cards in this NUMA zone.
         # Each name corresponds to one RDMA network interface card. Meanwhile, "allocatable" indicates the RDMA resources that can be allocated. Further, "capacity" indicates the total RDMA resources.
         - name: 0000:1a:00.0
           type: NIC
           resources:
             allocatable:
               vke.volcengine.com/rdma: "1"
             capacity:
               vke.volcengine.com/rdma: "1"
           # Information on pods allocated on this RDMA network interface card.
           allocations:
           # Format: Pod namespace/Pod name/Pod UID
           - consumer: test-rdma-metrics/test-rdma-host-57bezr9pt-76b4cbf99c-bm7k8/667e2f44-e5ec-496f-81c0-0794********
             # The amount of resources allocated by the pod on this RDMA network interface card.
             requests:
               vke.volcengine.com/rdma: "1"
         - name: 0000:3f:00.0
           type: NIC
           resources:
             allocatable:
               vke.volcengine.com/rdma: "1"
             capacity:
               vke.volcengine.com/rdma: "1"
     - name: "1"
       type: Socket
       resources: {}
       children:
       - name: "1"
         type: Numa
         resources:
           allocatable:
             cpu: "64"
             nvidia.com/gpu: "4"
             vke.volcengine.com/rdma: "2"
           capacity:
             cpu: "64"
             nvidia.com/gpu: "4"
             vke.volcengine.com/rdma: "2"
         allocations:
         - consumer: default/test-rdma-fc69fc8b-qv6s8/d981a1f8-ea64-440c-9155-3bab********
           requests:
             vke.volcengine.com/rdma: "2"
         children:
         - name: 0000:d1:00.0
           type: NIC
           resources:
             allocatable:
               vke.volcengine.com/rdma: "1"
             capacity:
               vke.volcengine.com/rdma: "1"
           allocations:
           - consumer: default/test-rdma-fc69fc8b-qv6s8/d981a1f8-ea64-440c-9155-3bab********
             requests:
               vke.volcengine.com/rdma: "1"
         - name: 0000:e7:00.0
           type: NIC
           resources:
             allocatable:
               vke.volcengine.com/rdma: "1"
             capacity:
               vke.volcengine.com/rdma: "1"
           allocations:
           - consumer: default/test-rdma-fc69fc8b-qv6s8/d981a1f8-ea64-440c-9155-3bab********
             requests:
               vke.volcengine.com/rdma: "1" 
   ```
