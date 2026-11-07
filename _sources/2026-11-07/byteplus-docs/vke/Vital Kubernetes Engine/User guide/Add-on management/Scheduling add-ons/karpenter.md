---
title: "karpenter"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/karpenter-add-on"
---

karpenter is the real\-time autoscaling add\-on for VKE. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="KubGNGy5"></span>
## Add\-on overview

karpenter is an open\-source Kubernetes node lifecycle management add\-on that intelligently provisions optimal nodes in real time for Pods unschedulable due to resource constraints. Compared with the traditional Cluster Autoscaler (CA), the karpenter add\-on delivers faster responses, more flexible resource selection policies, and higher resource utilization. For more details, see [Node autoscaling overview](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works).

As a managed add\-on, karpenter deploys no Kubernetes resources in your cluster and consumes zero computing resources on cluster nodes.

<span id="KvxWcNFP"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/karpenter).

<span id="3rzBTq4B"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Automatic scale\-in |After you enable this feature, automatic scale\-in is triggered if a certain number of idle nodes exist. This feature only applies to **pay\-as\-you\-go** nodes.<br><br><br>* **Scale\-in threshold for non\-GPU nodes**: Automatic scale\-in may be triggered if the CPU or memory utilization of a non\-GPU node is lower than the threshold. The utilization is calculated by using the following formula: `single resource usage/single resource total amount × 100%`. The value is an integer. Valid values: 0 to 100. When the value is 0, it indicates that scale\-in is not triggered.<br><br>* **Scale\-in threshold of GPU nodes**: The scale\-in policies of GPU nodes vary based on whether the mGPU capability is enabled. The value is an integer. Valid values: 0 to 100. When the value is 0, it indicates that scale\-in is not triggered.<br><br>   * mGPU disabled: automatic scale\-in may be triggered if the GPU resource usage (calculated with `single resource request amount ÷ single resource total amount * 100%`) of a node falls below this threshold.<br><br>   * mGPU enabled: automatic scale\-in may be triggered if the usage (calculated with `single resource request amount ÷ single resource total amount * 100%`) of any resources in mGPU, including GPU computing power, GPU video memory, system memory, and CPU, falls below this threshold.<br><br>* **Scale\-in trigger latency**: Automatic scale\-in is triggered if the node resource utilization remains lower than the threshold for the specified period. The value is an integer. Valid values: 1 to 60. Unit: **minutes**.<br><br>* **Pod termination timeout**: The maximum wait time for pod termination during node draining. The value is an integer. Valid values: 1 to 10000. Unit: **seconds**. |
   

5. Click **Confirm** to finish configuration.


<span id="jcSmi0Zl"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="s8B8zML8"></span>
## Related documentation


* [Cluster autoscaler overview](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works)

* [Configure the instant elasticity of nodes (Karpenter)](https://docs.byteplus.com/en/docs/vke/Configure_node_instant_autoscaler_Karpenter)
