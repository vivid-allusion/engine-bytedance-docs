---
title: "mgpu"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/mgpu-add-on"
---

The mgpu add\-on implements GPU resource sharing. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="9kXcT9dm"></span>
## Add\-on overview

The mgpu (multi\-container GPU) add\-on is a GPU sharing solution provided by VKE. It leverages kernel virtualization technology to isolate the computing power and video memory of GPUs. This enables multiple containers to share the same physical GPU card while ensuring performance and isolation.

After the mgpu add\-on is installed in the cluster, the system will create the following Kubernetes resources in the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|ek8s\-gpu\-agent |DaemonSet |The core workload of the add\-on. It collects and reports node\-level GPU resources (GPU memory and computing power) and enforces hard isolation and partitioning of shared GPU resources at the underlying layer. |
|ek8s\-gpu\-exporter |DaemonSet |The mGPU metric collector. It collects various operational mGPU metrics in real time, such as GPU memory utilization and compute utilization. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="lO0oQ0ew"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/mgpu).

<span id="hita4PcR"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **GPU** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deploy addons |Specify whether to install the resource monitoring add\-on mgpu\-exporter to enable containers to share GPUs. The add\-on is installed by default.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you use the default value. If you do not install the mgpu\-exporter, you cannot leverage cloud\-native observability to monitor mGPU\-related metrics.</div><br> |
   |Collection interval |Configure the metric collection interval for the mgpu\-exporter. You can set the metric collection interval based on your timeliness requirement. |
   |Health check |Select **enable pod liveness probe** to enable health checks. If it is enabled, the add\-on will automatically trigger restarts and restore resource reporting after a resource reporting exception is detected. |
   |Health Check Timeout |‌Configure the health check timeout period.‌ The system declares the health check failed if no response is received within this duration. |
   

5. Click **Confirm** to finish configuration.


<span id="CSJXyoHk"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the add\-on card still displays <strong>Upgradable</strong> after the update, you can upgrade it again to a higher version. Ensure the last upgrade is completed successfully if you choose to keep upgrading. The following methods can be used to validate the upgrade.</div>


<span id="BfscS8Pv"></span>
## Check add\-on status

After the add\-on installation/upgrade is complete, confirm whether the add\-on is working normally by using the console or the command\-line tool kubectl.


<Tabs>
<Tab zoneid="sNcYLRhH" title="Use the console">
<TabTitle>Use the console</TabTitle>

1. In the left navigation pane of the cluster management page, click **Addons**. Then, click the **GPU** tab.

2. On the vpc\-cni add\-on card, click  **\-\>**  in the upper\-right corner to view the add\-on deployment details.

3. Check whether all Pods in the DaemonSet `ek8s-gpu-agent` in the `kube-system` namespace are `running` and whether the value of the **Updated** field equals the total number of Pods. If all Pods are in the `Running` state and all Pods are updated, the upgrade is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_228e5613dadb2d69f6015a3ef0fe1e74.png) </span>

4.  In the `kube-system` namespace, check whether the **Updated** field on the details page of the `ek8s-gpu-exporter` Deployment equals the total number of Pods. If all Pods are updated, the upgrade is successful.


</Tab>
<Tab zoneid="pDGnt7mI" title="Use the kubectl CLI">
<TabTitle>Use the kubectl CLI</TabTitle>

1. [Connect to the target cluster using kubectl.](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster)

2. Run the following command to check whether the DaemonSet `ek8s-gpu-agent` in the `kube-system` namespace is in the READY state and whether the value of `UP-TO-DATE` equals the total number of Pods.

   ```Bash
   kubectl get daemonset ek8s-gpu-agent -n kube-system
   ```
   

   If all Pods are in the `READY` status and the value of `UP-TO-DATE` equals the total number of Pods, the upgrade is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41001c2701d6574fd6a1738f24e3a3c4.png) </span>

3. Run the following command to check whether the value of `UP-TO-DATE` for the DaemonSet `ek8s-gpu-exporter` in the `kube-system` namespace equals the total number of Pods.

   ```Bash
   kubectl get deployment ek8s-gpu-exporter -n kube-system
   ```
   

   If the value of `UP-TO-DATE` equals the total number of Pods, the upgrade is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f78eb941145d6513eebe66be53ac533e.png) </span>


</Tab>
</Tabs>


<span id="nKUjt9gZ"></span>
## Monitoring and alerting

<span id="flVzfysc"></span>
### Add\-on observability

The stability and performance of the mgpu add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability?lang=en).

<span id="sNM15NG7"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="x2i4KesN"></span>
## Related documentation


* [mGPU overview](https://docs.byteplus.com/en/docs/vke/mGPU-overview)

* [Configuring mGPU scheduling](https://docs.byteplus.com/en/docs/vke/Using-mGPU)

* [Allocating mGPU computing power](https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies)

* [Implementing multi-card sharing based on mGPUs](https://docs.byteplus.com/en/docs/vke/Multiple-GPU-sharing)

* [Implementing online-offline hybrid deployment based on mGPUs](https://docs.byteplus.com/en/docs/vke/Using_mGPU_for_online-offline_hybrid_deployment)

* [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability)
