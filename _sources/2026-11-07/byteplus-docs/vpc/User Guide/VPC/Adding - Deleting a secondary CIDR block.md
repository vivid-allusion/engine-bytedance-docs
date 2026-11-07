---
title: "Adding/Deleting a secondary CIDR block"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-secondary-CIDR-blocks"
---

## Overview

Secondary CIDR refers to an additional network segment added to the existing IPv4 and IPv6 CIDR blocks of a VPC.

For example: A company's VPC uses `192.168.0.0/20` and plans to create 15 subnets with a `/24` mask. Due to business expansion, adding new modules would involve complex configuration tasks such as security groups, routes, and IAM user permissions if a new VPC were created. Therefore, the company adds the secondary CIDR `192.168.16.0/20` to the VPC to meet new requirements.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a89385f97fae45d99a54c268477b9ac.png)

> **tip**

> For a VPC, both the primary CIDR block and the secondary CIDR are its network segments and are used in the same way.

## Application scenarios

* **Solving the problem of insufficient addresses**

   As business grows, even if network segments were planned in advance, it may still be difficult to adapt to business changes, leading to insufficient addresses. Enabling the secondary CIDR can resolve the issue of insufficient VPC addresses.

* **Reducing planning difficulty**

   As business development constantly changes, initial VPC network segment planning can be relatively conservative. If expansion is needed later, the secondary CIDR can be enabled. This not only reduces the difficulty of network planning but also reduces the cost of maintaining the original network plan. For more information, see [Network planning](https://docs.byteplus.com/en/docs/vpc/Network-planning).

## Add secondary CIDR block

> **tip**

> Both the feature that allows the secondary CIDR to belong to a different major segment from the primary CIDR and the feature that supports public CIDR blocks in VPCs are in beta stage. If you want to try, please contact your account manager.

### Action notes

* Once added, a secondary CIDR block cannot be modified.

* A single VPC is allowed to add up tofive secondary CIDR blocks.

* The secondary CIDR block must not overlap with any other existing CIDR blocks in the target VPC.

* Before the feature "Secondary CIDR can belong to a different major segment from the primary CIDR" is enabled:

   * The secondary CIDR must belong to the same major segment as the VPC's primary CIDR.

      For example, if the target VPC primary CIDR belongs to the `192.168.0.0/16` major segment, then the secondary CIDR must also belong to that major segment and cannot be from the `10.0.0.0/8` or `172.16.0.0/12` network segments.

   * If the VPC's primary CIDR is already the largest segment (e.g., `192.168.0.0/16`), then adding a secondary CIDR is not supported.

* After the feature "Secondary CIDR can belong to a different major segment from the primary CIDR" is enabled:

   * The secondary CIDR does not need to belong to the same major segment as the VPC's primary CIDR. VPC support: 192.168.0.0/16–24, 172.16.0.0/12–24, 10.0.0.0/8–24.

   * If the "VPC supports public CIDR blocks" feature is also enabled, except for the following network segments, all other network segments (including VPC segments) can be used as secondary CIDR blocks for the VPC.

      * 100.64.0.0/10

      * 224.0.0.0/4

      * 127.0.0.0/8

      * 0.0.0.0/8

      * 240.0.0.0/4

      * 169.254.0.0/16

      * 192.18.0.0/15

      * 33.0.0.0/8

      * 66.0.0.0/8

      * 9.0.0.0/8

> **warning**

> If there is a Vital Kubernetes Engine (VKE) cluster in the VPC, the following precautions should be taken when adding a secondary CIDR:

* > When the VKE network model is VPC\-CNI: VPC CIDR cannot conflict with the VKE Service CIDR.

* > When the VKE network model is Flannel: VPC CIDR cannot conflict with the VKE Service CIDR or Pod CIDR.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc)

2. In the top menu bar, select the target project and region.

3. Click the name of the target VPC.

4. On the **CIDR Block Management** tab, click **Add secondary IPv4 CIDR**.

5. Enter the secondary CIDR block to be added.

6. Click **OK** to complete the action.

### What to do next

After adding a secondary CIDR, you can use the secondary CIDR block to [Create subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).

## Delete secondary CIDR block

### Prerequisites

The VPC did not use a secondary CIDR block when creating the subnet. If already created, see [Deleting a subnet](https://docs.byteplus.com/en/docs/vpc/Deleting-a-subnet).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target project and region.

3. Click the name of the target VPC.

4. On the **CIDR Block Management** tab, click **Delete** to the right of the target Secondary CIDR block.

5. Click **Delete** to complete the action.

## Related documents

* [AssociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock)

* [DisassociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/DisassociateVpcCidrBlock)
