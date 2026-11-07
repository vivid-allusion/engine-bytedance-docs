---
title: "Multicast overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Multicast-Overview"
---

<span id="YKCPrk0H"></span>
## Overview

Multicast is a point\-to\-multipoint communication method that supports data packets sent by one server being received by multiple clients simultaneously.

Currently, Transit Router (TR) supports multicast functionality between Virtual Private Clouds (VPCs) of the same account within the same TR instance and between VPCs. It only supports static multicast sources and multicast members.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The TR multicast feature is in the beta stage. If you need a trial, please contact your account manager.</div>


<span id="k3aq2rTf"></span>
## Billing notes

Multicast traffic is charged for both inbound and outbound directions, specifically including:


* Inbound multicast traffic fee: Multicast traffic sent by the multicast source to the TR is counted as part of the traffic processing fee of the network instance attachment that forwards the multicast traffic.

* Outbound multicast traffic fee: Multicast traffic sent by the TR to multicast members is counted as part of the traffic processing fee of the network instance attachment that forwards the multicast traffic.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details, please see <a href="https://docs.byteplus.com/en/docs/6979/155973#.5Zyw5Z-f5YaF6LS555So">Traffic processing fee</a>.</div>


<span id="k3aq2rTf"></span>
## Terms


|Concept |Description |
|---|---|
|Multicast domain |The multicast communication scope consists of one TR and one or more VPC subnets.<br><br>Only resources within the multicast domain can send and receive multicast traffic. A TR can create multiple multicast domains, and different multicast domains cannot communicate with each other. |
|Multicast group |A collection of resources that send and receive the same multicast messages.<br><br>A multicast domain supports creating multiple multicast groups. |
|Multicast address |An IP address used to identify a multicast group. The IP address does not belong to a specific host but to a group of hosts. The IP address range of the TR multicast group is: 224.0.0.0–239.255.255.255.<br><br><br>* Within the same multicast domain, the IP addresses of different multicast groups cannot be the same.<br><br>* In different multicast domains, the IP address of different multicast groups can be the same. Resources within a multicast group with the same multicast address cannot communicate with each other. |
|Multicast source |Resources that send multicast traffic under a multicast group. Multiple multicast sources can be added to a multicast group. |
|Multicast member |Resources that receive multicast traffic under a multicast group. A multicast group can add multiple multicast members. |


<span id="NfbEJxGk"></span>
## Multicast matching principle

Multicast forwarding and unicast forwarding are independent of each other. As long as both the multicast source and multicast member's subnet are added to the multicast domain, multicast forwarding can be achieved.


* When subnets within a VPC communicate, multicast packets are not sent based on VPC routing but are directly sent to the TR instance belonging to the multicast domain for processing.

* When communicating between different VPCs, if the destination IP address of a multicast packet matches the multicast group IP address, multicast forwarding will follow the multicast group; otherwise, the multicast packet will be discarded.


<span id="NfbEJxGk"></span>
## Limits


* A subnet can only be added to one multicast domain.

* Multicast forwarding is only supported between VPCs in the same account and region. Cross\-account/cross\-region VPC multicast is not supported for now.

* Only IPv4 multicast is supported. IPv6 multicast is not supported for now.

* IGMP is not supported yet. Only manual configuration is supported for multicast sources and multicast members.

* Sharded messages are not supported yet.

* The network interface created by the TR in the VPC does not support being added as a multicast source or multicast member.

* After the multicast feature is enabled, it cannot be disabled.

* Route Policy and Forwarding Policy do not affect multicast traffic, but they may impact return packet data from multicast members to the multicast source.


For more quotas and usage limits, see [Limits](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04).

<span id="6FgqNA3l"></span>
## Configuration procedures


1. [Create a TR instance (enable multicast).](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instances-01)

2. [Create a VPC attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-vpc)

3. [Create a multicast domain and attach a subnet.](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-multicast-domain)

4. [Add a multicast source](https://docs.byteplus.com/en/docs/transitrouter/Managing-the-multicast-source#yWkTcEed)

5. [Add a multicast member](https://docs.byteplus.com/en/docs/transitrouter/Managing-multicast-members#Udkr59Yx)


&nbsp;
