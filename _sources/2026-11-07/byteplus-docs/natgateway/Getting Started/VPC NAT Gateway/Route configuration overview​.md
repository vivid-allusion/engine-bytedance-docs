---
title: "Route configuration overview​"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Route-configuration-principles"
---

This article introduces the routing principles and configuration process of the VPC NAT Gateway.

## Principle description

The VPC NAT Gateway routing configuration requires at least two route tables, described as follows:

|Route table |Description |Route entry |
|---|---|---|
|Route table 1 |Routes traffic from an Elastic Compute Service (ECS) to the peer CIDR block through the VPC NAT Gateway.​ |Destination CIDR: The peer CIDR block. Next Hop: The VPC NAT Gateway. |
|Route table 2 |Routes traffic from the VPC NAT Gateway to a Cloud Enterprise Network (CEN) or Transit Router (TR).​ |Destination CIDR: The peer CIDR block. Next Hop: The CEN or TR. |

> **tip**

> For easier explanation in this documentation, route table 1 is the system route table, and route table 2 is the custom route table.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4fcef6d89bbafa91c0774313f8626d03.png)

## Configure routing

### Prerequisites

You have created a VPC NAT Gateway. For related actions, see [Creating a VPC NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-a-VPC-NAT-Gateway).

### Configuration procedures

#### Step 1: Prepare the route table

1. [Create a custom route table](https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table): Create a custom route table in the VPC where the VPC NAT Gateway is located.

2. [Associate subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet#.5YWz6IGU5a2Q572R): Switch the subnet where the VPC NAT Gateway resides from the default system route table to the newly created custom route table.

At this point, the subnet with the cloud resources in the peer CIDR block uses the system route table, while the subnet with the VPC NAT Gateway uses the custom route table.

#### Step 2: Route traffic to the VPC NAT Gateway

[Add a route entry to the system route table](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#70HRpqsH): Add a route entry in the system route table with the destination CIDR set to the peer CIDR block and the next hop set to the VPC NAT Gateway, routing traffic to the peer CIDR block through the VPC NAT Gateway.

#### Step 3: Route traffic to Cloud Enterprise Network or Transit Router

* **Cloud Enterprise Network (CEN)** : After the current VPC and the peer VPC or Direct Connect Gateway are [attached to CEN](https://docs.byteplus.com/en/docs/cen/Network-instances-01), the custom route table automatically adds a route entry with the destination CIDR set to the peer CIDR block and the next hop set to CEN. The system route table already contains a route with the destination CIDR as the peer network, so it will not be added automatically.

* **Transit Router (TR)** : After creating an attachment connecting the TR to the VPC where the VPC NAT Gateway resides, manually add a route entry with the destination CIDR as the peer network and the next hop as the Transit Router in the custom route table.
