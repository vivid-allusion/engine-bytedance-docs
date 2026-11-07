---
title: "pod-identity-webhook"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/pod-identity-webhook-add-on"
---

As an automated add\-on in VKE clusters, pod\-identity\-webhook assists in implementing IRSA capabilities. This topic describes how to deploy and use the pod\-identity\-webhook add\-on in a cluster.

<span id="2JzhaXTh"></span>
## Add\-on overview

The pod\-identity\-webhook is an auxiliary add\-on for the IAM Role for Service Account (IRSA) feature. Its core capabilities and advantages are as follows:


* Automated injection of IRSA configuration: During the Mutating Admission stage of Pod creation, IRSA\-related configurations are automatically injected into eligible Pods, allowing users to use IRSA capabilities without manually modifying Pod YAML.

* Flexible configuration: Fine\-grained management can be achieved through namespace labels, ServiceAccount annotations, and Pod annotations. For example, enabling or disabling automatic injection, specifying associated IAM roles, setting OIDC token validity periods, and limiting which containers are injection targets.

* Feature compatibility: Environment variable injection and Volume injection are supported.


The pod\-identity\-webhook is a managed add\-on. By default, it does not deploy specific Kubernetes resources in your business cluster and does not consume compute resources on cluster nodes.

<span id="gZCmdhTZ"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/pod-identity-webhook).

<span id="QYs3NGML"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.


<span id="062zeFjm"></span>
## Upgrading add\-ons

You do not need to be concerned about upgrade issues for system\-managed add\-ons. System\-managed add\-ons prevent issues such as add\-on faults and unsatisfactory performance caused by users. It reduces user maintenance costs and enhances add\-on stability.

<span id="TPHagc1i"></span>
## Related documentation


* [IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview)

* [Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters)
