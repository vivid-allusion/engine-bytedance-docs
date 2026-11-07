---
title: "How do I provision cloud disk PVs when a cluster contains nodes of various ECS instance specifications?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_to_use_cloud_disk_PersistentVolumes_in_a_cluster_with_nodes_of_different_specifications"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

In a VKE cluster, worker nodes are fully compatible with ECS instances of new specifications. For details, see [Product announcement](https://docs.byteplus.com/en/docs/vke/Product_announcements).

A cluster may contain ECS nodes of various specifications. In such cases, the compatibility between different ECS specifications and cloud disk types is as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">VKE no longer supports creating StorageClasses, PersistentVolumes, and PersistentVolumeClaims of the Performance SSD (PTSSD) type. Existing PTSSD resources are not affected and can continue to be used until they are deleted.</div>


* <div data-tips="true" data-tips-type="warning">EBS no longer supports creating PTSSD volumes. Therefore, exercise caution when choosing instance families that are still available for sale and only support mounting PTSSD volumes. Existing PTSSD volumes are not affected.</div>


* The following ECS instance families support mounting only **PTSSD** volumes: General\-purpose g1, Compute\-optimized c1, Memory\-optimized r1, Big Data d1s, GPU\-accelerated g1t, and High Performance Computing GPU hpcg1v.

* ECS specifications that support mounting only **ESSD** volumes: Except for the specifications listed above, all other ECS instance specifications supported by VKE use ESSD volumes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the list of ECS instance specifications supported by VKE. To access it, log in to the <a href="https://console.byteplus.com/vke">VKE console</a> and go to the <strong>Create node pool</strong> page of the target cluster.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about ECS instance specifications, see <a href="https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types">Instance specifications</a>.   </div>
   


<span id=".6Zeu6aKY5b2x5ZON6K-05piO"></span>
## Impacts

When ECS nodes of multiple specifications are present in a cluster, if cloud disks are not used as described in this topic, the following issues may occur:

For example, you create [a static PersistentVolume (PV)](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes) of the **ESSD** type and associate this PV with a PersistentVolumeClaim (PVC). When you later create a workload (such as a Deployment), you mount and use this PVC. In this case, without any node affinity scheduling configuration, the pod corresponding to the workload may be scheduled to an older\-specification ECS node in the cluster. Since the volume cannot be properly mounted to the older\-specification ECS instance, the created pod will remain in the **Pending** state and fail to run normally.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

This part demonstrates how to create a Deployment. The procedure for creating other workloads is similar.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the target cluster and click its name.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node** to view the **specifications** of individual nodes.

4. Create a Deployment by following the steps described in [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   Configure the parameters below as described:

   * **Basic information**

      Configure the parameters according to your requirements. For parameter details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * **Container configuration**

      In the **Storage configuration** section, select and mount the target PVC. For other parameters, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * **Advanced settings**

      In the **Scheduling policy** section, enable **Node affinity scheduling** to schedule the workload that mounts the PV to a node of the supported specification. For more configuration instructions, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

      * If you select and mount a PV of the **ESSD** type in the **Storage configuration** section in the **Container configuration** step, add the new specifications obtained in Step 3, such as `ecs.c1ie.large` and `ecs.g1ie.8xlarge`.

      * If you select and mount a PV of the **PTSSD** type in the **Storage configuration** section in the **Container configuration** step, add the old specifications obtained in Step 3, such as `ecs.c1.large` and `ecs.g1.large`.
