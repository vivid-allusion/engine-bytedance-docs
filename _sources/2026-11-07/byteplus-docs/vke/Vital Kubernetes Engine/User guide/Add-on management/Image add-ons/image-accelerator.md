---
title: "image-accelerator"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/image-accelerator-add-on"
---

image\-accelerator is an image acceleration add\-on for VKE clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="LDgyaPLH"></span>
## Add\-on overview

The image\-accelerator add\-on for VKE clusters uses ‌Nydus lazy\-loading technology to accelerate container image pulls during Pod creation. It is suitable for the following scenarios:


* The image size is large, and the image content accessed after application startup has obvious local hotspots.

* The time required to pull the container image accounts for a large proportion of the overall container uptime.

* The container image changes frequently.


After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|image\-accelerator |Deployment |The core controller of the add\-on. It implements admission webhook logic and configuration injection. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="k11oOUwz"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/image-accelerator).

<span id="hpNsiEO5"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Image** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.

   
   |Parameter |Description |
   |---|---|
   |CPU |Configure the CPU request and limit for the add\-on controller Pod. We recommend adjusting these values based on the cluster node scale and actual workload.<br><br><br>* The CPU request is used for resource reservation during scheduling. The Pod will not be scheduled onto a node if the node's available CPU is below this value.<br><br>* The CPU limit restricts the maximum number of CPU cores the Pod can use. The Pod will be throttled if it exceeds this value. |
   |Memory |Configure the memory request and limit for the add\-on controller Pod. We recommend adjusting these values based on the cluster node scale and actual workload.<br><br><br>* The memory request is used for resource reservation during scheduling. The Pod will not be scheduled onto a node if the node's available memory is below this value.<br><br>* The memory limit restricts the maximum amount of memory the Pod can use. If the Pod exceeds this value, it will be killed due to OOM and restarted. |
   

5. Click **Confirm**.


<span id="WWtQLG3Q"></span>
## Upgrade the add\-on

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For the upgrade procedure and considerations, see [Upgrading the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="gSvUtDAD"></span>
## Monitoring and alerting

<span id="3XRBHFpb"></span>
### Add\-on observability

The stability and performance of the image\-accelerator add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the resource usage and health status of the image\-accelerator add\-on, such as webhook metrics, the number of Nydus Daemons, and the usage of Nydus Daemon memory. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.


1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, click **Image acceleration service monitoring** \> **Image lazy loading (Nydus) monitoring** to view the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4161a62a8b7a944adfae9865d8113c2.png) </span>


<span id="eqW1AS90"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="DwXsatFN"></span>
## Related documentation


* [Image lazy loading solutions](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution)

* [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability)
