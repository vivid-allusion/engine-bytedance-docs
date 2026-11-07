---
title: "IP address overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/IP-address-overview"
---

<span id=".566A5LuL"></span>
## Description

After an IP address is assigned to a network interface, other resources in the network can use this IP address to accurately locate and communicate with the ECS instance associated with the network interface.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IPv6 gateways and Dual\-Stack VPC are currently in beta. If you need a trial, contact your account manager.</div>


<span id=".5YiG57G7"></span>
## Classification


|Category |Description |
|---|---|
|Primary private IP address |The primary private IP address is a private IPv4 address that must be assigned to a network interface upon creation. It does not support active reclaim, and its lifecycle is tied to that of the network interface. |
|Secondary private IP address |Except for the primary private IP address, any other IPv4 or IPv6 address assigned to the network interface is referred to as a secondary private IP address. |


<span id=".SVB2NOS4jklQdjblr7nmr5Q="></span>
## Comparison between IPv4 and IPv6 addresses

The following table shows the comparison between BytePlus IPv4 and IPv6 addresses.


|Item |Private IPv4 address |Public IPv4 address |IPv6 address |
|---|---|---|---|
|Address length |32\-bit |32\-bit |128\-bit |
|Uniqueness |Repeatable |Globally unique |Globally unique |
|Internet access |No |Yes |Internet access is supported after you enable IPv6 Internet bandwidth. |
|Assignment method |Assigned from the IPv4 CIDR block of the VPC. |Assigned by BytePlus based on user applications. |Assigned from the IPv6 CIDR block of the VPC. |
|Network Interface address restriction |The number of IPv4 addresses that can be assigned to a network interface is limited by the ECS instance type. For details, see Limits. |You can associate each private IPv4 address of a network interface with a public IPv4 address. |The number of IPv6 addresses that can be assigned to a network interface is limited by the ECS instance type. For details, see Limits. |
|Chargeable |No |Yes |If IPv6 Internet bandwidth is not enabled, you are not charged. Otherwise, you are charged. |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The number of private IPv4 addresses and private IPv6 addresses that you can assign to the primary network interface or to any secondary network interface mounted to an ECS instance is limited by the private IP address quota of a single network interface. The quota is determined based on the [ECS instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

   > For example, the private IP address quota of a single network interface is six for an instance whose type is ecs.g3i.large. That is, you can assign up to six private IPv4 addresses (including the primary private IPv4 address) and six private IPv6 addresses to the primary or secondary network interface of an ECS instance whose type is [ecs.g3i.large](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNp).   
   

* You can manually assign up to nine secondary private IPv4 addresses and ten private IPv6 addresses to a secondary network interface that has never been mounted to an ECS instance.

* You can associate each IPv4 address of a network interface with an EIP.

* By default, IPv6 addresses of a network interface only support private network communication. To access the Internet over IPv6, you need to first enable IPv6 Internet access.


<span id=".5L2_55So5rWB56iL"></span>
## Procedure


<Tabs>
<Tab zoneid="PPKbumuoeg" title="IPv4">
<TabTitle>IPv4</TabTitle>

1. [Assign IPv4 addresses.](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address)

2. [Configure IPv4 addresses.](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances)

3. [View IP addresses.](https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses)

4. [(Optional) Associate EIPs](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP)


</Tab>
<Tab zoneid="lM9vSBHQ00" title="IPv6">
<TabTitle>IPv6</TabTitle>

1. [Assign IPv6 addresses.](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address)

2. [Configure IPv6 addresses.](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances)

3. [View IP addresses.](https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses)

4. [(Optional) Enable IPv6 Internet bandwidth.](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth)


</Tab>
</Tabs>
