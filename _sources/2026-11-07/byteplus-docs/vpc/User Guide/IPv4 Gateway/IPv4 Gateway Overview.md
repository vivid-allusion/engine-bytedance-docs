---
title: "IPv4 Gateway Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPv4-Gateway-Overview"
---

## Introduction​

IPv4 Gateway manages the inbound and outbound IPv4 internet traffic of a private network, enabling centralized control and fine\-grained management of such traffic.

If you need to manage IPv6 internet traffic, see [IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway).

## Direct Internet Access vs. Centralized IPv4 Gateway Management

|Direct Internet Access |Centralized IPv4 Gateway Management |
|---|---|
|**EIPs take precedence over subnet route tables.**  If an ECS is bound to an EIP, its IPv4 internet traffic bypasses the subnet route table and directly accesses the internet.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d54563cacff496a6e990fb00b6b29c7.png) |Follows the **Longest Prefix Match rule**: All IPv4 internet traffic must pass through the subnet route table to access the internet.<br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3dbf987945f8b0e313a6f7985ab377ea.png)<br><br> |

## Application scenarios

### **Centralized IPv4 Internet Traffic Gateway Management**

Centrally manage IPv4 Internet traffic entering and leaving the VPC. Unify control over Internet traffic to avoid security risks caused by users accidentally binding EIPs to ECS instances.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d085036545abb9c83e0d4c0fbb443d2b.png)

### **EIP Cross\-Region Disaster Recovery**

To ensure business stability, you can configure Internet egress points in multiple regions for your business resources. If the Internet egress in the current region fails, you can use the backup region's Internet egress to achieve cross\-region disaster recovery.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dfd875c175ae6ec75692b7cc8d5e054c.png)

## Billing

The IPv4 gateway is free of charge.

## Limitations

When a VPC is associated with an IPv4 gateway, the following limitations apply:

|Limit |Explanation |
|---|---|
|The IPv4 Gateway and the Passthrough NAT Gateway are mutually exclusive |A VPC with a Passthrough NAT Gateway cannot be associated with an IPv4 Gateway, and vice versa. |
|IPv4 Gateway and direct EIP are mutually exclusive |A VPC containing cloud resources bound to a direct EIP cannot be associated with an IPv4 gateway, and vice versa. |
|IPv4 Gateway and Anycast EIP are mutually exclusive |A VPC containing cloud resources bound to an Anycast EIP cannot be associated with an IPv4 gateway, and vice versa. |
|IPv4 Gateway and User CIDR Block are mutually exclusive |A VPC with a custom CIDR block cannot be associated with an IPv4 Gateway, and vice versa. |
|One\-to\-one binding |A single VPC can only be associated with one IPv4 gateway, and an IPv4 gateway can only be associated with one VPC. |

> **tip**

> EIPs bound to Classic Load Balancer (CLB) and Application Load Balancer (ALB) are not restricted by the IPv4 gateway. EIPs bound to Network Load Balancer (NLB) are restricted by the IPv4 gateway.

## Usage process

1. [Create IPv4 Gateway](https://docs.byteplus.com/en/docs/vpc/Creating-an-IPv4-Gateway)

2. [Attach and activate VPC](https://docs.byteplus.com/en/docs/vpc/Associating-Disassociating-a-VPC#.5YWz6IGU56eB5pyJ572R57uc)

3. [Configure routing entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry)

## Example Use Cases

* [Getting started](https://docs.byteplus.com/en/docs/vpc/IPv4-Gateway-Quick-start)

* [EIP Cross-Region Disaster Recovery](https://docs.byteplus.com/en/docs/vpc/EIP-Cross-Region-Disaster-Recovery)
