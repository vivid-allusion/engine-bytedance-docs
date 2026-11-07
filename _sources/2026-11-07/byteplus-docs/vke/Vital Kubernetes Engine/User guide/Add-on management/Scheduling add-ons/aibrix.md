---
title: "aibrix"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/aibrix-add-on"
---

As a part of a solution suite for generative artificial intelligence (GenAI) inference infrastructure, the aibrix add\-on provides the GPU workload autoscaling capability. This topic describes how to deploy and use the aibrix add\-on in a cluster.

<span id="0qhazpHr"></span>
## Add\-on overview

AIBrix is an open\-source Kubernetes\-based inference framework developed by ByteDance. It is used to provide core add\-ons for building scalable large model inference infrastructure. VKE provides the aibrix add\-on, which is mainly used in the AI cloud\-native inference suite, ServingKit. In managed clusters for heterogeneous computing in the ServingKit scenario, the aibrix add\-on provides an efficient, low\-cost, and scalable solution for large‑scale deployment of enterprise‑grade large models. It achieves this by leveraging multiple capabilities, such as optimized resource scheduling, adaptive scaling, cache‑aware routing, and heterogeneous computing management.

<span id="Byd0c9ry"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/aibrix).

<span id="7HauOkF1"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed.<br><br>You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   


<span id="9483rkIf"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays **Upgradable**, we recommend promptly upgrading it. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="r4DGgxpB"></span>
## Monitoring and alerting

<span id="58hmtuZe"></span>
### Add\-on observability

The stability and performance of the aibrix add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="n1WezgdJ"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="1Ti3LEiE"></span>
## Related documentation


* [ServingKit overview](https://docs.byteplus.com/en/docs/vke/Servingkit_overview)

* [Creating a managed heterogeneous computing cluster](https://docs.byteplus.com/en/docs/vke/Creating_a_managed_heterogeneous_computing_cluster)
