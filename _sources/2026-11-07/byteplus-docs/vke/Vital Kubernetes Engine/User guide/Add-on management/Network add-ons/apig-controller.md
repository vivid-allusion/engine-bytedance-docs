---
title: "apig-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/apig-controller-add-on"
---

apig\-controller is an Ingress controller add\-on built based on the cloud\-native API Gateway (APIG). It provides full lifecycle management and Layer 7 traffic routing. This topic describes how to install and upgrade the apig\-controller add\-on and lists related considerations.

<span id="m8nKULQ2"></span>
## Add\-on overview

apig\-controller serves as the core APIG add\-on for VKE in cloud\-native scenarios. Deeply integrated with the cloud\-native APIG capabilities, the add\-on monitors in\-cluster Ingresses and gateway\-related custom resources and dynamically converts them into APIG forwarding rules and configurations. Compared with traditional self\-managed gateways, it eliminates the burden of separate gateway node O&M and provides high\-performance, reliable API traffic management and security protection for microservices.

When the add\-on is installed, the system runs the corresponding controller workload in your cluster and registers the following CRDs:


|**Resource name** |**Resource type** |**Resource description** |
|---|---|---|
|apig\-controller |Deployment |The core Pods of the add\-on. The resource monitors Ingress resources within the cluster and automatically manages underlying APIG instances in the cloud. |
|apiginstance |CRD |The CRD resource that manages and monitors the lifecycle of cloud\-native APIG instances. For details, see [Creating APIG Ingresses by using kubectl](https://docs.byteplus.com/en/docs/vke/Create_an_APIG_Ingress_using_kubectl). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="ixeVmp93"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   

5. Click **Confirm** to finish configuration.


<span id="8bXLY7Jq"></span>
## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="2anoj1sS"></span>
## Related documentation


* [Ingress overview](https://docs.byteplus.com/en/docs/vke/Ingress-overview)

* [APIG Ingress](https://docs.byteplus.com/en/docs/vke/APIG-Ingress)
