---
title: "Creating a UDP protocol listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-UDP-listener"
---

## Action description

* The target port is not being listened by any other UDP listener.

* The Classic Load Balancer (CLB) instance has unallocated bandwidth. If none, adjust the bandwidth allocated to existing listeners or upgrade the CLB instance specification.

* Layer 4 listeners (TCP and UDP protocols) support forwarding requests to backend servers using IPv4 or IPv6.

## Procedures

1. Log in to [CLB Console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Configure Listener to the right of the target CLB instance.

4. Click Add Listener.

5. Refer to the table below to configure the protocol and port.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Listener name |Set the name of Listener. If left blank, it defaults to Protocol\-port, such as UDP\-80. |listener\-1 |
   |CLB protocol |Select the protocol type for CLB instance listener. This article uses UDP. |UDP |
   |Listening port<br><br> |Enter the listening port. The range is 1 to 65535.<br><br><br>* Listen on a single port: enter a single port. When the listener receives a UDP request to this port, it replaces the destination IP address and port in the request with the backend server's IP address and port before forwarding to the backend server.<br><br>   * Suitable for scenarios where backend server applications open a single port.<br><br>   * Only backend server groups with all\-port forwarding not enabled can be attached.<br><br>* Listen on all ports: enter a port range. When the listener receives a UDP request on this port, it replaces the destination IP in the request with the backend server's IP address before forwarding to the backend server.<br><br>   * For UDP listeners configured with full port forwarding, only one can be created per CLB instance.<br><br>   * Applicable to scenarios where backend servers open consecutive port ranges.<br><br>   * Only Backend server groups with all\-port forwarding enabled can be attached.<br><br><br>> **tip**<br><br><br><br>* > When backend servers require consecutive port ranges, you can either use a single listener with full\-port forwarding, or configure multiple listeners each handling different port ranges.<br><br><br>* > The full\-port listening feature is in beta. Contact customer service support to apply for trial.<br> |Listen on a single port, 80<br><br> |
   |Scheduling algorithm<br><br> |Specify the rule that the listener follows to forward requests.<br><br><br>* Weighted Round Robin (WRR): In this case, higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connection (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source hashing (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server. |Weighted Round Robin (WRR)<br><br> |
   |Timeout period |CLB will close the connection if no new access requests are received within this time range. The default UDP protocol timeout is 90 seconds, with a configurable range of 1 to 300 seconds. |90 seconds |

6. Refer to the table below to configure advanced features.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Access control<br><br> |Enable access control. When enabled, listening traffic forwarding will be restricted. For details, see ACL overview.<br><br>After turning on, select the control method and policy group.<br><br><br>* **Control method**<br><br>   * Denylist: the CLB instance denies requests from IP addresses in the denylist.<br><br>   * Allowlist: the CLB instance only allows requests from IP addresses in the allowlist.<br><br>* **Policy group**<br><br>   A policy group is a group of IP addresses. A maximum of 5 policy groups can be selected. |Enable, denylist, policy01<br><br> |
   |Proxy\-Protocol<br><br> |Turn on Proxy protocol or not. Enable Proxy protocol when the backend server needs the real source IP but the source IP in the packet is replaced (e.g., IPv6 requests forwarded to an IPv4 backend server).<br><br><br>* Enabling Proxy protocol requires corresponding adaptation on the backend server and does not support live smooth migration. Configure with caution.<br><br>* For usage examples, see Retrieving client source IP via proxy protocol. |No<br><br> |
   |Session Persistence<br><br> |Enable session persistence<br><br><br>* When enabled, load balancing forwards requests from the same source IP address to the same backend server.<br><br>* Session established timeout range: 1–3600 seconds. |Turn on, 1000 seconds<br><br> |
   |Bandwidth cap<br><br> |Whether to turn on exclusive bandwidth.<br><br><br>* Turn on: The listener exclusively uses the bandwidth of the CLB instance. Value range: 1 to the bandwidth of the CLB instance not exclusively used. Unit: Mbps.<br><br>* Don't enable: The listener shares the bandwidth of the CLB instance that is not exclusively used. |Turn on, 100Mbps<br><br> |
   |Connection Draining<br><br> |Enable Connection Draining<br><br><br>* When enabled, existing connections transmit normally within the connection draining timeout if the backend server is deleted or health checks fail.<br><br>* The connection draining timeout period ranges from 0 to 900 seconds. |Turn on, 100 seconds<br><br> |
   |Tags<br><br> |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

7. Click Next to configure backend server group information for the listener.

   1. Select the add method and backend server group as needed.

      * If there is already a backend server group that meets the requirements, you can search or scroll down to select it.

      * If there is no Server Group that meets your needs, you can create one. For detailed parameter information, see Creating a Server Group.

   2. Click Next to add a backend server to the Server Group.

      Select the addition method according to your needs and configure the backend servers.

      * If existing backend servers are available, you can choose to add them directly, and configure the port and weight of each backend server. For more information, refer to Adding a backend server.

      * If no backend servers are available, select Add Later after creating the listener.

      > **tip**

      * > When adding a backend server to a server group, ensure the security group allows traffic using the same protocol as the listener by referring to Configuring a backend server security group.

      * > If the CLB instance associated with the listener is an IPv4 instance, only IPv4 backend server groups can be configured; if the instance is dual\-stack, IPv4 or IPv6 backend server groups can be configured as needed.

8. Click Next and configure the health check according to the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Health check |Enable health check Once enabled, the CLB instance periodically sends requests to backend servers to test their operational status and determine availability. If a backend server is detected to be in poor health, traffic will stop being forwarded to it and will be redirected to other normally functioning backend servers. |Check |
   |Health check port |Enter the health check port, through which the backend server receives health check requests sent by the CLB instance. |1 |
   |Health check request |Specify the request string sent for health checks. |healthcheckrequest |
   |Expected correct response<br><br> |The response string expected to be returned when the health check result is normal.<br><br>> **tip**<br><br><br>> If Health Check Request is specified, you must configure this parameter.<br> |ok<br><br> |
   |Response timeout<br><br> |After turning on health check, enter the time to wait for the health check response.<br><br><br>* If no correct response is received from the backend server within the response timeout, the health check fails.<br><br>* Value range: 1 to 60 seconds. The default value is 2 seconds. |2 seconds<br><br> |
   |Detect interval<br><br> |After enabling health checks, type the health check interval.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 2–300 seconds. The default is 2 seconds, meaning a health check is performed on the backend server every 2 seconds. |2 seconds<br><br> |
   |Healthy threshold<br><br> |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are normal, its status changes from Abnormal to Normal.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times<br><br> |
   |Unhealthy threshold<br><br> |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When a specified number of consecutive health checks are executed on the same backend server and all results fail, its health check status changes from Normal to Abnormal.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times<br><br> |

9. Click Next.

10. Click **OK** to complete the action.

## Verify network connectivity

Now you have configured a UDP\-enabled CLB instance with forwarding, health checks, and access control capabilities. On the instance management dashboard, you can view the instance's EIP and private IP address. When the client sends requests to this IP and listening port, the CLB instance will forward traffic to your backend servers.

## Related documents

[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)
