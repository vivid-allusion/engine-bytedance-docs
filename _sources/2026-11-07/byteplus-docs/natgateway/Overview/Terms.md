---
title: "Terms"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Terms"
---

<span id="elastic-ip-address"></span>
## Elastic IP Address

An Elastic IP Address (EIP) is a public IP address that you can purchase and use as an independent resource. You can associate EIPs with Elastic Compute Service instances, secondary network interfaces, High\-Availability Virtual IP Addresses, Internet NAT Gateways, and Cloud Load Balancers. This improves communication over the internet.

<span id="snat-rule"></span>
## SNAT rule

Source Network Address Translation (SNAT) allows multiple ECS instances to access the internet through a shared elastic IP address. For example, after you create an SNAT rule for a subnet, all ECS instances that are not assigned EIPs in the subnet can access the internet.

<span id="dnat-rule"></span>
## DNAT rule

Destination Network Address Translation (DNAT) allows multiple ECS instances to share an EIP to provide services to the public network. For example, after you create a DNAT rule, users can access the service deployed on the ECS instances of the DNAT rule through the internet.
