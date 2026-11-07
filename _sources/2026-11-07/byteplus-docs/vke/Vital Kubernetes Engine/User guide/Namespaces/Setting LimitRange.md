---
title: "Setting LimitRange"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Setting-LimitRanges"
---

LimitRange in a namespace facilitates the appropriate allocation and management of resources to improve the utilization and availability of cluster resources. This topic describes how to set LimitRange for a namespace.

<span id="GULswXBg"></span>
## Usage instructions


* When you create or update a Pod in a namespace, if you do not specify ResourceQuotas for the resources, such as CPU and memory of a container, Kubernetes will apply the LimitRange set for the namespace to the container.

* If you do not specify a LimitRange for the namespace, objects (e.g., Pods, Containers, PersistentVolumeClaims) in it can use namespace or cluster resources without limit.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A namespace has been created in the VKE cluster. For instructions, see [Creating namespaces](https://docs.byteplus.com/en/docs/vke/Creating-a-namespace).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. Click **Cluster** in the left navigation bar.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Namespace**.

5. In the namespace list, find the target namespace and click `...` \> **Set LimitRange** in the **Actions** column.

6. Set LimitRange for the namespace.

   
   |**Type** |**Name** |**Description** |
   |---|---|---|
   |Container LimitRange |Default CPU request |The minimum CPU request that will be applied to each container in the namespace if you do not specify a CPU limit for containers. |
   ||Default CPU limit |The maximum CPU limit that will be applied to each container in the namespace if you do not specify a CPU limit for containers. |
   ||Default memory request |The minimum memory request that will be applied to each container in the namespace if you do not specify a memory limit for containers. |
   ||Default memory limit |The maximum memory limit that will be applied to each container in the namespace if you do not specify a memory limit for containers. |
   ||Minimum CPU |Set the minimum CPU usage of the container. The values of **Default CPU request and Default CPU limit** must be greater than or equal to **Minimum CPU** and cannot be left empty. |
   ||Maximum CPU |Set the maximum CPU usage of the container. The values of **Default CPU request and Default CPU limit** must be less than or equal to **Maximum CPU** and cannot be left empty. |
   ||Minimum memory |Set the minimum memory usage of the container. The values of **Default memory request and Default memory limit** must be greater than or equal to the value of **Minimum memory**, and cannot be left empty. |
   ||Maximum memory |Set the maximum memory usage of the container. The values of **Default memory request and Default memory limit** must be less than or equal to the value of **Maximum memory**, and cannot be left empty. |
   |Pod LimitRange |Maximum CPU |The maximum CPU usage of the pod. |
   ||Maximum memory |The maximum memory usage of the pod. |
   |PersistentVolumeClaim LimitRange |Minimum storage request |The minimum storage usage of the PersistentVolumeClaim (PVC). |
   ||Maximum storage request |The maximum storage usage of the PVC. |
   

6. After the configuration is complete, click **Confirm**.

   After you set LimitRange for the namespace, find the target namespace in the namespace list, and click **View details** in the **LimitRange** column to view the LimitRange information of the namespace.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you set LimitRange via kubectl or the native Kubernetes API (not in the console), ensure the LimitRange name matches the Namespace name. Otherwise, you won't view the LimitRange details after you click <strong>View details</strong> in the console.   </div>
