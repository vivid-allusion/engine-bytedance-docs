---
title: "keda"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/keda-add-on"
---

The keda add\-on provides an autoscaler driven by Kubernetes events to enhance the capability of elastic scaling. This topic describes how to deploy and use the keda add\-on in a cluster.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This add\-on is currently in <strong>public beta</strong>.</div>


<span id="AyByjxsC"></span>
## Add\-on overview

The keda add\-on is a Kubernetes\-based event\-driven autoscaler that provides fine\-grained resource management capabilities for VKE clusters. The core capabilities and advantages of the add\-on are as follows:


* Event\-driven scale\-out: KEDA supports automatic scale\-out based on various event sources. It is capable of handling sudden workload surges or responding to unpredictable demand spikes.

* Custom metric\-based scale\-out: Differing from HPA, KEDA can scale based on custom metrics. It provides higher flexibility when defining scale\-out triggers for application requirements.

* Resource efficiency: When no workloads exist, KEDA can scale replicas to zero. This effectively reduces resource consumption and costs.


The keda add\-on is suitable for event\-driven or serverless architecture applications that need to scale based on the number of messages in queues or topics. For example, topology reporting in RDMA scenarios and CPU core binding in NUMA\-aware scheduling.

<span id="hSJpGtI8"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/keda).

<span id="j0eWFiWx"></span>
## Install the add\-on

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This add\-on can be installed only in clusters of the following versions:</div>



* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24">Kubernetes v1.24</a>: v1.24.10\-vke.12 and later</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26">Kubernetes v1.26</a>: v1.26.10\-vke.13 and later</div>


* <div data-tips="true" data-tips-type="warning">Other later Kubernetes versions</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Node Label Selector |After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Node forced scheduling |After this feature is enabled, you can configure required node affinity. The core workloads of the add\-on are forcibly scheduled to nodes that satisfy all specified labels. If no node in the cluster meets the conditions, the core workloads will remain in the Pending state and cannot be scheduled. |
   |Resource configuration |Specify the CPU requests, CPU limits, memory requests, and memory limits of various resources in the add\-on. |
   


<span id="nn9rNZlh"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays **Upgradable**, we recommend promptly upgrading it. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For the upgrade procedure and considerations, see [Upgrading the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="vDbbDCjk"></span>
## Monitoring and alerting

<span id="l6uPfm87"></span>
### Add\-on observability

The stability and performance of the keda add\-on directly affect the functionality and effectiveness of your cluster. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="9W4QAYAO"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="SbyBBWY9"></span>
## Related documentation


* [Event-driven autoscaling (KEDA)](https://docs.byteplus.com/en/docs/vke/Horizontal_Pod_Autoscaler_based_on_event-driven-KEDA)
