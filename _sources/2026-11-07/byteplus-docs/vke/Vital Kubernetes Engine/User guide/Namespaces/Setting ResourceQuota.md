---
title: "Setting ResourceQuota"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Setting-ResourceQuotas"
---

The ResourceQuota of a namespace is used in scenarios where multiple teams or users share cluster resources. It limits the total amount of resources available to teams or users. For example, it limits the total amount of specific types of objects (container and service) that can be created and the total amount of compute resources (CPU and memory) in a namespace.

<span id="qseL482u"></span>
## Usage instructions

If you do not specify a ResourceQuota for a namespace, workloads deployed in the namespace can use computing, GPU, storage, and other cluster resources without limitation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A namespace has been created in the VKE cluster. For instructions, see [Creating namespaces](https://docs.byteplus.com/en/docs/vke/Creating-a-namespace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation bar.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Namespace**.

5. In the namespace list, find the target namespace and click `...` \> **Set ResourceQuota** in the **Actions** column.

6. Set ResourceQuota for the namespace, such as CPU requests, memory requests, CPU limits, and memory limits.

   
   |Type |Name |Description |
   |---|---|---|
   |Compute ResourceQuota |CPU request |Specify the upper limit for the total CPU requests of all pods in the `running` or `waiting` state in the namespace. |
   ||Memory request |Specify the upper limit for the total memory requests of all pods in the `running` or `waiting` state in the namespace. |
   ||CPU limit |Specify the upper limit for the total CPU of all pods in the `running` or `waiting` state in the namespace. |
   ||Memory limit |Specify the upper limit for the total memory of all pods in the `running` or `waiting` state in the namespace. |
   |GPU ResourceQuota |GPU quota |Specify the maximum total number of GPUs on all nodes in the namespace. |
   ||mGPU quota |[Public beta] Specify the maximum total number of mGPUs that containers can share across all nodes in the namespace. |
   |Storage ResourceQuota |Total amount of storage requests |Specify the upper limit for the total storage resource requests of all PVCs in the namespace. |
   ||Number of PersistentVolumeClaims |Specify the maximum number of PVCs in the namespace. |
   |Other ResourceQuota |Number of Pods |Specify the maximum total number of pods in the `running` or `waiting` state in the namespace. |
   ||Number of Secrets |Specify the maximum number of Secrets in this namespace. |
   ||Number of ConfigMaps |Specify the maximum number of ConfigMaps in the namespace. |
   ||Number of Services |Specify the maximum number of services in the namespace. |
   

6. After the configuration is complete, click **Confirm**.

   After you set ResourceQuota for the namespace, find the target namespace in the namespace list. Click **View details** in the **ResourceQuota** column to view the ResourceQuota information and resource usage.


&nbsp;

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip</div>


<div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you set ResourceQuota using kubectl or the native Kubernetes API (not via the console), ensure the names of ResourceQuota and Namespace are consistent. Otherwise, you won't be able to view ResourceQuota details after clicking <strong>View details</strong> in the console.</div>
