---
title: "Getting started"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPv4-Gateway-Quick-start"
---

This topic introduces how to quickly use an IPv4 gateway.

## ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_434a45201dee10b75643a5ac6bb32813.png)

## Preparations

Create a VPC and two ECSs bound to EIPs as shown in the figure above. For actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

## Procedures

### Step 1: Create IPv4 Gateway

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation tree, select **IPv4 Gateway**.

3. In the top menu bar, select your target Region.

4. Click **Create IPv4 Gateway**.

5. Enter the name of the IPv4 Gateway.

6. Click **Migrate** to complete the action.

### Step 2: Associate and activate VPC

1. Click **Associate and activate VPC** to the right of the target IPv4 Gateway.

2. Select the VPC and subnet route table from dropdown.

3. Click **Activate** to complete the action.

After association, the subnet route table selected from the dropdown above will automatically generate a route entry with the destination CIDR 0.0.0.0/0 and the next hop pointing to the IPv4 gateway.

> **warning**

> After the IPv4 gateway is associated with and activated for a VPC, resources within the VPC will query the subnet route table when accessing the IPv4 internet. If the route table does not contain a route entry with the IPv4 gateway as the next hop, Internet access will fail. Add this route entry to the target subnet route table based on your business needs. For specific steps, see [Adding a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

## Verification

1. Log in to the prepared ECS instance.

2. Run the `ping 114.114.114.114` command.

3. A successful ping indicates that the ECS is connected to the Internet. If the ping fails, check whether the subnet route table contains a route entry with the destination CIDR 0.0.0.0/0 and the next hop pointing to the IPv4 gateway.
