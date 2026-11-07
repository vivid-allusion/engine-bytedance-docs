---
title: "vpc-cni-controlplane"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vpc-cni-controlplane-add-on"
---

vpc\-cni\-controlplane is a control\-plane management add\-on for clusters that use the VPC\-CNI network model. This add\-on is suitable for advanced networking scenarios, such as configuring independent security groups for Pods and dynamically binding EIPs. This topic describes the basic features, limits, and configuration guidelines of the vpc\-cni\-controlplane add\-on.

<span id="1mPiuB3Q"></span>
## Add\-on overview

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This add\-on is mandatory when you create a cluster with the Trunk ENI feature enabled.</div>


vpc\-cni\-controlplane is a core control\-plane add\-on provided by VKE for clusters that use the VPC\-CNI network model. By collaborating with underlying network interfaces, it processes container network logic on the control plane in clusters and provides more refined, advanced network resource scheduling capabilities for Pods. Its core capabilities include:


* **Pod\-level security group management**: Configures and binds dedicated security groups for individual Pods to achieve finer\-grained network isolation control.

* **Dynamic EIP allocation and binding**: Automatically applies for and binds EIPs based on annotations during Pod creation to enable independent public network access for Pods.

* **Trunk ENI support**: Serves as the control plane base for the Trunk ENI networking feature, ensuring high\-density, highly isolated network communication scheduling.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">‌This is a managed component.‌ It deploys no Kubernetes resources in your cluster and consumes zero computing resources on cluster nodes.</div>


<span id="I3SfKgrf"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/vpc-cni-controlplane).

<span id="JZRWFUy3"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Bind EIP to pods |Specify whether to bind EIP to pods. For details, see [Binding independent EIP to pods](https://docs.byteplus.com/en/docs/vke/Associating-an-EIP-with-a-pod). |
   |Static IP for pods |Specify whether to assign static IP addresses to pods. For details, see [Assigning static IP addresses to pods](https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod). |
   

5. Click **Confirm** to finish configuration.


<span id="9Xa2trOg"></span>
## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="NBiXLr7j"></span>
## Related documentation


* [Binding dedicated EIP to pods](https://docs.byteplus.com/en/docs/vke/Associating-an-EIP-with-a-pod)

* [Elastic network interface dedicated to a pod with Trunk ENI](https://docs.byteplus.com/en/docs/vke/Using-Trunk-ENI-to-enable-the-exclusive-ENI-mode-for-pods)

* [Configuring Static IPs for pods](https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod)
