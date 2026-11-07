---
title: "log-collector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/log-collector-add-on"
---

The log\-collector is a cluster log collection add\-on. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="8E92ZF61"></span>
## Add\-on overview

The log\-collector is a log collection client that runs on cluster nodes. Deployed as a DaemonSet on each node, it is used to discover and collect stdout logs and file logs from container applications on the node, and to send the logs to Torch Log Service (TLS). This provides a unified data source for subsequent log search, analysis, alerting, and visualization. After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|log\-collector |DaemonSet |The core collector of the add\-on. It runs on each node and is used for log collection on the node. |
|log\-collector\-controller |Deployment |The add\-on controller. It is used to synchronize cluster information to TLS to create a machine group and distribute the configured collection rules to each node. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="hd8BrG1X"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/log-collector).

<span id="pld4Ek42"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Management method |Select the management method of the add\-on. Valid values:<br><br><br>* **Managed**: Indicates that the add\-on is deployed in managed mode.<br><br>* **Unmanaged**: Indicates that the add\-on is deployed in unmanaged mode.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required only when you install the add\-on in a serverless cluster.</div><br> |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **VCI deployment**: Deploys the add\-on on VCIs. Additional fees will be incurred if you use VCI. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |LogCollector Configuration |Configure the resource quotas of LogCollector.<br><br><br>* **CPU request**: The minimum CPU that a container requires.<br><br>* **CPU limit**: The maximum CPU that can be allocated to a container. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Memory request**: The minimum memory required by the container.<br><br>* **Memory limit**: The maximum memory value that a container is allowed to use. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Pod scheduling based on taints and tolerations**: After you enable this feature, you can set taint toleration values. The core workloads of LogCollector can be scheduled onto nodes with specified taints. |
   |LogController Configuration |Configure the resource quotas of LogCollector Controller. Valid values:<br><br><br>* **CPU request**: The minimum CPU that a container requires.<br><br>* **CPU limit**: The maximum CPU that can be allocated to a container. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Memory request**: The minimum memory required by the container.<br><br>* **Memory limit**: The maximum memory value that a container is allowed to use. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Pod scheduling based on taints and tolerations**: After you enable this feature, you can set taint toleration values. The core workloads of LogCollector Controller can be scheduled onto nodes with specified taints. |
   |Allow access to Secrets |Specify whether to create collection configurations by mounting Secrets as environment variables. For more details, see [Collecting container logs (DaemonSet-Pod environment variables)](https://docs.byteplus.com/en/docs/tls/Use-Pod-to-configure-a-DaemonSet). |
   

5. Click **Confirm** to finish configuration.


<span id="UyGf4GEq"></span>
## Upgrading add\-ons

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before upgrading the add\-on, carefully read the <a href="https://docs.byteplus.com/en/docs/vke/log-collector">add\-on release notes</a>, especially the mentioned impacts after changes.</div>


The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="S7iAutl2"></span>
## Related documentation


* [Collecting container logs](https://docs.byteplus.com/en/docs/vke/Collecting-container-logs)

* [Collecting container logs by using environment variables](https://docs.byteplus.com/en/docs/vke/Collecting-container-logs-using-environment-variables)

* [Collecting the logs of the ingress-nginx add-on](https://docs.byteplus.com/en/docs/vke/Collecting-ingress-nginx-logs)
