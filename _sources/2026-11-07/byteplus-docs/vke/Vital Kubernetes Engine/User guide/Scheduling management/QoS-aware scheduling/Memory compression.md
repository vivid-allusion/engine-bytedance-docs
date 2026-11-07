---
title: "Memory compression"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/memory-compression"
---

Memory compression is implemented based on the Katalyst add\-on. It can automatically detect and compress cold memory without affecting application containers, improving memory utilization. This topic describes how to enable and use memory compression in a VKE cluster.

<span id="YYVL5F6M"></span>
## Background

The memory requested by applications is often not planned rigorously. The actual frequently accessed hot memory, namely the Working Set Size, is usually less than 80% of the total requested amount, while the remainder is cold memory that stays resident for a long time but is rarely accessed. The kernel reclaims memory proactively only when memory thresholds are reached. As a result, in long\-running and high\-density deployment scenarios, a node may appear to be out of memory while a large amount of cold memory is actually idle, which becomes a major bottleneck to improving overall resource utilization.

VKE provides the memory compression feature based on the Katalyst add\-on to address the above issues.

<span id="XDKH81G7"></span>
## Limits

Take note of the following limitations and considerations when using this feature:


* This feature depends on Katalyst add\-on version v0.5.13\-vke.17 or later.

* This feature is only supported for Pods deployed on Elastic Compute Service (ECS). Pods deployed on Elastic Container Instance (VCI) are not supported.

* The node kernel version must meet one of the following requirements:

   * Cgroup v1 is used, and the node image must be veLinux 1.0. The kernel version must be 5.10.200\-5.6.ve1.x86_64 (CentOS\-compatible) or 5.10.200\-5\-velinux1u6\-amd64, or later.

   * Cgroup v2 is used, for example, in veLinux 2 or Ubuntu 22.04.


<span id="sApcEn2u"></span>
## Prerequisites


* The cluster is in the **Running** state and has available ECS nodes.

* Katalyst add\-on version v0.5.13\-vke.17 or later is installed, and the **memory compression** feature is enabled. For details, see [Katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).


<span id="Q8TASADo"></span>
## Procedure

<span id="HBDQEsJQ"></span>
### Step 1: Configure nodes for memory compression


1. Change the kubelet parameter **fail\-swap\-on** to **false**. For information about configuring the parameter for existing and new nodes, see [Configuring kubelet parameters for a node pool](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee693096805902999a349aa89fee1462.png) </span>

2. Configure node labels.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the target cluster.

   3. On the cluster management page, add labels to nodes as follows.

      
      <Tabs>
      <Tab zoneid="Z7Hns8TM" title="Add a label at the node pool level">
      <TabTitle>Add a label at the node pool level</TabTitle>
      
      1. In the left navigation pane, click **Nodes** \> **Node pool**.
      
      2. On the **Node pool** page, find the target node pool and click **Edit** in the **Actions** column.
      
      3. On the **Edit node pool** page, specify the **Node labels** parameter and select **Enable auto renew for node labels and taints** in the **Advanced settings** section in the **Node pool configuration** step. This change applies to all existing and subsequently added nodes in the node pool.
      
         * Label 1: `vke.node.katalyst.deploy: true` indicates that the Katalyst add\-on must be installed and used on the nodes.
      
         * Label 2: `vke.node.memory-compression: true` indicates that memory compression must be enabled on the nodes.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04630c3f5f0fa3bca841410215fa1d1d.png) </span>
      
      4. Update the configurations of the node pool based on the console wizard.
      
      
      </Tab>
      <Tab zoneid="YXZCldv3" title="Add a label at the node level">
      <TabTitle>Add a label at the node level</TabTitle>
      
      1. In the left navigation pane, click **Nodes** \> **Node**.
      
      2. On the **Node** page, find the target node and click `...` \> **Label management** in the **Actions** column.
      
      3. On the **Node details page**, click **Add new** on the **Label** tab, add the following label to the node, and then click **Confirm**.
      
         * Label 1: `vke.node.katalyst.deploy: true` indicates that the Katalyst add\-on must be installed and used on the nodes.
      
         * Label 2: `vke.node.memory-compression: true` indicates that memory compression must be enabled on the nodes.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eb9ee4c37bf6fbcd9b64ad5381291b58.png) </span>
      
      
      </Tab>
      </Tabs>
      

3. Verify that memory compression is enabled on the node.

   1. Log in to the node using the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

   2. Run the following commands to confirm that the Linux virtual memory compression feature (zram) has been initialized on the node.

      * Confirm that the zram device itself has been created.

         ```Bash
         zramctl
         
         # The expected response is as follows:
         NAME       ALGORITHM  DISKSIZE    DATA   COMPR   TOTAL  STREAMS  MOUNTPOINT
         /dev/zram0 lzo-rle      61.6G    296M  239.4M  246.9M       32  [SWAP]
         ```
         

      * Confirm that zram has been enabled as swap.

         ```Bash
         swapon --show
         
         # The expected response is as follows:
         NAME       TYPE       SIZE   USED PRIO
         /dev/zram0 partition 61.6G 392.8M  100
         ```
         


<span id="UUWV2KIg"></span>
### Step 2: Create a workload

The following example demonstrates how to create a Deployment. For information about creating other workloads, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).


1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following sample file `stress-ng.yaml` serves as an example.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: stress-ng  # Deployment name.
     namespace: default  # The namespace of the Deployment.
     labels:
       app: stress-ng
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: stress-ng
     template:
       metadata:
         labels:
           app: stress-ng
           vke.pod.memory-compression: "true"  # Whether to enable memory compression. Value: true (enabled) or false (disabled).
         annotations:
           katalyst.kubewharf.io/qos_level: shared_cores # (Optional) The marker indicating whether the application is online or offline. Value: shared_cores (default value, online application) or reclaimed_cores (offline application).
       spec:
         nodeSelector:  # Node selector. This ensures that the Deployment is scheduled to nodes where memory compression is enabled, that is, the nodes configured in Step 1.
           vke.node.memory-compression: "true"
         containers:
           - name: stress-ng
             image: doc-cn-beijing.cr.volces.com/vke/stress-ng:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
             imagePullPolicy: IfNotPresent
             resources:
               requests:
                 cpu: "2"
                 memory: 4Gi
               limits:
                 cpu: "4"
                 memory: 8Gi
             command:
               - /usr/bin/stress-ng
               - --vm
               - "2"
               - --vm-bytes
               - 3G
               - --vm-keep
               - --vm-hang
               - "0"
               - --metrics-brief
               - --timeout
               - 3600s
   ```
   

3. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f stress-ng.yaml
   ```
   


<span id="Jl1Mxngb"></span>
### Step 3: Verify the configuration

You can confirm whether memory compression has been enabled for the Pod by checking zram usage, Cgroup memory usage, and more. For more verification and monitoring methods, see the [Memory compression monitoring](https://docs.byteplus.com/en/docs/vke/memory-compression#KTtSdvMs) section in this topic.


1. Run the following command to view the node where the Pod is scheduled.

   ```Bash
   kubectl get pod <pod-name> -o wide
   ```
   

2. Log in to the node where the Pod has been scheduled using the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

3. Run the following command to check zram usage.

   ```Bash
   zramctl
   
   # Example response:
   NAME       ALGORITHM DISKSIZE  DATA   COMPR TOTAL STREAMS MOUNTPOINT
   /dev/zram0              61.6G  2.3G 1002.5M    1G      32 <swap>
   ```
   

4. Run the following command to view the Pod's memory usage reduced through memory compression.

   If there is a difference between `memory.memsw.usage_in_bytes` and `memory.usage_in_bytes`, the Pod's cold memory has been successfully compressed into zram.

   ```Bash
   echo $(( $(cat /sys/fs/cgroup/memory/kubepods/burstable/podxxxxxx/memory.memsw.usage_in_bytes) - $(cat /sys/fs/cgroup/memory/kubepods/burstable/podxxxxxx/memory.usage_in_bytes) ))
   # Replace podxxxxxx with the actual Cgroup directory name of the target Pod (based on the Pod UID).
   
   # Expected return value in bytes: After conversion, 2047434752 ÷ 1024 ÷ 1024 ≈ 1952 MiB ≈ 2 GiB:
   2047434752
   ```
   


<span id="XJ0iw5ea"></span>
## Appendix

<span id="hOPrERlH"></span>
### Memory compression configuration instructions

Memory compression\-related configurations are stored in the TransparentMemoryOffloadingConfiguration (TMO) CRD. When memory compression is enabled, the system automatically creates a default configuration file: `katalyst-system/tmo-default`. To further adjust the memory compression feature, edit TransparentMemoryOffloadingConfiguration as needed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Adjust parameters based on the comments in the YAML file. We recommend keeping the default values for parameters without comments.</div>


```YAML
apiVersion: config.katalyst.kubewharf.io/v1alpha1
kind: TransparentMemoryOffloadingConfiguration
metadata:
  labels:
    vke.node.katalyst.deploy: "true"
  name: tmo-default
  namespace: katalyst-system
spec:
  config:
    podSelector:   # Specifies which Pods should enable memory compression.
      labelSelector:
        matchLabels:
          vke.pod.memory-compression: "true"           
 #   namespaceSelector:   # Specifies that all Pods in a namespace enable memory compression. To adjust this setting, delete the # marker before the parameter.
 #     matchLabels:
 #       tmo.enabled: "true"
 #     matchExpressions:
 #       - key: environment
 #         operator: In
 #         values:
 #           - production
 #           - staging
    qosLevelConfig:   # You can configure memory compression policies independently for each Katalyst QoSLevel.
    - configDetail:
        enableSwap: true  # Memory compression capability switch, values: true (Open), false (Default value, Close). When writing a custom TMO CRD, this switch must be set to true.
        enableTMO: true  # Whether to write a custom TMO CRD related to memory compression configuration, values: true (Open), false (Default value, Close).
        swappiness: 160  # When the kernel performs memory reclaim, this parameter controls the preference for reclaiming anonymous pages or file-backed pages. Valid values range from 0 to 200. The closer the value is to 0, the more likely the kernel is to reclaim file-backed pages. Otherwise, it is more likely to reclaim anonymous pages.
 #       swapMaxOvercommitRatio: 0.3  # Maximum proportion by which swap usage plus memory usage can exceed the memory limit.
 #       psiPolicy:
 #         maxProbe: 0.05  # Maximum memory reclaim proportion per round.
 #         psiAvg60Threshold: 0.1  # As the Pod PSI approaches this value, reclaim intensity weakens.
 #       refaultPolicy:
 #         maxProbe: 0.05  # Maximum memory reclaim proportion per round.
 #         reclaimAccuracyTarget: 0.99  # Continue increasing reclaim when reclaim accuracy is higher than this value.
 #         reclaimScanEfficiencyTarget: 0.6  # Continue increasing reclaim when reclaim efficiency is higher than this value.
      qosLevel: reclaimed_cores
    - configDetail:
        enableSwap: true
        enableTMO: true
        swappiness: 80
      qosLevel: shared_cores
  nodeLabelSelector: vke.node.memory-compression=true
  priority: 10
```


<span id="KTtSdvMs"></span>
### Memory compression monitoring metrics

Memory compression monitoring metrics are as follows. To monitor the feature, you need to [enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) and configure [container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability), then select the following memory compression\-related metrics in the Katalyst metric list. After enabling metric observability, you can view the metrics in the [preset dashboard](https://console.byteplus.com/observe/dashboard/dashboard/2927/view?type=builtin).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Enabling the following metrics incurs VMP fees. For detailed billing information, see <a href="https://docs.byteplus.com/en/docs/vmp/billing-overview">Product billing</a>.</div>



|**Object** |**Metric name** |**Meaning** |
|---|---|---|
|Pod / Container |katalyst_memory_offloading_target_bytes |Target reclaim amount calculated by the TMO policy, representing the number of bytes of memory expected to be offloaded from the target object in the current round. |
||katalyst_memory_handler_offloading_requested_bytes |Volume of reclaim requests actually received and submitted to asynchronous execution queues by the TMO execution side. |
||katalyst_memory_handler_offloading_reclaimed_bytes |Memory usage reduction observed after execution of `memory.reclaim`, representing the actual reclaim effect of the current round. |
||katalyst_memory_offloading_unavailable_total |Number of times TMO is considered temporarily unavailable on the policy side, distinguished by `reason` such as metric missing, high node pressure, `mapped file` protection trigger, or policy abnormality. |
||katalyst_memory_handler_offloading_unavailable_total |The number of times TMO is considered temporarily unavailable on the execution side, distinguished by `reason` for causes such as `memory.reclaim` failure, unsupported `swappiness`, `swap limit` setting failure, zram not ready, or Cgroup path abnormality. |
||katalyst_memory_cgroup_reclaim_direct |Periodic increase in memory reclaim events directly triggered for the target object. |
||katalyst_memory_cgroup_reclaim_kswapd_bytes |Periodic increase in the number of bytes reclaimed by the background `kswapd` for the target object. |
||katalyst_memory_cgroup_oom |Periodic increase in the number of OOM events for the target object. |
|Node |zram_orig_data_size_bytes |The size of the original data stored in zram. |
||zram_compr_data_size_bytes |Size of compressed data stored in zram. Use this metric together with `zram_orig_data_size_bytes` to calculate compression gains. |
||zram_disksize_bytes |Logical capacity of the zram device exposed to swap. |
||zram_mem_used_bytes |The actual memory size occupied by the zram device. |
||zram_mem_limit_bytes |Maximum memory available to the zram device. |
||zram_mem_used_max_bytes |Peak memory usage of the zram device. |
||zram_unavailable |Indicates that zram is unavailable. The `reason` label distinguishes causes such as initialization in progress, precheck failure, and startup failure. |
||zram_same_pages |Count of identical\-content pages in zram (indicates compression/deduplication efficacy). |
||zram_pages_compacted_total |Cumulative count of pages compressed and organized by zram. |
||zram_huge_pages |Number of large pages in zram that cannot be efficiently compressed. A high value may indicate reduced compression gains. |
||zram_failed_reads_total |Cumulative number of zram read failures. |
||zram_failed_writes_total |Total number of zram write failures. |
||zram_invalid_io_total |Cumulative number of invalid I/O operations for zram. |
||zram_notify_free_total |Cumulative number of page\-release notifications received by zram. |
||zram_comp_algorithm_info |Current zram compression algorithm information (with the `algorithm` label). |
||zram_bd_count_pages |Number of pages occupied by the zram backing device. |
||zram_bd_reads_total |Cumulative number of reads from the zram backing device. |
||zram_bd_writes_total |Cumulative number of writes to the zram backing device. |
