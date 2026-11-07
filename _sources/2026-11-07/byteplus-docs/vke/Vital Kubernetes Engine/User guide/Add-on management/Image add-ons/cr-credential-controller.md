---
title: "cr-credential-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/cr-credential-controller-add-on"
---

The cr\-credential\-controller add\-on enables credential\-free pulling of private images in VKE clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="mLRpFZLY"></span>
## Add\-on overview

cr\-credential\-controller is an add\-on provided by VKE to enable credential\-free pulling of private images. It supports automatic management of Container Registry access credentials in the cluster and allows you to specify the scope of credential\-free image pulling (namespaces and ServiceAccounts). This eliminates repeated manual credential configuration for private image pulling and implements secure, easy, and automated authentication.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|cr\-credential\-controller |Deployment |The core workload of the add\-on. It generates image\-pull Secrets for designated namespaces and ServiceAccounts. It automates the credential mount configuration during workload creation to ensure that workloads can automatically pull private images. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="qN9bHkb8"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/cr-credential-controller).

<span id="LO5MmfWW"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Image** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment form |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on two Vital Container Instances (VCIs) with 0.25 vCPU and 0.5 GiB specifications. Additional fees will be charged. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Container Registry configuration |The configuration of the target CR instance for secret\-free image pulling.<br><br><br>* **Region**: Select the region where the target CR instance is located.<br><br>* **Container Registry instance**: Select the target CR instance and its domain name. Any private images newly pushed to the instance can also be pulled without a Secret.<br><br>   Click **Add instance** to select multiple CR instances in the same region.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Click <strong>Add Container Registry configuration</strong> to select CR instances from different regions as the target instances for secret\-free image pulling.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Private images that are newly pushed by the selected CR instances will be pulled without a Secret.</div><br> |
   |Secret\-free configuration |Specify the secret\-free configuration in VKE.<br><br><br>* **Namespace**: Specify in\-cluster namespaces that can pull private images without credentials.<br><br>   The default value `*` indicates that all namespaces can pull private images without credentials. You can enter one or more specific namespace names. If you specify more than one, separate them with commas (`,`).<br><br>* **ServiceAccount**: Kubernetes ServiceAccounts that can use the add\-on.<br><br>   The default value `*` indicates that all ServiceAccounts in the specified namespaces can pull private images without credentials. You can enter one or more specific ServiceAccounts. If you specify more than one, separate them with commas (`,`). |
   |Parameter configuration |The webhook parameter configuration of the add\-on. You can enable or disable the webhook of the add\-on by using the **WebhookConfigurationEnable** parameter.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have high timeliness requirements for pulling container images from CR, you can enable <strong>WebhookConfigurationEnable</strong> to promptly inject credentials and other preset configurations. However, if you enable this feature, system performance may be affected. If you do not have high timeliness requirements, we recommend that you disable this feature.</div><br> |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   

5. Click **Confirm** to finish configuration.


<span id="9TtKWAJT"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="3Kfijtu5"></span>
## Monitoring and alerting

<span id="cWjCThsU"></span>
### Add\-on observability

The stability and performance of the cr\-credential\-controller add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="vkxmtClA"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="E3pIAPQu"></span>
## Related documentation


* [Creating workloads by pulling private images with the secret-free add-on](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller)

* [Image repository observability](https://docs.byteplus.com/en/docs/vke/Container-Registry-observability)
