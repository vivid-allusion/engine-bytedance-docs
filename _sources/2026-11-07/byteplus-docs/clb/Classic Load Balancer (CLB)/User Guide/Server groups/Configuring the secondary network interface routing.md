---
title: "Configuring the secondary network interface routing"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Operation scenario

A secondary network interface is an Elastic Network Interface (ENI). You can add a secondary network interface that has been bound to an Elastic Cloud Server (ECS) instance as a backend server to the backend server group of a Classic Load Balancer (CLB) instance.

For the secondary network interfaces bound to a backend server group, you can easily and efficiently adjust the ECS instances that receive CLB\-forwarded requests by switching the ECS instances bound to the secondary network interfaces, achieving high availability cluster building, low\-cost failover, and refined network management.

<span id=".6L6F5Yqp572R5Y2h6Lev55Sx6YWN572u"></span>
## Configuring route entries for a secondary network interface

After adding a secondary network interface bound to an ECS instance to the backend server group of a CLB instance, you must configure the route entries for the secondary network interface to respond to requests from clients or the CLB instance.

The network interface routing to be configured for Layer 4/Layer 7 listeners is as follows, and the routing configuration method and prerequisites refer to [Configuring network interface routing](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After configuring the route entries, if the ECS instance is restarted, all manually added route entries will be cleared and must be configured again.</div>


<span id=".5Zub5bGC55uR5ZCs5Zmo"></span>
### Layer 4 listener

The TCP/UDP listener transparently transmits the client source IP and sends health check requests to the backend server using addresses in the CIDR block `100.64.0.0/10` or `fd00:64::/32`. Therefore, you must configure the following route entries in the ECS instance:


|Destination Address |Destination Address Mask |Gateway Address |Network interface |Hop Count |
|---|---|---|---|---|
|100.64.0.0 |255.192.0.0 |IPv4 gateway address of the subnet where the network interface is located |Secondary network interface name, for example, eth1 |100 |
|fd00:64::/32 |\- |IPv6 gateway address of the subnet where the network interface is located |Secondary network interface name, for example, eth1 |100 |
|Client address allowed to access |Client address mask allowed to access |Gateway address of the subnet where the network interface is located |Secondary network interface name, for example, eth1 |100 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the allowed client addresses are set to <code>0.0.0.0/0</code> or <code>::/0</code>, then the metric for the secondary network interface route should not be set to 0 when configuring. Otherwise, it will conflict with the default route of the primary network interface, causing data packets to be returned using the primary rather than the secondary network interface route.</div>


<span id=".5LiD5bGC55uR5ZCs5Zmo"></span>
### Layer 7 listener

HTTP/HTTPS listeners will establish a separate connection with the backend server using the CIDR block address `100.64.0.0/10` and send health check requests to the backend server. Therefore, you only need to configure the following route entries in the ECS instance:


|Destination Address |Destination Address Mask |Gateway Address |Network interface |Hop Count |
|---|---|---|---|---|
|100.64.0.0 |255.192.0.0 |Gateway address of the subnet where the network interface is located |Secondary network interface name, for example, eth1 |100 |
