---
title: "Creating an ALB Ingress through the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console"
---

The Application Load Balancer (ALB) Ingress, built on the BytePlus ALB, delivers powerful Ingress traffic management that is capable of meeting the stability and availability demands of large\-scale Layer 7 processing in cloud\-native applications.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* To prevent cluster\-level Ingress exceptions, do not directly modify any components (including listeners, backend server groups, or forwarding rules) of the ALB instance managed by an ALB Ingress from the ALB console. Any such modifications are undertaken at your own risk.

* Do not modify any content prefixed with `k8s_` in the name of a listener or backend server group.

* Do not modify any content prefixed with `k8s_` in the description of a forwarding rule.

* Modifying the resource configuration specified or maintained by an ALB Ingress directly on the server side may pose a risk of the configuration being overwritten.

* If multiple ALB Ingresses specify different certificates for the same domain name and a certificate already exists for that domain name, the system will decide whether to overwrite the existing certificate according to the status of the certificate specified by the respective ALB Ingress:

   * If the certificate specified by the ALB Ingress does not exist, the existing certificate will not be overwritten.

   * If the certificate specified by the ALB Ingress has expired, the existing certificate will not be overwritten.

   * If the certificate specified by the ALB Ingress already exists and has not expired, the existing certificate will be overwritten.

* Using ALB incurs fees for the use of cloud infrastructure resources. For details, see [ALB billing](https://docs.byteplus.com/en/docs/clb/Billing-rules).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The clusters have been created. For details, see[ Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* (Optional) If you want to create an ALB Ingress that uses HTTPS, a certificate has been created. For details, see [Configuring ALB Ingresses over HTTPS](https://docs.byteplus.com/en/docs/vke/ALB_Ingress_configuring_the_HTTPS_protocol).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To use certificates from Certificate Center, log in to the BytePlus console with your account, click <a href="https://console.byteplus.com/iam/service/attach_role/?ServiceName=alb">Service authorization</a>, and on the page that appears, click <strong>Authorize now</strong> to complete cross\-service authorization.</div>



* (Optional) To configure the following features for an ALB Instance, make sure that you have completed necessary add\-on upgrade and configuration:

   * The alb\-ingress\-controller add\-on has been installed and upgraded to v0.31.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

   * To configure WAF protection for an ALB instance, create a Web Application Firewall instance in advance. For details, see [Creating WAF instances](https://docs.byteplus.com/en/docs/6511/75932).

   * To configure the log delivery feature for an ALB instance, create a log project and a log topic in advance. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects) and [Log topics](https://docs.byteplus.com/en/docs/tls/Managing_topics).

   * To configure an access control list (ACL) for an ALB listener, configure an access policy group in advance. For details, see [Access control](https://docs.byteplus.com/en/docs/clb/Access-control).

   * To specify custom configurations for the listener, create custom configurations in advance. For details, see [Custom configurations](https://docs.byteplus.com/en/docs/clb/Custom-configurations).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster for which you need to configure an Ingress.

4. In the left navigation bar of the cluster management page, click **Services and Ingresses \> Ingress**. On the page that appears, click **Create Ingress**.

5. Configure the Ingress based on the following instructions.

   * **Basic configuration**

      
      |Parameter |Description |
      |---|---|
      |Name |Specify an Ingress name based on the on\-screen prompts. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the Ingress belongs. We recommend that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Annotation |Click **Add annotation** to create an annotation, which is a key\-value pair. You can also configure specific annotations in the Ingress YAML files to achieve more comprehensive Layer 7 LoadBalancer capabilities and more diverse service routing rules. For details, see [Configuring ALB Ingresses by using annotations](https://docs.byteplus.com/en/docs/vke/Configuring-an-ALB-Ingress-using-annotations). |
      

   * **Ingress configuration**

      
      |Parameter |Description |
      |---|---|
      |Ingress type |The implementation of the Ingress controller. VKE provides three Ingress types based on different load balancer types. In this example, select **Application Load Balancer (ALB)** . |
      

   * **Load balancer configuration**

      
      |Parameter |Description |
      |---|---|
      |Port mapping |It is available only to clusters using the VPC\-CNI network model. This mode is enabled by default. This mode allows pods to directly serve as the backend of load balancing and supports health checks, eliminating the need for NodePort\-based forwarding.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The number of backend servers allowed by an ALB load balancer is limited, so you need to plan backend servers reasonably. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Limits">ALB constraints</a>.</div><br> |
      |Load balancer |Select an existing load balancer or have a new one automatically created. There are two access modes: **Internet** and **Private network**.<br><br><br>* **Use existing**: select an existing ALB instance or one that has been created for this cluster. When an ALB instance is reused, the existing listener rules are not overwritten, so ensure that the forwarding rules of the listener do not conflict.<br><br>* **Automatically create**: have a new ALB instance automatically created. You need to configure the following parameters. For detailed parameter descriptions, see [Creating ALB instances](https://docs.byteplus.com/en/docs/clb/Creating-an-instance):<br><br>   * **Name**: set a load balancer name in accordance with the displayed naming rules.<br><br>   * **Subnet**: select a private subnet that provides private IP addresses for LoadBalancer instances.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can select subnets in multiple availability zones to achieve high availability of containerized business applications.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After a LoadBalancer instance is created successfully, its private IP address cannot be changed.      </div><br>      <br><br>   * **Line type**: select the line type for public network services. Different line types vary in performance and billing. Supported line types include **BGP (multi\-line)** , **BGP convergence**, **China Mobile**, **China Telecom**, **and China Unicom**.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">All the line types, except <strong>BGP (multi\-line)</strong>, are beta features of Elastic IP Address. To apply for these beta features, contact your account manager.      </div><br>      <br><br>   * **Billing method**: select a billing method for the LoadBalancer instance. The following billing methods are available:<br><br>      * **Pay\-as\-you\-go \- bandwidth cap**: it will be charged based on usage duration with an upper limit on bandwidth.<br><br>      * **Pay\-as\-you\-go \- actual traffic**: it will be charged based on the actual amount of traffic flowing to the Internet instead of usage duration.<br><br>   * **Bandwidth upper limit**: the maximum bandwidth for Internet access measured in Mbps. The upper limit of bandwidth can be changed anytime as needed.<br><br>   * **Shared bandwidth package**: disabled by default. You can enable **Add to shared bandwidth package** and select an existing shared bandwidth package if necessary.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A shared bandwidth package is a cloud resource that can be reused to share bandwidth. Using a single shared bandwidth package to cover multiple public IPs within the same region or the IPv6 Internet bandwidth billing can help you reduce the cost for Internet access. For details, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/What-is-Bandwidth-Package">What is a shared bandwidth package?</a>      </div><br>      <br><br>   * **IP version**: select an IP version. Only **IPv4** is supported.<br><br>   * **Delete protection**: select whether to enable delete protection for the ALB instance. ‌Deletion protection prevents accidental deletion of the ALB instance via the console or OpenAPI. To delete the ALB Instance, you must first disable deletion protection on the basic information page of the ALB instance. |
      |Access log transmission to TLS |Configure the log delivery feature of the ALB instance. Click **Edit configuration**. In the pop\-up dialog box, specify a log project and log topic. |
      |Enable WAF protection |Configure WAF protection for the ALB instance. After you enable this feature, select a WAF instance. |
      |Backend server group |Configure the scheduling algorithm and health check for backend server groups that receive forwarded traffic:<br><br><br>* **Scheduling algorithm**: It is the rules that the listener follows when forwarding requests.<br><br>   * **Weighted Round Robin**: traffic is forwarded based on weight values. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>   * **Weighted Least Connection**: traffic is forwarded first to the backend with the smallest real\-time ratio of connections to weight.<br><br>   * **Source Hashing**: traffic is always forwarded to a single backend server if the hash of the source IP remains unchanged.<br><br>* **Health check**: optional and can be enabled if needed. If enabled, the following parameters are available:<br><br>   * **Health check method**: The request method for performing health checks on backend servers. Supported methods include **GET** and **HEAD**, with **GET** used by default.<br><br>      * The HEAD method allows the server to return only the headers and thereby reduces backend overhead. To use the HEAD method, ensure that your server supports this method.<br><br>      * To use the GET method, ensure that your server supports this method.<br><br>   * **Health check domain name**: After you specify a domain name for health check, ALB will set the domain name in the host field. If no domain name is configured, the host field will be empty, and ALB will not include the host field in the request. In this case, the default domain name is the internal network IP address of the backend server group.<br><br>   * **Health check path**: The default health check path is`/`. To perform a health check using a page other than the default homepage of the application server, you must specify the exact path.<br><br>   * **Normal status code**: Select status codes that indicate the normal status of your server. By default, **2xx** and **3xx** are selected.<br><br>   * **Response timeout**: the waiting time for health check response. It will be determined to be an anomaly if the backend server does not respond correctly within the specified time.<br><br>   * **Detection interval**: the time interval between health check requests. The default interval is 2 seconds, which means the backend server will be checked every 2 seconds.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The time interval of health check needs to be longer than the response timeout.      </div><br>      <br><br>   * **Health threshold**: the number of health check requests required to determine that the backend server is running properly. The default number is 3, which means the backend server is determined to be "healthy" if all the 3 requests get the responses indicating a normal status.<br><br>   * **Unhealthy threshold**: the number of health check requests to determine that the backend server is not running properly. The default number is 3, meaning that if a backend server is abnormal for three consecutive health checks, it is considered unhealthy. |
      

   * **Listener configuration**

      
      |Parameter |Description |
      |---|---|
      |Protocol |Select a protocol that is used for listening to backend server groups. Supported protocols include **HTTP** and **HTTPS**.<br><br>When the Ingress is created, the ALB instance automatically creates a listener based on your listener configuration, with the default name `k8s_<randomly generated string>`. |
      |Port number |The port number that the backend server group listens on. If you do not specify a port number, the default port number is `80` for **HTTP** and `443` for **HTTPS**. |
      |Certificate |When you select **HTTPS** for **Protocol**, you need to select a server certificate to support encryption and authentication for data transmission. You need to create a key and bind the server certificate. By default, all the specified domain names use the same key.<br><br><br>* Select a certificate source from the dropdown menu. You can select **All certificates**, **Application Load Balancer (ALB)** , or **Certificate Center**.<br><br>* Select a secret from the secret drop\-down menu. If no secret is available, click **Create Secret** to create one. When you create a secret, you need to configure the following parameters:<br><br>   * **Name**: set a secret name in accordance with the displayed naming rules. Secret names must be unique within the same namespace.<br><br>   * **Namespace**: select the namespace of this Ingress.<br><br>   * **Certificate source**: Choose the source of the encryption certificate. Supported sources include **Application Load Balancer (ALB)**  and **Certificate Center**.<br><br>   * **Project**: Select the project where the certificate is located.<br><br>   * **Server certificate**: select a server certificate.<br><br><br>Apart from the default behavior of binding all domains to the same key for an ALB Ingress, you can click **Add certificate** to specify a key for a particular domain . If a requested domain matches the specified domain, the key for the specified domain is used. If a requested domain does not match the specified domain, the default key for all domains is used.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta·Apply for trial</strong></a>] Creating HTTPS ALB Ingresses with certificates from Certificate Center is currently in beta.‌ To use this feature, contact your account manager to get a trial for your account.</div><br> |
      |Access control |Configure the ACL of the listener. Click **Edit configuration**. In the pop\-up dialog box, enable access control.<br><br><br>* **Control modes**: after you enable access control for the listener, you need to specify an access control mode. Valid values:<br><br>   * **Allowlist**: This mode allows access only from IP addresses within the selected policy group.<br><br>   * **Blocklist**: This mode denies access from IP addresses within the selected policy group.<br><br>* **Policy groups**: Configure policy groups.<br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><div data-tips="true" data-tips-type="default">You can select up to five policy groups. Each policy group can include up to 300 IP address entries. Each IP address entry can be an IP address or a CIDR address block. For more information about policy groups, see <a href="https://docs.byteplus.com/en/docs/clb/Access-control">Access control</a>.</div><br> |
      |Custom configuration |Implement custom configuration for ALB listeners. Click **Edit configuration**. In the pop\-up box, select an existing custom configuration policy. |
      

   * **Forwarding configuration**

      
      |Parameter |Description |
      |---|---|
      |Forwarding rules |If the target address of a request hits a forwarding rule, the request is forwarded to the corresponding **service**. Click **Add forwarding rule** to add one or more forwarding rules.<br><br><br>* **Domain name**: when the requested domain name matches the domain name set here, the request is forwarded to the specified service.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You cannot set a domain name pattern that ends with <code>*</code>.   </div><br>   <br><br>* **Path**: when the requested path matches the path set here, the request is forwarded to the specified service. You can configure path matching by using a regular expression or non\-regular expression. For details, see [Regular expression-based path matching.](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-using-kubectl#.5Yy56YWN5q2j5YiZ6KGo6L6-5byP6Lev5b6E)<br><br>* **Path matching rule**: ALB Ingresses support only prefix matching.<br><br>   **Prefix matching**: any path matching this prefix is accessible. For example, if the mapped URL is `/foo`, both `/foo/v1` and `/foo/v2` can access the backend service.<br><br>* **Service**: the target service and port to which the request is forwarded If no service is available, create a service based on the instructions in [Services](https://docs.byteplus.com/en/docs/vke/Service-overview).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the network model of the cluster is Flannel, you can select only a NodePort or LoadBalancer service.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the network model of the cluster is VPC\-CNI:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the <strong>LB\-to\-pod direct access mode</strong> is enabled for the Ingress, you can select a NodePort, LoadBalancer, or ClusterIP service.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the <strong>LB\-to\-pod direct access mode</strong> is not enabled for the Ingress, you can select only a NodePort or LoadBalancer service.   </div><br>   <br><br>* **Traffic speed limit**: [[Beta·Apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] By default, this feature is not enabled. After you enable this feature, set the **requests per second (QPS)**  to reasonably limit the request rate and prevent complete service disruption from excessive requests to certain components of the service. |
      

6. Click **Confirm** to create the Ingress.
