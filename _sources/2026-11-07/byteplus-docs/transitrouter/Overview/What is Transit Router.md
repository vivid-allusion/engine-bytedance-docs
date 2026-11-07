---
title: "What is Transit Router"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01"
---

<span id=".566A5LuL"></span>
## Overview

Transit Router (TR) can connect [Virtual Private Clouds (VPCs)](https://docs.byteplus.com/en/docs/vpc/What-is-VPC), [Virtual Private Networks (VPNs)](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network), [Direct Connect (DC) Gateways](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect), or other TRs. It supports flexible routing rules to enable communication and isolation between networks. It allows private interconnectivity and isolation between cloud resources, and between VPCs and on\-premises data centers, in various complex networking scenarios.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cce191a5d1339214f071bc84887f2043.png) </span>

<span id=".57uE5oiQ6YOo5YiG"></span>
## Compositions

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2581794014aeaf4dc0b051ad926b9773.png) </span>


|Compositions ||Description |Limits |
|---|---|---|---|
|TR instance ||The foundation of the TR service. Receives traffic from an attachment and forwards it based on the TR route table associated with that attachment. |Partial ECS instance types do not support the TR service. For details, see the [Instance type](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01#.5Lit6L2s6Lev55Sx5Zmo5LiO5LqR5LyB5Lia572R55qE5a-55q-U) row. |
|Attachment |Intra\-region attachment |The connection established between a TR instance and a network instance (VPC, VPN, DC Gateway, or TR) in the same region. This enables private network interconnectivity within the region.<br><br><br>* Each TR instance can contain multiple attachments.<br><br>* When creating a VPC attachment, the system automatically creates a network interface as the **attachment point**. Each VPC attachment can contain multiple attachment points. |\-\- |
||Inter\-region attachment |The connection is established between TR instances in two different regions. This enables private network interconnectivity across regions. |TR instances on both ends of an inter\-region attachment must belong to the same account. |
|Bandwidth package ||Provides bandwidth resources for private network interconnectivity in inter\-region attachment. |\-\- |
|TR route table ||The basis for a TR to forward traffic. It provides capabilities such as associated forwarding, static routing, route learning, and route synchronization. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01)<br><br><br>* Each TR instance can contain multiple TR route tables to forward traffic of different attachments based on different access requirements.<br><br>* Multiple attachments can be associated with the same TR route table. |Each intra\-region attachment must be associated with exactly one TR route table. This specifies which TR route table the TR uses to forward access traffic from that attachment. |


<span id=".6K6_6Zeu5pa55byP"></span>
## Access methods


* **Console access**

   You can log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter), and manage your resources directly via the webpage.

* **API access**

   You can also initiate requests programmatically using either HTTP or HTTPS for online API calls or secondary development. For specifics, see [API reference](https://docs.byteplus.com/en/docs/transitrouter/Overview).

* **SDK access**

   You can use the SDK to call APIs more conveniently to create and manage TR resources. For details, see [SDK reference](https://docs.byteplus.com/en/docs/transitrouter/Transit-Router-SDK-overview).


<span id=".5Lit6L2s6Lev55Sx5Zmo5LiO5LqR5LyB5Lia572R55qE5a-55q-U"></span>
## Comparison between TR and CEN


|Comparison item |Cloud Enterprise Network |Transit Router |
|---|---|---|
|Application scenario |Supports simple network topologies for full interconnectivity across accounts and regions. It is suitable for scenarios requiring rapid network\-wide connectivity.<br><br><br>* Supports private network interconnectivity between multiple VPCs.<br><br>* Supports private network interconnectivity between multiple VPCs and multiple on\-premises data centers. |Supports complex network topologies across accounts and regions.<br><br>Besides building fully connected networks, TRs also flexibly isolate networks. You can construct any network topology as needed. It is suitable for complex scenarios like hub\-and\-spoke networking.<br><br><br>* Supports private network interconnectivity and isolation between multiple VPCs.<br><br>* Supports private network interconnectivity and isolation between multiple VPCs and multiple on\-premises data centers. |
|Configuration mode |* Load VPCs into a CEN to enable full interconnectivity between different VPCs.<br><br>* Load a VPC and a DC Gateway into the same CEN to enable private network interconnectivity between the VPC and the on\-premises data center. |* Create attachments between a TR instance and a VPC, then configure routes as needed. This enables communication and isolation between different VPCs.<br><br>* Create attachments from the same TR instance to both a VPC and an IPsec\-VPN connection (or a DC Gateway). Then, configure routes as needed to flexibly enable communication and isolation between the VPC and the IPsec\-VPN connection/DC Gateway.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">IPsec\-VPN connection is a component of the VPN service. <a href="https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network">Learn more</a>   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">DC Gateway is a component of the Direct Connect service. <a href="https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect">Learn more</a>   </div><br>    |
|Network Instances |Supports network instances of VPC and DC Gateway. |Supports network instances of VPC, VPN, DC Gateway, and TR. |
|Route configuration |* Simple configuration without manual route addition. The CEN automatically learns routes by [installing network instances](https://docs.byteplus.com/en/docs/cen/Network-instances-01).<br><br>* All routes share a single route table, preventing network isolation. |* Flexible configuration, supporting manual addition and automatic learning for routing setup.<br><br>   * Add a route manually by [creating a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#gT1BKfqN).<br><br>   * Enable TR to learn routes automatically from associated network instances by [creating a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06#.5Yib5bu66Lev55Sx5a2m5Lmg).<br><br>* Quickly and flexibly adjust TR forwarding rules through associated forwarding and forwarding policies.<br><br>* Supports custom route tables to realize network isolation through different TR route tables and route policies. |
|Instance type |All ECS instance types support the CEN service. |Elastic Compute Service (ECS) instance types that do not support the TR service: General\-purpose g1, Compute\-optimized c1, Memory\-optimized r1, Local SSD i1, Big Data Storage d1s, GPU Accelerated g1t, GPU Accelerated g1tl, Local SSD EBM ebmi2, General\-purpose EBM ebmg2i, General\-purpose EBM ebmg2a, High Frequency Compute\-optimized EBM ebmhfc2i, Security Enhanced EBM ebmg2t (beta). |
