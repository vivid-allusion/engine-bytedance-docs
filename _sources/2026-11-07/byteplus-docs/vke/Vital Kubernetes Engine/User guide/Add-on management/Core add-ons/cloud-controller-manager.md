---
title: "cloud-controller-manager"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/cloud-controller-manager-add-on"
---

The cloud\-controller\-manager add\-on is a core managed VKE add\-on that manages the lifecycle of cloud resources such as nodes and load balancers in clusters. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="SBZsS3Wh"></span>
## Add\-on overview

cloud\-controller\-manager (hereinafter referred to as CCM) integrates Kubernetes clusters with cloud infrastructure capabilities. It connects to cloud resources (load balancing, networking, and more) for load balancing, networking, and other scenarios. CCM provides the following major capabilities.


|Feature |Description |
|---|---|
|Load balancer management |For a Service of type LoadBalancer, CCM automatically creates and configures the LoadBalancer resources (such as CLB or NLB) for the Service and completes associated configurations (such as listeners and backend server groups). When the backend endpoints of the Service or cluster nodes change, CCM automatically synchronizes and updates the backend members of the load balancer. This ensures that traffic is always forwarded to the latest available backend. |
|Node lifecycle management |CCM tracks the real\-time health status of cluster nodes. When it detects that the underlying ECS VM is taken offline or deleted, CCM automatically removes the corresponding Node from the cluster. This prevents workloads from being scheduled to unavailable machines. |
|Cross\-node network connectivity |When a cluster uses Flannel as its network add\-on, CCM enables network connectivity between Pods and nodes, as well as cross\-node connectivity between Pods. CCM writes the Pod CIDR information of each node to the VPC routing tables to enable cross\-node container network communication. This capability generally requires no additional configuration and takes effect immediately after installation. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">As a managed add\-on, it does not run additional Controller Pod workloads in your business cluster or consume computing resources on nodes. It also has the following characteristics:</div>



* <div data-tips="true" data-tips-type="default"><strong>Non\-removable</strong>: As the foundation for cloud resource integration into clusters, this add\-on is locked as a core protected resource to prevent service network disruptions due to accidental deletion.</div>


* <div data-tips="true" data-tips-type="default"><strong>Fully managed maintenance</strong>: Security patches and routine maintenance are ‌centrally and automatically managed by VKE.</div>



<span id="ZgReaCIu"></span>
## Parameter configuration


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Core** tab.

4. Move the pointer over the add\-on card and click **Configuration** to configure parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |list of custom route tables |Specify the ID of the custom route table to which cluster nodes' Pod CIDR blocks will be added, for example, `vtb-1ksnixokth***`. You can specify multiple routing table IDs separated by half\-width commas (`,`). A multi\-ID example is `vtb-1ksnixokth***,vtb-1fulov614g***`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Before configuring this add\-on parameter, ensure that the custom routing table has been created. For details, see <a href="https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table">Creating routing tables</a>.</div><br> |
   

5. Click **Confirm** to finish configuration.


<span id="h063Upxg"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="zH9zwuM5"></span>
## Related documentation


* [Creating CLB services via the console](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console)

* [Creating CLB services via kubectl](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-using-kubectl)

* [Configuring CLB LoadBalancer Services by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations)

* [Configuring an NLB Service using annotations](https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations)
