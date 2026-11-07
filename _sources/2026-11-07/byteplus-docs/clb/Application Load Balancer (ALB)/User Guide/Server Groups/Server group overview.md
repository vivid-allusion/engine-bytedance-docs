---
title: "Server group overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Server-groups-Overview"
---

Server group is a logical collection of backend servers. The ALB instance determines the server group to forward client requests to based on your configured forwarding rules. Then, the ALB instance distributes requests to backend servers within the server group according to your configured load balancing policy. The backend servers receive and process the requests.

<span id=".5pyN5Yqh5Zmo57uE57G75Z6L"></span>
## Server Group Type

When creating a server group, you need to specify its type, which determines the type of backend servers that can be added.

The server group types supported by ALB instances include “server” and “IP”. To use the IP type server group, contact customer service support or [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645).


|**Server Group Type** |**Backend server types** |**Explanation** |
|---|---|---|
|Server |Backend servers can be of the following two types:<br><br><br>* [ECS](https://docs.byteplus.com/docs/ecs/What-is-Elastic-Compute-Service) instance<br><br>* Secondary network interface bound to ECS instance |ecs instances and server groups must be in the same VPC. |
|IP |The backend server can have an IP address in the following VPC CIDR blocks:<br><br><br>* 10.0.0.0/8<br><br>* 172.16.0.0/12<br><br>* 192.168.0.0/16 |You can add IP addresses within the VPC to which the server group belongs. With Remote IP enabled and network connectivity ensured, you can also add IP addresses from VPCs different from the server group or from local data centers. |


<span id="7a77119c"></span>
## **Backend communication protocol and health check protocol**

When creating a server group, you must specify the backend communication protocol and health check protocol. There is a specific correspondence between the listener type, backend communication protocol, and health check protocol. For example, HTTP listeners support backend communication protocols including HTTP and HTTPS, and health check protocols including HTTP and TCP. See the table below for details.


|**Listener type** |**Backend communication protocol** |**Health check protocol** |
|---|---|---|
|HTTP |HTTP、HTTPS |HTTP、TCP |
|HTTPS |HTTP、HTTPS |HTTP、TCP |
|HTTP/2 |HTTP、HTTPS、gRPC |HTTP、TCP |
|QUIC |HTTP、HTTPS |HTTP、TCP |


<span id="54fce4d7"></span>
## Health check

The health check feature of ALB must be configured at the server group level. The health check feature for server groups is enabled by default. You can apply a health check template to the server group or customize the health check configuration.

When you enable health check for a server group, ALB regularly sends health check requests to check the status of backend servers within the server group. If a backend server fails to respond properly to ALB's health check requests, traffic from clients will not be routed to that server. ALB forwards data transfer to backend servers that are healthy. This ensures business continuity.

For more information about health checks, see [Health Check](https://docs.byteplus.com/docs/clb/ALB-Health-check).

<span id="fb2ad847"></span>
## Scheduling algorithm

Scheduling algorithms at the server group level are also called load balancing algorithms. Load balancing algorithms determine how client requests distribute among backend servers. ALB supports the following load balancing algorithms:


* **Weighted Round Robin (WRR)** : WRR generates a fixed request distribution sequence based on preset weight values. Within one polling cycle, backend servers with higher weights receive more requests. WRR only considers the backend server's weight and ignores the actual load. This algorithm applies when the request quantity and individual request processing time are relatively stable, but there are significant performance differences among backend servers.

* **Weighted Least Connections (WLC)** : ALB dynamically calculates the value of "current connections/weight" for backend servers and routes new requests to the backend server with the smallest value. The WLC algorithm considers both the load and weight of backend servers. This algorithm suits scenarios with high request volumes and large variations in individual request processing time, helping prevent overloading any single backend server.

* **Source Address Hash (SH)** : Requests from the same source IP address are routed to the same backend server. The SH algorithm does not consider the weight or load of backend servers and always routes requests from the same client to the same backend server. This algorithm suits scenarios requiring session persistence based on the source IP address.


For more details about load balancing algorithms, see [load balancing algorithm](https://docs.byteplus.com/docs/clb/Load-balancing-algorithms).

<span id="df695477"></span>
## Session Persistence

ALB provides Cookie\-based session persistence. When you enable this feature for a server group, ALB forwards requests from the same client to the same backend server based on cookies.

For more information about session persistence, see [Configure cookie-based session persistence](https://docs.byteplus.com/docs/clb/Cookie-based-session-persistence).

<span id="18b3997b"></span>
## Cross\-AZ Load Balancing

The cross\-AZ load balancing feature at the ALB instance level is enabled by default and cannot be disabled. Instance nodes in each availability zone receive client requests simultaneously. By default, instance nodes in one availability zone distribute received requests to backend servers across all availability zones where the ALB instance is located.

You can disable cross\-AZ load balancing at the server group level. After disabling this feature, instance nodes distribute requests only to backend servers within the same availability zone.

For more information about cross\-AZ load balancing, see [Cross-AZ Load Balancing](https://docs.byteplus.com/docs/clb/Cross-zone-load-balancing).

<span id="c23457cd"></span>
## Description of server group configuration


* server groups and ALB instances operate independently. a server group can associate with any listener of ALB instances within the same VPC.

* multiple IPv4 backend servers can be added to a single server group.

* a backend server can be added to different server groups.

* backend servers in different availability zones within the same region can join the same server group.
