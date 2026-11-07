---
title: "csi-fsx"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on"
---

The csi\-fsx add\-on is a unified storage driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-fsx add\-on and provides relevant considerations.

<span id="u5NgJXOC"></span>
## Add\-on overview

The csi\-fsx is a next\-generation high\-performance storage add\-on provided by VKE. It is primarily used to mount various backend storage services, such as TOS and EFS, to Pods in a cluster through a unified interface. Compared with earlier storage add\-ons, this add\-on provides higher read/write performance, stronger fault self\-healing capabilities, and a more comprehensive permission management mechanism.

As an unmanaged add\-on, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-fsx\-node |DaemonSet |A storage\-mounting Pod that runs on each worker node in the cluster. As a standard CSI node driver, it receives and processes actual mount and unmount requests on the node. |
|fsx\-agent |Pod |The FSX client. When a workload is created in the cluster and uses FSX to mount a storage volume, the system synchronously creates this Pod to mount the specified volume. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="1FMrVrrG"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-fsx).

<span id="ciaIjudx"></span>
## Add\-on configuration

<span id="uCjgurBp"></span>
### Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card and click **Deploy**.

   
   |Parameter |Description |
   |---|---|
   |Service account |Displays the service account information of the csi\-fsx add\-on, which cannot be modified. |
   |Namespace |Displays the namespace where the service account of the csi\-fsx add\-on is located. The default namespace is kube\-system, and cannot be changed. |
   |Authentication method<br><br> |Select **IAM roles for service accounts (IRSA)**  to enable IRSA authentication, and select the target IAM role.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You need to enable IRSA OIDC for IRSA authentication. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters">Using IRSA in clusters</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The IAM role needs to use the OIDC identity provider type and be configured with a trust relationship that trusts the service account in this cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx">Using IRSA for storage mounting authentication</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After you configure the authentication method, you cannot modify the method. To change the authentication method, uninstall and reinstall the add\-on.</div><br> |
   

5. Click Confirm.


<span id="6HCcz6bo"></span>
### Client configuration

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The FSX client (FSX Agent) is a proxy add\-on used for authentication, volume mounting, and data read/write between nodes and backend storage (such as TOS and EFS) in VKE. For client configuration, you can specify different client image versions, client resources, and cleanup policies, and implement node‑level canary upgrades or custom configurations for heterogeneous nodes based on labels. For more configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients">Using FSXSet to implement client upgrades and differentiated configuration</a>.</div>



1. In the lower\-right corner of the csi\-fsx add\-on card, click  **`...`**   **\> Client configuration**.

2. In the Client configuration panel, click **Create client configuration** to configure a custom client.

   
   |Parameter |Description |
   |---|---|
   |Parameter |The FSXSet resource name. This name needs to be unique within the cluster and cannot conflict with other FSXSet resource names. |
   |Client image |Select the FSX client image version to use from the drop\-down list. |
   |Cleanup policy |Specify whether the system automatically recycles (destroys) the FSX client Pod on a node when no workload Pods on the node use FSX volumes.<br><br><br>* **No cleanup**: The client Pod keeps running. This is suitable for storage with frequent access, where you want to eliminate latencies caused by client Pod recreation.<br><br>* **Auto cleanup**: The system automatically destroys idle client Pods. This applies to resource‑sensitive nodes or nodes with infrequent access. |
   |FSXSet label value |Specify a custom node label value. The FSX client configuration will apply only to nodes with this label value.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The tag key is fixed as <code>fsx.csi.volcengine.com/group</code>. You only need to configure the label value.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If a node does not match any custom label value, the system default policy named default will be applied.</div><br> |
   |Resource configuration |Configure the CPU and memory requests and limits for the FSX client container based on the performance requirements for nodes. |
   |**More configuration** ||
   |Cache directory on node |It is used to store temporary data generated by the FSX client when the client reads from or writes to remote storage. This accelerates repeated reads and reduces network I/O pressure. The `/tmp/fsx` directory is used by default. |
   

3. Click **Confirm**.


<span id="kFWdYaGj"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="3IXGsLHb"></span>
## Monitoring and alerting

<span id="74zk0X1o"></span>
### Add\-on observability

The stability and performance of the csi\-fsx add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [CSI Storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the running status of the FSX client and the csi\-fsx link. It covers metrics including the FSX client bandwidth, IOPS, latency, I/O errors, controller errors, CPU utilization, memory utilization, client count, and client versions. In addition, it monitors the request frequency, failure frequency, processing latency, and lifecycle management metrics for both the fsx\-service and fsx\-agent. You can specify a custom time range for querying information and set the information refresh mode to manual or automatic refresh.


1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Storage service monitoring** \> **FSX monitoring** to view the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69e1d2c8a443f108b2bebd4158efcbf4.png) </span>


<span id="TdeFkzuP"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="lYom8yRK"></span>
## Related documentation


* [FSX client introduction](https://docs.byteplus.com/en/docs/vke/FSX_client_introduction)

* [FSXSet resource introduction](https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources)

* [FSX client migration](https://docs.byteplus.com/en/docs/vke/Migrating_FSX_clients)

* [Upgrading FSX clients](https://docs.byteplus.com/en/docs/vke/FSX_client_hot_upgrade)

* [FSX authentication methods](https://docs.byteplus.com/en/docs/vke/FSX_authentication_method)

* [Using IRSA to implement authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx)

* [Using FSXSet to implement client upgrades and differentiated configuration](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients)

* [Using FSXSet to implement differentiated configurations for clients](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients?lang=en)

* [Using FSXSet to implement on-demand client creation](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_on-demand_client_creation?lang=en)

* [Using FSXSet to implement smooth client upgrades](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_smooth_client_upgrades?lang=en)


&nbsp;
