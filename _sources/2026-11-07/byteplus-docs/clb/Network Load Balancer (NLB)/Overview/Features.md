---
title: "Features"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Features"
---

This topic introduces the main features of the Network Load Balancer (NLB) and compares them with the Layer\-4 functionalities of the Classic Load Balancer (CLB).

<span id=".5Lqn5ZOB5Yqf6IO9"></span>
## Product features

The main features of the NLB are shown in the table below.


|Feature |Sub\-feature |Capabilities |Documentation |
|---|---|---|---|
|NLB instance<br><br><div style="text-align: center"><br></div><br><br><br><div style="text-align: center"><br></div><br><br><br><div style="text-align: center"><br></div><br><br><br><div style="text-align: center"><br></div><br> |IP version |Supports IPv4 and dual stack (IPv4 and IPv6) types. |[Creating an NLB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance) |
||Instance Network Type |Supports internet and private network types. The network types of IPv4 addresses and IPv6 addresses are independent of each other. |[Product type](https://docs.byteplus.com/en/docs/clb/What-is-Network-Load-Balancer) |
||Multi\-active Availability Zones |Requests to the NLB instance domain name resolve to all service IP addresses across Availability Zones, enabling multi\-active disaster recovery capabilities. |[Creating an NLB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance) |
||Forwarding across all zones<br><br> |The NLB instance by default supports forwarding across all zones, improving overall service availability. After the NLB instance is successfully created, you can set to enable/ disable all zone forwarding functionality as needed.<br><br><br>* Enable all zone forwarding: NLB instances route requests to backend servers within other Availability Zones.<br><br>* Disable all zone forwarding: NLB instances route requests only to backend servers within the same Availability Zone (AZ), reducing network latency by eliminating inter\-AZ traffic. |[Enabling/Disabling all zones forwarding](https://docs.byteplus.com/en/docs/clb/Enabling-Disabling-all-zones-forwarding)<br><br> |
||Access control<br><br> |By default, an NLB instance is associated with a security group upon creation. You can configure security group rules to control the traffic accessing the NLB, or use Network ACL rules configured for the subnet of the NLB instance to achieve access control. |* [Managing the associated security group](https://docs.byteplus.com/en/docs/clb/Managing-attached-security-groups)<br><br>* [Managing an Network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules) |
|Listener |Listening protocol |Supports TCP, UDP, and TLS. |[Creating a listener](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener) |
||Full port listening |A single listener supports port range listening, which can simplify listener configuration and improve configuration efficiency. ||
|Server Group<br><br><div style="text-align: center"><br></div><br><br><br> |Cross\-VPC Backend Server |The NLB supports adding Elastic Compute Service (ECS) instances, network interfaces, or servers within IDC as backend servers via IP addresses across VPCs. |[Adding the cross-VPC backend server](https://docs.byteplus.com/en/docs/clb/NLB-Adding-removing-backend-server) |
||Scheduling algorithm |Supports Weighted Round Robin (WRR), Weighted Least Connections (WLC), and Source IP Hash (SH) scheduling algorithms. |[Routing algorithm principle](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview#YF78LR8p) |
||Health check |NLB examines the operational status of backend servers through the health check feature, allowing customized protocols and ports for health checks. When the operational status of a backend server is detected as poor, it stops forwarding requests to the server and routes them to other backend servers that are operating normally. |[Health check exception troubleshooting guide](https://docs.byteplus.com/en/docs/clb/NLB-Troubleshooting-exceptions-found-in-health-check) |
||Session Persistence |Sticky session allows the backend server to remember the session state of the same user for a specified period, enabling it to identify the user and maintain its session information in subsequent requests. |[Creating a server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group) |
||Connection Draining |Connection draining allows NLB to maintain existing connections for a specified duration when backend servers are removed or fail health checks, ensuring in\-flight requests complete normally. ||
||Client IP Preservation<br><br> |NLB forwards access requests from the client to the backend server while carrying the client IP address by default. After enabling client IP Preservation for the server group, the backend server can directly obtain the client IP address without additional configuration.<br><br>The client IP Preservation function is unavailable in the following scenarios. You can obtain the source IP via the Proxy\-Protocol:<br><br><br>* When the IP version of the client request differs from the server group, enabling client IP Preservation will not take effect.<br><br>* Cannot be enabled when the server group type is set to **IP type**. |[Creating a server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group)<br><br> |
||Obtaining the client IP via the Proxy Protocol |If client IP Preservation is not enabled in the server group, or if the client's request uses a different IP protocol against the backend server, the backend server can obtain the client's IP address via the Proxy Protocol. |[Creating a server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group) |


<span id="4XaCYGhU"></span>
## Comparison between NLB and CLB

The main differences between NLB and Layer\-4 CLB are shown in the table below.


|Comparison item |NLB |CLB |
|---|---|---|
|Network performance |A single instance supports up to 100 million concurrent connections and 100Gbps bandwidth. |A single instance supports up to 1 million concurrent connections and 10 Gbps bandwidth. |
|Disaster Recovery and Session Affinity<br><br> |* Active\-active disaster recovery across Availability Zones<br><br>* NLB\-to\-backend\-server affinity can be achieved by disabling all zone forwarding |Active and standby availability zones for disaster recovery<br><br> |
|Access control |Reuse the security group and Network Access Control List to implement Identity and Access Management (IAM) |Access control is implemented through allowlist/denylist policy groups. |
|Backend Mounting Capability<br><br> |* Server groups operate independently from the instance, and a single server group can be mounted to multiple different instances.<br><br>* For IP\-mode backend server groups, the communication between the instance and the backend server uses the IP address within the instance's VPC. When connected via Cloud Enterprise Network (CEN) or Transit Routers, routes propagate automatically, requiring no manual routing configuration. |* The server group belongs to the instance and can only be mounted to its associated instance.<br><br>* For IP\-mode server groups, communication with backend servers uses IP addresses from 100.64.0.0/10 range. When connecting through Cloud Enterprise Network (CEN) or Transit Router (TR). Manual return\-path routing configuration is required, introducing considerable configuration complexity.<br><br><br> |
|Health check |Support flexibly selecting health check protocols and ports as needed. |The health check protocol and port are set to default and cannot be specified. |
|Full port listening |A single instance can add 5 all\-port listeners by default; for an upgrade, contact your account manager. |By default, within a single instance, only one full\-port listener of the same protocol can be added, which means up to two full\-port listeners can be added (one for TCP protocol and one for UDP protocol). |
|Client IP Preservation |Supports on\-demand selection of whether to enable client IP preservation for backend servers. |For server\-type backend servers, client IP Preservation is enabled by default and cannot be modified. |
