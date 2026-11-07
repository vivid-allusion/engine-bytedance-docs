---
title: "core-dns"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/core-dns-add-on"
---

core\-dns is a built\-in domain resolution add\-on for clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="6JmTyqYS"></span>
## Add\-on overview

core\-dns is a mandatory DNS add\-on for VKE clusters. When Services or Pods in a cluster need to communicate with each other, they access each other via Service names, for example, `service-demo.default.svc.cluster.local`. The core\-dns add\-on implements in\-cluster domain name resolution by translating Service names into actual internal IP addresses, ensuring smooth connectivity across the entire business architecture.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|coredns |Deployment |The core workload of the add\-on. It receives, processes, and forwards DNS resolution requests within the cluster. |
|kube\-dns |Service |The fixed access endpoint (ClusterIP) that exposes the in\-cluster DNS service. All Pods in the cluster use the endpoint to send resolution requests. |
|coredns |ConfigMap |The core resolution configuration (Corefile) of the add\-on. It supports custom internal domain resolution rules or external DNS forwarding policies. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="CFlGZgzK"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/core-dns).

<span id="ibeEkw5B"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **DNS** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Resource configuration |Configure the add\-on resource quotas, including the CPU request, CPU limit, memory request, and memory limit. |
   

5. Click **Confirm** to finish configuration.


<span id="XPhK9iLj"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="31CiZyqv"></span>
## Monitoring and alerting

<span id="rJOxKWeN"></span>
### Add\-on observability

The stability and performance of the core\-dns add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard mainly displays the resource usage and health of the core\-dns add\-on, including CPU usage, memory usage, UP status, and QPS metrics for each workload. You can specify a custom time range for querying information and set the information refresh mode to manual or automatic refresh.


1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Network services monitoring** \> **Core\-DNS monitoring** to view the monitoring dashboard. 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83de158f74508c45ab6b9fecb9d32916.png) </span>


<span id="nfHNUZcy"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="sa7F25Y2"></span>
## Related documentation


* [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en)

* [CoreDNS best practices](https://docs.byteplus.com/en/docs/vke/CoreDNS-best-practices)
