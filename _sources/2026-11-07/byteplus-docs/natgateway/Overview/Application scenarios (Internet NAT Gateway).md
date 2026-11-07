---
title: "Application scenarios (Internet NAT Gateway)"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Scenarios"
---

This topic describes application scenarios for Internet NAT Gateway.

<span id=".5L2_55SoU05BVOiuv-mXruWFrOe9kQ=="></span>
## Enable Internet access via SNAT

When multiple Elastic Compute Service (ECS) instances in a Virtual Private Cloud (VPC) need to access the Internet, you can use SNAT entries of the Internet NAT Gateway to minimize Elastic IP Addresses (EIPs) and avoid exposing ECS IPs directly on the Internet. This enables secure, convenient, and efficient Internet access.

SNAT entries support four granularities: VPC, subnet, ECS, and custom CIDR block. You can flexibly configure them according to your business needs.

Using subnet granularity as an example, the diagram below illustrates the scenario of accessing the Internet with an SNAT entry.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b979112b1cb3169adeefc4555c74b5a.png) </span>


* ECS instances in Subnet 1 can access the Internet through the Internet NAT Gateway and EIP 1 under SNAT entry 1.

* ECS instances in Subnet 2 can access the Internet through the Internet NAT Gateway and EIP 2 under SNAT entry 2.


<span id=".5L2_55SoRE5BVOWQkeWFrOe9keaPkOS-m-acjeWKoQ=="></span>
## Provide services to Internet via DNAT

When multiple ECS instances in a virtual private cloud need to serve the Internet, you can use DNAT entries on an Internet NAT Gateway to reduce EIP usage and avoid exposing their private IPs directly on the Internet.


* DNAT entry 1 maps port 12 of ECS1's private IP to port 12 of the EIP. Under DNAT entry 1, ECS1 can serve the Internet through the Internet NAT Gateway and the EIP.

* DNAT entry 2 maps port 34 of ECS2's private IP to port 34 of the EIP. Under DNAT entry 2, ECS2 can serve the Internet through the Internet NAT Gateway and the EIP.


<span id=".5ZCM5LiA5LiqVlBD5aSa5Liq5YWs572RTkFU572R5YWz"></span>
## Multiple Internet NAT Gateways in the same VPC

If the Internet connection count of ECS instances in a virtual private cloud exceeds the limit of a single Internet NAT Gateway, you can create multiple Internet NAT Gateways within the same VPC and allocate connections across them to ensure stable operation.

If ECS instances in different subnets of the same VPC access different Internet destinations, you can create multiple Internet NAT Gateways within the VPC and route traffic through different gateways for finer traffic management.

The following diagram illustrates the scenario of multiple Internet NAT Gateways in the same VPC.


* ECS instances in subnet 1 access the Internet through Internet NAT Gateway 1 and EIP 1.

* ECS under subnet 2 accesses the Internet through Internet NAT Gateway 2 and EIP 2.


<span id=".5pys5Zyw5pWw5o2u5Lit5b-D5L2_55So5LqR5LiK5YWs572RTkFU572R5YWz"></span>
## On\-premises data center uses an Internet NAT Gateway

When multiple servers in an on\-premises data center connected via Direct Connect (DC) need Internet access or provide services to the Internet, you can use the BytePlus Internet NAT Gateway to enable those servers to access or provide services to the Internet.

<span id=".5aSa5LiqVlBD5YWx5Lqr5LiA5Liq5YWs572RTkFU572R5YWz"></span>
## Multiple VPCs share an Internet NAT Gateway

When multiple ECS instances in multiple VPCs (same or cross\-region) need to access the Internet or provide services to external users, you can use Cloud Enterprise Network (CEN) and an Internet NAT Gateway. This setup allows those ECS instances in multiple VPCs to share one Internet NAT Gateway for Internet access or service provision.

&nbsp;
