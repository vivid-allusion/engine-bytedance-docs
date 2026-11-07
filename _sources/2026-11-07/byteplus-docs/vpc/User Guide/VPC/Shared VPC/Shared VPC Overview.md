---
title: "Shared VPC Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Shared-VPC-Overview"
---

## Introduction

Shared VPC allows multiple accounts to share a single VPC. Through a shared VPC, multiple accounts can create and manage cloud resources (such as ECS servers and Classic Load Balancer (CLB) ) within the same VPC. This enables unified network planning, centralized cloud resource management, simplifies network structure, and reduces network operational costs.

* **Resource Owner:**  The owner of the shared VPC, i.e., the initiating account that shares the VPC.

* **Shared user:**  The user of the shared VPC, i.e., the recipient account. This account can create and manage cloud resources within the shared subnets.

## Application scenarios

When multiple enterprise accounts require unified planning and centralized management of their network, the Shared VPC functionality can be used. Usage methods:

* Network Administrator Account M: Plans subnet CIDR blocks uniformly and assigns them to business accounts as needed.

* Business Account A: Has access to Shared Subnet A and can create cloud resources within it.

* Business Account B: Has access to Shared Subnet B and can create cloud resources within it.

* Business Account C: Has access to Shared Subnet C and can create cloud resources within it.

   ...

* Business Account N: Has access to Shared Subnet N and can create cloud resources within it.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f90f33c524c9c9b6fc36835a2398a5a9.png)

## Permission notes

After sharing a VPC from one account to multiple accounts, the permissions of the **Resource owner** versus **Shared user** for **The VPC and related resources** are as follows:

|Resource ||Actions executable by the resource owner |Operations available to shared users |
|---|---|---|---|
|Resources within the VPC |Virtual Private Cloud (VPC) |Full operational permission |Shared users are granted view permissions but restricted from modifying or deleting the VPC. |
||Subnet |Full operational permission |View permission only for shared subnets; modification and deletion are not supported |
||Route Table |Full operational permission |View permission only for Route Tables associated with shared subnets; modification and deletion are not supported |
||Network ACL |Full operational permission |View permission only for Network ACLs associated with shared subnets; modification and deletion are not supported |
||Network interface |* Created by resource owner: Full operational permission<br><br>* Created by resource sharer: View\-only access; modification and deletion are not permitted |* Created by resource owner: No permission<br><br>* Created by shared user: Full permission |
||Security group |* Created by resource owner: Full operational permission<br><br>* Created by resource sharer: View\-only access; modification and deletion are not permitted |* Created by resource owner: No permission<br><br>* Created by shared user: Full permission |
||HAVIP |Full operational permission |No permission |
|Related resources |Flow Log |* Flow logs can be created for shared VPCs or subnets. Traffic from network interfaces created by consumer accounts within the VPC will be logged.<br><br>* Flow logs can only be created for network interfaces provisioned by the resource owner. Interfaces created by shared users are not supported. |No permission |
||Traffic Mirror |* Mirror site: Only support network interfaces created by the resource owner as mirror sites.<br><br>* Traffic mirror target: Only support network interfaces created by the resource owner as traffic mirror targets. |No permission |
||Prefix List |* Created by the Resource Owner: Full operational permissions, but can only associate with route tables and security groups created by the resource owner<br><br>* Created by shared user: No permission |* Created by resource owner: No permission<br><br>* Created by shared user: Full permissions, but can only associate with security groups created by the same shared user |
||NAT Gateway |Full operational permissions to configure NAT gateways, either within a shared subnet or within a separately provisioned subnet, to provide internet services for cloud resources in the shared subnet |No permission |
||VPN |Full operational permissions to configure VPN connections, either within a shared subnet or within a separately provisioned subnet, establishing a temporary, secure, and reliable communication tunnel over the internet for cloud resources within the shared subnet |No permission |
||Cloud Enterprise Network |Full operational permissions to attach the VPC to a Cloud Enterprise Network (CEN) instance, enabling private connectivity between resources within the shared subnet and resources in other VPCs or on\-premises IDCs |No permission |
||Transit Router |Full operational permissions to create a VPC\-type network instance connection within a Transit Router, enabling on\-demand private connectivity between resources within the shared subnet and resources in other VPCs or on\-premises IDCs |No permission |

> **tip**

> After subnet sharing is deactivated, the shared user can no longer use that subnet to create new cloud resources; however, any existing resources they previously created continue to function normally.

* Tag: Within a shared VPC, both the resource owner and resource sharers can add tags to any resource for which they have view permissions.

* Project: Within a shared VPC, any resource for which a user (owner or sharer) has only view permissions is automatically placed into the user's default project. This assignment cannot be changed.

## Limitations

* A single subnet can be shared with a maximum of 50 accounts. A single account can receive up to 50 shared subnets.

* Subnets belonging to the default VPC cannot be shared.

* Currently, authorized accounts can create the following cloud resources within shared subnets, as listed in the table below:

   |Classification |Cloud resource |
   |---|---|
   |Compute |[Elastic Compute Service (ECS)](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service) |
   ||[Auto Scaling (AS)](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling) |
   |Network | [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) |
   ||[Network Load Balancer(NLB)](https://docs.byteplus.com/en/docs/clb/What-is-Network-Load-Balancer) |
   ||[Application Load Balancer (ALB)](https://docs.byteplus.com/en/docs/clb/Introduction) |
   |Container and middleware |[Vital Kubernetes Engine](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Kubernetes-Engine) |

## Usage process

1. Configure enterprise organization

2. [Enable shared VPC](https://docs.byteplus.com/en/docs/vpc/Managing-shared-VPC)

3. [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group)

4. Create cloud resources:

   * [Create Elastic Compute Service (ECS)](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances)

   * [Create Classic Load Banlancer (CLB)](https://docs.byteplus.com/en/docs/clb/CLB-instances-01)

   * [Create Application Load Balancer (ALB)](https://docs.byteplus.com/en/docs/clb/Creating-an-instance)
