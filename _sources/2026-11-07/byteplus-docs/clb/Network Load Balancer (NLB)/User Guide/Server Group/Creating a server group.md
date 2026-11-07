---
title: "Creating a server group"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The server group receives traffic forwarded by the Network Load Balancer (NLB) instance. To use NLB, you must create a server group and add at least one backend server.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select **Server group**.

4. Click **Create Server Group**, and refer to the table below to configure the basic information of the server group.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Name |Enter server group name |rsp01 |
   |Server Group Type |Select the type of the server group.<br><br><br>* Server Type: Only the Elastic Compute Service (ECS) instances or secondary network interfaces within the same VPC as the server group can be added as backend servers.<br><br>* IP Type: You can only add IP addresses as backend servers. You can add IP addresses from other VPCs or on\-premises IDCs as backend servers, as long as they are network\-reachable. |Server type |
   |IP version |Protocol type for the backend server's private IP address. Currently, only IPv4 backend servers can be added. |IPv4 |
   |VPC |Select a server group in the same Virtual Private Cloud (VPC) as the NLB instance. |vpc01 |
   |Backend protocol |The protocol used by the NLB instance to forward traffic to the backend server.<br><br><br>* TCP: Only support associating with TCP and TLS listeners.<br><br>* UDP: Only support associating with UDP listeners. |TCP |
   |Scheduling algorithm |Select the rules that the server group follows to forward requests.<br><br><br>* Weighted Round Robin (WRR): In this case, higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connection (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source hashing (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server.<br><br><br>[Prerequisite](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview) |Weighted Round Robin (WRR) |
   |Session Persistence |Enable session persistence<br><br><br>* After the sticky session feature is enabled, the NLB forwards access requests from the same Source IP address to the same backend server for processing.<br><br>* **Session persistence timeout period** ranges from 1 to 3600 seconds. |Disable |
   |Connection Draining |Enable Connection Draining<br><br><br>* After enabling, when a backend server is deleted or a health check exception occurs, existing connections will transmit normally within the connection draining timeout period.<br><br>* **Timeout period of connection draining** ranges from 0 to 900 seconds. |Disable |
   |Client IP Preservation |Whether to enable client IP address preservation.<br><br>After enabling, NLB instance forwards the Source IP address of the client to the server group. The backend server can obtain the client's source IP without additional settings. After the server group is created, you can view this information on the details page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The client IP Preservation function is unavailable in the following scenarios. You can obtain the source IP via the Proxy\-Protocol:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the IP version of the client request differs from the server group, enabling client IP Preservation will not take effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cannot be enabled when the server group type is set to <strong>IP type</strong>.</div><br> |Check |
   |Proxy\-Protocol |Enable the Proxy\-Protocol<br><br>After enabling, NLB instance forwards the Source IP address of the client to the server group through the Proxy\-Protocol protocol. The Proxy\-Protocol needs to be configured on the server. For detailed information on this feature, see [Obtaining client source IP](https://docs.byteplus.com/en/docs/clb/NLB-Obtaining-the-client-Source-IP-address). |Disable |
   |All\-port forwarding |When the service ports of all backend servers in the server group are the same as the listening port, you can enable all\-port forwarding.<br><br>When enabled, this server group only supports attaching listeners with all\-port forwarding enabled, and backend servers in the group do not need to specify ports. NLB forwards traffic to backend servers based on the front\-end request port (i.e., listening port) by default. |Disable |
   |Allowing backend security group |Enable the **Allow backend security group** feature. After enabling, the security group of backend servers in the Server Group no longer validates NLB traffic and is allowed by default. This feature has the following Precautions:<br><br><br>* Only Server Group of server type supports enabling this feature; Server Group of IP type does not support enabling.<br><br>* Enable this feature, existing connections will still go through backend security group rule verification and only apply to new connections. New connections will not go through backend security group rule verification.<br><br>* Disable this feature, existing connections will still bypass the security group rule verification and only apply to new connections. New connections will go through backend security group rule verification.<br><br>* If you need to restrict IP access to backend server services, do not enable this feature and continue to control it through the security group. |No |
   

5. Configure health check information according to the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Health check |Select whether to enable the health check feature. After enabling health checks, NLB can check whether the backend server status is normal, stop forwarding requests to abnormal backend servers, and ensure overall service availability.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling health checks may result in requests being forwarded to abnormal backend servers. To ensure continuous availability of the service, it is discouraged to disable health checks.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Health checks consume a certain amount of network resources. To minimize their impact on your business operations, it is advised to reduce the health check frequency and increase the interval between checks based on your specific workload.</div><br> |Check |
   |Health check protocol |The protocol type of the health check request.<br><br><br>* **TCP**: Send SYN handshake packets to detect whether the backend server port status is normal.<br><br>* **HTTP**: Sends HEAD or GET requests to simulate browsing behavior and check if the application of the backend server is functioning properly. HTTP\-specific parameters are as follows:<br><br>   * **Health check method**: Select the request method for performing health checks on backend servers.<br><br>      * **GET**: GET requests obtain responses that include both response headers and response body, requiring the server to support the GET method.<br><br>      * **HEAD**: HEAD request responses only return the response header information, reducing backend overhead. Support for the HEAD method is required on the server.<br><br>   * **Health check domain name**: Type the domain name of the health check request, which must be set to the actual externally\-facing address provided on the backend server. If not specified, the default backend server private IP address will be used.<br><br>   * **Health check path**: URL of the health check request. This parameter must be set to the real address of the backend server that provides services for entities beyond the local VPC. If not specified, the default is `/`.<br><br>   * **Health status code**: Configure the response code. If the selected type of response code is received, the server is determined to be in a normal and available state.<br><br>* UDP: Sends ICMP or UDP probing packets to detect whether the backend server is functioning properly. Unique arguments for UDP protocol are as follows:<br><br><br>Custom request/response: Enable or disable the switch for specifying health check characters.<br><br><br>   * Once enabled, configure the following parameters:<br><br>      * Custom request: Type the health check request characters.<br><br>      * Custom response: Type the character for the health check response.<br><br>   * When disabled, specifying a character is unnecessary.<br><br><br>[Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Health-check-overview)<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the backend protocol of the server group is TCP, health check does not support the UDP protocol.</div><br> |TCP |
   |Health check port |Configure the port used for the health check.<br><br><br>* **Use the backend server port**: Health checks are performed on the backend server's port by default, with no need to specify an additional port.<br><br>* **Specify a specific port**: This option is mandatory when the all\-port forwarding feature is enabled. Port ranges from 1 to 65535. |Use backend server port |
   |Response timeout |Configure the waiting time for the health check response.<br><br><br>* If no valid response is received from the backend server within the response timeout period, the health check is considered abnormal.<br><br>* Value range: 1 to 60 seconds. Default timeout period: 3 seconds. |3 seconds |
   |Detect interval |Enter the interval for performing health checks.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 3 to 300 seconds. The default interval is 10 seconds, meaning a health check is performed on the backend server every 10 seconds. |10 seconds |
   |Healthy threshold |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Normal**, its status changes from **Abnormal** to **Normal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
   |Unhealthy threshold |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are **Abnormal**, its status changes from **Normal** to **Abnormal**.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
   

6. Refer to the table below to configure the project and tag for the server group.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Affiliated Project |Select the project to which the server group belongs. [Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Project-Management) |default |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources [Prerequisite](https://docs.byteplus.com/en/docs/clb/Tag-management)<br><br>Click the Add icon, enter the Tag key and Tag value, and add tags to the server group. |* Tag key: rsp\-key<br><br>* Tag value: rsp\-test |
   

7. Click **OK** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Once the server group is created, you need to Add at least one backend server to process client access traffic properly.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateNLBServerGroup](https://docs.byteplus.com/en/docs/clb/CreateNLBServerGroup)
