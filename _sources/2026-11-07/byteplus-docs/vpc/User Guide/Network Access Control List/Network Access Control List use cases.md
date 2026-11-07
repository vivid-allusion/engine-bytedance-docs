---
title: "Network Access Control List use cases"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Network-ACL-use-cases"
---

This topic provides configuration examples of Network Access Control List (Network ACL) for common applications.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To prevent misoperations that attach a Network Access Control List, causing data flow failure, the default rules of the Network Access Control List allow all traffic. If you need to use the Network Access Control List, you can modify the default as needed.</div>


<span id="z7xQG6Ce"></span>
## Intercommunication and isolation of resources between subnets within the same VPC

Subnets in the same Virtual Private Cloud (VPC) are connected to each other by default. If needed, subnets can be attached to a Network Access Control List to restrict intercommunication and isolate resources among different subnets.

As shown in the diagram: Two subnets within the same VPC are attached to the same Network Access Control List, and rules are configured in the Network Access Control List to enable communication between ECS\-A and ECS\-C, while isolating them from ECS\-B.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7cba6cc786c1f4ee49b71eaa4a676c43.png) </span>

<span id="m1nPjaxZ"></span>
## Restrict access to resources in a subnet

If all resources within a subnet only support access from specific addresses, you can use a Network Access Control List. After a subnet is attached to a Network Access Control List, you can configure Network ACL entries to restrict traffic from non\-current VPCs from accessing resources in the current subnet.

As shown in the figure: Attach the subnet to the Network Access Control List, configure the Network ACL entry, and allow only the client 10.0.1.11 to access the resources within the subnet.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_107c0971b03958e73e072fdc6758be9c.png) </span>

&nbsp;
