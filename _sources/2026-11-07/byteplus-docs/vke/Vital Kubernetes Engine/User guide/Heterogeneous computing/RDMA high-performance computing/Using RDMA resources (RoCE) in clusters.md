---
title: "Using RDMA resources (RoCE) in clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters"
---

Vital Kubernetes Engine (VKE) can use Remote Direct Memory Access (RDMA) resources through add\-ons to eliminate bottlenecks of computing tasks brought by traditional network communication. This topic introduces how a VKE cluster uses RDMA resources provided by RDMA over Converged Ethernet (RoCE) high\-performance compute (HPC) clusters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[public beta]: VKE clusters featured with access to RDMA resources are currently in public beta.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id="FB6mYRWw"></span>
### RDMA overview


* RDMA is a high\-performance network protocol that reduces CPU usage and memory bandwidth bottlenecks, as well as improves bandwidth utilization. It comes with the following advantages:

   * **Zero Copy**: Applications can transfer data without involving the network software stack, allowing data to be directly sent to the buffer or directly received from the buffer without being copied to the network layer.

   * **Kernel Bypass**: RDMA provides a proprietary Verbs interface, allowing applications to transfer data directly from user space without switching context between kernel and user modes.

   * **CPU Offload**: Applications can access memory on remote hosts without consuming any CPU there. Remote memory will be read without any help from remote processes (or CPUs), and the content read from them will not be written into the remote CPU caches.

* The High Performance Compute (HPC) cluster is a cluster computing environment used to handle large\-scale computing tasks, usually composed of a large number of compute nodes interconnected by an RDMA high\-speed network. It supports both RoCE and InfiniBand.

   An HPC cluster can provide powerful computing capability, large memory, high\-speed storage, and networks to meet the demands of compute\-intensive, data\-intensive, or combined workloads. In an HPC cluster, computing tasks are assigned to each compute node for parallel processing, fully utilizing the computing power of multiple nodes to accelerate computation and improve efficiency. For details, see [HPC cluster overview](https://docs.byteplus.com/en/docs/gpu/HPC-cluster-overview).


<span id="TOxsmFyq"></span>
### RDMA add\-on mode

In the RoCE network mode, the RDMA add\-on supports the following modes. The following table describes different modes and their usage restrictions.


|**RDMA add\-on mode** |**Mode description** |**Usage limits** |
|---|---|---|
|shared |Create a shared virtual network interface for pods in the cluster by virtualizing the RDMA physical network interface. |* Each RDMA physical network interface can only provide one shared virtual network interface.<br><br>* The RDMA NIC mask needs to be less than 30, such as `/29` and `/28`. |
|shared\-multi |Create multiple shared virtual network interfaces for pods as needed in the cluster by virtualizing the RDMA physical network interface. |* We recommend that you do not use this mode with GPUs.<br><br>* The RDMA NIC mask needs to be less than 30, such as `/29` and `/28`. |
|shared\-host |All RDMA NICs in the host are plugged into containers as IPVLAN sub\-interfaces and provided to pods in the container cluster.<br><br><div data-tips="true" data-tips-type="tip">Description</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently in beta. To use it, submit an application.</div><br> |* Katalyst topology scheduling is not supported.<br><br>* The RDMA NIC mask needs to be less than 30, such as `/29` and `/28`.<br><br>* To use the shared\-host mode, the add\-on version needs to meet the following requirements:<br><br>   * Upgrade the rdma\-device\-plugin add\-on to v3.5.1\-vke.12 or later version.<br><br>   * Upgrade the vpc\-cni add\-on to v1.8.9 or later version. |
|exclusive | **[Not recommended] ** RDMA physical NICs are directly assigned to pods in the container cluster. This method applies to scenarios where physical devices cannot be virtualized or partitioned. |* This mode cannot be used in the vePFS scenario.<br><br>* Performance degradation occurs when some models use this mode. We do not recommend that you use this mode if no forcible dependency exists, such as the scenario where a model uses the BF3 mini NIC.<br><br>* New models introduced after 2026 are not guaranteed to support this mode. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If your pods need to use HostNetwork, we recommend that you use RDMA resources provided by open source add\-ons. For details, see the <a href="https://github.com/Mellanox/k8s-rdma-shared-dev-plugin">open source documentation</a>.</div>


<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

The following document introduces the officially proven practices. To achieve the expected results and comply with the Vital Kubernetes Engine (VKE) [Limits](https://docs.byteplus.com/en/docs/vke/Limits), you need to strictly follow the procedures (or operate on the recommended resources) in this document. If you want to use another solution, consult your account manager.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* A pod cannot use mGPU and RDMA add\-ons simultaneously.

* RDMA devices can be used only in clusters with the VPC\-CNI network model, and the vpc\-cni add\-on must be upgraded to v1.7.1 or later version.

* The Kubernetes version of the cluster must meet the following requirements: If the cluster version is outdated, upgrade it first. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

   * Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE

   * [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.15\-vke.12 or later

   * [Kubernetes v1.20](https://docs.byteplus.com/en/docs/6460/108842): v1.20.15\-vke.18 or later

* For the methods and the restrictions on using RDMA topology\-aware scheduling, see [RDMA topology-aware scheduling](https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling).

* If a NCCL network error occurs in an environment running RDMA, please refer to [FAQ](https://docs.byteplus.com/en/docs/vke/How_to_deal_with_the_error_ibv_create_cq_allocate_memory_in_a_RDMA_enabled_environment) for solutions.


<span id=".5pON5L2c5q2l6aqk77ya5paw5bu66LWE5rqQ77yI5o6o6I2Q77yJ"></span>
## Procedure: Create resources (recommended)

We recommend that you use RDMA resources when you create a VKE cluster and node pool. The detailed steps are as follows.

<span id=".5q2l6aqk5LiA77ya5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
### Step 1: Create an HPC cluster


1. Log in to the [HPC cluster console](https://console.byteplus.com/ecs/hpcCluster).

2. Click **Create HPC cluster** and finish configurations based on the parameter descriptions in the table below.

   
   |Parameter |Description |
   |---|---|
   |Region and AZ |Intranets within different regions are completely isolated. It is recommended to select a region as close as possible to where your business is located to reduce network latency and improve access speed. AZ (Availability Zones) refers to areas isolated from each other in terms of electricity and network.<br><br>In this case, resources such as node subnets, instance types, and HPC clusters are required to be in a single availability zone. For example: Availability zone C. |
   |Name |Enter a name for HPC cluster. |
   |Cluster properties |Select a property for HPC cluster. Each property has its own limits. RoCE is selected in this scenario.<br><br><br>* RoCE (RDMA over Converged Ethernet) is a network communication protocol designed based on Ethernet technology to realize Remote Direct Memory Access. It features high performance and high cost\-efficiency, suitable for data exchange among instances in an HPC cluster.<br><br>* InfiniBand is a network communication protocol designed based on dedicated network hardware to implement Remote Direct Memory Access, featuring high throughput and low latency, and suitable for data exchange among instances in an HPC cluster. Cluster property needs to be selected according to the instances.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">HPC clusters of infiniBand can only work with <code>ecs.hpcpni3.45xlarge</code>, which is one of the High Performance Computing Optimized instances. Apart from that one, all the remaining instances can be candidates for RoCE\-powered HPC clusters.<code></code></div><br><br><br>* <div data-tips="true" data-tips-type="tip">InfiniBand clusters can only add or expand infiniBand\-powered instances. Similarly, RoCE clusters apply the same logic.</div><br> |
   |Description |Provide descriptions or comments for the HPC cluster. |
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu66ZuG576k5bm25YeG5aSH6LWE5rqQ"></span>
### Step 2: Create a cluster and prepare resources

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This step only covers the key parts of configuring RDMA resources, such as creating a node pool, adding node labels, setting Kubelet custom parameters, and installing RDMA add\-ons. For how to create and configure a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating clusters</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click **Create cluster** and specify the required parameters.

   The table below contains instructions as well as descriptions of key parameters in this step. Please follow the instructions in the table and configure the rest as needed.

   
   |**Parameter** |**Description** |
   |---|---|
   |Network model |Select a Container Network Interface (CNI) for the cluster. In this case, **VPC\-CNI is required.** <br><br><br>* **Flannel**: an independent underlay network model based on which a high\-performance network for clusters can be built along with the global routing capabilities of VPCs.<br><br>* **VPC\-CNI**: an underlay network model built based on Elastic Network Interfaces (ENI) on VPC, providing high network performance. |
   

3. On the Node pool configuration (optional) page, you need to finish key configurations, including settings of a new node pool, node labels, and Kubelet custom parameters. Click **Next: Addon configuration** when you finish all necessary settings on this page.

   The table below contains instructions as well as descriptions of key parameters in this step. Please follow the instructions in the table and configure the rest as needed.

   
   |**Parameter** |**Description** |
   |---|---|
   |Node pool management |Select **Create now**. |
   |ECS node source |Select **Create node** in this case. |
   |Availability zone |Availability Zones (AZs) are physically isolated infrastructure units within a single region, featuring independent power and networking systems. AZs communicate with each other over internal networks. Different regions have their own availability zones. See [Regions and Availability Zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones) for details.<br><br>In this case, resources such as node subnets, instance types, and HPC clusters are required to be in a single availability zone. For example: Availability zone C. |
   |Node subnet |Select subnets available in the list for the nodes. |
   |Instance type |Instance type defines resources such as CPU, memory, GPU, RDMA of a node. In this case, instance types enabled with RDMA device are required, e.g., High Performance Computing Optimized instances. |
   |High\-performance computing cluster |A cluster computing environment used to handle large\-scale computing tasks, typically consisting of a large number of worker nodes interconnected through a high\-speed RDMA network to process complex tasks collaboratively.<br><br>In this scenario, the RoCE HPC cluster created in Step 1 is selected. |
   |Node labels |Labels in VKE function identically to Kubernetes labels. Labels can be used to define attributes for nodes, facilitating node operations and management. A label can be added in batches to all the nodes in the node pool.<br><br>In this scenario, manually add the label `vke.node.rdma.mode: {value}` to configure the RDMA mode for nodes or the node pool. The following modes are available: exclusive, shared, shared\-multi, and shared\-host.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Except for ecs.hpcg1ve.21xlarge and North\-China ecs.hpcpni2.28xlarge, we recommend that you select the shared mode for instance types.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can select or deselect <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool">Enable auto renew for node labels and taints</a> to determine whether to synchronously add new labels to existing nodes in the pool. Caution! Disabling this option might make the cluster unable to use existing RDMA nodes in the pool.</div><br> |
   |Kubelet configs |For businesses that are highly sensitive to latency, Kubelet custom parameters can be used to create a NUMA affinity policy. The resources allocated for a container or pod can be mapped to one or more NUMA nodes to improve business performance.<br><br><br>* If the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), you need to add the custom parameter `topologyManagerPolicy: best-effort`. This ensures that GPU and RDMA can be allocated to the same NUMA node.<br><br>* When the RDMA mode is shared\-host, no additional configuration is required. |
   

4. In the Addon configuration step, select the rdma\-device\-plugin add\-on and configure other add\-ons based on your business requirements. Click **Next: Confirm Configuration** to go to the next page.

5. After confirming that the cluster information and billing details are correct, read the Vital Kubernetes Engine Specific Terms of Service, select the checkbox to accept them, and then click **Confirm** to start creating the cluster.


<span id=".5q2l6aqk5LiJ77ya5L2_55SoLXJkbWEt6LWE5rqQ"></span>
### Step 3: Use RDMA Resources

After the cluster is created, RDMA resources can be used when workloads are being created. In this scenario, a Deployment is used as an example.


<Tabs>
<Tab zoneid="edHwNthmIh" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane of the cluster management page, click **Workload \> Deployment** to go to the Deployment management page.

3. Click **Create Deployment**. In the ResourceQuota section in the Container configuration step, specify the number of RDMA cards based on your business requirements. For the descriptions of other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), we recommend that you set the number of RDMA cards to the total number of cards in the host or half the number to achieve optimal performance for GPU training or inference tasks. For example, when the host has four RDMA NICs, you can set the number of RDMA cards to 2 or 4. When the system has eight RDMA NICs, you can set the number of RDMA cards to 4 or 8.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can use the shared\-host mode if you do not want to be concerned about the number of RDMA NICs. You cannot configure the shared\-host mode in the console. To use this mode, you can configure it by using the YAML configuration based on the following instructions.   </div>
   


</Tab>
<Tab zoneid="QUF8TsMfoB" title="Configuring through YAML">
<TabTitle>Configuring through YAML</TabTitle>

* When the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), execute the following YAML code to configure RDMA resources for the pod.

   * In the `spec.containers.resources` field, use `vke.volcengine.com/rdma` to apply for RDMA NIC for the pod.

   * In the pod annotation, use `k8s.volcengine.com/pod-networks` to specify the number of NICs. We recommend setting the number of RDMA cards to the total number of cards in the host, or half the number to achieve optimal performance for GPU training or inference tasks. For example, when the host has four RDMA NICs, you can set the number of RDMA cards to 2 or 4. When the system has eight RDMA NICs, you can set the number of RDMA cards to 4 or 8.

   * In most cases, you need to use the `spec.containers.securityContext` field to request the IPC_LOCK privilege.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: rdma-test
     annotations:
       k8s.volcengine.com/pod-networks: |
         [
           {
             "cniConf":{
                 "name":"rdma"
             }
           }
         ]
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
           vke.volcengine.com/rdma: 1
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
   

   The preceding sample code provides an example of how to automatically create an RDMA NIC. To create multiple RDMA NICs, copy the code block in `k8s.volcengine.com/pod-networks` multiple times.

   ```YAML
   {
       "cniConf":{
           "name":"rdma"
       }
   }
   ```
   

* When the RDMA mode is shared\-host, execute the following YAML code to configure RDMA resources for the pod.

   * In the `spec.containers.resources` field, use `vke.volcengine.com/rdma-host` to apply for the RDMA resources of the entire host for the pod. The value is 1 and cannot be changed.

   * In the pod annotation, use `k8s.volcengine.com/pod-networks` to specify the number of NICs. Differing from other modes, the shared\-host mode allows you to configure only one code block. If you configure more than one code block, an error will occur.

   * In most cases, you need to use the `spec.containers.securityContext` field to request the IPC_LOCK privilege.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: rdma-test
     annotations:
       k8s.volcengine.com/pod-networks: |
         [
           {
             "cniConf":{
                 "name":"rdma"
             }
           }
         ]
   spec:
     containers:
     - name: rdma-test
       image: busybox
       command:
       - /bin/sh
       - -c
       - sleep 10000
       resources:
         requests:
           vke.volcengine.com/rdma-host: 1
         limits:
           vke.volcengine.com/rdma-host: 1
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
   





</Tab>
</Tabs>


When you run NCCL in the container in shared mode, you need to explicitly specify the NCCL_IB_GID_INDEX environment variable. You can execute the `source nccl_env.sh` command to obtain the RDMA environment variables. The content of the sample script `nccl_env.sh` for dynamically obtaining NCCL environment variables is as follows.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure that the configuration of NCCL_IB_GID_INDEX is valid. You can execute the show_gids command to obtain the gid index for RoCE v2 IPv4. The script invoked by the show_gids command is available on the host.</div>


```Bash
#!/usr/bin/env bash

devs=()
ports=()
idxes=()
rdmaIdx=""
rdmaRate=""
rdmaErr=""

function scan_devices() {
    allocDevs=()
    for d in $(ls /sys/class/infiniband/) ; do
      allocDevs+=($d)
    done
    for d in "${allocDevs[@]}" ; do
      for p in $(ls /sys/class/infiniband/$d/ports/) ; do
        for g in $(ls /sys/class/infiniband/$d/ports/$p/gids/) ; do
        gid=$(cat /sys/class/infiniband/$d/ports/$p/gids/$g);
        if [ $(echo $gid | cut -d ":" -f -1) != "0000" ] ; then
          continue
        fi
        if [ $gid = 0000:0000:0000:0000:0000:0000:0000:0000 ] ; then
          continue
        fi

        RoCEVer=$(cat /sys/class/infiniband/$d/ports/$p/gid_attrs/types/$g 2>/dev/null| grep -o "[Vv].*")
        if [ ${RoCEVer,,} != "v2" ]; then
          continue
        fi

        # device not Up
        ethDev=$(cat /sys/class/infiniband/$d/ports/$p/gid_attrs/ndevs/$g 2>/dev/null)
        if [[ ! -f /sys/class/net/$ethDev/dev_id ]] || [[ ! -f /sys/class/net/$ethDev/carrier ]] || (( ! $(cat /sys/class/net/$ethDev/carrier 2> /dev/null) == 1 )); then
          continue
        fi

        mtu=$(cat /sys/class/net/$ethDev/mtu 2>/dev/null)
        if [[ -z "$mtu" ]] || (( mtu <= 1500 )); then
          continue
        fi

        devs+=($d)
        ports+=($p)
        idxes+=($g)
        done #g (gid)
      done #p (port)
    done #d (dev)
    if [[ -z $devs ]]; then
      echo "Not found RDMA device, list devices error"
      return 1
    fi
}

function export_nccl_env() {
  scan_devices
  if [[ -z $devs ]]; then
    echo "Not found RDMA device, get max rate device error"
    return 1
  fi
  for ((i=0; i<${#devs[@]}; i+=1)); do
    rate=$(cat /sys/class/infiniband/${devs[i]}/ports/${ports[i]}/rate 2>/dev/null|cut -f 1 -d " ")
    if [[ -z "$rdmaRate" ]] || [[ "$rate" -gt "$rdmaRate" ]]; then
      rdmaDevs=(${devs[i]})
      rdmaPorts=(${ports[i]})
      rdmaIdx=${idxes[i]}
      rdmaErr=""
      rdmaRate=$rate
    elif [[ "$rate" == "$rdmaRate" ]]; then
      rdmaDevs+=(${devs[i]})
      rdmaPorts+=(${ports[i]})
      if [[ "$rdmaIdx" != "${idxes[i]}" ]]; then
        rdmaErr="rdma devs index inconsistent"
      fi
    fi
  done

  if [[ -n $rdmaErr ]]; then
      echo $rdmaErr
      return 1
  fi

  hca=()
  for ((i=0; i<${#rdmaDevs[@]}; i+=1)); do
    hca+=("${rdmaDevs[i]}:${rdmaPorts[i]}")
  done
  IFS=","
  export NCCL_IB_HCA=${hca[*]}
  unset IFS

  export NCCL_IB_GID_INDEX=$rdmaIdx
}

export_nccl_env
```


<span id="MaB2muw1"></span>
## Procedure: Existing resources

If you have already created a VKE cluster and node pool, you can directly use RDMA resources in the existing VKE cluster and node pool by performing the following steps.

<span id=".5q2l6aqk5LiA77ya5a6J6KOFLXJkbWEt6K6-5aSH5o-S5Lu2"></span>
### Step 1: Install the RDMA device add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane, click **Addons**. Find the `rdma-device-plugin` add\-on on the **Network** tab.

3. Move the pointer over the add\-on card and click **Deploy** to install the RDMA device add\-on in the cluster.


<span id=".5q2l6aqk5LqM77ya5YeG5aSH6IqC54K56LWE5rqQ"></span>
### Step 2: Prepare node resources

Prepare nodes that support RDMA devices, such as High Performance Computing Optimized nodes. You can create nodes or use existing nodes that meet your business requirements. Manually add the label `vke.node.rdma.mode: {value}` to configure the RDMA usage mode for nodes or the node pool. The following modes are available: exclusive, shared, shared\-multi, and shared\-host.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Except for ecs.hpcg1ve.21xlarge and North\-China ecs.hpcpni2.28xlarge, we recommend that you select the shared mode for instance types.</div>


* <div data-tips="true" data-tips-type="warning">If you switch the RDMA mode by modifying the label, make sure that all existing workloads have finished running, and restart the nodes to make the new mode take effect.</div>



<span id=".5pa55byP5LiA77ya5a2Y6YeP6IqC54K55re75Yqg5qCH562-"></span>
#### Step 1: Add a label to an existing node


1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane, click **Nodes** \> **Node**. Find the target node and in the Actions column, click `...` \> **Label management**.

3. Click **Add new** to add the preceding label to the existing node. Then, click **Confirm** to save the configurations.

   The following sample code shows the YAML content.

   ```YAML
   type: Node
   label:
       vke.node.rdma.mode: shared
    status:
      capacity:
        vke.volcengine.com/rdma: 4
   ```
   


<span id=".5pa55byP5LqM77ya6IqC54K55rGg5re75Yqg6IqC54K55qCH562-"></span>
#### Method 2: Add node labels to the node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane, click **Nodes** \> **Node pool** to create a node pool, or click **Edit** in the Actions column that corresponds to the target cluster. Add node labels to the node pool and then click **Confirm** to save the configurations.


<span id=".5q2l6aqk5LiJ77ya5L-u5pS56IqC54K5LWt1YmVsZXQt5ouT5omR566h55CG562W55Wl"></span>
### Step 3: Modify the kubelet topology management policy of the node

The node kubelet topology management policy varies based on the RDMA mode.


* If the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), you need to configure a node kubelet topology management policy and add the custom parameter `topologyManagerPolicy: best-effort`. This ensures that GPU and RDMA can be allocated to the same NUMA node. 

* When the RDMA mode is shared\-host, you do not need to configure a node kubelet topology management policy.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">When you modify custom kubelet parameters for an existing node pool, the configurations only take effect on new nodes and do not apply to existing nodes by default. To apply changes to existing nodes, you need to synchronize the configurations for existing nodes. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool">Existing node configuration synchronization</a>.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane, click **Nodes** \> **Node pool** to go to the node pool management page.

3. Click the name of the target node pool. On the **Kubelet configs** tab, click **Edit** in the upper\-right corner to manually add parameters. Then, click **Confirm** to save the configurations. 

   The following sample code shows the YAML content.

   ```YAML
   topologyManagerPolicy: best-effort
   ```
   


<span id=".5q2l6aqk5Zub77ya5L2_55SoLXJkbWEt6LWE5rqQ"></span>
### Step 4: Use RDMA resources

After the configurations are complete, RDMA resources can be used when workloads are being created. In this scenario, a Deployment is used as an example.


<Tabs>
<Tab zoneid="rkzeqwtGQB" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation pane of the cluster management page, click **Workload \> Deployment** to go to the Deployment management page.

3. Click **Create Deployment**. In the ResourceQuota section in the Container configuration step, specify the number of RDMA cards based on your business requirements. For other workload configurations, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), we recommend that you set the number of RDMA cards to the total number of cards in the host or half the number to achieve optimal performance for GPU training or inference tasks. For example, when the host has four RDMA NICs, you can set the number of RDMA cards to 2 or 4. When the system has eight RDMA NICs, you can set the number of RDMA cards to 4 or 8.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can use the shared\-host mode if you do not want to be concerned about the number of RDMA NICs. You cannot configure the shared\-host mode in the console. To use this mode, you can configure it by using the YAML configuration based on the following instructions.   </div>
   


</Tab>
<Tab zoneid="DglCziNaIz" title="Configuring through YAML">
<TabTitle>Configuring through YAML</TabTitle>

* When the RDMA mode is exclusive, shared, or shared\-multi (1:N shared), execute the following YAML code to configure RDMA resources for the pod.

   * In the `spec.containers.resources` field, use `vke.volcengine.com/rdma` to apply for RDMA NIC for the pod.

   * In the pod annotation, use `k8s.volcengine.com/pod-networks` to specify the number of NICs. We recommend setting the number of RDMA cards to the total number of cards in the host, or half the number to achieve optimal performance for GPU training or inference tasks. For example, when the host has four RDMA NICs, you can set the number of RDMA cards to 2 or 4. When the system has eight RDMA NICs, you can set the number of RDMA cards to 4 or 8.

   * In most cases, you need to use the `spec.containers.securityContext` field to request the IPC_LOCK privilege.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: rdma-test
     annotations:
       k8s.volcengine.com/pod-networks: |
         [
           {
             "cniConf":{
                 "name":"rdma"
             }
           }
         ]
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
           vke.volcengine.com/rdma: 1
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
   

   The preceding sample code provides an example of how to automatically create an RDMA NIC. To create multiple RDMA NICs, copy the code block in `k8s.volcengine.com/pod-networks` multiple times.

   ```YAML
   {
       "cniConf":{
           "name":"rdma"
       }
   }
   ```
   

* When the RDMA mode is shared\-host, execute the following YAML code to configure RDMA resources for the pod.

   * In the `spec.containers.resources` field, use `vke.volcengine.com/rdma-host` to apply for the RDMA resources of the entire host for the pod. The value is 1 and cannot be changed.

   * In the pod annotation, use `k8s.volcengine.com/pod-networks` to specify the number of NICs. Differing from other modes, the shared\-host mode allows you to configure only one code block. If you configure more than one code block, an error will occur.

   * In most cases, you need to use the `spec.containers.securityContext` field to request the IPC_LOCK privilege.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: rdma-test
     annotations:
       k8s.volcengine.com/pod-networks: |
         [
           {
             "cniConf":{
                 "name":"rdma"
             }
           }
         ]
   spec:
     containers:
     - name: rdma-test
       image: busybox
       command:
       - /bin/sh
       - -c
       - sleep 10000
       resources:
         requests:
           vke.volcengine.com/rdma-host: 1
         limits:
           vke.volcengine.com/rdma-host: 1
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
   





</Tab>
</Tabs>


When you run NCCL in the container in shared mode, you need to explicitly specify the NCCL_IB_GID_INDEX environment variable. You can execute the `source nccl_env.sh` command to obtain the RDMA environment variables. The content of the sample script `nccl_env.sh` for dynamically obtaining NCCL environment variables is as follows.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure that the configuration of NCCL_IB_GID_INDEX is valid. You can execute the show_gids command to obtain the gid index for RoCE v2 IPv4. The script invoked by the show_gids command is available on the host.</div>


```Bash
#!/usr/bin/env bash

devs=()
ports=()
idxes=()
rdmaIdx=""
rdmaRate=""
rdmaErr=""

function scan_devices() {
    allocDevs=()
    for d in $(ls /sys/class/infiniband/) ; do
      allocDevs+=($d)
    done
    for d in "${allocDevs[@]}" ; do
      for p in $(ls /sys/class/infiniband/$d/ports/) ; do
        for g in $(ls /sys/class/infiniband/$d/ports/$p/gids/) ; do
        gid=$(cat /sys/class/infiniband/$d/ports/$p/gids/$g);
        if [ $(echo $gid | cut -d ":" -f -1) != "0000" ] ; then
          continue
        fi
        if [ $gid = 0000:0000:0000:0000:0000:0000:0000:0000 ] ; then
          continue
        fi

        RoCEVer=$(cat /sys/class/infiniband/$d/ports/$p/gid_attrs/types/$g 2>/dev/null| grep -o "[Vv].*")
        if [ ${RoCEVer,,} != "v2" ]; then
          continue
        fi

        # device not Up
        ethDev=$(cat /sys/class/infiniband/$d/ports/$p/gid_attrs/ndevs/$g 2>/dev/null)
        if [[ ! -f /sys/class/net/$ethDev/dev_id ]] || [[ ! -f /sys/class/net/$ethDev/carrier ]] || (( ! $(cat /sys/class/net/$ethDev/carrier 2> /dev/null) == 1 )); then
          continue
        fi

        mtu=$(cat /sys/class/net/$ethDev/mtu 2>/dev/null)
        if [[ -z "$mtu" ]] || (( mtu <= 1500 )); then
          continue
        fi

        devs+=($d)
        ports+=($p)
        idxes+=($g)
        done #g (gid)
      done #p (port)
    done #d (dev)
    if [[ -z $devs ]]; then
      echo "Not found RDMA device, list devices error"
      return 1
    fi
}

function export_nccl_env() {
  scan_devices
  if [[ -z $devs ]]; then
    echo "Not found RDMA device, get max rate device error"
    return 1
  fi
  for ((i=0; i<${#devs[@]}; i+=1)); do
    rate=$(cat /sys/class/infiniband/${devs[i]}/ports/${ports[i]}/rate 2>/dev/null|cut -f 1 -d " ")
    if [[ -z "$rdmaRate" ]] || [[ "$rate" -gt "$rdmaRate" ]]; then
      rdmaDevs=(${devs[i]})
      rdmaPorts=(${ports[i]})
      rdmaIdx=${idxes[i]}
      rdmaErr=""
      rdmaRate=$rate
    elif [[ "$rate" == "$rdmaRate" ]]; then
      rdmaDevs+=(${devs[i]})
      rdmaPorts+=(${ports[i]})
      if [[ "$rdmaIdx" != "${idxes[i]}" ]]; then
        rdmaErr="rdma devs index inconsistent"
      fi
    fi
  done

  if [[ -n $rdmaErr ]]; then
      echo $rdmaErr
      return 1
  fi

  hca=()
  for ((i=0; i<${#rdmaDevs[@]}; i+=1)); do
    hca+=("${rdmaDevs[i]}:${rdmaPorts[i]}")
  done
  IFS=","
  export NCCL_IB_HCA=${hca[*]}
  unset IFS

  export NCCL_IB_GID_INDEX=$rdmaIdx
}

export_nccl_env
```


<span id="60WOlgoO"></span>
## Validate results

<span id="VX4jyGnF"></span>
### Viewing information about RDMA NIC

After you create a pod and configure RDMA resources, you can view the RDMA NIC mounted to the pod in the console or in YAML. This topic provides an example of how to view NIC information in the console.


1. Click the name of the target pod to go to the pod details page.

2. Click the **Overview** tab. In the **Networking** section, you can view the information about the RDMA NIC mounted to the pod.

3. In the upper right corner of the pod details page, click `...` \> **Edit Yaml** to view the YAML configuration of the pod. You can view information about the RDMA NIC mounted to the pod, such as the IP address and MAC address.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the RDMA add\-on mode is exclusive, the RDMA NIC on the host is in the Down state.   </div>
   

<span id="VX4jyGnF"></span>
### Viewing RDMA monitoring data

You can check whether the allocated RDMA resources have been used based on the metrics provided in RDMA monitoring data. For the method of viewing RDMA monitoring data, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability) or [Viewing instance GPU/RDMA monitoring data](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data).
