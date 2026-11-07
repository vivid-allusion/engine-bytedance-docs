---
title: "Creating an NLB Service via the console"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating_an_NLB_Service_via_the_console"
---

VKE supports creating a LoadBalancer Service using an NLB. This topic describes how to create an NLB Service via the console.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring a LoadBalancer Service, be sure to carefully read <a href="https://docs.byteplus.com/en/docs/vke/LoadBalancer_service_usage_precautions">Considerations for using LoadBalancer Services</a>.</div>


<span id="eDXRgClM"></span>
## Usage limits


* Only the VPC\-CNI network model supports the LB\-to\-pod direct access mode, which allows direct binding of the auxiliary Pod ENI to the backend of an NLB.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In LB\-to\-pod direct access mode, the number of backend servers allowed by an NLB is limited and must be planned appropriately. For details, see <a href="https://docs.byteplus.com/en/docs/clb/NLB-Constraints">NLB constraints</a>.   </div>
   

* To connect to an NLB instance, make sure that the cloud\-controller\-manager add\-on is upgraded to v1.46.0 or later. For details, see [cloud-controller-manager](https://docs.byteplus.com/en/docs/vke/cloud-controller-manager-add-on).


<span id="5qEBKX3Z"></span>
## Prerequisites


* A workload has been created. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment), [Creating StatefulSets](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet), and [Creating DaemonSets](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Currently, only the following workloads can be associated: Deployment, StatefulSet, and DaemonSet.   </div>
   

<span id="bEAXov0V"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Services and Ingresses** \> **Service**. On the page that appears, click **Create Service** to configure a Service.

   * **Basic information**

      
      |**Parameter** |**Description** |
      |---|---|
      |Name |Enter a name for the Service. Make sure the name is unique under the same namespace. |
      |Namespace |Select the namespace to which the Service belongs. It is recommended that you select the namespace created by yourself or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
      |Tag |Click **Add new** to configure labels for the Service. Labels are used to define various attributes of Services, facilitating batch filtering and other operations. |
      |Annotation |Click **Add annotation** to add a key\-value pair as an annotation to the Service. You can also implement more load balancing capabilities by configuring specific annotations in the YAML file for the Service. For details, see [Using annotations to configure an NLB Service](https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations). |
      

   * **Access configuration**

      
      |**Parameter** |**Description** |
      |---|---|
      |Access type |Configure the access type for the Service. For this example, select **LoadBalancer**. |
      |Load balancing type |Configure the load balancing type for the Service. In this example, select **NLB**. |
      |LB\-to\-pod direct access mode |This parameter is shown only in clusters using the VPC\-CNI network model. It is enabled by default. When it is enabled, the Pod ENI is directly bound to the backend of the load balancer. Note that the load balancer cannot handle too many backend servers. Therefore, you need to make sure the number of servers is acceptable to the load balancer in the topology. For details, see [NLB constraints](https://docs.byteplus.com/en/docs/clb/NLB-Constraints). |
      |Load balancer |Configure the load balancer instance for the Service. You can select an instance or have one automatically created as needed. There are two access modes: **Public NAT for internet endpoint** and **Private network**.<br><br><br>* **Use existing**: Only existing NLB instances that are not used in VKE are supported. If you use an existing NLB instance, the existing listener rules of that instance are not overwritten. We recommend selecting newly created NLB instances unless under special circumstances.<br><br>* **Automatically create**: Automatically create a new NLB instance. You need to configure the following parameters. For parameter details, see [Creating NLB instances](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not use automatically created NLB instances in other Ingress or Service resources to prevent orphaned resources.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Automatically created NLB instances will be deleted synchronously when the Service is deleted. Do not manually modify the listener configuration of such NLB instances.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use existing NLB instances, only NLB instances created via the Load Balancer console are supported, whereas NLB instances created via the VKE console are not supported.   </div><br>   <br><br>   * **Name**: Provide a custom NLB instance name that complies with on\-screen naming rules.<br><br>   * **IP version**: Configure the IP version for the NLB instance. Currently, only IPv4 is supported and cannot be changed.<br><br>   * **Availability zones and subnets**: Select the availability zone and subnet for the NLB instance. Multiple availability zones can be configured simultaneously to achieve a high\-availability deployment.<br><br>      * **Subnet**: Select the subnets for deploying the NLB instance and allocate either public or private IP addresses.<br><br>      * **IPv4 address**: Select the method for allocating IP addresses to the NLB instance. After the NLB instance is created successfully, its private IP address cannot be changed.<br><br>         * **Automatically allocate IP**: Automatically allocate 3 private IPv4 addresses to the NIC associated with the NLB, including 1 Service IP address and 2 Local IP addresses.<br><br>         * **Manually allocate IP**: Manually enter an IPv4 address within the subnet range. The specified IPv4 address will be used as the Service IP address for the NIC associated with the NLB, and the system will also automatically allocate 2 Local IP addresses.<br><br>      * **Elastic IP Address**: Configure an EIP for the NLB instance. This parameter is required only when you configure an NLB instance of the **Public NAT for internet endpoint** type.<br><br>         * **Purchase a new EIP**: Purchase a new EIP when creating the NLB instance. The IP defaults to pay\-as\-you\-go billing based on actual traffic volume, with the BGP (multi\-line) line type and a maximum bandwidth of 200Mbps.<br><br>         * **Use an existing EIP**: Select an existing EIP. A valid EIP must meet the following conditions:<br><br>            * The EIP has not been added to a shared bandwidth package.<br><br>            * The EIP attributes (including line type, billing type, security protection type, and public egress) must be consistent across all availability zones for the same NLB instance.<br><br>   * **Security group**: Select at least one security group to associate with the NLB instance. In addition to the specified security groups, the NLB automatically associates a managed security group. For details, see [Managed security groups](https://docs.byteplus.com/en/docs/clb/NLB-Instance-Overview#.5a6J5YWo57uE).<br><br>   * **Cross\-zone forwarding**: When this option is enabled, traffic accessing the NLB can be forwarded to backend servers in other availability zones. This enhances disaster recovery and reliability, achieving high security isolation.<br><br>   * **Project**: Configure the owning project of the NLB instance. If a public NLB instance is added to a project, the EIP created synchronously is also added to the same project.<br><br>   * **Resource label**: Provide custom resource tags. Tags allow you to classify, search, and aggregate resources with similar characteristics from different dimensions. Click **Add new**, and enter the **key** and **value** based on the on\-screen prompts. |
      |Listener configuration |* **Whether to enable TLS**: Set whether the listener enables encrypted transmission over TLS. If this option is enabled, connections between the client and the load balancer use a TLS handshake and an encrypted channel.<br><br>* **Certificate source**: Configure the source of the server certificate used by the TLS listener. Currently supported options include **SSL certificate from BytePlus Certificate Center** and **Private certificate from BytePlus Certificate Center**.<br><br>* **Select a server certificate**: Select the server certificate used by the TLS listener.<br><br>* **Two\-way authentication**: Set whether to enable TLS two\-way authentication (mTLS). If this option is enabled, the server presents its certificate to the client, and the client also presents its certificate to the server. The load balancer validates the client certificate's validity based on the CA certificate you configured.<br><br>   * **CA certificate source**: When selecting two\-way authentication, choose the CA certificate type used to validate client certificates. Currently supported options include **Private root CA** and **Private subordinate CA**.<br><br>   * **CA certificate**: Configure the CA certificate used to validate client certificates during two\-way authentication.<br><br>* **TLS security policy**: Configure the type of security policy allowed for the TLS listener. Currently supports **System default policy** and **Custom policy**.<br><br>* **TLS security policy**: Select the TLS listener security policy. If you select **System default policy**, you can set it to a preset policy, such as **tls_cipher_policy_1_0, tls_cipher_policy_1_1, tls_cipher_policy_1_2, tls_cipher_policy_1_2_strict, or tls_cipher_policy_1_2_strict_with_1_3**. |
      |Backend server group |* **Scheduling algorithm**: These are the rules that the listener follows when forwarding requests.<br><br>   * **Weighted Round Robin**: Traffic is forwarded based on weight values. The higher the weight of the backend server, the more frequently (probabilistically) it is selected as the forwarding destination.<br><br>   * **Weighted Least Connection**: Traffic is forwarded first to the backend with the smallest real\-time ratio of connections to weight.<br><br>   * **Source Hashing**: Requests from the same source IP are forwarded to the same backend server based on consistent hashing on the source IP address.<br><br>* **Bypass the backend security groups**: After this option is enabled, traffic from the NLB instance is allowed by default and no longer undergoes validation against the backend ECS or ENI security group rules.<br><br>* **Health check**: Set whether to enable health checking as needed. If health checking is enabled, the following parameters are available:<br><br>   * **Health Check Protocol**: Select the protocol for health checks. Supported options include TCP, HTTP, and UDP.<br><br>   * **Health check port**: When the health check protocol is TCP or UDP, specify the port used for health checks. Supported options include **Use the backend server port** and **Specify a specific port**.<br><br>   * **Custom request/response**: When the health check protocol is UDP, you can configure a custom response string for a custom request string.<br><br>      * **Custom request**: The request string for health checks. It can contain only letters and numbers. The maximum length is 64 characters.<br><br>      * **Custom response**: The expected response string for health checks. It can contain only letters and numbers. The maximum length is 64 characters.<br><br>   * **Health check method**: When the health check protocol is HTTP, specify the method for health checks.<br><br>   * **Health check domain name**: When the health check protocol is HTTP, configure the domain name for health checks.<br><br>   * **Health check path**: When the health check protocol is HTTP, configure the path for health checks.<br><br>   * **Normal status code**: When the health check protocol is HTTP, specify the HTTP status code that indicates a normal health check.<br><br>   * **Response timeout**: The waiting time for a health check response. If the backend server does not respond correctly within the specified time, it is considered anomalous.<br><br>   * **Detection interval**: The time interval between health check requests. For example, if the interval is set to 10 seconds, a health check is performed on the backend server every 10 seconds.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The time interval of health check needs to be longer than the response timeout.      </div><br>      <br><br>   * **Health threshold**: The number of health check requests required to determine that the backend server is running as expected. For example, if the value is set to 3, the backend server is considered healthy if it passes 3 consecutive health checks with a "Normal" result.<br><br>   * **Unhealthy threshold**: The number of health check requests required to mark a backend server as unhealthy. For example, if the value is set to 3, the backend server is considered unhealthy if it fails 3 consecutive health checks with an "Abnormal" result. |
      |Port mapping |Create the mapping between the Service port and the container port:<br><br><br>* **Name**: Enter a name for the port mapping.<br><br>* **Service level port**: Enter a port used to access the Service. Duplicate ports are not allowed for Services using the same protocol.<br><br>* **Protocol**: Select **TCP** or **UDP**.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When health checking is enabled:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the health check protocol is TCP or HTTP, you can set this parameter to TCP or UDP.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the health check protocol is UDP, you can set this parameter to UDP.   </div><br>   <br><br>* **Container port**: Specify the port of the container, which is a port number through which the workload provides services externally. e.g., the default port number for Nginx is 80. |
      |Label selector |Services are bound to backend pods through label selectors.<br><br><br>* **Add new**: Specify the label on the workload to which the Service will be bound. You can find workload labels by clicking **Workload** in the left navigation pane of the cluster management page.<br><br>* **Associated workload**: Select the deployment with which the service will be associated. Currently, only Deployment, StatefulSet, and DaemonSet are supported.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When a LoadBalancer Service is associated with workloads deployed using VCI, only the <strong>LB\-to\-pod direct access mode</strong> is supported. In this case, the <strong>LB\-to\-pod direct access mode</strong> is enabled by default and cannot be disabled.</div><br> |
      

4. Click **Confirm** to finish configuration.


<span id="tYastV1h"></span>
## Validate results

The LoadBalancer Service you created successfully can be found in the Service list. The **External endpoint** is the public or private domain name of the NLB instance connected to this Service.

Find the target Service and select **Edit Yaml** from the drop\-down menu in the **Actions** column to view the configuration details of the Service, including the ID of the NLB instance connected to this Service. You can use the NLB instance ID to find the corresponding NLB instance in the [NLB console](https://console.byteplus.com/nlb).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a description of the annotations in the NLB Service configuration, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring_an_NLB_Service_using_annotations">Configuring NLB Services via annotations</a>.</div>


&nbsp;
