---
title: "IP Address Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IP-address-Overview"
---

<span id=".566A5LuL"></span>
## Introduction​

Once an IP address is assigned to a network interface, other resources in the network can precisely locate the ECS instance to which the interface is attached using this IP address and communicate with it.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IPv6 gateway and dual\-stack VPC are currently in beta stage. If you need a trial, please contact the account manager.</div>


<span id=".5YiG57G7"></span>
## Classification


|Category |Explanation |
|---|---|
|Primary Private IP |The primary private IP is an IPv4 address that must be assigned to the network interface upon creation. It cannot be actively reclaimed and its lifecycle is tied to the network interface. |
|Secondary Private IP |Except for the primary private IP, any other IPv4 or IPv6 addresses assigned to a network interface are referred to as secondary private IPs. |


<span id=".SVB2NOS4jklQdjblr7nmr5Q="></span>
## IPv4 vs. IPv6

The comparison between on\-cloud IPv4 addresses and IPv6 addresses is shown in the table below:


|Comparison item |Private IPv4 address |Public IPv4 address |IPv6 address |
|---|---|---|---|
|Address length |32\-bit |32\-bit |128\-bit |
|Uniqueness |Can be duplicated |Globally Unique |Globally Unique |
|Internet Access available |No |Yes | can access the public network after enabling IPv6 internet bandwidth |
|Allocation method |Assigned from IPv4 CIDR blocks of a VPC. |User applies, system assigns. |Assigned from the VPC's IPv6 CIDR block. |
|Network Interface address restriction |The number of IPv4 addresses that a Network Interface can assign is limited by the ECS instance type. For details, see **Limits** **.**  |Each private IPv4 address of a network interface can be bound to one public IPv4 address. |The number of IPv6 addresses that can be assigned to a network interface is limited by the Elastic Compute Service (ECS) specification. For details, see **Limits**. |
|Is there a charge |No |Yes |No fee will be charged if IPv6 Internet bandwidth is not activated. Fees apply once IPv6 Internet bandwidth is enabled |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The primary network interface and secondary network interface of the ECS can be assigned private IPv4 addresses and private IPv6 addresses, which are limited by the [ECS instance type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types)'s **Private IP address for each network interface** quota.

   > Such as [ecs.g3i.large](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNp) single Network Interface private IP quota is 6. That is, the specification of the ECS primary Network Interface or secondary Network Interface can be assigned up to 6 private IPv4 addresses (including the main private IPv4 address) and 6 private IPv6 addresses.   
   

* An unmounted secondary network interface can be custom\-assigned up to 9 Secondary Private IPv4 addresses and 10 private IPv6 addresses.

* Each private IPv4 address on a network interface can be associated to one EIP.

* The IPv6 address of network interface  supports private network communication only by default. Internet access requires enabling IPv6 internet bandwidth.


<span id=".5L2_55So5rWB56iL"></span>
## Usage process


* IPv4

   1. [Assign IPv4 address](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address)

   2. [Configure IPv4 address](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances)

   3. [View IP address](https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses)

   4. [(Optional) Associate an EIP](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP)

* IPv6

   1. [Assign IPv6 address](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address)

   2. [Configure IPv6 address](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances)

   3. [View IP address](https://docs.byteplus.com/en/docs/ecs/Viewing-IPv4-or-IPv6-addresses)

   4. [(Optional) Enable IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth)


&nbsp;

&nbsp;
