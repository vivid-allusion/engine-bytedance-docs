---
title: "Cluster route synchronization"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Cluster_ingress_synchronization"
---

When the API Gateway connects to a Vital Kubernetes Engine (VKE) cluster, it supports listening for changes in Ingress routes within the cluster and synchronizing them to the routing table. This article describes how to synchronize routes from the VKE cluster to the API Gateway. Achieve seamless migration; use the API Gateway as the traffic entry point for the cluster.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

In the cluster, the correspondence between Ingress resources and API Gateway resources is as follows:


|Ingress resources |API Gateway resources |
|---|---|
|host |Services and custom domain names |
|backend |VKE Type Upstream |
|rule |Routing |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The API Gateway instance has been created. For specific operations, refer to [Create instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

* The VKE clusters to be connected have already been imported. For specific operations, refer to [Import VKE clusters](https://docs.byteplus.com/en/docs/apig/Import_container_cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* To ensure data consistency, resources synchronized by Ingress (that is, custom domain names, Upstream, and routes whose source is Ingress) cannot be operated in the console.

* The number of characters for both the Ingress host and path must not exceed 255, otherwise synchronization will fail.

* Ingress host must not use a custom domain name that already exists in the gateway console. To avoid synchronization failure, ensure that the Ingress host does not conflict with the gateway's existing custom domain name.

* If there is a conflict between your Ingress route and the console route rule, the request will be forwarded to the route that was created earlier.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [APIG console](https://console.byteplus.com/veapig).

2. In the top navigation bar, choose the target region.

3. After selecting the target instance in **Instance Management**, click **Import container cluster**.

4. In the Cluster list, select the cluster whose Ingress route needs to be synchronized, and click **Edit** in the **Actions** column.

5. On the Import cluster page, check **Enable route synchronization**, and configure the following information as required.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After enabling route synchronization, the API Gateway will automatically listen for changes in Ingress resources and apply the relevant configuration. It converts Ingress resources into services, custom domain names, routes, upstreams, and other resources, merging them into the current gateway.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Caution: After you turn off route synchronization, the API Gateway will stop listening to Ingress resources and will delete custom domain names, routes, and Upstream resources that were synchronized from Ingress. Please proceed with caution!   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Specify IngressClass |Configure the scope of the listening ingressClass. After the Ingress resources are specified, the API Gateway will listen to them in the cluster.<br><br><br>* **Sync all**: Listens to all Ingress resources in the cluster.<br><br>* **Custom Scope**: listening to Ingress resources of the specified IngressClass.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The ingressClass is a resource in the cluster that describes the Ingress controller. It is used to declare an Ingress controller implementation within a Kubernetes cluster, and any Ingress resources associated with this ingressClass will be handled by the corresponding Ingress controller.</div><br> |
   |IngressClass |* When the configuration for **Specify IngressClass** is set to **Custom Scope**, it is necessary to specify the IngressClass to be monitored. For example, when specifying the ingressClass to be listened to as nginx, it means listening to and synchronizing the Nginx Ingress in the cluster.<br><br>* Support specifying multiple IngressClasses.<br><br>* **Listening for resources with an empty ingressClass**. Once this option is checked, ingress resources not associated with any ingressClass will also be monitored by the gateway. |
   |Specify namespace |Monitoring Ingress resources within the specified namespace.<br><br><br>* **Sync all**: Monitoring Ingress resources under all namespaces in the current cluster.<br><br>* **Custom scope**: monitoring Ingress resources in specified namespaces. Multiple namespaces can be specified. |
   |Switch traffic entry point |After the traffic entry switch is enabled, the IP address of the cluster Ingress will be changed to the current gateway's IP address. That is, the API Gateway serves as the entry point for cluster traffic.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After configuring route synchronization, your Ingress Gateway and API Gateway will take effect simultaneously. To use API Gateway as the traffic entry point for the cluster, enable this switch, and go to your domain name provider to resolve your domain name to the IP address of the API Gateway.</div><br> |
   

6. Click **Confirm**.


<span id=".5pON5L2c57uT5p6c"></span>
## Validating results

After enabling cluster route synchronization, when you create Ingress resources in the cluster, the API Gateway will automatically monitor changes to Ingress resources. It will convert these resources into services, domain names, upstreams, and other resources, and merge them into the current gateway.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, up to 1000 Ingress routes can be synchronized, and the time required to synchronize a single route is approximately 1 second.</div>


<span id="CtqCULYn"></span>
### Create a route in the cluster

Create a specified type of route in the cluster. For example, in this document, the route created is an Nginx Ingress route. The configuration example in this document is shown in the following figure.

<span id="8QUzhLcX"></span>
### View synchronization route list

The host of routing rules in the cluster will be mapped to services and custom domain names under the API Gateway.


1. In the left navigation bar, select **Route management \> Service list (Domain name)** . On the Service list page, services that are named after the host name are those synchronized from the cluster.

2. Click the service name to go to the service overview page. Select the **Domain name management **  tab to view custom domain names synchronized from Ingress.


The rule of the routing rule in the cluster will be mapped to a route under the corresponding service in the API Gateway. In the left navigation bar, select **Route Management \> Route List**. In the route list, view routes with the source type Ingress. The route name is `${host}-${path}-${pathType}-${backend.service}`.

The backend of the Ingress in the cluster will be converted to a VKE type Upstream under the API Gateway. In the left navigation bar, select **Backend Management \> Upstream List**, and on the Upstream List page, choose the **Ingress** tab to view the Upstream synchronized from Ingress.

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next


1. For custom domain names synchronized via Ingress, you need to go to your DNS provider to [add a CNAME record](https://docs.byteplus.com/en/docs/apig/Adding_CNAME_record) and point the custom domain name to the default domain name of the current API Gateway service. Without adding a CNAME record, client requests sent via a custom domain name cannot be correctly resolved to the API Gateway.

2. For custom domain names synchronized via Ingress, please check whether ICP registration has been completed. If ICP filing is not completed, external traffic will be blocked.
