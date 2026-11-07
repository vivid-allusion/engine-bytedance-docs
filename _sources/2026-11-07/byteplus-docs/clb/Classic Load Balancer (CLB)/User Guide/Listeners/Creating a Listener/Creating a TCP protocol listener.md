---
title: "Creating a TCP protocol listener"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Creating-a-TCP-listener"
---

## Action description

* The target port is not monitored by other TCP/HTTP/HTTPS listeners.

* The Classic Load Balancer (CLB) instance has unallocated bandwidth. If none, adjust the bandwidth allocated to existing listeners or upgrade the CLB instance specification.

* Layer 4 listeners (TCP and UDP protocols) support forwarding requests to IPv4 or IPv6 backend servers.

## Procedures

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Configure Listener to the right of the target CLB instance.

4. Click Add Listener.

5. Refer to the table below to configure basic information.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Listener name |Enter the listener name. If left blank, it defaults to **Protocol\-port**, such as TCP\-80. |listener\-1 |
   |CLB protocol |Select the protocol type for CLB instance listener. This article uses TCP. |TCP |
   |Listening port |Enter the listening port. The range is 1 to 65535.<br><br><br>* Listen by single port: enter a single port. When the listener receives a TCP request on this port, it replaces the destination IP and port in the request with the backend server’s IP address and port, then forwards the request to the backend server.<br><br>   * Applicable to backend server applications opening a single port.<br><br>   * Only backend server groups with all\-port forwarding not enabled can be attached.<br><br>* Listen to all ports: enter the port range. When the listener receives a TCP request within this port range, it replaces the destination IP in the request with the backend server's IP address before forwarding to the backend server.<br><br>   * For all\-port TCP listeners, a CLB instance supports creating only one.<br><br>   * Applicable to backend server applications opening a continuous port range.<br><br>   * Only Backend server groups with all\-port forwarding enabled can be attached.<br><br><br>> **tip**<br><br><br><br>* > For backend server applications opening a continuous port range, besides using a single listener with all\-port listening, you can also add multiple listeners to listen on different ports.<br><br><br>* > The listener all\-port listening feature is in the beta stage. Contact your account manager to request a trial.<br> |Listen by single port, 80 |
   |Scheduling algorithm |Select the rule followed by the listener to forward requests.<br><br><br>* Weighted Round Robin (WRR): In this case, higher weights values receive more frequent polling attempts (higher probability).<br><br>* Weighted Least Connection (WLC): First calculate the current connections/weight value of the backend server, then dispatch the request to the backend server with the smallest value.<br><br>* Source hashing (SH): A consistency hash based on the Source IP address, allowing the same source to be scheduled to the same backend server. |Weighted Round Robin (WRR) |
   |Timeout period |Set the timeout period. If no data is transferred over the connection within the timeout period, it will be automatically disabled. Value range: 10–900 seconds, default is 900 seconds. |900 seconds |

6. Refer to the table below to configure advanced features.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Access control |Enable access control. When enabled, it restricts the traffic that the listener forwards. For details, see ACL overview.<br><br>After enabling, select the control method and policy group.<br><br><br>* **Control method**<br><br>   * Denylist: CLB instance denies requests forwarded from IP addresses in the denylist.<br><br>   * Allowlist: CLB instance only allows requests forwarded from IP addresses in the allowlist.<br><br>* **Policy group**<br><br>   A policy group is a set of IP addresses. Up to 5 policy groups can be selected. |Enable, denylist, policy01 |
   |Proxy\-Protocol |Enable the Proxy Protocol. Enable the Proxy Protocol when the backend server needs the real source IP but the packet source IP is replaced (e.g., IPv6 requests forwarded to IPv4 backend servers).<br><br><br>* Enabling the Proxy Protocol feature requires backend server adaptation and does not support smooth online migration. Configure carefully.<br><br>* For usage examples, see Retrieving client source IP via proxy protocol. |No |
   |Session Persistence |Enable session persistence<br><br><br>* When enabled, CLB forwards requests from the same source IP address to the same backend server for processing.<br><br>* Value range for session persistence timeout: 1–3600 seconds. |Enabled, 1000 seconds |
   |Bandwidth cap |Enable exclusive bandwidth.<br><br><br>* Enable: the listener exclusively uses the bandwidth of the CLB instance. Value range: 1 to the bandwidth not exclusively occupied by the CLB instance. Unit: Mbps.<br><br>* Don't enable: The listener shares the bandwidth of the CLB instance that is not exclusive. |Enabled, 100 Mbps |
   |Connection Draining |Enable Connection Draining<br><br><br>* When enabled, if the backend server is deleted or the health check fails, existing connections transmit normally within the connection draining timeout period.<br><br>* The connection draining timeout period ranges from 0 to 900 seconds. |Enabled, 100 seconds |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/clb/Tag-management).<br><br>Click the Add icon, input the tag key and tag value, and add a tag for the listener. |* Tag key: listener\-key<br><br>* Tag value: listener\-test |

7. Click Next to configure backend server group information for the listener.

   1. Select the add method and backend server group as needed.

      * If a suitable backend server group already exists, search or select from the dropdown.

      * If there is no backend server group that meets the requirements, you can create a new one. For detailed parameter introduction, see Creating a Server Group.

   2. Click Next to add a backend server to the Server Group.

      Select the add method and configure the backend servers as needed.

      * If existing backend servers are available, you can choose to add them directly, and configure the port and weight of each backend server. For more information, refer to Adding a backend server.

      * If no backend servers are available, select to add them after creating the listener.

   > **tip**

   > When adding a backend server to a server group, ensure the associated security groups permit relevant traffic (same protocol and port as the listener). For details, see Configuring a backend server security group.

8. Click Next and configure the health check according to the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Health check |Enable health check Once enabled, the CLB instance will periodically send requests to backend servers to test their operational status and determine their availability. If a backend server is detected to be in poor health, traffic will stop being forwarded to it and will be redirected to other normally functioning backend servers. |Check |
   |Health check port |Enter the health check port. The backend server receives health check requests sent by the CLB instance through this port. |80 |
   |Response timeout |After enabling health check, enter the wait time for health check responses.<br><br><br>* If no correct response is received from the backend server within the response timeout, the health check fails.<br><br>* Value range: 1–60 seconds. Default is 2 seconds. |2 seconds |
   |Detect interval |After enabling health checks, type the health check interval.<br><br><br>* The detect interval must be greater than or equal to the response timeout period.<br><br>* Value range: 2 to 300 seconds. The default is 2 seconds, meaning a health check is performed every 2 seconds on the backend server. |2 seconds |
   |Healthy threshold |After enabling health checks, specify the number of consecutive successful health checks required to consider a backend server normal.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are normal, its status changes from Abnormal to Normal.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |
   |Unhealthy threshold |After enabling health checks, enter the number of consecutive health check failures required to determine backend server failure.<br><br><br>* When the same backend server undergoes consecutive health checks for a specified number of times and all results are abnormal, its status changes from Normal to Abnormal.<br><br>* Value range: 2 to 10 times. Default: 3 times. |3 times |

9. Click the **Next** button.

10. Click the **OK** button to complete creation.

## Verify network connectivity

Now you have configured a TCP\-enabled CLB instance with forwarding, health checks, Identity and Access Management (IAM), and other features. On the instance management main list page, you can see the instance’s public network/private IP, and when clients access the instance’s IP and listening port, the instance forwards requests to backend servers.

## Related documents

[CreateListener](https://docs.byteplus.com/en/docs/clb/CreateListener)
