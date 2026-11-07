---
title: "What is NAT Gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway"
---

The NAT Gateway provides network address translation services for Elastic Compute Service (ECS) within the Virtual Private Cloud (VPC).

<span id=".5YWs572RTkFU572R5YWz"></span>
## Internet NAT Gateway

The Internet NAT Gateway is an enterprise\-level public gateway that provides public address translation services for ECS within the VPC. It supports SNAT and DNAT entries, enabling multiple ECSs to share a public IP to access the internet or provide services to the internet.


|Feature |Description |
|---|---|
|SNAT entry |Source address translation: When an ECS instance actively accesses the internet, the Internet NAT gateway replaces the source address and port in the access request with the Elastic IP Address (EIP) and port before forwarding. |
|DNAT entry |Destination address translation. This means mapping the EIP and its port bound to the nat gateway to the ECS instance’s private IP and port. When the EIP and port are accessed, the internet nat gateway replaces the destination address and port in the access request with the ECS instance’s private IP and port before forwarding. |


<span id=".56eB572RTkFU572R5YWz"></span>
## VPC NAT Gateway

The VPC NAT Gateway provides private address translation services for ECS within a VPC. Multiple ECSs can communicate with other VPCs or on\-premises data centers through the VPC NAT Gateway.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b763085ee56fa4327e26fba60848b55a.png) </span>


|Feature |Description |
|---|---|
|SNAT entry |Source address translation. When an ECS accesses resources outside this VPC, the VPC NAT Gateway replaces the source address and port in the request with the NAT IP address and port before forwarding. |
|DNAT entry |Destination address translation. When the NAT IP address and port are accessed, the VPC NAT Gateway replaces the destination address and port in the request with the ECS's private IP address and port before forwarding. |
|NAT IP |Allocated from the subnet of the vpc nat gateway for ip address translation. |
