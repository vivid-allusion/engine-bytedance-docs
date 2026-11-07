---
title: "Ingress diagnosis"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Ingress_diagnosis"
---

Ingress diagnosis helps you identify risks in Ingress resources, such as ALB Ingresses and CLB Ingresses, within VKE clusters. This topic describes how to configure the Ingress diagnosis feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The Ingress feature has been configured. For details, see [Ingresses](https://docs.byteplus.com/en/docs/vke/Ingresses).

<span id=".6YWN572u6K-K5pat"></span>
## Configuring diagnosis


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Diagnosis**. On the page that appears, click **Create diagnosis task** to configure an Ingress diagnostic task.

   
   |Parameter |Description |
   |---|---|
   |Diagnosis type |Specify the type of resource to be diagnosed. For this example, select **Ingress**. |
   |URL address |Specify the URL address to be diagnosed. |
   

4. Click **Confirm** to complete the configuration. The system will start the diagnosis and generate a diagnostic report.


<span id=".5p-l55yL6K-K5pat57uT5p6c"></span>
## Viewing diagnostic results

After the diagnostic task is complete, if it is in the **Anomaly** state, it indicates that risks exist. You can click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic report.

The diagnostic result will display all diagnostic items, including successful, failed, and warning ones. You need to view these items on the **Pending** tab and resolve the issues.

<span id=".5LiL6L296K-K5pat5oql5ZGK"></span>
## Downloading diagnostic reports

After the diagnostic task is complete, you can download the diagnostic report in PDF format.


1. After the diagnostic task is complete, click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic result.

2. Click **Download the report** in the upper\-right corner to download the diagnostic report in PDF format.


<span id=".6K-K5pat6aG56K-05piO5ZKM5L-u5aSN5bu66K6u"></span>
## Diagnostic item descriptions and fix suggestions

<span id=".aW5ncmVzcy3or4rmlq0="></span>
### Ingress diagnosis

Ingress diagnosis mainly checks the availability of Ingress resources in the cluster and the compliance of annotation usage with specifications. The following table describes the main check items.


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Whether the Ingress exists |Check whether the corresponding Ingress resources exist. |* Check whether the provided URL has a corresponding Ingress rule.<br><br>* If the URL is correct, the issue may lie with the Ingress rule. For example, a regular expression is used as the path instead of the `use-regex` annotation.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The provided URL must contain a complete domain name and path. For example, <code>example.com/demo</code>. Otherwise, the diagnosis will fail and indicate that the Ingress does not exist.</div><br> |\- |
|Whether an address exists on the Ingress |Check whether the address of the Ingress has been updated by the Ingress controller. |Check whether the corresponding Ingress controller exists for the IngressClass, and whether the controller is working as expected. For details, refer to the check results of other items. |\- |
|Whether the nginx.com/nginx.org annotation is used |Check whether a commercial Ingress annotation that starts with `nginx.com/nginx.org` is used. This configuration cannot be used on the community edition NGINX Ingress controller. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |
|Whether mirror\-uri is used |Check whether the `nginx.ingress.kubernetes.io/mirror-uri` annotation is used. This annotation was deprecated in v0.24.0. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |
|Whether grpc\-backend is used |Check whether the `nginx.ingress.kubernetes.io/grpc-backend` annotation is used. This annotation was deprecated in v0.21.0. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |
|Whether base\-url\-scheme is used |Check whether the `nginx.ingress.kubernetes.io/base-url-scheme` annotation is used. This annotation was deprecated in v0.22.0. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |
|Whether session\-cookie\-hash is used |Check whether the `nginx.ingress.kubernetes.io/session-cookie-hash` annotation is used. This annotation was deprecated in v0.24.0. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |
|Whether secure\-backends are used |Check whether the `nginx.ingress.kubernetes.io/secure-backends` annotation is used. This annotation was deprecated in v0.21.0. |Check the current Ingress controller version. Remove this annotation or use another annotation. |\- |


<span id=".57uE5Lu26K-K5pat"></span>
### Add\-on diagnosis

Add\-on diagnosis mainly checks the startup parameters of the Ingress add\-on, the Ingress service, and whether pods work as expected. The following table describes the main check items.


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Proportion of ready pods for the Ingress |Check whether the proportion of ready pods in the Ingress Deployment is 100%. If the proportion is less than 100%, it indicates that an issue exists with the Ingress pod, such as a start failure or health check failure. |View the readiness status of ingress\-nginx\-controller for the Deployment in the kube\-system namespace. If necessary, view the events and process the fault based on the event prompts. |\- |
|Whether the Ingress service exists |Check whether the service exists in the Ingress startup parameters. After this service is deleted, the Ingress may fail to start. |Check whether the service is mistakenly deleted, and fix the issue. |[Creating NGINX Ingresses in the console](https://docs.byteplus.com/en/docs/vke/Creating-an-Nginx-Ingress-in-the-console) |
|Whether the Ingress service has events |Check whether warning or error events exist on the Ingress service. This may be caused by invalid CLB instance configurations. |View the warning or error events of the service and process the fault based on the event prompts. |\- |
|Whether the Ingress service has endpoints |Check whether the Ingress service has valid endpoints. If endpoints do not exist, the CLB instance will be unable to forward traffic to the Ingress controller. |* Check whether the configurations of the label selector for the service are correct.<br><br>* Check whether the back\-end pods of the service are mistakenly deleted, and fix the issue. |\- |
|Whether the Ingress service is of the Load Balancer type |Check whether the service specified in the Ingress startup parameters is of the LoadBalancer type. If it is not of this type, the Ingress controller may not be accessed over the public network. |Check whether a service of the Load Balancer type is required.<br><br><br>* Not required: This warning can be ignored.<br><br>* Required: Change the type of service to Load Balancer. |[Creating Load Balancer services via the console](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console) |
|Whether the Ingress service has external IP addresses |Check whether an IP address is allocated to the service. If it does not exist, the Ingress cannot be accessed over the public network. |View service events and check whether the service status and the CLB quota are normal. |\- |
|Whether the leader pod exists |Check whether the leader election is successful and whether a leader pod exists. If it does not exist, this may be because the pod may start for a short period, or some issues exist with the Ingress controller permissions configuration. |\- |\- |
|External traffic policy of the Ingress service |Check the external traffic policy of the service, which is used to distribute external traffic after being routed to the cluster. |The default external traffic policy is `Local`, which can be changed to `Cluster`. We recommend that you use `Local` mode. Otherwise, the client source IP may not be retained, which will result in inaccurate CLB instance health checks. |[NodePort](https://docs.byteplus.com/en/docs/vke/NodePort) |


<span id=".Y2xiLeiviuaWrQ=="></span>
### CLB instance diagnosis

CLB instance diagnosis mainly checks the status, maximum number of connections, QPS, and health check for the Ingress controller CLB instance. The following table describes the main check items.


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Health check failure of the Ingress controller CLB instance |Check whether the CLB instance has health check failures in the last 3 days. This may be caused by excessive add\-on load or configuration errors. |Check whether exceptions occur on the Ingress controller service, and whether the add\-on load is high. Process the fault based on the event prompts. |\- |
|Whether the CLB instance of the Ingress controller exists |Check whether the CLB instance of the Ingress controller exists. |In the [CLB console ](https://console.byteplus.com/clb), check whether the corresponding CLB instance exists. If the CLB instance was mistakenly deleted, you can restore it by recreating the service. |\- |
|CLB instance ID |Check whether the CLB instance ID of the Ingress controller exists. |\- |\- |
|Health check status of the Ingress controller CLB instance |Check whether the health check status of the CLB instance back\-end servers that correspond to the Ingress is normal. |Check whether exceptions occur on the Ingress controller service, and whether the add\-on load is high. |\- |
|New connection rate of the Ingress controller CLB instance |Check whether the maximum rate of new connections for the CLB instance in the last 3 days exceeds 80% of the upper limit. After the rate of new connections reaches the upper limit, new connections cannot be established for a short period of time, which will cause client access failures. |The new CLB connections are excessive. To prevent your business from being affected, upgrade the instance type. |[Configuring the Load Balancer service using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) |
|Maximum number of connections for the Ingress controller CLB instance |Check whether the maximum number of CLB connections in the last 3 days exceeds 80% of the upper limit. After the number of connections reaches the upper limit, new connections cannot be established, which may cause clients to be unable to access the service. |The maximum CLB connections are excessive. To prevent your business from being affected, upgrade the instance type. |[Configuring the Load Balancer service using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-a-LoadBalancer-Service-using-annotations) |
|Whether Host and SecretName are configured during TLS configuration |Check whether both the `Host` and `SecretName` fields are configured when the Ingress TLS rule is configured. |Specify both the `Host` and `SecretName` fields, and make sure that the `Host` field matches the certificate information. |[Configuring HTTPS for Nginx Ingress](https://docs.byteplus.com/en/docs/vke/Configuring-HTTPS-for-an-Nginx-Ingress) |
