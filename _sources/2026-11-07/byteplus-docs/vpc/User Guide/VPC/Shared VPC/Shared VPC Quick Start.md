---
title: "Shared VPC Quick Start"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Getting-Started-with-Shared-VPC"
---

## Background introduction

An enterprise has multiple business departments, each with its own account. Different departments have different network requirements: Business Department A needs to access the internet. Business Department B only needs private network access to internal resources. Business Department C needs to provide services to the internet. The current architecture uses a Shared VPC for management, as shown below:​​

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c92239a68eb506f851ea47705a36d94d.png)

* Network Admin Account M:​​ Creates a VPC​​ and provisions multiple subnets.

   * Deploys a public NAT Gateway in Subnet Network​​ to enable internet access for resources in Subnet A

   * Shares subnet A with business account A (i.e., department A).

   * Shares subnet B with business account B (i.e., department B).

   * Shares subnet C with business account C (i.e., department C).

* Business Account A: Uses Subnet A to create multiple ECS instances and configures them to access the internet through a public NAT gateway.

* Business Account B: Uses Subnet B to create multiple ECS instances and configures them for private network access to the ECS instances in Subnet A.

* Business Account C: Uses Subnet C to create multiple ECS instances and a CLB instance, configuring the ECS instances to provide services to the internet via the CLB instance.

## Preparations

* Add the network management account M and business accounts A, B, and C to the same enterprise organization.

* Using the network management account M, create a VPC (named VPC\-1) and 4 subnets (named Subnet\-A, Subnet\-B, Subnet\-C, and Subnet\-Network).

* Apply for an EIP address (named EIP\-1).

## Procedures

### Network admin configuration

Log in to the network administrator account M, configure a public NAT gateway, enable the VPC sharing feature, and share Subnet A with Account A, Subnet B with Account B, and Subnet C with Account C.

#### Configure the public NAT gateway

1. [Create NAT gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway): Select VPC\-1 for the VPC and select subnet Network for the subnet.

2. [Associate EIP](https://docs.byteplus.com/en/docs/natgateway/Associating-or-disassociating-an-EIP): Associate an EIP with the Internet NAT gateway.

3. [Create SNAT rule](https://docs.byteplus.com/en/docs/natgateway/Managing-SNAT-rules): Create a subnet\-level SNAT rule, selecting subnet\-A for the subnet.

> **tip**

> This topic uses only the default system route table. If different subnets are associated with different route tables, you will need to add a custom route entry in those route tables with a destination CIDR block of `0.0.0.0/0` and the next hop set to the public NAT gateway instance. For actions, see [Adding a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

#### Enable shared VPC

Follow the steps below to share Subnet A with Account A, Subnet B with Account B, and Subnet C with Account C.

1. Log in to the [Resource Sharing Console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left\-side navigation pane, select **Resource sharing \> Shared by me**.

3. In the top menu bar, select your target Region.

4. In the Shared Unit tab, click **Create shared unit**.

5. Configure relevant parameters based on the table below.

   |Parameters |Explanation |Example A |Example B |Example C |
   |---|---|---|---|---|
   |Unit name |Type in a name for the shared unit. |Shared subnet A |Shared Subnet B |Shared subnet C |
   |Regions |Select the region where the shared VPC resides. |China (Beijing) |China (Beijing) |China (Beijing) |
   |Product |Select vpc \- subnet. |Virtual Private Cloud \- Subnet |Virtual Private Cloud \- Subnet |Virtual Private Cloud \- Subnet |
   |ID |Select the IDs of subnets to share. |Select the ID of subnet A |Select the ID of subnet B |Select the ID of subnet C |
   |Shared policy name |Defaults to and only supports RSDefaultPermissionForSubnet. |RSDefaultPermissionForSubnet |RSDefaultPermissionForSubnet |RSDefaultPermissionForSubnet |
   |Resource user |Select only allow sharing with the same organization within the enterprise. |Only allow sharing with the same organization within the enterprise |Only allow sharing with the same organization within the enterprise |Only allow sharing with the same organization within the enterprise |
   |Add by business organization |Enable Add via enterprise organization and select the master account. |ID of account A |ID of account B |ID of Account C |

6. Click **Next**, confirm everything is correct, then click **Confirm** to complete the actions.

### Configure business account A

Log in to business account A and create multiple ECSs without EIP addresses in Subnet\-A of VPC\-1. Configure these servers to access the Internet through the Internet NAT Gateway.

1. Configure Security Group:

   1. [Create Security Group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group): When Account A creates an ECS in Subnet A of VPC\-1, it cannot associate the VPC's default security group Default. Therefore, a new security group must be created within VPC\-1.

   2. [Add security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules): In addition to the default security group rules, allow the following traffic:

      |Direction |Strategy |Protocol type |Port range |Source IP address |Description |
      |---|---|---|---|---|---|
      |Inbound |Allow |TCP |22 |0.0.0.0/0 |For remote login to ECSs |
      |Inbound |Allow |ALL |ALL |192.168.2.0/24 |For private network connectivity between ECSs and business account B. |

2. [Create ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances): Create multiple ECSs without EIPs in Subnet A of VPC\-1, assigning the newly created security group.

3. Verification: Log in to the ECS and execute the `ping 8.8.8.8` command in the command line to verify whether the ECS can access the internet. The output should be similar to the following figure:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aed0bf5c79b46e65b3794c772034bb2e.png)

   > **tip**

   > If the access fails, log in to the network administrator account M to check whether the SNAT rules are configured correctly and verify that the route table associated with Subnet\-A has a route configured to the public NAT gateway.

### Configure business account B

Log in to business account B and create multiple ECSs without EIP addresses. Configure these servers to access the ECSs in Subnet\-A through the VPC.

1. Configure Security Group:

   1. [Create Security Group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group): When creating ECSs in Subnet\-B of VPC\-1 from account B, it is not possible to associate them with VPC\-1's default security group Default. Therefore, a new security group must be created within VPC\-1.

   2. [Add security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules): In addition to the default security group rules, allow the following traffic:

      |Direction |Strategy |Protocol type |Port range |Source IP address |Description |
      |---|---|---|---|---|---|
      |Inbound |Allow |TCP |22 |0.0.0.0/0 |For remote login to ECSs |
      |Inbound |Allow |ALL |ALL |192.168.1.0/24 |For private network connectivity between ECSs and business account A. |

2. [Create ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances): Create multiple ECSs without EIP addresses in Subnet\-B of VPC\-1, attaching the newly created security group to these servers.

3. Verification: Log in to the ECS and execute the `ping <ECS in Subnet A>` command in the command line to verify whether the ECS can access the VPC. The output should be similar to the following figure:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f630b83513034c99dd8140c97e82aa54.png)

### Configure business account C

Log in to business account C and execute the following operations:

1. Configure Security Group:

   1. [Create Security Group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group): When creating ECSs in Subnet\-C of VPC\-1 from account C, it is not possible to associate them with VPC\-1's default security group Default. Therefore, a new security group must be created within VPC\-1.

   2. [Add security group rules](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules): In addition to the default security group rules, allow the following traffic:

      |Direction |Strategy |Protocol type |Port range |Source IP address |Description |
      |---|---|---|---|---|---|
      |Inbound |Allow |TCP |22 |0.0.0.0/0 |For remote login to ECSs |
      |Inbound |Allow |TCP |80 |0.0.0.0/0 |Receive IPv4 client requests forwarded by the CLB |
      |Inbound |Allow |TCP |80 |100.64.0.0/10 |Receive health check request |

2. [Create ECS](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances): Create multiple ECSs without EIP addresses in Subnet\-C of VPC\-1, attaching the newly created security group.

3. Set up the backend service for the newly created Elastic Compute Service .

4. Configure CLB: When creating a public CLB, select the shared Subnet\-C for subnet configuration. For specific operational steps, see [Layer-4 CLB Quick start](https://docs.byteplus.com/en/docs/clb/Layer-4-CLB-01).
