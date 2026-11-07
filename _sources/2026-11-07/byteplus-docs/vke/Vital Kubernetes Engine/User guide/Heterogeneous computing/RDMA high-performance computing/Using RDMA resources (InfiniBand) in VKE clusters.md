---
title: "Using RDMA resources (InfiniBand) in VKE clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_RDMA_resources_in_VKE_clusters_InfiniBand"
---

Vital Kubernetes Engine (VKE) can use Remote Direct Memory Access (RDMA) resources through add\-ons to eliminate bottlenecks of computing tasks brought by traditional network communication. This article introduces how a VKE cluster uses RDMA resources provided by InfiniBand high\-performance compute clusters.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[Public beta]: VKE clusters featured with access to RDMA resources are currently in public beta.</div>


<span id="Cg038wz2"></span>
## Background information

<span id="jZ8tUiaa"></span>
### RDMA overview


* RDMA is a high\-performance network protocol that reduces CPU usage and memory bandwidth bottlenecks, as well as improves bandwidth utilization. It comes with the following advantages:

   * **Zero Copy**: Applications can transfer data without involving the network software stack, allowing data to be directly sent to the buffer or directly received from the buffer without being copied to the network layer.

   * **Kernel Bypass**: RDMA provides a proprietary Verbs interface, allowing applications to transfer data directly from user space without switching context between kernel and user modes.

   * **CPU Offload**: Applications can access memory on remote hosts without consuming any CPUs on those hosts. Remote memory will be read without any help from remote processes (or CPUs), and the content read from them will not be written into the remote CPU caches.

* The High Performance Compute (HPC) cluster is a cluster computing environment used to handle large\-scale computing tasks, usually composed of a large number of compute nodes interconnected by an RDMA high\-speed network. It supports both RoCE and InfiniBand.

   An HPC cluster can provide powerful computing capability, large memory, high\-speed storage, and networks to meet the demands of compute\-intensive, data\-intensive, or combined workloads. In an HPC cluster, computing tasks are assigned to each compute node for parallel processing, fully utilizing the computing power of multiple nodes to accelerate computation and improve efficiency. For more details, please refer to the [HPC cluster overview](https://docs.byteplus.com/en/docs/gpu/HPC-cluster-overview).


<span id="BMT3NxCZ"></span>
### RDMA add\-on mode

In the InfiniBand network mode, the RDMA add\-on supports the following modes. The following table describes different modes and their usage restrictions.


|**RDMA add\-on mode** |**Mode description** |**Limit** |
|---|---|---|
|ib\-shared (shared) |Create a shared virtual network interface for pods in the cluster by virtualizing the RDMA physical network interface. |Each RDMA physical network interface can only provide one shared virtual network interface. |
|ib\-shared\-multi (1:N shared) |Create multiple shared virtual network interfaces for pods as needed in the cluster by virtualizing the RDMA physical network interface. |We recommend that you do not use this mode with GPUs. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your pods need to use HostNetwork, we recommend that you use RDMA resources provided by open source add\-ons. For details, see the <a href="https://github.com/Mellanox/k8s-rdma-shared-dev-plugin">open source documentation</a>.</div>


<span id="ckl8pRpH"></span>
## Cautions

The following content introduces the proven practices of VKE. Reading the [Limits](https://docs.byteplus.com/en/docs/vke/Limits) and strictly following the steps described below are highly recommended. If you want to use another solution, consult your account manager.

<span id="zA6u0nOw"></span>
## Limits


* A pod cannot use mGPU and RDMA add\-ons simultaneously.

* RDMA devices can only work with the VPC\-CNI network model and it is required to use version v1.7.1 or higher VPC\-CNI cluster networking components.

* Kubernetes version v1.24.15\-vke.12 or higher, or version starts from v1.20.15\-vke.18 in v1.20 series is required. You can visit the console of the cluster and find the current version of Kubernetes in the cluster basic information page. See [How to find the Kubernetes version of a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster) for details.

* RDMA metrics feedback and RDMA topology\-aware scheduling are not available when using RDMA of an InfiniBand HPC cluster.

* If a NCCL network error occurs in an environment running RDMA, please refer to [FAQ](https://docs.byteplus.com/en/docs/vke/How_to_deal_with_the_error_ibv_create_cq_allocate_memory_in_a_RDMA_enabled_environment) for solutions.


<span id="cST51SR7"></span>
## Steps

<span id="ac22vrUp"></span>
### Step 1: Create HPC cluster


1. Log in to the [HPC cluster console](https://console.byteplus.com/ecs/hpcCluster).

2. Click **create HPC cluster** and finish configurations based on the parameter descriptions in the table below.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5a5ecbb79984756af4bac16861b1517.png) </span>


|**Parameters** |**Description** |
|---|---|
|Region and AZ |Intranets within different regions are completely isolated. It is recommended to select a region as close as possible to where your business is located to reduce network latency and improve access speed. AZ (Availability Zones) refers to areas isolated from each other in terms of electricity and network.<br><br>In this case, resources such as node subnets, instance types and HPC clusters are required to stay in a single availability zone. For example: Availability zone C. |
|Name |Enter a name for HPC cluster. |
|Cluster properties |Select a property for HPC cluster. Each property has its own limits. Select InfiniBand in this case.<br><br><br>* RoCE (RDMA over Converged Ethernet) is a network communication protocol designed based on Ethernet technology to realize Remote Direct Memory Access. It features high performance and high cost\-efficiency, suitable for data exchange among instances in an HPC cluster.<br><br>* InfiniBand is a network communication protocol designed based on dedicated network hardware to implement Remote Direct Memory Access, featuring high throughput and low latency, and suitable for data exchange among instances in an HPC cluster. Cluster property needs to be selected according to the instances.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">HPC clusters of infiniBand can only work with ecs.hpcpni3.45xlarge, which is one of the High Performance Computing Optimized instances. Apart from that one, all the remaining instances can be candidates for RoCE\-powered HPC clusters.</div><br><br><br>* <div data-tips="true" data-tips-type="default">InfiniBand clusters can only add or expand infiniBand\-powered instances. Similarly, RoCE clusters apply the same logic.</div><br> |
|Description |Provide descriptions or comments for the HPC cluster. |


<span id="ac22vrUp"></span>
### Step 2: Create a cluster and prepare resources

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This step only covers the key parts of configuring RDMA resources, such as creating a node pool, adding node labels, setting Kubelet custom parameters, and installing RDMA add\-ons. For creating and configuring a new cluster,see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Create a cluster</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke). Click **Cluster** in the left navigation bar to go to the cluster management page.

2. Click **Create cluster** and finish the configurations for the step 1 **cluster configuration**, then click **Next: node pool configuration**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b7ec6bd66485ab784f94b58e189c909.png) </span>

The table below contains instructions as well as descriptions of key parameters in this step. Please follow the instructions in the table and configure the rest as needed.


|**Parameters** |**Description** |
|---|---|
|Network model |Select a Container Network Interface (CNI) for the cluster. In this case, **VPC\-CNI is required.** <br><br><br>* **Flannel**: an independent underlay network model based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.<br><br>* **VPC\-CNI**: an underlay network model built based on Elastic Network Interfaces (ENI) on VPC, providing high network performance. |



3. On the Node pool configuration (optional) page, you need to finish key configurations, including settings of a new node pool, node labels, and Kubelet custom parameters. Click **Next: Addon configuration** when you finish all necessary settings on this page.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ed271f9b4754273c8eb56de7ad39fcd.png) </span>

The table below contains instructions as well as descriptions of key parameters in this step. Please follow the instructions in the table and configure the rest as needed.


|**Parameter** |**Description** |
|---|---|
|Worker node |Select **Create now**. |
|Node source |Select **Create node** in this case. |
|Availability zone |Availability zones (AZ) are physically isolated infrastructure units within a single region, featuring independent power and networking systems. AZs communicate over internal networks. Different regions have their own availability zones. See [Regions and Availability Zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones) for details.<br><br>In this case, resources such as node subnets, instance types and HPC clusters are required to stay in a single availability zone. For example: Availability zone C. |
|Node subnet |Select subnets available in the list for the nodes. |
|Instance type |Instance type defines resources such as CPU, memory, GPU, RDMA of a node. In this case, instance types enabled with RDMA device are required, e.g., High Performance Computing Optimized instances. |
|High Performance Computing Optimized |A cluster computing environment used to handle large\-scale computing tasks, typically consisting of a large number of worker nodes interconnected through a high\-speed RDMA network to process complex tasks collaboratively.<br><br>In this case, the InfiniBand\-powered HPC cluster created in step 1 should be selected. |
|Node labels |This is the same as the Label in Kubernetes, which is used to define attributes for nodes, facilitating later operations on nodes such as filtering. A label can be added to all the nodes in the pool in batch.<br><br>In this case, the label `vke.node.rdma.mode: {value}` is added manually to indicate what RDMA mode the node pool is working in. The available modes include ib\-shared (shared) and ib\-shared\-multi (1:N shared).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Except for <code>ecs.hpcg1ve.21xlarge</code> and North\-China <code>ecs.hpcpni2.28xlarge</code> , it is highly recommended to choose the ib\-shared mode for instance types.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The option <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool">Enable auto renew for node labels and taints</a> allows existing nodes in the pool to automatically update labels you added on this page. Caution! Disabling this option might make the cluster unable to use existing RDMA nodes in the pool.</div><br> |
|Kubelet configs |For businesses that are highly sensitive to latency, Kubelet custom parameters can be used to create NUMA affinity policy. The resources allocated for a Container (or Pod) can be mapped to one (or more) NUMA nodes to improve business performance.<br><br>In this case, the custom parameter `topologyManagerPolicy: best-effort` is required, so that  GPU and RDMA can be allocated to the same NUMA node. |



4. On the Addon configuration page, ensure that rdma\-device\-plugin is checked. Other add\-ons can be selected as needed. Click **Next: Configuration confirmation** to go to the next page.

5. Ensure that all the information of the new cluster and billing details are correct, read the "VKE Dedicated Service Terms" and click the checkbox to agree, then click **Confirm** on the page to start creating the cluster.


<span id="tJP8VddV"></span>
### Step 3: Use RDMA Resources


1. Connect to the cluster using kubectl. See [Connecting to cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) for details.

2. Use RDMA resources through YAML. The following example shows how to enable RDMA for a pod.


```YAML
apiVersion: v1
kind: Pod
metadata:
  name: rdma-test
spec:
  containers:
  - name: rdma-test
    image: busybox
    command:
    - /bin/sh
    - -c
    - sleep 10000
    resources:
      limits:
        vke.volcengine.com/infiniband-rdma: 1
    securityContext:
      capabilities:
        add:
        - IPC_LOCK
    volumeMounts:
      - mountPath: /dev/shm   
        name: cache-volume
      - name: nvidia-topology  # Non-bare metal instance types need to mount this directory. NCCL will obtain the real topology from virtualTopology.xml.
        mountPath: /var/run/nvidia-topologyd
        readOnly: true
  volumes:
  - emptyDir:
      medium: Memory
    name: cache-volume
  - name: nvidia-topology               
    hostPath:
      path: /var/run/nvidia-topologyd
      type: DirectoryOrCreate
```
