---
title: "prometheus-adapter"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/prometheus-adapter-add-on"
---

The prometheus\-adapter is an adapter component for cluster custom metrics. It converts Prometheus metrics into the format required by the custom metric API. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="ggGKqFWD"></span>
## Add\-on overview

The prometheus\-adapter add\-on exposes metrics from Prometheus through the Kubernetes Custom Metrics API. This enables Horizontal Pod Autoscaler (HPA) in Kubernetes to use these metrics for autoscaling. After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|Prometheus\-adapter |Deployment |The core workload of the add\-on. It is used to run logic for metric conversion and exposure. |
|Prometheus\-adapter |Service |The add\-on service. It provides the add\-on with a stable in\-cluster access point for the API Server to call. |
|prometheus\-adapter\-config |ConfigMap |The core settings of the add\-on, including Prometheus native metric conversion rules. You can use this configuration file to specify custom Prometheus metrics that need to be converted and used. For details, see [Achieving autoscaling based on custom metrics](https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling). |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="pu9KS50n"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/prometheus-adapter).

<span id="T7cPve8k"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed for clusters that use the **VPC\-CNI** network model. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Prometheus workspace |The add\-on uses the VMP workspace bound to the cluster. If you do not configure a VMP workspace for the cluster, follow the on\-screen prompts to go to the **Operation and maintenance configuration** tab on the cluster details page and configure a VMP workspace for the cluster. |
   

5. Click **Confirm** to finish configuration.


<span id="QcBLneSH"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="T5WtVZXj"></span>
## Monitoring and alerting

<span id="8erRsYJ8"></span>
### Add\-on observability

The stability and performance of the prometheus\-adapter add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="Up5c8oMF"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="9suuG1or"></span>
## Related documentation


* [Achieving autoscaling by using GPU and network metrics](https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling)

* [Achieving autoscaling by using custom metrics](https://docs.byteplus.com/en/docs/vke/Using_custom_metrics_for_autoscaling)

* [Autoscaling based on self-managed Prometheus](https://docs.byteplus.com/en/docs/vke/Horizontal_Pod_Autoscaler_based_on_self-built_Prometheus)
