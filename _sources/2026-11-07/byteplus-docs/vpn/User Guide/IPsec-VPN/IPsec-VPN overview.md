---
title: "IPsec-VPN overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/IPsec-VPN-overview"
---

IPsec\-VPN establishes a communication tunnel between the customer gateway and cloud resources, supporting both VPN gateway and Transit Router (TR) cloud resources. Charging varies depending on the type of resource associated with IPsec\-VPN. For details, see [Billing overview](https://docs.byteplus.com/en/docs/vpn/Billing-overview).

When creating an IPsec\-VPN connection, configure the key, encryption, authentication algorithm, negotiation mode, and other data exchange parameters. You must ensure the cloud IPsec configuration matches the configuration on the target VPN gateway or firewall. Otherwise, the communication tunnel cannot be established.

<span id=".5L2_55So5rWB56iL"></span>
## Use process

<span id=".SVBzZWPov57mjqXnu5HlrppWUE7nvZHlhbM="></span>
### Associate IPsec\-VPN connections with VPN gateway

For detailed setup, see [Connecting a VPC to multiple data centers via IPsec-VPN connection with static routing](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8483aaf74bdb796dddebbc218dd09c7c.png) </span>

<span id=".SVBzZWPov57mjqXnu5HlrprkuK3ovazot6_nlLHlmag="></span>
### Attach IPsec\-VPN connections to TR

For detailed setup, see [Implementing interconnectivity between independent VPCs and a data center](https://docs.byteplus.com/en/docs/transitrouter/Best-Practices-02).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5d7e8aa2b6fb330d9ed884cfb7f9cd9.png) </span>
