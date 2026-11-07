---
title: "Creating CLB Ingresses through the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-CLB-Ingress-in-the-console"
---

A CLB Ingress combines a load balancer and Ingress controller to enable more powerful Ingress traffic management. This topic describes how to configure a CLB Ingress.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you begin, thoroughly read <a href="https://docs.byteplus.com/en/docs/vke/Precautions_for_using_CLB_Ingress">CLB Ingress considerations</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool has been installed on your on\-premises computer. For details, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

* The target cluster has been connected through kubectl. For details, see [Connecting clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* A service has been created. For details, see [Creating services](https://docs.byteplus.com/en/docs/vke/NodePort).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the cluster for which you want to configure an Ingress.

4. In the left navigation bar, click **Services and Ingresses**. On the page that appears, click **Create Ingress**.

   * **Basic configuration**

      
      |Parameter |Description |
      |---|---|
      |Name |Specify an Ingress name based on the on\-screen prompts. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the Ingress belongs. We recommend that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Annotation |Click **Add annotation** to create an annotation, which is a key\-value pair. You can also configure specific annotations in the Ingress YAML files to achieve more comprehensive Layer 7 LoadBalancer capabilities and more diverse service routing rules. For details, see [Using annotations to configure CLB Ingresses](https://docs.byteplus.com/en/docs/vke/Configuring-a-CLB-Ingress-using-annotations). |
      

   * **Ingress configuration**

      
      |Parameter |Description |
      |---|---|
      |Ingress type |Select the type of Ingress controller. In this example, **CLB** is selected. |
      

   * **Load balancer configuration**

      
      |Parameter |Description |
      |---|---|
      |LB\-to\-pod direct access mode |It is available only to clusters using the VPC\-CNI network model. This mode is enabled by default. This mode allows pods to directly serve as the backend of load balancing and supports health checks, eliminating the need for NodePort\-based forwarding.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The number of backend servers supported by a CLB is limited, so you need to plan backend servers accordingly. For details about the limitations, see <a href="https://docs.byteplus.com/en/docs/clb/Product-Overview-07">Constraints and limits of CLB</a>.</div><br> |
      |Load balancer |Select an existing load balancer or have a new one automatically created. There are two access modes: **Public NAT for internet endpoint** and **Private access**.<br><br><br>* **Use existing**: Use an existing CLB instance that is not used by Vital Kubernetes Engine. Using an existing CLB instance will not bring any changes to the existing listener rules of that instance.<br><br>   We recommend creating a new CLB instance unless it is required to use the existing ones.<br><br>* **Automatically create**: Automatically create a new CLB instance. You need to configure the following parameters. For detailed parameter descriptions, see [Creating LoadBalancer instances](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not use this automatically created CLB instance in another Ingress or service to prevent orphaned resources.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The CLB created through Vital Kubernetes Engine console features multiple availability zones. If the current region supports fault tolerance across multiple availability zones, LoadBalancer instances are created in the primary and secondary availability zones by default. When the primary one fails, traffic is switched to the secondary one.   </div><br>   <br><br>   * **Name**: Set a load balancer name in accordance with the displayed naming rules.<br><br>   * **Subnet**: Select a private subnet that provides private IP addresses for LoadBalancer instances.<br><br>      After a LoadBalancer instance is created successfully, its private IP address cannot be changed.<br><br>   * **Line type**: Select a line type for Internet access. Different line types vary in performance and billing standards. Available options include **BGP (multi\-line)** , ** Fusion BGP**, **China Mobile**, **China Telecom**, and ** China Unicom**.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">All the line types, except <strong>BGP (multi\-line)</strong>, are beta features of Elastic IP Address. To apply for these beta features, contact your account manager.      </div><br>      <br><br>   * **Billing method**: Select a billing method for the LoadBalancer instance. The following billing methods are available:<br><br>      * **Pay\-as\-you\-go \- bandwidth limit**: It will be charged based on usage duration with an upper limit on bandwidth.<br><br>      * **Pay\-as\-you\-go \- actual traffic**: It will be charged based on the actual amount of traffic flowing to the Internet instead of usage duration.<br><br>      * **Bandwidth limit**: The maximum bandwidth for Internet access measured in Mbps. The upper limit of bandwidth can be changed anytime as needed.<br><br>      * **IP version**: Select an IP version. Currently, only **IPv4** is supported.<br><br>      * **Instance specification**: Select a CLB instance specification. You need to select a specification that meets your actual performance requirements for your application. For specification details, see [Product types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). |
      |Listener |The listener is responsible for monitoring the requests on the LoadBalancer and distributing traffic. You need to select a scheduling algorithm for the listener and decide whether to enable health check:<br><br><br>* **Scheduling algorithm**: It is the rules that the listener follows when forwarding requests.<br><br>   * **Weighted Round Robin**: Traffic is forwarded based on weight values. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>   * **Weighted Least Connection**: Traffic is forwarded first to the backend with the smallest real\-time ratio of connections to weight.<br><br>   * **Source Hashing**: Traffic is always forwarded to a single backend server if the hash of the source IP remains unchanged.<br><br>* **Health check**: Optional and can be enabled if needed. If enabled, the following parameters are available:<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The health check path for a CLB Ingress type only supports <code>/</code> and cannot be changed.   </div><br>   <br><br>   * **Health check method**: select a request method used to perform a health check on the listener. Available options include **GET** and **HEAD**. The **GET** method is used by default.<br><br>      * The HEAD method allows the server to return only the headers and thereby reduces backend overhead. To use the HEAD method, ensure that your server supports this method.<br><br>      * To use the GET method, ensure that your server supports this method.<br><br>   * **Normal status code**: select status codes that indicate the normal status of your server. By default, **2xx** and **3xx** are selected.<br><br>   * **Response timeout**: the waiting time for health check response. It is considered anomalous if the backend server fails to respond correctly within the specified time.<br><br>   * **Detection interval**: the time interval between health check requests. The default interval is 2 seconds, which means the backend server will be checked every 2 seconds.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The time interval of health check needs to be longer than the response timeout.      </div><br>      <br><br>   * **Health threshold**: the number of health check requests required to determine that the backend server is running properly. The default number is 3, which means the backend server is determined to be "healthy" if all the 3 requests get the responses indicating a normal status.<br><br>   * **Unhealthy threshold**: The number of health check requests required to mark a backend server as unhealthy. The default value is 3, meaning a backend server is marked "unhealthy" if all 3 requests return abnormal responses. |
      

   * **Listener configuration**

      
      |Parameter |Description |
      |---|---|
      |Protocol |Select a protocol for the listener. VKE supports two external protocols: **HTTP** and **HTTPS**.<br><br>When an Ingress is created, the CLB instance automatically provisions a listener based on your listener configurations. The listener follows the naming convention `k8s_ <namespace of the CLB Ingress>_<CLB Ingress name>_<port number>` (for example, `k8s_ default_demo-ingress_80`). |
      |Port number |The port number that the listener listens on. If you do not specify a port number, the default port number is `80` for **HTTP** and `443` for **HTTPS**. |
      |Certificate |When you select **HTTPS** for **Protocol**, you need to select a server certificate to support encryption and authentication for data transmission. You need to create a key and bind the server certificate. By default, all the specified domain names use the same key.<br><br><br>* Select a certificate source from the certificate drop\-down menu. Available certificate sources include **All certificates**, **CLB**, and ** Certificate center**.<br><br>* Select a secret from the secret drop\-down menu. If no secret is available, click **Create Secret** to create one. When you create a secret, you need to configure the following parameters:<br><br>   * **Name**: set a secret name in accordance with the displayed naming rules. Secret names must be unique within the same namespace.<br><br>   * **Namespace**: select the namespace of this Ingress.<br><br>   * **Certificate source**: select the source of the encryption certificate. Supported sources include **CLB** and ** Certificate center**.<br><br>   * **Project**: Select the project where the certificate is located.<br><br>   * **Server certificate**: select a server certificate.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using certificates from the certificate center to create HTTPS\-enabled CLB Ingresses is currently in the beta stage. To use this feature, contact your account manager to <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>apply for a trial</strong></a>.</div><br> |
      

   * **Forwarding configuration**

      
      |Parameter |Description |
      |---|---|
      |Forwarding rules |If the target address of a request hits a forwarding rule, the request is forwarded to the corresponding **service**. Click **Add forwarding rule** to add one or more forwarding rules.<br><br><br>* **Domain name**: When the requested domain name matches the domain name set here, the request is forwarded to the specified service.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You cannot set a domain name pattern that ends with <code>*</code>.   </div><br>   <br><br>* **Path**: When the requested path matches the one set here, the request is forwarded to the specified service.<br><br>* **Path matching rule**: A CLB Ingress supports only **prefix** matching. Any path that hits the prefix condition is accessible. For example, if the path is `/foo`, both `/foo/v1` and `/foo/v2` can access the backend service.<br><br>* **Service**: the target service and port to which the request is forwarded. If no service is available, create one by following steps described in [Services](https://docs.byteplus.com/en/docs/vke/Service-overview).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the network model of the cluster is Flannel, you can select a service only in the NodePort or LoadBalancer (direct pod access disabled) category.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the network model of the cluster is VPC\-CNI:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you enable <strong>LB\-to\-pod direct access mode</strong>, you can select a service in the NodePort, LoadBalancer (direct pod access enabled or disabled), or ClusterIP category.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not enable <strong>LB\-to\-pod direct access mode</strong>, you can select a service only in the NodePort or LoadBalancer (direct pod access enabled or disabled) category.   </div><br>    |
      

5. Click **Confirm**.
