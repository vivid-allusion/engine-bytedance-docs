---
title: "Observability of registered clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Enable_observation"
---

Cloud\-native observability provides fully managed, high\-performance, and high\-stability cluster observability and alerting services. This topic describes how to enable the cloud\-native observability feature in a registered cluster.

<span id="ATa6veZB"></span>
## Background

The cloud\-native observability feature is implemented based on the VMP service and uses the prometheus\-agent add\-on to enable observability of basic cluster resources. Therefore, to enable cloud\-native observability, you first need to create a VMP workspace and install the prometheus\-agent add\-on in the cluster.

<span id="bsVO2L7g"></span>
## Prerequisites


* A third\-party cluster has been registered to VKE. For details, see [Registering existing clusters via a proxy](https://docs.byteplus.com/en/docs/vke/Register_the_cluster_by_proxy).

* A VMP workspace has been created, and its Remote Write URL has been obtained from the overview. For more information, see [Creating workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* (Optional) To access and collect metric data over the private network and store it in the workspace, make sure that a proxy has been configured in advance. For example, you can configure  PrivateLink **.** 


<span id="QeRZ859s"></span>
## Procedure

<span id="TLrfOZBI"></span>
### Step 1: Bind to a workspace


1. Log in to the [VKE console](https://console.byteplus.com/vke).

3. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the registered cluster to go to its management page.

4. In the left navigation bar, click **Overview**, and specify the target workspace on the **Operation and maintenance configuration** tab. After completing the configuration, click **Confirm**.

   
   |Parameters |Description |
   |---|---|
   |Prometheus workspace |Select an existing VMP workspace and bind it to the cluster.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This action only binds the workspace to the cluster and does not actually collect data.</div><br> |
   |Proxy address configuration |Specify the proxy address, which is used to store the collected data in the workspace.<br><br><br>* If public network access is enabled for the workspace, you can directly use the Remote Write URL.<br><br>* If public network access is not enabled for the workspace, to store collected metric data in the workspace using private network access, you need to combine the proxy domain name and the workspace path in the Remote Write URL to form the proxy address. For example, if the  PrivateLink write endpoint is `http://ep-5gsbi9i0953473inqk8bb5fi.epsvc-22j124xxxxxxxxxxxxxxxxx.cn-shanghai.privatelink.volces.com:8080`, and the Remote Write URL of the workspace is `http://write.prometheus-cn-shanghai.ivolces.com/workspaces/axxxxxx-acxx-4dxx-99xx-6b08xxxxxxxx/api/v1/write`, then the combined proxy address is `http://ep-5gsbi9i0953473inqk8bb5fi.epsvc-22j124xxxxxxxxxxxxxxxxx.cn-shanghai.privatelink.volces.com:8080/workspaces/axxxxxx-acxx-4dxx-99xx-6b08xxxxxxxx/api/v1/write`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you still have questions about configuring the proxy address, you can submit a ticket or contact your account manager to obtain technical support.</div><br> |
   


<span id="VnFGPcs8"></span>
### Step 2: Deploy the collector


1. In the left navigation bar, click **Addons**.

2. Click the **Monitoring** tab. Then, find the prometheus\-agent add\-on, move the mouse over the add\-on card, and click **Deploy**.

4. Configure the add\-on parameters and click **Confirm**. For detailed instructions on configuring prometheus\-agent add\-on parameters, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id="WGtM6pnt"></span>
### Step 3: Enable cloud\-native observability


1. In the left navigation bar of the cluster management page, click **Cloud native observability** \> **Overview** to go to the service activation page.

2. Click **Activate basic observability** to enable cloud\-native observability.


<span id="m08MLSed"></span>
## Subsequent configurations

<span id="Xek6fIfa"></span>
### Monitoring dashboards

Cloud\-native observability provides monitoring dashboards for registered clusters. The dashboards include container runtime metrics, node runtime metrics, Kubelet runtime metrics, and status metrics for various resource objects. After enabling cluster observability and configuring collection rules, you can view the preset monitoring dashboards. For details, see [Container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The dashboard type, dashboard quantity, and chart quantity provided by cloud\-native observability for managed clusters and registered clusters differ slightly. Refer to the console for the authoritative information.</div>


<span id="LeHVRVW2"></span>
### Metric configuration

After enabling cloud\-native monitoring for a registered cluster, you can configure collection rules according to your actual requirements. Select the target add\-ons, specific metrics, and collection interval, or discard some unnecessary metrics based on actual requirements. For details, see [Container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).

<span id="WIvY0IHa"></span>
### Alerting configuration

After enabling cloud\-native monitoring for a registered cluster, you can configure alert rules according to your actual requirements. You can use custom or preset alert templates to quickly complete alert configuration for the registered cluster. For details, see [Container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability).
