---
title: "Migrating from NGINX Ingresses to APIG Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Migrating_from_NGINX_Ingresses_to_APIG_Ingresses"
---

As the Ingress NGINX Controller has entered the retirement process, continuing to use NGINX Ingresses will gradually introduce risks to scalability, security, and stability. To ensure business security, we recommend promptly migrating from NGINX Ingresses to other Ingress alternatives. This topic describes how to safely migrate from NGINX Ingresses to APIG Ingresses.

<span id="fMCU7NNc"></span>
## Background

<span id="UM4i8tLt"></span>
### Issues caused by the end of maintenance of NGINX Ingresses

NGINX Ingress maintenance will be discontinued soon (see [[Product announcement] NGINX Ingress EOM](https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM) for details). Continued use of NGINX Ingresses will lead to the following problems:


* **Security risks**: No future security patches will be available. As a result, your applications are exposed to unfixed vulnerabilities.

* **Functional bottlenecks**: No new features will be developed. This makes it difficult to support business needs for complex scenarios such as advanced API governance (rate limiting, circuit breaking, and so on) and multi\-protocol support (gRPC and WebSocket).

* **Long\-term stability risks**: Lack of official technical support will make it challenging to resolve issues quickly, affecting business continuity.


<span id="Ze4DYvLe"></span>
### Feasibility of APIG Ingresses as an alternative

As a replacement for NGINX Ingresses, an APIG Ingress offers inherent migration advantages:


* **High compatibility and reduced costs**: It supports the core resource structure, common annotations, path rules, and TLS configurations of NGINX Ingresses. This compatibility minimizes the need to rewrite configurations and means low migration costs.

* **Enhanced capabilities:**  Compared with an NGINX Ingress, an APIG Ingress provides more comprehensive API governance capabilities (rate limiting, authentication, and canary deployment). It also offers full lifecycle management (version control and release workflows) and cross\-cluster traffic scheduling. It can support long\-term business development.

* **Professional R&D support:**  The APIG team has extensive experience in cloud\-native traffic governance and can provide continuous and stable support.


<span id="INWc3iai"></span>
## Migration process

Assume that you have deployed a business application in a VKE cluster and configured an NGINX Ingress that contains domain and path forwarding policies. You also have configured DNS to resolve a custom domain name (example.com). The NGINX Ingress will forward client\-initiated requests targeting example.com to the Pod for the corresponding Service based on the forwarding policies.

To align with your business development needs and considerations for maintainability and security, you decide to migrate from the NGINX Ingress to an APIG Ingress. For business stability, you want to retain the existing externally\-facing domain name and IP address of the back\-end server. In this scenario, you can deploy an APIG Ingress within the VKE cluster, configuring it with forwarding policies identical to those of the NGINX Ingress, and then perform traffic migration by adjusting the weight settings in DNS resolution.

When all traffic is transferred to the APIG Ingress after the migration, delete the NGINX Ingress resolution record from the DNS and the NGINX Ingress resource from the cluster. The entire migration is seamless and transparent to clients.

<span id="uIlNNqe7"></span>
## Migration steps

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">We recommend migrating traffic during off\-peak business hours.</div>


* <div data-tips="true" data-tips-type="warning">Before migrating traffic, first compare the forwarding policies and functionality of the NGINX Ingress and APIG Ingress, and conduct thorough testing to ensure strict functional consistency. This practice helps prevent undesired influences on your business from the migration. If the capabilities or annotations supported by APIG do not meet your business requirements, <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx">submit a ticket</a> or contact our technical support.</div>


* <div data-tips="true" data-tips-type="warning">Using APIG will incur fees.</div>



<span id="vvZE949U"></span>
### Step 1: Create an APIG instance


1. Log in to the [APIG console](https://console.byteplus.com/veapig).

2. In the left navigation bar, select **Instance management**. On the Instance management page, click **Create instance** to create an APIG instance. For configuration steps and parameter details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).

3. Click the name of the APIG instance to enter the APIG instance configuration page.

4. In the left navigation bar, click **Import container cluster**. On the page that appears, click **Import cluster** to import the target cluster and monitor the NGINX Ingress resource in the cluster.

   * In the cluster list, select the target cluster.

   * Enable **Route synchronization**. For **Specify ingressClass**, select **Custom scope**. In the **IngressClass** text box, enter the value of the `ingressClassName` field of the NGINX Ingress in the cluster (nginx in this example).

5. Run the following command to confirm that the back\-end service in the cluster is accessible through the APIG instance. In the following command, `118.xxx.xxx.xxx` is the IP address of the access entry for the APIG instance. You can use the default IP address or a custom IP address for the instance. For details, see [Adding access entries](https://docs.byteplus.com/en/docs/apig/Adding_access_entrance).

   ```Bash
   curl http://example.com --resolve example.com:80:118.xxx.xxx.xxx
   ```
   

   If the following result appears, the back\-end service in the cluster is accessible by using the IP address of the access entry for the APIG instance.

   ```HTML
   <!DOCTYPE html>
   <html>
   <head>
   <title>Welcome to nginx!</title>
   <style>
   html { color-scheme: light dark; }
   body { width: 35em; margin: 0 auto;
   font-family: Tahoma, Verdana, Arial, sans-serif; }
   </style>
   </head>
   <body>
   <h1>Welcome to nginx!</h1>
   <p>If you see this page, the nginx web server is successfully installed and
   working. Further configuration is required.</p>
   
   <p>For online documentation and support please refer to
   <a href="http://nginx.org/">nginx.org</a>.<br/>
   Commercial support is available at
   <a href="http://nginx.com/">nginx.com</a>.</p>
   
   <p><em>Thank you for using nginx.</em></p>
   </body>
   </html>
   ```
   


<span id="B1CgPA3I"></span>
### Step 2: Switch traffic to the APIG instance

Assume that before the migration, you have added an A record that points the domain name to the public address of the NGINX Ingress. At this point, you can add the IP address of the APIG instance to the original DNS record and gradually shift traffic from the NGINX Ingress to the APIG Ingress.

In this topic, the DNS service on BytePlus is used for demonstration.


1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns).

2. In the left navigation bar, click **Domain management**.

3. In the domain name list, click the target domain name to go to the domain name details page.

4. Edit the target DNS record to add the IP address of access entry for the APIG instance.

5. Click **Submit** to complete the configuration.

6. Verify that the business traffic is forwarded to the APIG Ingress as expected, with no anomalies.


<span id="UIb1l4bC"></span>
### Step 3: Delete redundant resources

After traffic is correctly forwarded by the APIG Ingress and all persistent connections of the NGINX Ingress are processed, you can monitor traffic forwarding for a certain period of time. If no anomalies are detected, you can then delete redundant resources.


1. Delete the DNS record of the NGINX Ingress. After the DNS TTL (time to live) has elapsed, all new requests will be routed to the APIG instance.

2. Delete the NGINX Ingress resource from the cluster. Only perform this after confirming no traffic on the NGINX Ingress via continuous monitoring using the [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability) feature of VKE [cloud-native observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).


<span id="lJluwBll"></span>
## Other considerations

<span id="K4dc5HTh"></span>
### Handling incompatible annotations

During migration, you may encounter NGINX\-specific annotations that are not supported by an APIG Ingress. In this case, consider the following suggestions:


* If the features are configurable in the console but not via annotations, configure them in the [APIG console](https://console.byteplus.com/veapig).

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">For annotations not supported by APIG, we recommend against configuring them directly using YAML. These custom configurations will be lost when they are applied by using the console or when the ingress\-controller add\-on is restarted or updated.   </div>
   

* APIG will continuously enhance compatibility with NGINX annotations to support more needs. For configurations not supported by either the console or annotations, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000170&FlowKey=DhvSFwiOSXyEVSlGZJXx) or contact technical support.


<span id="vRPrSZZU"></span>
### Rollback process

If any anomaly is detected during or after migration to the APIG instance, you can roll back the traffic migration. Rollback is the reverse process of migration, with the same basic principle: achieving lossless rollback by changing the IP address in the DNS record from the IP address for the APIG instance to the one associated with the NGINX Ingress.
