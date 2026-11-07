---
title: "Creating NGINX Ingresses in the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-Nginx-Ingress-in-the-console"
---

Vital Kubernetes Engine (VKE) provides a community edition of the NGINX Ingress controller, which converts Ingresses into NGINX configurations and uses NGINX for Layer 7 traffic forwarding. This topic describes how to configure Nginx Ingresses in the console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The ingress\-nginx add\-on has been installed. For details, see [Installing ingress-nginx](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list on the right side, click the name of the target cluster.

3. In the left navigation bar, click **Services and Ingresses \> Ingress**. On the page that appears, click **Create Ingress**.

   * Basic configuration

      
      |Parameter |Description |
      |---|---|
      |Name |Specify an Ingress name based on the on\-screen prompts. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the Ingress belongs. We recommend that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Annotation |It is the annotation in Kubernetes. You can configure specific annotations to achieve more diverse Layer 7 load balancing capabilities and Ingresses.<br><br>You can select a common annotation from the drop\-down list. You can also click **Add annotation** to add multiple annotations for an Ingress at the same time. For the descriptions of common annotations, see [Common annotations of NGINX Ingresses](https://docs.byteplus.com/en/docs/vke/Common_annotations_for_Nginx_Ingress). |
      

   * Ingress configuration

      
      |Parameter |Description |
      |---|---|
      |Ingress type |Specify the type of the Ingress Controller. In this example, select **ingress\-nginx**. |
      |Ingress Class |Specify an Ingress controller. Valid values:<br><br><br>* **nginx (default add\-on)** : Use the default ingress\-nginx add\-on in the cluster. If it is shown as not installed, install the add\-on based on the on\-screen prompts. For details about add\-on configuration, see [Ingress-nginx add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=).<br><br>* Custom ingress\-nginx: Use the custom ingress\-nginx application. You can deploy a custom ingress\-nginx application in the **Application Center**. For detailed instructions, see [Deploying multiple Nginx Ingress controllers](https://docs.byteplus.com/en/docs/vke/Deploying-multiple-Nginx-Ingress-controllers).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you perform operations as an IAM user, the BytePlus root user needs to attach the <strong>senior developer</strong> or <strong>developer</strong> role of the current cluster and all namespaces (or specified namespaces) of the cluster to the IAM user. Otherwise, custom ingress\-nginx may be unavailable. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions">Configuring RBAC permissions</a>.</div><br> |
      

   * Listener configuration

      
      |Parameter |Description |
      |---|---|
      |Certificate configuration |Specify whether to enable HTTPS and configure an encryption certificate.<br><br><br>* **Enable**: Use HTTPS, which means that port 443 is open.<br><br>* **Not enabled**: Only use HTTP, which means that only port 80 is opened.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>HTTPS</strong> is enabled, the system will open both port 80 and port 443 by default. To ensure data security, we recommend that you configure a port 80 redirect, which redirects requests from HTTP to HTTPS. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-redirect-rules-for-an-Nginx-Ingress">Configuring redirect rules for NGINX Ingresses</a>.</div><br> |
      |Certificate |Configure the Transport Layer Security (TLS) certificate that needs to be bound to achieve data encryption and authentication.<br><br><br>* If you set the value to **Default**, it indicates that all domain names are bound to the same TLS certificate.<br><br>* If you set the value to **Specify**, it indicates that the specified domain names are bound to the specified TLS certificates.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If no certificate is available, click <strong>Create Secret</strong> to create a secret of the <strong>Certificate (TLS)</strong> type. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Secret">Creating secrets</a>.</div><br> |
      

   * Forwarding configuration

      
      |Parameter |Description |
      |---|---|
      |Session persistence |This feature is not enabled by default. After you enable session persistence, the Ingress continuously forwards access requests from the same client to the same backend server for processing. |
      |Forwarding rules |If the target address of a request hits a forwarding rule, the request is forwarded to the corresponding **service**. Click **Add forwarding rule** to add one or more forwarding rules.<br><br><br>* **Domain name**: When the requested domain name matches the domain name set here, the request is forwarded to the specified service. When you select HTTPS and specify a certificate, the domain name set here must be consistent with the domain name in the certificate.<br><br>* **Path**: When the requested path matches the path set here, the request is forwarded to the specified service.<br><br>* **Path matching rule**: the path matching rule. Valid values:<br><br>   * **Prefix matching**: Any path that meets the prefix condition is accessible. For example, if the mapped URL is `/foo`, both `/foo/v1` and `/foo/v2` can access the backend service.<br><br>   * **Exact matching**: Only paths that exactly match the condition will be forwarded to the backend service.<br><br>* **Service**: The target service and port to which the request is forwarded. If no service is available, create a service based on the instructions in [Services](https://docs.byteplus.com/en/docs/vke/Service-overview). |
      

4. Click **Confirm** to create the NGINX Ingress.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

After the NGINX Ingress is configured, you can view the configuration result in the console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The VIP column in the Ingress list displays the public or private IP address of the load balancer corresponding to an NGINX Ingress. You can use this IP to search for the load balancer and view its details in the <a href="https://console.byteplus.com/clb">Load Balancer console</a>.</div>
