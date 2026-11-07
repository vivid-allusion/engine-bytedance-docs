---
title: "Creating and managing a server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Managing-server-groups"
---

This topic explains how to create and manage server groups in the ALB console.

<span id=".5Yib5bu65pyN5Yqh5Zmo57uE"></span>
## Create server group

<span id="tWMAzbJ2"></span>
### Action notes


* After creating an ALB instance, you need to create a server group and add at least one backend server to handle client requests.

* Correspondence between listener type, backend communication protocol, and health check protocol is as follows:

   
   |**Listener type** |**Communication protocol** |**Health check protocol** |
   |---|---|---|
   |HTTP |HTTP, HTTPS |HTTP, TCP |
   |HTTPS |HTTP, HTTPS |HTTP, TCP |
   |QUIC |HTTP, HTTPS |HTTP, TCP |
   |HTTP/2 |HTTP, HTTPS, gRPC |HTTP, TCP |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">gRPC is a high\-performance, open\-source remote procedure call (RPC) framework developed by Google. gRPC is implemented based on the HTTP/2 protocol, leveraging its advantages such as multiplexing, header compression, binary framing, and server push. Additionally, gRPC uses Protocol Buffers as its Interface Definition Language (IDL) and default binary serialization protocol, supporting cross\-language, cross\-platform service communication. These characteristics make gRPC suitable for scenarios like microservices architecture, cloud\-native applications, and real\-time data transmission.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only Standard Edition ALB instances support HTTPS and gRPC as backend communication protocols. To use these protocols, please contact your account manager.   </div>
   


<span id="FxR9lKBV"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click **Create backend server group**.

5. To configure the related parameters, see the table below.

   
   |**Configuration item** |**Description** |Sample value |
   |---|---|---|
   |Server group type |Select the type of server group to create. Both server type and IP type are supported.<br><br><br>* **Server type**:<br><br>   * Only ECS instances and secondary network interfaces bound to ECS instances can be added as backend servers.<br><br>   * The added ECS instances and secondary network interfaces must belong to the same VPC as the server group.<br><br>* **IP type**:<br><br>   * Only IP addresses can be added as backend servers.<br><br>   * Before enabling the "Remote IP" feature, any IP address you add must belong to the same VPC as the server group. After enabling the "Remote IP" feature, you can add IP addresses from a different VPC than the server group, or IP addresses from a local IDC.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The IP\-type server group is in beta stage. If you need a trial, please contact your account manager.   </div><br>    |Server type |
   |Name |Enter server group name The naming rules are as follows:<br><br><br>* Must start with a Chinese character or an English letter.<br><br>* Only Chinese characters, English letters, numbers, periods (.), underscores (_), and hyphens (\-) are allowed.<br><br>* A maximum of 128 characters is allowed. |ServerGroup\-A |
   |VPC |Select the VPC to which the server group belongs. The server group and the ALB instance it will be associated with must reside in the same VPC. |VPC\-A |
   |Load balancing algorithm |Specify the scheduling algorithm. The scheduling algorithm at the server group level is also called the load balancing algorithm. This algorithm determines how client requests are distributed among backend servers.<br><br><br>* **Weighted Round Robin (WRR)** : ALB generates a fixed request allocation sequence based on preset weights. Within a polling cycle, backend servers with higher weights receive more requests. The WRR algorithm only considers the backend servers' weights, not their load. It is suitable for scenarios where request processing times are relatively consistent, but the performance of different backend servers varies significantly.<br><br>* **Weighted Least Connections (WLC)** : ALB dynamically calculates the load metric for each backend server and then routes new requests to the server with the lowest load metric. A server's load metric is equal to its current number of connections divided by its weight. The WLC algorithm considers both the load and weight of backend servers. It is suitable for scenarios where request processing times vary greatly.<br><br>* **Source Address Hash (SH)** : Requests from the same source IP address are always routed to the same backend server. The SH algorithm does not consider the weight or load of backend servers. It is suitable for scenarios requiring session persistence based on source IP. |Weighted Round Robin (WRR) |
   |Communication protocol |Specify the communication protocol between the ALB instance and the backend server.<br><br>The protocol can be HTTP, HTTPS, or gRPC.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The backend communication protocol cannot be changed after the server group is created.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only Standard Edition ALB instances support HTTPS and gRPC.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Server groups with gRPC enabled can only be associated with HTTP/2 listeners.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">They also only support forwarding rules where the specified forwarding action is "Forward to".</div><br> |HTTP |
   |Health Check |Select whether to enable the health check feature.<br><br>Health check is enabled by default. After a server group is associated with a listener, ALB initiates health check requests to backend servers according to specified rules to monitor their health status.<br><br>You can disable the health check feature as needed. However, if this feature is disabled, ALB cannot determine the health status of backend servers. If a backend server is actually abnormal, ALB will still forward requests to it.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the health check feature is enabled, there are some default health check configurations. Please review these default settings to ensure they meet your expectations. You can also adjust the configurations as needed.</div><br> |Enable |
   |Health check template |Set the health check template. You can select an existing health check template or choose **Custom health check**. |Custom health check |
   |Health check protocol |When you set the **Health check template** to **Custom health check**, you need to configure the health check protocol.<br><br>The health check protocol can be HTTP or TCP:<br><br><br>* HTTP: ALB sends a GET or HEAD request to the backend server and determines the health check result based on the HTTP response code. If the backend server returns a "Normal Status Code", the health check is considered successful.<br><br>* TCP: ALB attempts to establish a TCP connection with the backend server and determines the health check result based on the outcome of the TCP three\-way handshake. If the TCP three\-way handshake completes successfully, the health check is considered successful.<br><br><br>The required configuration parameters differ depending on the health check protocol. For details, see "Other health check configurations" section below. |HTTP |
   |Other Health Check Configurations (Health Check Protocol: HTTP) |When the health check protocol is HTTP, you need to configure the following health check parameters:<br><br><br>* **Health check port**: Specifies the port used by ALB for health checks. By default, the port of the backend server is used for the ALB health check. You can also specify a different port for health check.<br><br>* **Protocol version**: Specifies the version of health check protocol. Protocol versions: **HTTP1.0** and **HTTP1.1**.<br><br>* **Health check method**: Specifies the HTTP request method used by ALB when initiating health check requests.<br><br>   * GET: When ALB initiates a GET request, the backend server returns both HTTP response headers and the response body.<br><br>   * HEAD: When ALB initiates a GET request, the backend server returns both HTTP response headers and the response body. Compared to the GET method, this can reduce data transmission and lower the load on the backend server. When choosing this method, you must ensure that the backend server supports HEAD requests.<br><br>* **Health check domain**: Enter the domain name used by ALB for health checks. The value must meet the following requirements:<br><br>   * Only English letters, numbers, half\-width periods (.), and hyphens (\-) are allowed.<br><br>   * It must contain at least one half\-width period (.), but cannot begin or end with a half\-width period (.). Each level of the domain name cannot start or end with a hyphen (\-).<br><br>   * A maximum of 128 characters is allowed.<br><br>   * Must be an exact domain name that complies with domain name specifications, e.g., www.test.com. Wildcard domain names are currently not supported.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the protocol version is <strong>HTTP/1.0</strong>: If you do not specify a domain name, ALB uses the backend server's private IP address as the destination for health checks. However, the health check request will not include a Host header.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the protocol version is <strong>HTTP/1.1</strong>: If you do not specify a domain name, ALB uses the backend server's private IP address as the destination for health checks and uses this IP address as the value for the Host header in the health check request.   </div><br>   <br><br>* **Health check path**: Enter the specific URL path used by ALB for health checks. The default value is `/`, which indicates the root directory. The value must meet the following requirements:<br><br>   * Must start with a forward slash `/`.<br><br>   * A maximum of 128 characters is allowed.<br><br>   * Only English letters, numbers, and the following special characters are allowed: \-_ / .% ?# & ＝.<br><br>* **Normal status code**: Select the status codes that indicate a successful health check. You can check one or more of the following options: 2XX, 3XX, 4XX, and 5XX. 2XX and 3XX are selected by default.<br><br>   * If the actual response status code falls within your selected range(s), the health check is considered successful.<br><br>   * If the actual response status code does not fall within your selected range(s), the health check is considered failed.<br><br>   * For example: If you do not select 4XX, but the backend server returns a status code in the 4XX range, ALB will consider that health check attempt failed.<br><br>* **Response Timeout**: Set the response timeout period.<br><br>   * If ALB does not receive a response from the backend server within the specified time, it is judged as a timeout and the health check fails.<br><br>   * Value range: 1\-60. Default value: 2. Unit: seconds.<br><br>* **Detect interval**: Set the time interval at which ALB sends health check requests to a single backend server.<br><br>   * Value range: 1\-300. Default value: 2. Unit: seconds.<br><br>   * It is recommended to set this interval according to business needs to avoid frequent health check requests causing performance pressure on backend servers.<br><br>* **Health threshold**: Sets the healthy threshold, which is the number of consecutive successful health checks required to determine a backend server as normal.<br><br>   * Once this threshold is reached, ALB considers the abnormal backend server recovered and will continue to forward requests to it.<br><br>   * Value range: 2–10. Default value: 3.<br><br>* **Unhealthy threshold**: Sets the unhealthy threshold, which is the number of consecutive failed health checks required to determine a backend server as abnormal.<br><br>   * Once this threshold is reached, ALB considers the backend server abnormal and will stop forwarding requests to it.<br><br>   * Value range: 2–10. Default value: 3. |\-\- |
   |Other Health Check Configurations (Health Check Protocol: TCP) |When the health check protocol is TCP, you need to configure the following health check parameters:<br><br><br>* **Health check port**: Specifies the port used by ALB for health checks. By default, the port of the backend server is used for the ALB health check. You can also specify a different port for health check.<br><br>* **Response Timeout**: Set the response timeout period.<br><br>   * If ALB does not receive a response from the backend server within the specified time, it is judged as a timeout and the health check fails.<br><br>   * Value range: 1\-60. Default value: 2. Unit: seconds.<br><br>* **Detect interval**: Set the time interval at which ALB sends health check requests to a single backend server.<br><br>   * Value range: 1\-300. Default value: 2. Unit: seconds.<br><br>   * It is recommended to set this interval according to business needs to avoid frequent health check requests causing performance pressure on backend servers.<br><br>* **Health threshold**: Sets the healthy threshold, which is the number of consecutive successful health checks required to determine a backend server as normal.<br><br>   * Once this threshold is reached, ALB considers the backend server recovered and will continue to forward requests to it.<br><br>   * Value range: 2–10. Default value: 3.<br><br>* **Unhealthy threshold**: Sets the unhealthy threshold, which is the number of consecutive failed health checks required to determine a backend server as abnormal.<br><br>   * Once this threshold is reached, ALB considers the backend server abnormal and will stop forwarding requests to it.<br><br>   * Value range: 2–10. Default value: 3. |\-\- |
   |Cross\-zone load balancing |Configure the cross\-zone load balancing feature at the server group level. This feature is enabled by default.<br><br>For a detailed introduction to the cross\-zone load balancing feature, see [Cross-zone load balancer](https://docs.byteplus.com/docs/clb/Cross-zone-load-balancing). |Enable |
   |Session Persistence |Set session persistence feature. This feature is disabled by default. After enabling the session persistence feature, ALB forwards requests from the same client to the same backend server.<br><br>ALB supports the following session persistence modes:<br><br><br>* **Cookie placement**: When a client sends its first request to ALB, ALB selects a backend server based on the load balancing algorithm, processes the request, and inserts a Cookie in the response returned to the client. When subsequent client requests carry this Cookie, the ALB forwards them to the corresponding backend server.<br><br>   When selecting this mode, you need to set a session persistence timeout period. The timeout period determines the validity duration of the inserted Cookie in the client's browser.<br><br>* **Rewrite cookie**: You need to specify the name of the Cookie to be rewritten. When the ALB detects that the backend server's response contains a Cookie with the specified name, it rewrites the value of that Cookie. When subsequent client requests carry the rewritten Cookie, the ALB forwards them to the corresponding backend server.<br><br><br>For more information on the session persistence feature, see [Configuring cookie-based session persistence](https://docs.byteplus.com/docs/clb/Cookie-based-session-persistence).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The priority of session persistence is higher than the load balancing algorithm. For example, if you set the Source IP Hash algorithm for a server group and also enable session persistence for it, ALB will ignore the Source IP Hash algorithm. In this case:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">For the first request from a client, ALB defaults to selecting a backend server based on the Weighted Round Robin algorithm.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Subsequent requests from that client will always be forwarded to the same backend server.</div><br><br><br><br><div data-tips="true" data-tips-type="warning">If you prefer ALB to forward requests from the same client to the same backend server based on the Source IP Hash algorithm, do not enable session persistence.</div><br> |Disable |
   |Slow start |Enable slow start feature. After enabling, newly added backend servers in the server group will have their weights gradually increased by ALB from 0 to the configured target weight at a constant rate within the slow start duration. This achieves smooth distribution of service traffic and prevents the new backend from being instantly overwhelmed.<br><br><br>* The slow start feature can only be enabled when the scheduling algorithm of the server group is weighted round robin.<br><br>* Apart from adding new backend servers, restarting a backend server or recovering it from an abnormal state to a normal state will also trigger the slow start feature. |Enable |
   |Slow start duration |After enabling slow start, you need to configure the duration of the slow start period. Value range: 30 to 900 seconds. |60 |
   |Description |Enter the description of the server group. |\-\- |
   |Project |Select a project for the server group. A Project is a resource management method provided by BytePlus. Using projects, you can group and manage your cloud resources.<br><br>If you do not select a project, the server group will be added to the **default** project by default. |default |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources [Learn more](https://docs.byteplus.com/en/docs/clb/Tag-Overview)<br><br>Click the Add icon, enter the Tag key and Tag value, and add tags to the server group. |server\-key<br><br>server\-vaule |
   

6. Click **Save** to complete the action.


<span id="372d9445"></span>
### What to do next

After creating a server group, you can proceed with [Add backend server](https://docs.byteplus.com/docs/clb/Managing-server-groups#.5re75Yqg5ZCO56uv5pyN5Yqh5Zmo).

<span id=".5Yig6Zmk5pyN5Yqh5Zmo57uE"></span>
## Delete a server group

<span id="3XeAsca5"></span>
### Action notes


* After deletion, the association between backend servers and the server group is removed, but the backend servers themselves are not deleted.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Deleted server groups cannot be recovered, so please proceed with caution.   </div>
   

   * A server group that is already associated with a listener cannot be deleted. To delete it, you must first disassociate it. For detailed operations, see [Modifying and deleting a forwarding rule](https://docs.byteplus.com/docs/clb/Modifying-and-deleting-a-forwarding-rule).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click **Delete** to the right of the target server group.

5. Click **Delete** to complete the action.


<span id=".5re75Yqg5ZCO56uv5pyN5Yqh5Zmo"></span>
## Add server

<span id="NoCR09WY"></span>
### Action notes


* After creating a server group, you need to add backend servers to it to handle client requests.

* A server group can contain multiple backend servers. A single backend server can be added to multiple server groups.


<span id=".5re75Yqg5pyN5Yqh5Zmo57G75Z6L55qE5ZCO56uv5pyN5Yqh5Zmo"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click **Add backend server** to the right side of the target backend server group.

   * **Server type:** 

      1. On the **Select backend server** page, check the backend servers to add, then click **Next: configure ports and weights**.

         This page displays ECS instances that are in the same VPC as the backend server group. You can use the instance name, ID, or private IP address to search for the target ECS instance.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Currently, ALB only supports IPv4 backend servers.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The security group rules of the backend servers must allow traffic from the 100.64.0.0/10 CIDR block. Otherwise, client requests may fail to reach the backend servers, and health checks will also fail. For more information, see <a href="https://docs.byteplus.com/en/docs/clb/Allowing-ALB-to-access-back-end-servers">Configuring a backend server security group</a>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">After enabling Advanced mode on this page, you can select the secondary network interface attached to an ECS instance as the backend server. You can select the IP address(es) of one or multiple secondary network interfaces as needed. If using a secondary network interface as a backend server, you need to manually configure the network interface routing to ensure the backend server can correctly respond to requests from clients or the ALB instance. For more information, see <a href="https://docs.byteplus.com/en/docs/clb/Associating-a-secondary-network-interface-with-an-instance">Configuring a network interface routing</a>.         </div>
         

      2. On the **Configure ports and weights** page, set the port and weight for the backend servers.

         To batch\-configure the same port or weight for multiple backend servers, you can select those servers and click **Set same weight** or **Set same port** below the list, then enter a value.

         
         |**Configuration item** |**Description** |
         |---|---|
         |Port |Configure the port of backend server. The port used by the backend server to provide services and receive requests. Value range: 1\-65535. |
         |Weight |Set the weight of backend server. Default: 100. Value range: 0–100.<br><br><br>* Weight determines the proportion of traffic distribution. Backend servers with higher weights receive more requests.<br><br>* Proportion of requests received by a single backend server = (Weight of that backend server) / (Sum of weights of all backend servers in the server group).<br><br>* If the weight of a backend server is 0, ALB will not forward requests to it.<br><br>* When the load balancing algorithm applied to the server group is Source IP Hash, ALB will no longer forward requests based on weight values. |
         |Clone |Optional. Click **Clone** to duplicate an added backend server entry. After cloning, please enter a different port number in the new entry. This approach allows ALB to forward requests to different ports on the same backend server. |
         |Delete |Optional. Click **Delete** to delete the added backend server. |
         

      3. Click **Save** to complete the action.

   * **IP type** **:** 

      1. On the **Add IP address** page, add the IP address.

         This page displays the VPC ID and CIDR block to which this server group belongs.

         You can configure the added IP addresses according to your actual needs. Please see the table below for explanations of the related parameters.

         
         |**Configuration item** |**Description** |
         |---|---|
         |IP address |Enter the IP address of the backend server. The IP address must be a private IP address.<br><br><br>* You can add IP addresses from the VPC where the server group belongs. If you add the IP address of a secondary network interface attached to an ECS instance, you need to [configure network interface routing](https://docs.byteplus.com/docs/clb/Associating-a-secondary-network-interface-with-an-instance#0096abaf) to ensure the backend server can correctly respond to requests from clients or the ALB instance.<br><br>* With the Remote IP feature enabled and ensuring network connectivity, you can also add IP addresses from VPCs different from the server group's VPC or from your on\-premises IDC.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Currently, ALB only supports IPv4 backend servers.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The security group rules of the backend servers must allow traffic from the 100.64.0.0/10 CIDR block. Otherwise, client requests may fail to reach the backend servers, and health checks will also fail. For more information, see <a href="https://docs.byteplus.com/docs/clb/Allowing-ALB-to-access-back-end-servers">Configuring a backend server security group</a>.</div><br> |
         |Remote IP |Configure the "Remote IP" feature.<br><br><br>* When the added IP address does not belong to the VPC CIDR block of the server group, you must enable the remote IP feature.<br><br>* When the added IP address belongs to the VPC CIDR block of the server group, you do not need to enable the remote IP feature. |
         |Port |Configure the port of backend server. The port used by the backend server to provide services and receive requests. Value range: 1\-65535. |
         |Weight |Set the weight of backend server. Default: 100. Value range: 0–100.<br><br><br>* Weight determines the proportion of traffic distribution. Backend servers with higher weights receive more requests. Proportion of requests received by a single backend server = (Weight of that backend server) / (Sum of weights of all backend servers in the server group).<br><br>* If the weight of a backend server is 0, ALB will not forward requests to it.<br><br>* When the load balancing algorithm applied to the server group is Source IP Hash, ALB will no longer forward requests based on weight values. |
         |Add port |Optional. Click **Add port** to add more ports. This approach allows ALB to forward requests to different ports on the same backend server. |
         |Delete |Optional. Click **Delete** to delete the added backend server. |
         

      2. Click **Save** to complete the action.


<span id=".56e76Zmk5ZCO56uv5pyN5Yqh5Zmo"></span>
## Remove backend server

After a backend server is removed, ALB will no longer forward client requests to it.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click the name of the target backend server group.

5. On the **Backend server** tab, click **Delete** to the right of the target backend server.

6. Click **Delete** to complete the action.
