---
title: "vci-virtual-kubelet"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet-add-on"
---

The vci\-virtual\-kubelet add\-on schedules and runs Vital Container Instance (VCI) instances through virtual nodes. This topic describes how to deploy and use the vci\-virtual\-kubelet add\-on in a cluster.

<span id="TUIhToV7"></span>
## Add\-on overview

The vci\-virtual\-kubelet add\-on is implemented based on the community Virtual Kubelet project and functions as the scheduling adapter for VCI. After the add\-on is installed, a virtual node is automatically created in the VKE cluster. exposes the Serverless container computing power of VCI to the Kubernetes scheduler as virtual nodes. After the scheduler schedules Pods onto this virtual node, vci\-virtual\-kubelet translates operations such as Pod creation, running, and status synchronization into API calls to VCI. As a result, Pods run on VCI as they are scheduled onto ordinary ECS nodes.

The vci\-virtual\-kubelet is a managed add\-on. By default, it does not deploy specific Kubernetes resources in your business cluster and does not consume compute resources on cluster nodes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This add\-on is required for VCI. If you need to use VCI in a VKE cluster, install this add\-on.</div>


<span id="eguhb9nU"></span>
## Add\-on versions

For the vci\-virtual\-kubelet add\-on, the release notes, new features added in each version, and optimization descriptions are provided. For details, see [Add-on release notes](https://docs.byteplus.com/en/docs/vke/vci-virtual-kubelet).

<span id="eXLlAOfA"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Inventory awareness frequency |Adjust the frequency of queries of inventory information for VCI. We recommend that you set the value to 60s for the first time.<br><br>For the description of the VCI inventory\-aware scheduling feature, see [VCI inventory-aware scheduling](https://docs.byteplus.com/en/docs/vke/VCI-inventory-aware-scheduling). |
   


<span id="pkRuwfoV"></span>
## Upgrading add\-ons

You do not need to be concerned about upgrade issues for system\-managed add\-ons. System\-managed add\-ons prevent issues such as add\-on faults and unsatisfactory performance caused by users. This reduces user maintenance costs and enhances add\-on stability.

<span id="fPxsjym3"></span>
## Related documentation


* [Virtual Kubelet and virtual nodes](https://docs.byteplus.com/en/docs/vke/Virtual-Kubelet-and-virtual-nodes)
