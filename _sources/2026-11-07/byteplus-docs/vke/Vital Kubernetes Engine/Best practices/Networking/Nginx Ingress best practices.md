---
title: "Nginx Ingress best practices"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Nginx-Ingress-best-practices"
---

Nginx Ingress is an implementation of Kubernetes Ingress, which enables you to manage and route Ingress traffic. This topic describes common best practices of the ingress\-nginx add\-on.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">NGINX Ingress support will soon be discontinued. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM">[Product announcement] NGINX Ingress EOM</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

VKE provides a community edition of the Nginx Ingress controller, which converts Ingresses into Nginx configurations and uses Nginx for Layer 7 traffic forwarding.

<span id=".5bi455So5pON5L2c"></span>
## Common operations

<span id=".6YWN572u5a6e5L6L5Liq5pWw"></span>
### Specifying the number of instances

After you install the ingress\-nginx add\-on in a VKE cluster, the default number of instances for the add\-on is 2. You can also adjust the number of instances to achieve high availability of production.


1. Log in to the [VKE console](https://console.byteplus.com/vke) **.** 

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the **ingress\-nginx** add\-on and click **Deploy**.

4. In the **ingress\-nginx specifications** dialog box, set the **Number of instances** parameter to the desired value, and then click **Confirm**.

5. (Optional) When the number of ECS nodes is greater than or equal to the number of instances, you need to configure the anti\-affinity scheduling policy for **ingress\-nginx\-controller**. In this way, multiple instances of the add\-on are distributed across different nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you install the ingress\-nginx add\-on, it is deployed in the cluster as a Deployment, which is named <strong>ingress\-nginx\-controller</strong>.   </div>
   

   1. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

   2. On the **Deployment** page, find **ingress\-nginx\-controller** under the **kube\-system** namespace and in the **Actions** column, click `...` \> **Update**.

   3. Modify the configurations based on the following sample figure.

      * Sample figure for console operations:

      * YAML file code snippet:

         ```YAML
         podAntiAffinity:
           requiredDuringSchedulingIgnoredDuringExecution:
           - labelSelector:
               matchLabels:
                 app.kubernetes.io/name: ingress-nginx
             namespaces:
             - kube-system
             topologyKey: kubernetes.io/hostname
         ```
         


<span id=".5L-u5pS56LWE5rqQ6ZmQ5Yi2"></span>
### Modifying resource limits

By default, for ingress\-nginx\-controller, the CPU upper limit is 0.5 cores, and the memory upper limit is 1 GiB. If your business traffic is high, we recommend that you set the CPU upper limit to at least 1 core and the memory limit to at least 2 GiB. You can adjust the resource limits of the ingress\-nginx\-controller add\-on based on your business requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before you change the resource quota for ingress\-nginx\-controller, make sure that the number of instances is at least 2. For detailed operations, see the <a href="https://docs.byteplus.com/en/docs/vke/Nginx-Ingress-best-practices#.6YWN572u5a6e5L6L5Liq5pWw">Specifying the number of instances</a> section of this topic.</div>


* <div data-tips="true" data-tips-type="tip">After you change the configurations, perform a rolling update on the instances. In this case, business traffic may experience fluctuations, and persistent connections may be interrupted and re\-established within 1 minute. Therefore, we recommend that you perform this operation during business off\-peak hours.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the **ingress\-nginx** add\-on and click **Configuration**.

5. In the **ingress\-nginx specifications** dialog box, set the **Nginx configuration** parameter to your desired value, then click **Confirm**. For more parameter descriptions, see the [ingress-nginx addon](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.aW5ncmVzcy1uZ2lueC3nu4Tku7Y=)


&nbsp;

<span id=".5LiT5bGe6IqC54K5"></span>
### Dedicated nodes

To ensure the high performance and stability of Nginx Ingress, you can deploy multiple ingress\-nginx\-controller instances on nodes with high specifications to avoid resource preemption between different instances and single points of failure.

The following content describes the configuration procedure to enable each ingress\-nginx\-controller instance to exclusively occupy one dedicated node. Two instances are used as an example.


1. Create two dedicated worker nodes in the cluster. You can add two new nodes to an existing node pool, or add two dedicated nodes by creating a node pool. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).

2. Add a label with the `key as ingress-nginx` and `value as true` to each dedicated node. For detailed operations, see [Label management](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.5qCH562-566h55CG).

3. Add a taint to each dedicated node to prohibit pods without toleration from being scheduled to the dedicated nodes. Add a label with the same `key and value` to each taint. For detailed operations, see [Taint management](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.5rGh54K5566h55CG).

4. Configure a taint toleration rule for the workload to schedule ingress\-nginx\-controller instances to the dedicated nodes. For detailed parameter descriptions, see the parameter descriptions of scheduling policies in [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

   * Sample figure for console operations:

   * YAML file code snippet:

      ```YAML
      tolerations:
      - effect: NoExecute
        key: ingress-nginx
        operator: Equal
        value: "true"
      ```
      

5. Configure the same taint toleration rule for DaemonSets, such as log\-collector. In this way, the corresponding instances can be deployed and run on the dedicated nodes.

6. Configure nodeSelector to schedule ingress\-nginx\-controller instances only to the dedicated nodes.

   ```YAML
   nodeSelector:
     ingress-nginx: "true"
   ```
   

7. Configure an anti\-affinity scheduling policy. In this way, the two instances of ingress\-nginx\-controller cannot be scheduled to the same node, which ensures high reliability.

   ```YAML
   podAntiAffinity:
     requiredDuringSchedulingIgnoredDuringExecution:
     - labelSelector:
         matchLabels:
           app.kubernetes.io/name: ingress-nginx
       namespaces:
       - kube-system
       topologyKey: kubernetes.io/hostname
   ```
   

8. After configuration is complete, view the deployment status of ingress\-nginx\-controller instances.


<span id=".55uR5o6n5ZKM5ZGK6K2m"></span>
### Monitoring and alerting

You can use cloud\-native observability to monitor ingress\-nginx\-controller and configure alerts based on your business requirements. For details, see [Ingress service observability](https://docs.byteplus.com/en/docs/vke/Ingress-observability).

<span id=".5pel5b-X5oyB5LmF5YyW"></span>
### Log persistence

By default, ingress\-nginx\-controller logs are not persistently stored. You need to configure and enable log persistence to persistently collect, store, and query ingress\-nginx\-controller logs. To better display the content of ingress\-nginx\-controller logs and improve readability, VKE provides ingress\-nginx\-controller log collection as an independent feature.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You need to activate TLS. To activate it, log in to the <a href="https://console.byteplus.com/tls">TLS console</a> and follow the on\-screen prompts.</div>


* <div data-tips="true" data-tips-type="tip">You need to install the <strong>log\-collector</strong> add\-on and <strong>ingress\-nginx</strong> add\-on. For related operations, see <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on">Installing add\-ons</a>.</div>


* <div data-tips="true" data-tips-type="tip">You need to create a <strong>log project</strong> and a <strong>log topic</strong> in TLS. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_projects">Log projects</a> and <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics">Log topics</a>.</div>


1. Enable the log collection feature for the ingress\-nginx add\-on. For detailed operations, see [Collecting the logs of the ingress-nginx add-on](https://docs.byteplus.com/en/docs/vke/Collecting-ingress-nginx-logs).

2. View the logs of the ingress\-nginx add\-on.

3. If you no longer need ingress\-nginx logs, you can click the **Addon log** tab and then click **Disable ingress access log**. After you disable this feature, the system will no longer collect logs from the ingress\-nginx\-controller add\-on.


<span id=".6Ieq5a6a5LmJ6YWN572u5Y6f55Sf5Y-C5pWw"></span>
### Specifying custom native parameters

In a Kubernetes cluster, Ingresses manage externally accessible API objects in cluster services and provide Layer 7 load balancing capability. Ingresses can be configured with advanced features, such as externally accessible URLs, rewrite configuration, HTTPS service, and canary release.

For ingress\-nginx\-controller, VKE adopts a configuration method fully compatible with the community. For configuration descriptions, see [Nginx configuration](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/).

Some advanced features and configurations natively supported by ingress\-nginx can be configured and achieved through annotations. Configurations in the annotation of each Ingress YAML only apply to the current Ingress. For more information, see [Annotations](https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/).

<span id=".6YWN572u56S65L6L77ya6Ieq5a6a5LmJ5pyA5aSn6K-35rGC5L2T"></span>
## Sample configuration: Specify the maximum request body size

For Nginx, when the request body size exceeds the maximum allowed value, a `413` error is returned to the client. You can specify this size by using the `client_max_body_size` parameter.


1. To specify a global parameter for all Ingresses in the cluster, add the proxy\-body\-size key\-value pair to the ingress\-nginx\-controller under kube\-system in the **ConfigMap**.

   After you update the ConfigMap, enter the ingress\-nginx\-controller container under kube\-system to check whether the Nginx configurations take effect.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_817610ef4bb50dacaa33b9c6a2da0824) </span>

2. To use a custom value for only a **specific Ingress**, add an annotation to this Ingress.

   ```Bash
   nginx.ingress.kubernetes.io/proxy-body-size: 20m
   ```
   

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_97b8bcd2316aa1e7e46aae7cbcc617bd) </span>
