---
title: "Configuring custom scheduling parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters"
---

Vital Kubernetes Engine (VKE) supports custom parameters for the scheduler\-plugin add\-on. This allows you to specify custom scheduler behavior to meet your pod scheduling requirements. This topic describes how to configure custom scheduler parameters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The scheduler\-plugin add\-on has been installed. For detailed operations, see [scheduler-plugin](https://docs.byteplus.com/en/docs/vke/scheduler-plugin-add-on).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

Only clusters that use the following Kubernetes versions support custom scheduler parameters:


* [Kubernetes V1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.6\-vke.7 or later.

* [Kubernetes V1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.15\-vke.18 or later.

* Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE.


If your Kubernetes version does not meet the requirements, upgrade the control plane of your cluster. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

<span id=".YmlucGFjay1zcHJlYWQt562W55Wl6LWE5rqQ5p2D6YeN6YWN572u"></span>
## Resource weights in Binpack and Spread policies

After you configure a node scheduling policy, you can specify custom resource weights for the Binpack and Spread scheduling policies.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the cluster that you need to configure.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. On the **Scheduling** tab, find the scheduler\-plugin and click **Configuration**.

5. In the **Node scheduling policy** section, modify the **Resource weight** configuration as needed. 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no custom resource weight is configured, the  Binpack/Spread policy uses the default weight 1 for CPU and memory resources.   </div>
   

   
   |Parameters |Description |
   |---|---|
   |Resources |The following resource types are supported:<br><br><br>* **CPU**<br><br>* **Memory**<br><br>* **GPU** (evaluated based on the computing power of NVIDIA\-type GPU resources)<br><br>* **mGPU** (evaluated based on the computing power of mGPU resources)<br><br>* **GPU (NPU\-A2)** <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">VKE follows the resource weight policy of native Kubernetes. For details, see <a href="https://kubernetes.io/docs/concepts/scheduling-eviction/resource-bin-packing/#enabling-bin-packing-using-requestedtocapacityratio">RequestedToCapacityRatio</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you configure GPU and mGPU resource weights, you can combine node scheduling with GPU card scheduling. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters#.YmlucGFjay1zcHJlYWQt6LCD5bqm562W55Wl57uE5ZCI6K-05piO">Combinations of Binpack and Spread scheduling policies</a>.</div><br> |
   |Weight |The weight of a selected resource ranges from 1 to 10. A higher weight produces a higher score. That means when the system schedules pods to a node, the available capacity of the target resource on the node is prioritized. |
   


<span id=".YmlucGFjay1zcHJlYWQt6LCD5bqm562W55Wl57uE5ZCI6K-05piO"></span>
## Combinations of Binpack and Spread scheduling policies

If your workload involves GPU compute nodes and GPU cards, you can combine the two scheduling policies as described below:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Node\-level Binpack and Spread scheduling policies are effective for both mGPU and regular GPUs.</div>



|Node scheduling policy |GPU card scheduling policy |Scheduling mode |Application scenario |
|---|---|---|---|
|Spread (default) |Binpack (default) |* Pods are spread to nodes with low GPU allocation rate.<br><br>* Containers are preferentially scheduled to GPUs with high packing rates on nodes. |High fault isolation performance is achieved among nodes and a small number of fragmented resources exist. |
|Spread |Spread |* Pods are spread to nodes with low GPU allocation rate.<br><br>* Containers are prioritized for GPU cards with low packing rates on the node. |Nodes and GPU cards have strong fault isolation, but fragmented resources are relatively abundant. It is applicable to high\-availability scenarios. |
|Binpack |Binpack |* Pods are prioritized for nodes with high GPU allocation rates.<br><br>* Containers are preferentially scheduled to GPUs with high packing rates on the node. |Fault isolation is relatively weak, but resource fragmentation is minimal. This prevents resource waste caused by resource fragmentation from shared services. It is applicable to GPU high\-utilization scenarios. |
|Binpack |Spread |* Pods are preferentially scheduled to nodes with high GPU allocation rates.<br><br>* Containers are prioritized for GPU cards with low packing rates on the node. |GPU cards have strong fault isolation, and a large number of fragmented resources exist. |
