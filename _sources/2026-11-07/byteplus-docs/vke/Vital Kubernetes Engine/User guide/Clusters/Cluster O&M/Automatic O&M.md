---
title: "Automatic O&M"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Operation-and-maintenance-configuration"
---

Automatic O&M is a periodic cluster O&M capability provided by VKE. It can automatically perform O&M and upgrades for the cluster control plane, Kubernetes version, and add\-on version. This topic describes how to configure the automatic O&M window and tasks for a cluster.

<span id="8ZfbG6Al"></span>
## Background

The automatic cluster O&M feature can reduce operational overhead. After you enable it, you can periodically upgrade clusters and add\-ons to later supported versions so that you can use the new features they provide.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The automatic cluster O&M feature does not include the node check and self\-healing feature. To configure this feature, see <a href="https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair">Configuring node check and self\-healing</a>.</div>


<span id="aRTJLLHe"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the cluster management page.

3. In the left navigation pane, click **Operation and maintenance configuration**.

4. In the **Automatic operation and maintenance window** section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a35fadf95a4230151380709c3d0ef185.png) </span>icon to configure the automatic O&M feature for the cluster.

   
   |Parameter |Description |
   |---|---|
   |Operation and maintenance window |* **Operation and maintenance cycle**: The day of the week on which automatic O&M is performed. Available options include **Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, and Sunday**.<br><br>* **Start time**: The duration of automatic O&M. The value is an integer. Value range: 4 to 24. Unit: hours. Minimum value: 4 hours.<br><br>* **Operation and maintenance time**: The start time of automatic O&M. The value is an integer. Value range: 00 to 23. This configuration is in the UTC+8 time zone and uses a 24‑hour format. For example, if the value is set to 2, automatic O&M will start at 2:00 AM.<br><br>* **Exemption window**: The start date and end date for stopping automatic O&M. The window can be up to 60 days. In scenarios such as business\-critical periods or network lockdowns, you can configure an exemption window to prohibit the system from performing automatic O&M operations. |
   |Operation and maintenance Jobs |* **Control plane O&M**<br><br>   * **Cluster control plane daily operation and maintenance**: The system performs routine O&M on the managed cluster control plane, such as fixing security vulnerabilities and making configuration changes. After you enable Automatic operation and maintenance window, O&M tasks will be periodically performed on the cluster control plane based on the interval you set.<br><br>   * **Cluster patch version auto\-upgrade**: After you select this option, the system will automatically generate upgrade tasks and upgrade the Kubernetes version of the cluster to the latest available patch version. Patch versions include Kubernetes community patch versions and VKE patch versions. For example, v1.26.10\-vke.23 will be upgraded to v1.26.15\-vke.26. For policies related to cluster upgrades, see [Kubernetes version support policy](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy).<br><br>* **Data plane O&M**<br><br>   * **Add\-on version is automatically upgraded**: After you select this option, the system will automatically generate tasks based on the O&M window and upgrade the selected add\-ons to the latest available version.<br><br>   * **Automatic upgrade add\-on**: After you select **Add\-on version is automatically upgraded**, select the add\-ons to be automatically upgraded.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Cluster control plane daily operation and maintenance</strong> is selected by default and cannot be canceled.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Currently, only some add\-ons support automatic upgrades. Refer to the add\-ons available in the console. To quickly upgrade add\-ons, manually upgrade them on the "Addons" page. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div><br> |
   

5. Click **Confirm**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also enable the automatic cluster O&M feature when creating a cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-cluster">Creating managed clusters</a>.   </div>
   

<span id="2iNRnjGQ"></span>
## Validate results

After enabling the automatic O&M feature, you can select **Cluster jobs** in the left navigation pane to view the execution status of historical O&M jobs.

<span id="YtL9HVcC"></span>
## Related documentation

If the automatic O&M feature does not meet your requirements, you can also manually upgrade the cluster version or add\-on version. The related documents are as follows:


* [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster)

* [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on)
