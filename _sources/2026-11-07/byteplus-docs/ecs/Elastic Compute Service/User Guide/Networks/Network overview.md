---
title: "Network overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Networks-overview"
---

The BytePlus platform provides a variety of network products you can use to build **VPC** or **Internet** environments for your cloud resources. You can use these products to set up independent and isolated network environments in the cloud. You can also use these products to establish communication channels in various business scenarios, such as between cloud resources, or between cloud resources and on\-premises resources (such as the Internet and local servers). This way, resources can be shared and data can be exchanged.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic describes only the network products directly relevant to ECS instance usage.</div>


<span id=".572R57uc57G75Z6L"></span>
## Network types

<span id=".56eB572R"></span>
### VPC

A VPC provides an isolated, self\-configurable virtual network environment for cloud resources, offering enhanced security. You have full control over your VPC and the resources within the VPC.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3d386b846aa72505a5c041610c3cdc0a.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For all BytePlus cloud resources, you need to use​ <a href="https://docs.byteplus.com/en/docs/ecs/VPC-overview">VPC</a> to build a basic network environment.</div>


By default, VPCs cannot communicate with the Internet, and different VPCs cannot communicate with each other and are completely isolated.


* If you want to connect your VPC to the Internet, you need to use Internet products. For more information, see the following **Internet** section.

* To connect cloud resources across different VPCs, you need to use products such as Cloud Enterprise Network (CEN), Transit Router (TR), and PrivateLink. For more information, refer to [VPC application scenarios](https://docs.byteplus.com/en/docs/vpc/Application-scenarios).

* To connect cloud resources to on\-premises resources, such as the Internet or local servers, you need to use products such as Direct Connect (DC) and Virtual Private Network (VPN). For more information, refer to [VPC application scenarios](https://docs.byteplus.com/en/docs/vpc/Application-scenarios).


**Related operation guides:** 


* [Setting up IPv4 VPCs](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC)

* [Setting up IPv6 VPCs](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv6-VPC)


<span id=".5YWs572R"></span>
### Internet

[Elastic IP Address (EIP)](https://docs.byteplus.com/en/docs/ecs/EIP-overview) provides an IP connectivity service that can be independently purchased and owned for cloud resources. You only need to associate an EIP with an ECS instance, and the ECS instance can communicate flexibly and conveniently with the Internet or with other cloud or on\-premises resources that have an associated EIP.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38116bdd733576d836fc19177ec7c9e5.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In addition to EIP, BytePlus provides you with multiple products for connecting to the Internet. For more information, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Application-scenarios">VPC application scenarios</a>.</div>


**Related operation guides:** 


* [Applying for EIPs and associating EIPs with ECS instances](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP-and-associating-an-ECS-instance)

* [Changing EIP configuration](https://docs.byteplus.com/en/docs/ecs/Changing_EIP_configuration)
