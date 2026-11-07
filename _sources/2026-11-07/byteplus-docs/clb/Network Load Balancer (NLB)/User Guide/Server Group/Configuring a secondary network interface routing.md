---
title: "Configuring a secondary network interface routing"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Configuring-the-secondary-network-interface-routing"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The secondary network interface is an elastic network interface. A secondary network interface associated with an ECS instance can act as the backend server of an Network Load Balancer (NLB) instance.

By switching the ECS instances associated with the secondary network interface, you can efficiently adjust the ECS instances receiving NLB forwarded requests, enabling a high availability cluster, low\-cost failover, and granular network management.

<span id=".6YWN572u6K-05piO"></span>
## Configuration instructions

When an ECS instance's attached secondary network interface acts as a backend server for an NLB instance, you need to configure the network interface routing to respond to requests from clients or the NLB. For route configuration methods and prerequisites, see Modifying Network Interface Routes.


* When client address preservation is enabled for the server group, the source address in forwarded requests received by backend servers becomes the client IP address, and health check requests also originate from the NLB instance's LIP address. You need to configure the following routing information within the ECS instance:

   
   |Destination address |Destination address mask |Gateway address |Network interface |Route hop count |
   |---|---|---|---|---|
   |IPv4 address of the subnet associated with NLB instance |IPv4 subnet mask of the subnet associated with NLB instance |IPv4 gateway address of the subnet where the network interface resides<br><br>For example, 192.168.1.1 |Secondary network interface name, such as eth1 |100 |
   |IPv6 address of the subnet to which the NLB instance belongs |\-\- |IPv6 gateway address of the subnet where the network interface resides<br><br>For example, 2000:1000:XX:XX::1 |Secondary network interface name, such as eth1 |100 |
   |Allowed client address |Allowed client address mask |IPv4 or IPv6 gateway address of the subnet where the network interface resides |Secondary network interface name, such as eth1 |100 |
   

* When client address preservation is disabled for the server group, the source address in forwarded requests received by backend servers becomes the LIP address of the NLB instance, and health check requests also originate from the NLB instance's LIP address. Therefore, configure the following routing information inside the ECS instance:

   
   |Destination address |Destination address mask |Gateway address |Network interface |Route hop count |
   |---|---|---|---|---|
   |IPv4 address of the subnet associated with NLB instance |IPv4 subnet mask of the subnet associated with NLB instance |IPv4 gateway address of the subnet where the network interface resides<br><br>For example, 192.168.1.1 |Secondary network interface name, such as eth1 |100 |
   |IPv6 address of the subnet to which the NLB instance belongs |\-\- |IPv6 gateway address of the subnet where the network interface resides<br><br>For example, 2000:1000:XX:XX::1 |Name of the secondary network interface, such as eth1 |100 |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the allowed client addresses are set to 0.0.0.0/0 or ::/0, then the metric for the secondary network interface route should not be set to 0 when configuring. Otherwise, it will conflict with the default route of the primary network interface, causing data packets to be returned using the primary rather than the secondary network interface route.   </div>
