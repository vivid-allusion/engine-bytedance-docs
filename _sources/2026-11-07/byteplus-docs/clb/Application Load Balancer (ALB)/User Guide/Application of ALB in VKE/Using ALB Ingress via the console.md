---
title: "Using ALB Ingress via the console"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-an-ALB-Ingress"
---

Please configure and manage ALB Ingress in the VKE console. Do not configure or update it in the ALB console, as this may cause exceptions in the Ingress service. If your business requires configuring and managing ALB Ingress via the VKE console, please refer to this topic.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about Vital Kubernetes Engine (VKE), see <a href="https://docs.byteplus.com/en/docs/vke/Ingress-overview">Official documentation</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Vital Kubernetes Engine console](https://console.byteplus.com/vke).

2. In the left\-side navigation pane, click **Cluster**.

3. On the cluster list page, click the target cluster for which you need to configure routing rules.

4. In the left navigation pane of the cluster management page, select **Services and routes \> Route rules**, then click **Create route rule**.

5. Configure the routing rules according to the following instructions.

   **Basic configuration**

   
   |Parameter |Notes |
   |---|---|
   |Name |Configure the Name for the routing rule according to the system prompt.<br><br>The name must be unique within the same namespace. |
   |Namespace |Select the namespace to which the routing rule belongs.<br><br>It is recommended to choose a custom namespace you created or the system\-default **default** namespace. For more details on namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Annotation |Click **Add annotation** to add annotations (key\-value pairs) to the routing rule.<br><br>You can implement richer Layer\-7 load balancing capabilities and more diverse service routing rules by configuring specific annotations in the routing rule's YAML file. For detailed configuration via annotations, see [Configuring ALB Ingress via Annotations](https://docs.byteplus.com/en/docs/vke/Configuring-an-ALB-Ingress-using-annotations). |
   

   **Ingress configuration**

   
   |Parameter |Notes |
   |---|---|
   |Ingress type |Ingress Controller Implementation: Select **ALB**. |
   

   **Load balancer configuration**

   
   |Parameter |Notes |
   |---|---|
   |Load Balancer |Select an existing load balancer or automatically create a new one based on your business needs. Support both **Public** and **Private** access modes.<br><br><br>* Use Existing: Supports using an existing ALB instance that is already associated with and created for this cluster. When reusing the same ALB instance, existing listener rules will not be overwritten. Therefore, please ensure that the forwarding rules of the listeners do not conflict.<br><br>* Auto Create: Automatically creates a new ALB instance. You need to configure the following parameters. For detailed descriptions, see [Creating an instance](https://docs.byteplus.com/docs/clb/Creating-an-instance).<br><br>   * Name: Customize the name of the ALB instance according to the naming rules indicated by the system.<br><br>   * Subnet: Provides a private network deployment environment for the ALB instance and allocates a private IP address. The private IP address cannot be modified after the ALB instance is created successfully.<br><br>   * ISP: When creating a public network instance, you need to configure the line type for the internet service. Different line types vary in performance and billing standards. By default, only BGP (multi\-line) is supported.<br><br>   * Billing Method: When creating a public network instance, you must select the billing method for the internet service.<br><br>      * Pay\-by\-bandwidth: After specifying a bandwidth cap, you are billed based on usage duration, regardless of actual traffic.<br><br>      * Pay\-by\-data\-transfer: After specifying a bandwidth cap, you are billed based on the actual outbound internet traffic used, regardless of usage duration.<br><br>   * Bandwidth cap: The maximum bandwidth for the EIP, measured in Mbps. You can adjust the Internet bandwidth cap at any time as needed after the instance is created.<br><br>   * IP Version: The type of IP address version. Currently, only IPv4 is supported. |
   |Server group |Configure the scheduling algorithm and health check for the backend server group receiving traffic:<br><br><br>* Scheduling Algorithm: Specifies the algorithm used for traffic distribution among different backend servers within the group.<br><br>   * Weighted Round Robin (WRR): Backend servers with higher weights have a greater probability of receiving user requests. WRR is suitable for scenarios where request volume and processing time can be stably predicted.<br><br>   * Weighted Least Connections (WLC): The system calculates the value of "current connections / weight" for each backend server and schedules requests to the server with the smallest value. WLC is suitable for situations with high request volume and variable processing times, helping to resolve issues of excessive load on individual servers.<br><br>   * Source Address Hash (SH): Requests from the same source address are scheduled to the same backend server. The scheduling process is independent of server weight. Client requests will always be processed on a specific backend server, making it suitable for scenarios requiring session persistence.<br><br>* Health Check: Choose whether to enable health checks as needed. If health check enabled, configure the following parameters:<br><br>   * Health Check Method: The request method used to check the health of backend servers. Supports GET or HEAD, with GET being the default.<br><br>      * HEAD method: The server only returns header information, which can reduce backend overhead, but requires the server to support the HEAD method.<br><br>      * GET method: Requires the server to support the GET method.<br><br>   * Health Check Domain: If configured, the ALB will set this domain in the request's Host header. If left blank, the Host header will be empty, and the ALB will default to using the backend server's private IP instead of attaching a Host field.<br><br>   * Health Check Path: The default path is `/`. Specify a different path if the page used for health checks is not the application server's default homepage.<br><br>   * Normal status code: If a response code of the selected type is received, the server is determined to be normal. 2xx and 3xx are selected by default.<br><br>   * Response Timeout: The time to wait for a health check response. If the backend server does not respond correctly within the specified time, the health check will be marked as abnormal.<br><br>   * Check Interval: The time interval between health check executions. The default is 2 seconds, meaning a health check is performed every 2 seconds.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The check interval must be greater than the response timeout.      </div><br>      <br><br>   * Healthy threshold: The number of health checks to mark a backend server as normal. The default is 3. A backend server is determined to be normal after 3 consecutive successful health checks.<br><br>   * Unhealthy threshold: The number of health checks to mark a backend server as abnormal. The default is 3. A backend server is determined to be abnormal after 3 consecutive failed health checks. |
   

   **Listener configuration**

   
   |Parameter |Notes |
   |---|---|
   |Protocol |The protocol listened to by the backend server group. Vital Kubernetes Engine supports both **HTTP** and **HTTPS** protocols.<br><br>When the routing rule creation is complete, the ALB instance will automatically create a listener based on your configuration, with a default name format of `k8s_<randomly generated string>`. |
   |Certificate |When **HTTPS** is selected as the external **Protocol**, you need to bind a server certificate to support encrypted data transmission authentication. You need to create a key and bind it to a server certificate. By default, all domains will use the same key:<br><br>Click **Create key**, configure the key parameters as described below, then click **Create**.<br><br><br>* Name: Set a name for the key according to the system's naming rules. The name must be unique within the same namespace.<br><br>* Namespace: Select the same namespace as this routing rule.<br><br>* Server Certificate: Select the server certificate for the ALB instance. If no available certificate exists, see [Certificate management](https://docs.byteplus.com/docs/clb/Adding-and-deleting-a-certificate).<br><br>* Tags: Tags for the key, used to define different attributes for easier bulk filtering and management.<br><br><br>For ALB Ingress HTTPS, besides using a single certificate (Key) for all domains by default, you can also click **Add certificate** to bind a specific certificate to a specified domain. If the requested domain matches a specified domain, the key bound to that domain is used. If it does not match any specified domain, the default key for all domains is used. |
   

   **Forwarding configuration**

   
   |Parameter |Notes |
   |---|---|
   |Forwarding rules |When the access address of a request matches a forwarding rule, the request will be forwarded to the corresponding **Service** for processing. Click **Add forwarding policy** to add multiple forwarding policies.<br><br><br>* Domain: When the domain of a request matches the domain set here, the request is forwarded to the specified service.<br><br>* Path: When the path of a request matches the path set here, the request is forwarded to the specified service.<br><br>* Path Matching Rule: For ALB Ingress type routing rules, only prefix matching is currently supported.<br><br>* Service: The target service and port to which the request is forwarded. If no available service exists, create a service, see [Service](https://docs.byteplus.com/en/docs/vke/Service-overview) for details. |
   

6. Click **Create** to complete the ALB Ingress routing rule creation.
