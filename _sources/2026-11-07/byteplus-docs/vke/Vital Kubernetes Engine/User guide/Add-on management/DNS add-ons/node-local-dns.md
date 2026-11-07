---
title: "node-local-dns"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/node-local-dns-add-on"
---

The node\-local\-dns add\-on provides node\-level DNS caching proxy capabilities for VKE clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="pjFaeV0i"></span>
## Add\-on overview

node\-local\-dns is a DNS add\-on provided by VKE based on the NodeLocal DNSCache solution in the community. By deploying a DNS caching proxy on each cluster node, it improves the performance and stability of DNS service discovery in large\-scale clusters.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|node\-local\-dns |DaemonSet |A DNS cache proxy running on each node provides DNS service for the pods on that node, improving cluster DNS performance. |
|node\-local\-dns\-admission |Deployment |Enables automatic injection of NodeLocal dnsConfig into pods. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="8L2RtpaH"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/node-local-dns).

<span id="gro37BtI"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **DNS** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Default not inject configuration |Configure whether to inject DNSConfig into Pods by default.  <br><br><br>* **Enable**: By default, DNSConfig is not injected into Pods. To inject DNSConfig, add the `dns-config-injection=enable` label to the Pods or namespace as needed.<br><br>* **Disable**: By default, DNSConfig is injected into Pods. This is the default setting for general scenarios. After the node\-local\-dns add\-on is installed in the cluster, the system injects DNSConfig into Pods and prioritizes the local DNS cache.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When injection is <strong>disabled</strong>, you can still add the <code>dns-config-injection=disable</code> label to the Pods or namespace to prevent DNSConfig injection. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache">Using NodeLocal DNSCache as a DNS caching proxy</a>.</div><br> |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Replicas |Configure the default replica count for the node\-local\-dns\-admission resource. |
   |Resource configuration |Configure the add\-on resource quotas, including the CPU request, CPU limit, memory request, and memory limit. |
   

5. Click **Confirm** to finish configuration.


<span id="DTmA5zNr"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="dotQHLWl"></span>
## Monitoring and alerting

<span id="jpxexMHf"></span>
### Add\-on observability

The stability and performance of the node\-local\-dns add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the resource usage and health status of the node\-local\-dns add\-on, such as the DNS request, DNS error rate, and DNS forwarding. You can specify a custom time range for querying information and set the information refresh mode to manual or automatic refresh.


1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Network services monitoring** \> **Node\-local\-dns monitoring** to view the monitoring dashboard. 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83de158f74508c45ab6b9fecb9d32916.png) </span>


<span id="lZjD7nA8"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="ulnpf6Xz"></span>
## Related documentation


* [DNS service observability](https://docs.byteplus.com/en/docs/vke/DNS-service-observability?lang=en)

* [Using NodeLocal DNSCache as a DNS caching proxy](https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache)
