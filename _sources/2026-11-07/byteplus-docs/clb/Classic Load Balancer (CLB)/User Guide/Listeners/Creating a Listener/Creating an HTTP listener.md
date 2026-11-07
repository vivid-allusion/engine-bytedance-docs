---
title: "Creating an HTTP listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener"
---

<span id="naXblh0H"></span>
## Instructions


* A port can only be listened to by one listener.

* A Classic Load Balancer (CLB) instance cannot create new listeners when the aggregate bandwidth of its existing listeners equals the instance's maximum bandwidth limit. If creation is still required, first either adjust bandwidth for existing listeners via [Edit Listener](https://docs.byteplus.com/en/docs/clb/Editing-the-listener) settings or upgrade the specification of the CLB instance through [Changing instance specification](https://docs.byteplus.com/en/docs/clb/CLB-instances-03) to ensure that the total bandwidth remains below the instance's maximum bandwidth limit.

* Currently, the Layer 7 listeners (HTTP/HTTPS) can only forward IPv6 access requests to IPv4 backend servers.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target project and target region.

3. Click **Configure Listener** on the right side of the target CLB instance.

4. Click **Add Listener**, and refer to the table below to complete the basic configuration of the listener.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Listener name |Configure the listener name. If left blank, it defaults to **Protocol\-port**, such as HTTP\-80. |listener\-1 |
   |CLB protocol |Select the protocol type for CLB instance listening. |HTTP |
   |Listening port |Specify the listening port. The listener will distribute access requests from this port to the backend server group. |80 |
   |Scheduling algorithm |Specify the rule that the listener should observe when forwarding requests.<br><br><br>* **WRR**: A server with a higher weight is assigned a larger share of the requests.<br><br>* **WLC**: The requests are distributed to the server with the smallest ratio of current connections to weight.<br><br>* **SH**: It is the source IP\-based consistent hashing algorithm that distributes requests with the same source IP to the same server. |WRR |
   

5. Configure the timeout period by referring to the table below.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Client connection idle timeout period |Input the long connection timeout period between the client and CLB. If there is no access request within the timeout period, CLB will terminate the current connection until a new connection is established when the next request arrives.<br><br>Input range: 0–900 seconds, where 0 means disabling the long connection. |75 seconds |
   |Client request header timeout period |Input the timeout period for reading the client's request header. The client makes a request to the CLB. If the client does not transmit the entire header within the timeout period, the CLB will return a 408 error code to the client, indicating a request timeout.<br><br>Input range: 30 to 120 seconds. |60 seconds |
   |Client request body timeout period |input the timeout period for reading the client's request body. The client initiates a request to the CLB. If the client does not send any request body within the timeout period, the CLB will return a 408 error code to the client, indicating that the request timed out.<br><br><br>* This timeout period is set only between two consecutive read actions, not for the entire transmission process of the request.<br><br>* Input range: 30 to 120 seconds. |60 seconds |
   |Client forwarding response timeout period |Input the timeout period for CLB to send responses to the client. CLB sends a response to the client. If the client does not receive any content within the timeout period, the connection will be disabled.<br><br><br>* This timeout is set only between two consecutive write operations, not for the entire response transmission process.<br><br>* Input range: 1 to 3600 seconds. |60 seconds |
   |Backend response timeout period |Input the timeout period for CLB to read the response from the backend server. CLB sends a request to the backend server. If the backend server receiving the request does not respond within the timeout period, the connection will be disabled.<br><br><br>* This timeout period is only set between two consecutive read operations, not for the entire response transmission process.<br><br>* Input range: 30–3600 seconds. |60 seconds |
   |Backend request forwarding timeout period |Input CLB to transmit requests to backend server's timeout period. CLB sends requests to the backend server, and if the backend server does not receive any content within the timeout period, this connection will be disabled.<br><br><br>* This timeout is set only for the period between two consecutive write operations, not the entire request transmission process.<br><br>* Input range: 30 to 3600 seconds. |60 seconds |
   |Backend server connection timeout period |Input the connection establishment timeout period between CLB and the backend server. If the connection between the CLB and the backend server is not established within the timeout period, terminate the connection establishment action.<br><br><br>* It is recommended to be greater than the health check timeout.<br><br>* Input range: 4 to 120 seconds. |4 seconds |
   

6. Configure more advanced features for the listener by referring to the table below.

   
   |Name |Explaination |Sample Value |
   |---|---|---|
   |Access Control<br><br> |Specify whether the allow list and deny list are configured on the listener, that is, allowing or denying access of certain IPs to the listener. The default value is Off. For details, refer to [ACL Overview](https://docs.byteplus.com/en/docs/clb/Access-control-list-01).<br><br>After enabling the Access Control List (ACL) feature, select the access control mode and ACL name.<br><br><br>* **Control mode**<br><br>   * Blocklist: Deny access to the CLB instance from IPs in the selected policy group. If no IP is added to the selected ACL, all source IPs are allowed to access this listener.<br><br>   * Allowlist: Only allow access to the CLB instance from IPs in the selected policy group. If no IP is added to the selected ACL, all source IPs are prohibited to access this listener.<br><br>* **ACL name**<br><br>   Select one or more ACLs. IPs in the ACLs will be added to the deny list or allow list. You can select up to five ACLs. If no policy group exists yet, click **Create access control policy group** in the selection box and refer to [Creating a policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups). |On, denylist, policy01 |
   |Sticky session |When the scheduler is **Weighted Round Robin (WRR)** , enabling sticky session for the listener is optional.<br><br>After the sticky session feature is enabled, the CLB instance forwards access requests from the same session to the same backend server for processing based on the cookie. You need to select the cookie processing mode and specify the sticky session timeout or cookie name.<br><br>**Cookie processing method**: Supports both Cookie Insertion and Cookie Rewriting.<br><br><br>* **Cookie Insertion**: The CLB notes the backend server to which the client's request is initially forwarded and injects Cookies (CLBSERVERID and CLBSERVERCORSID) into the response before forwarding it to the client. Later when the client initiates an access request, the request carries this cookie information, and the CLB instance forwards the access request to the corresponding backend server.<br><br>   This method requires specifying the Cookie expiration time (**Session persistence timeout duration**). The sticky session timeout is 1000 seconds by default. The value ranges from 1 to 86400, in seconds.<br><br>* **Cookie rewriting**: You define the name of the backend cookie to be rewritten. When the client's first request is responded to by the backend server and reaches CLB, the CLB locates the specified cookie name in the response and rewrites it before forwarding the response to the client. Later when the client initiates an access request, the request carries the specified cookie, and the CLB instance forwards the access request to the corresponding backend server.<br><br>   When selecting this method, you must specify the cookie to be injected into the response, namely the **Cookie Name**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the cookie in the response returned by the backend server does not match the cookie name you specified, the CLB instance will not rewrite the cookie, and the access request will be forwarded normally according to the configured scheduler by default.   </div><br>    |Enable, embed Cookie, 1000 seconds |
   |Bandwidth  |Choose whether to enable bandwidth limit for the listener.<br><br>After enabling this feature, you must set the maximum bandwidth (in Mbps) of the listener, which is the remaining unallocated bandwidth of the CLB instance specification to which the listener belongs. |Enable, 100Mbps |
   |Max new connections limit |Input CLB's maximum limit of new connections as needed.<br><br><br>* Value range: 1 to the CLB's maximum limit of new connections. The default is CLB's maximum limit of new connections.<br><br>* When new connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is in beta. To use this feature, contact customer service support.</div><br> |30000 |
   |Max concurrent connections |Input CLB's maximum limit of concurrent connections as needed.<br><br><br>* Value range: 1 to the CLB's maximum limit of concurrent connections. The default is CLB's maximum limit of concurrent connections.<br><br>* When concurrent connections captured by the listener exceed the configured threshold, excess connections will be discarded and not forwarded to the backend server.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is in beta. To use this feature, contact customer service support.</div><br> |300000 |
   |Tag |A tag consists of a key\-value pair. You can use tags to classify and search for resources. For more information about tags, refer to [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the add icon, input the Tag key and Tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |
   

7. Click **Next** to configure the default backend server group.

   1. Select the addition method and backend server group as needed.

      * If there is already a Server Group that meets your needs, you can search or pull down to select.

      * If there is no Server Group that meets your needs, you can create one. For detailed parameter information, please refer to [Create Server Group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group).

   2. Click **Next** to add a backend server to the Server Group.

      Select the addition method and configure the backend server as needed.

      * If existing backend servers are available, you can choose to add them directly, and configure the port and weight of each backend server. For more information, refer to [Adding a backend server](https://docs.byteplus.com/en/docs/clb/Adding-a-server).

      * If no backend server is available, create a listener and then add a backend server.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a listener is created, the system will automatically create a default forwarding rule and associate it with the default backend server group. The default forwarding rule has an empty domain name and a URL path of <code>/</code>.This means enabling it to forward requests for any domain and URL. When the request does not match other forwarding rules in the listener, the request will be forwarded to the default backend server group based on the default forwarding rule. For more information about forwarding rules, refer to <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01">Configuring a forwarding rule</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When selecting an existing backend server group or adding a backend server to a server group, ensure the security group allows traffic using the same protocol as the listener by referring to <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">Configuring a backend server security group</a>.   </div>
   

8. Click **Next** to configure health check information, as shown below.

   In this example, the default health check configuration is retained. If modification is required, refer to [Configuring health check](https://docs.byteplus.com/en/docs/clb/Editing-health-check) for detailed parameter descriptions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After configuring the health check information, the CLB instance will periodically send requests to the backend server to check its running status and determine its availability. When a backend server is found unhealthy, the listener stops sending traffic to this server and forwards the traffic to other backend servers that run normally.   </div>
   

9. Click **Next** to review all configuration information of the listener, and complete the creation of the listener.

   * If the configuration information is incorrect, click the add icon, back to the corresponding page and change the configuration.

   * After verifying the configuration details, click **OK** to create the listener.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


* HTTP listeners Enable Gzip data compression by default.

   When a client request includes the `Accept-encoding: gzip` header, the CLB compresses responses from the backend server before returning them to the client, provided the responses contain the files of specific types (including text/plain, text/css, text/xml, application/xml, text/javascript, application/x\-javascript, application/json, application/javascript, application/x\-protobuf).

* Besides forwarding traffic to the default backend server group's servers, you can also add forwarding rules to direct traffic to servers in other Server Groups. For specific actions, refer to [Configuring a forwarding rule](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01).


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)
