---
title: "Subnet route table use cases"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Route-table-use-cases"
---

A route table directs traffic within a Virtual Private Cloud (VPC) by specifying the next\-hop cloud resource, which then forwards the VPC traffic. This topic introduces the applications of route tables across various cloud products.

<span id=".5Luj55CG5YWs572R6K6_6Zeu"></span>
## Proxy Internet Access

<span id=".5YWs572RTkFU572R5YWz"></span>
### Public NAT Gateway

Creating a public NAT gateway and configuring SNAT rules allows the ECSs associated with the SNAT rules to access the internet through the NAT gateway. The routing of the NAT gateway is as shown in the following diagram:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d4523ab91b083630ef229145354b2f35.png) </span>

<span id=".5LqR5pyN5Yqh5Zmo"></span>
### Elastic Compute Service (ECS)

ECS\-1 in Subnet\-1 has an EIP bound to it and has a self\-built SNAT service configured. The ECS\-2 in Subnet\-2 accesses the internet through ECS\-1. The route configuration is shown in the figure below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b08a193cea3d1317cf802e6bff77dee.png) </span>

<span id=".6L6F5Yqp572R5Y2h"></span>
### Secondary network interfaces

ECS\-1 in Subnet\-1 uses its secondary network interface, which is bound to an EIP address, and has a self\-configured SNAT service running. The ECS\-2 in Subnet\-2 accesses the internet by routing its traffic through ECS\-1. The route configuration is shown in the figure below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a1e56beb0a2c976b9147712dda04869.png) </span>

<span id=".5omT6YCaVlBD5LiOVlBD"></span>
## Interconnection between VPCs

<span id=".5LqR5LyB5Lia572R"></span>
### Cloud Enterprise Network (CEN)

When multiple VPCs are attached to a CEN, their route tables automatically synchronize relevant routing entries. For example, after VPC\-A and VPC\-B are connected to the CEN, newly added route entries in the routing table are shown in the diagram below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7719f6d9a5f288ceaad31ff1aa4db139.png) </span>

<span id=".5Lit6L2s6Lev55Sx5Zmo"></span>
### Transit Router (TR)

The Transit Router enables interconnection and isolation between multiple VPCs. For example, VPC\-A and VPC\-B can communicate with VPC\-C, while VPC\-A and VPC\-B remain isolated from each other. The relevant routing configuration is illustrated in the diagram below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ca5927755658038dcf9dbc650b404aba.png) </span>

<span id=".5omT6YCaVlBD5LiO5pys5ZywSURD"></span>
## Connect a VPC to an on\-premises IDC

<span id=".VlBO6L-e5o6l"></span>
### VPN Connect

A VPN connect establishes secure communication between a VPC and an on\-premises IDC (Data Center). The required route configuration for the VPC is shown in the diagram below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46dc7d9752c5344832b92291ae020e1e.png) </span>

<span id=".5LiT57q_6L-e5o6l"></span>
### Direct Connect (DC)

A more robust and performant connection can be established using CEN in conjunction with Direct Connect. Using CEN as an example, the relevant routing configuration that enables this interconnectivity is illustrated in the following diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90317b7e8a512185e42afd540d94c086.png) </span>
