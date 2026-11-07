---
title: "Creating APIG Ingresses in the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-APIG-Ingress-in-the-console"
---

Built based on [API Gateway (APIG)](https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway), APIG Ingress functions as a managed cloud\-native gateway that features Ingress traffic management that ensures high availability and scalability of cloud\-native applications.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* It is applicable only to clusters that use the VPC\-CNI network model.

* You will be charged for using APIG resources when you use APIG Ingresses.

* The APIG service is available only in certain regions and availability zones. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/apig/Regions_and_availability_zones).

* Do not change the APIG instance that is maintained by the APIG Ingress in the APIG console without authorization. Otherwise, configurations in the two consoles may become inconsistent, causing Ingress services in the cluster to behave abnormally, and you will be responsible for the consequences.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The APIG service has been activated. If the service is not activated, log in to the [APIG console](https://console.byteplus.com/veapig) and activate the service based on the on\-screen prompts.

* The apig\-controller add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A KubeConfig for private networks has been generated in the cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* (Optional) If you need to connect to an existing APIG instance, make sure that an instance in the **Running** state exists in the APIG console. For details, see [Creating instances](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the cluster for which you want to configure an Ingress.

4. In the left navigation bar of the cluster management page, click **Services and Ingresses \> Ingress**. On the page that appears, click **Create Ingress**.

5. Configure the Ingress based on the following instructions.

   * Basic configuration

      
      |Parameter |Description |
      |---|---|
      |Name |Specify an Ingress name based on the on\-screen prompts. The name must be unique within the same namespace. |
      |Namespace |Select the namespace to which the Ingress belongs. We recommend that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Annotation |Click **Add annotation** to create an annotation, which is a key\-value pair. |
      

   * Ingress type

      
      |Parameter |Description |
      |---|---|
      |Ingress type |The implementation type of the Ingress controller. For this example, select **Cloud\-native API gateway**. |
      

   * APIG specification settings

      
      |Parameter |Description |
      |---|---|
      |Gateway specifications |Select an existing gateway or choose to automatically create a gateway based on your business requirements. Valid values:<br><br><br>* **Use existing**: Selects a created APIG instance.<br><br>* **Automatically create**: automatically creates an APIG instance. You need to specify the following parameters:<br><br>   * **Name**: Specify a name for the APIG instance based on the naming rules promoted by the system.<br><br>   * **Subnet**: Configure availability zones and subnets for the APIG instance to allocate IP addresses within the Virtual Private Cloud (VPC).<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can select subnets in multiple availability zones to achieve high availability of containerized business applications.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You cannot change the private IP addresses of the APIG instance after it is created.      </div><br>      <br><br>   * **Billing method**: the billing method of the APIG instance. Valid values:<br><br>      * **Pay\-as\-you\-go \- by bandwidth limit**: The APIG instance will be charged based on the upper limit of bandwidth.<br><br>      * **Pay\-as\-you\-go \- by actual traffic**: The APIG instance will be charged based on the actual outbound traffic.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When you use the <strong>Pay\-as\-you\-go \- by actual traffic</strong> billing method, the instance is billed only based on actual traffic and is not affected by the bandwidth upper limit. However, you can control instantaneous traffic by configuring a bandwidth upper limit to keep the costs under control. In this case, the default bandwidth upper limit is 200 Mbit/s.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The Bandwidth limit parameter is used to specify the maximum bandwidth of the Load Balancer instance associated with the APIG. To increase the bandwidth, you can bind a custom Load Balancer instance in the APIG console. For details, see <a href="https://docs.byteplus.com/en/docs/apig/Adding_access_entrance">Adding access entrances</a>.      </div><br>      <br><br>   * **Bandwidth limit**: the maximum bandwidth of the public IP address. Unit: Mbit/s. After the instance is created, you can [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000170) to adjust the upper limit of public bandwidth.<br><br>   * **IP version**: Select an option. Only **IPv4** is supported.<br><br>   * **Instance specification**: Select or configure instance specifications. Valid values:<br><br>      * **Recommended specifications**: You can select system\-recommended APIG instance specifications. Metrics vary based on different specifications, such as node specifications, CLB specifications, and QPS performance.<br><br>      * **Custom specification**: You can specify instance specifications, including **Node specification**, **Number of replicas**, and **CLB specification** of the instance. |
      |Backend upstream |Configure the load balancing algorithm for the backend server group that receives forwarded traffic. Valid values:<br><br><br>* **Poll**: All requests are distributed to pods associated with the Kubernetes service in turn. This algorithm is suitable for scenarios where all pods have the same specifications.<br><br>* **Random**: Requests are randomly allocated to pods.<br><br>* **Minimum connections**: Requests are allocated to the pod with the smallest number of connections. |
      

   * Listener configuration

      
      |Parameter |Description |
      |---|---|
      |Protocol |Select a protocol for the listener. VKE supports two external protocols: **HTTP** and **HTTPS**. |
      |Certificate |When you select **HTTPS** for **Protocol**, you need to bind a server certificate to achieve encryption and authentication for data transmission. For details, see [Creating secrets](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, all domain names are bound to the same certificate after you select HTTPS. You can specify a domain name to use a specific certificate. In this case, if the requested domain name matches the specified domain name, the certificate specified for the domain name is used. Otherwise, the default certificate used by all domain names is used.</div><br> |
      

   * Forwarding configuration

      
      |Parameter |Description |
      |---|---|
      |Forwarding rules |If the target address of a request hits a forwarding rule, the request is forwarded to the corresponding **service**. Click **Add forwarding rule** to add one or more forwarding rules.<br><br><br>* **Domain name**: When the requested domain name matches the domain name set here, the request is forwarded to the specified service. When you select HTTPS and specify a certificate, the domain name set here must be consistent with the domain name in the certificate.<br><br>* **Path**: When the requested path matches the path set here, the request is forwarded to the specified service.<br><br>* **Path matching rule**: the path matching rule. Valid values:<br><br>   * **Prefix matching**: Any path that meets the prefix condition is accessible. For example, if the mapped URL is `/foo`, both `/foo/v1` and `/foo/v2` can access the backend service.<br><br>   * **Exact matching**: Only paths that exactly match the condition will be forwarded to the backend service.<br><br>* **Service**: the target service and port to which the request is forwarded. If no service is available, create a service based on the instructions in [Services](https://docs.byteplus.com/en/docs/vke/Service-overview). |
      

6. Click **Confirm** to create the APIG Ingress.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation

After the APIG Ingress is configured, you can log in to the [APIG console](https://console.byteplus.com/apig) to view the APIG instance that is synchronously created.

Click the name of the APIG instance to go to the instance details page, where you can view the information about the instance, such as **Service** and **Upstream**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about APIG configuration, see <a href="https://docs.byteplus.com/en/docs/apig/What_is_an_API_Gateway">APIG documentation</a>.</div>


<span id=".6L-Q57u06YWN572u"></span>
## Operation and maintenance configuration

<span id=".572R5YWz5a6e5L6L55uR5o6n"></span>
### APIG instance monitoring

After the APIG instance that corresponds to the APIG Ingress is created, you can use [Vital Managed Service for Prometheus (VMP)](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus) to implement monitoring and alerting for the APIG instance. For details, see [Monitoring and alerts](https://docs.byteplus.com/en/docs/apig/Monitoring_and_Alerts).

<span id=".5aaC5L2V5pu05o2iLWh0dHBzLeivgeS5pg=="></span>
### Replacing an HTTPS certificate

You need to perform the following steps to replace the HTTPS certificate for the APIG Ingress.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. On the Cluster page, click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar, click **Services and Ingresses \> Ingress**. In the Ingress list, find the Ingress for which you need to update the HTTPS certificate and click **Update** in the **Actions** column.

4. In the **Listener configuration** section, click **Create Secret ** to create a secret.

5. Create and upload the new certificate and key, and then click **Confirm** to update the Ingress.

6. Click the name of the target Ingress to go to the Ingress details page. Click the **Event** tab to view the successful reconciliation events for the Ingress.
