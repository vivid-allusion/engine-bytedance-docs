---
title: "ingress-nginx"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ingress-nginx-add-on"
---

ingress\-nginx is a gateway add\-on that implements Layer 7 traffic management and routing based on open\-source Nginx. This topic describes how to install and upgrade the ingress\-nginx add\-on and lists related considerations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id="MXBICM8x"></span>
## Add\-on overview

The ingress\-nginx add\-on is a cluster traffic gateway provided by VKE. It reads Ingress routing rules from the cluster, automatically converts them into Nginx configurations, receives external requests via Nginx, and forwards the requests to in\-cluster applications. This add\-on is widely adopted in the Kubernetes community and is suitable for most common web scenarios.

After the ingress\-nginx add\-on is installed in the cluster, the system will create the following Kubernetes resources in the kube\-system namespace.


|**Resource name** |**Resource type** |**Resource description** |
|---|---|---|
|ingress\-nginx\-controller |Deployment |The core controller Pods. The resource contains the Nginx proxy and controller logic. It receives external requests, parses routing rules, and forwards requests to the corresponding backend services based on the rules. |
|ingress\-nginx\-controller |Service |Unified access point for the controller. The resource is of type LoadBalancer. It connects to the load balancer to route external traffic to the controller. |
|ingress\-nginx\-controller\-admission |Service |The admission control service for the controller. The resource is used for Kubernetes Admission Webhook verification. When you create or modify an Ingress, it pre\-checks Nginx syntax to prevent gateway crashes caused by invalid configurations. |
|ingress\-nginx\-controller\-metrics |Service |The monitoring service for the controller. It is used to expose the operational status and metric data of the add\-on. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">VKE supports deploying multiple independent NGINX Ingress controllers within a cluster. Each controller operates independently so that you can expose different services externally based on your actual business needs or scenarios. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers">Deploying multiple Nginx Ingress controllers</a>.</div>


* <div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>



<span id="bhoJS9wS"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/ingress-nginx).

<span id="5ILUQbuz"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   * **Nginx configuration**

      
      |Parameter |Description |
      |---|---|
      |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
      |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. Specify the type of nodes on which the add\-on is deployed. Valid values:<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on Elastic Compute Service (ECS) nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
      |Number of instances |Specify the number of NGINX instances. |
      |Node Label Selector |After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
      |Pod scheduling based on taints and tolerations |After you enable this feature, you can set taint toleration values. The core workloads of the add\-on can be scheduled onto nodes with specified taints. |
      |Nginx configuration |Configure the ResourceQuota of NGINX instances. Valid values:<br><br><br>* **CPU request**: The minimum CPU that a container requires.<br><br>* **CPU limit**: The maximum CPU that can be allocated to a container. Containers will be terminated if the actual usage exceeds the limit.<br><br>* **Memory request**: the minimum memory required by the container.<br><br>* **Memory limit**: the maximum memory value that a container is allowed to use. Containers will be terminated if the actual usage exceeds the limit. |
      

   * **CLB basic information**

      
      |Parameter |Description |
      |---|---|
      |Load balancing type |The network type of the CLB instance. Valid values: **Public network** and **Private network**. |
      |Availability zone |The availability zones of the CLB instance. Valid values: **Primary availability zone** and **Standby availability zone**. |
      |Billing type |The billing type of the CLB instance. Currently, only **Pay\-as\-you\-go** is supported. |
      |Billing method |The billing method of the CLB instance. Valid values:<br><br><br>* **Billing by specification**: Select an instance specification and pay based on your actual usage duration.<br><br>* **Billing by usage**: You do not need to specify the instance specification and pay for it according to the actual resources consumed by the instance. |
      |Instance specification |This parameter is required if you set the **Billing method** parameter to **Billing by specification**.<br><br>Select the instance type for the CLB instance. Different instance types have different specification limits. The specification parameters are as follows:<br><br><br>* **Maximum number of connections**: The maximum number of connections that the CLB instance can process simultaneously. When the number of connections on the instance exceeds the defined maximum limit, new connection requests are dropped.<br><br>* **Number of new connections (CPS)** : The rate of new connections per second that the CLB instance can handle. When the rate of new connections per second exceeds this limit, new connection requests are dropped.<br><br>* **Queries per second (QPS)** : The number of HTTP/HTTPS queries (requests) that the CLB instance can complete per second. When the query rate exceeds this limit, new connection requests are dropped.<br><br>* **Bandwidth (Mbps)** : The maximum data transfer rate supported by the CLB instance when processing network traffic.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To update configurations of CLB instances, you need to enable the option <strong>Updating instance</strong> first. </div><br><br><br>* <div data-tips="true" data-tips-type="tip">To prevent your business traffic from being affected, we recommend that you compare the current specifications of the CLB instance displayed in the CLB console with the selected instance specifications on the update page and confirm that the instance specifications after the update meet your business requirements before you update the CLB instance.</div><br> |
      |Write protection |Specify whether to enable Write protection for the CLB instance.<br><br><br>* **Enable**: You cannot modify or delete CLB instances created by the cluster in the CLB console.<br><br>* **Close**: You can modify or delete CLB instances created by the cluster in the CLB console. |
      

   * **Networking**

      
      |Parameter |Description |
      |---|---|
      |Subnet |Select the subnet of the CLB instance. |
      |IP version |Select the IP version of the CLB instance subnet. Only IPv4 addresses are supported. |
      

   * **Bind EIP**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">You need to specify this parameter only if you set the <strong>Load balancing type</strong> parameter to <strong>Public network</strong>.      </div>
      

      
      |Parameter |Description |
      |---|---|
      |Line type |Specify the line type of the CLB instance. Valid values: **BGP (multi\-line)** , **Fusion BGP**, **China Mobile**, **China Telecom**, and **China Unicom**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">All the line types, except <strong>BGP (multi\-line)</strong>, are beta features of EIP. To use these beta features, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> or contact your account manager.</div><br> |
      |Billing method |Specify the billing method of the EIP bound to the CLB instance. Valid values:<br><br><br>* **Pay\-as\-you\-go \- bandwidth limit**: It will be charged based on usage duration with an upper limit on bandwidth.<br><br>* **Pay\-as\-you\-go \- actual traffic**: It will be charged based on the actual amount of traffic flowing to the Internet instead of usage duration. |
      |Bandwidth limit |Specify the maximum bandwidth of the EIP associated with the CLB instance. |
      |Shared bandwidth packet |Select Add to shared bandwidth package, and select an existing shared bandwidth package.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A shared bandwidth package is a reusable cloud resource for sharing bandwidth. It aggregates multiple public IPs and IPv6 public bandwidths from the same region into a shared bandwidth pool, reducing public bandwidth costs through bandwidth sharing. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package</a>?</div><br> |
      

5. Click **Confirm** to finish configuration.


<span id="dP0IAZIO"></span>
## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="nnvsXvZw"></span>
## Related documentation


* [Ingress overview](https://docs.byteplus.com/en/docs/vke/Ingress-overview)

* [Nginx Ingress](https://docs.byteplus.com/en/docs/vke/Nginx-Ingress)

* [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability)
