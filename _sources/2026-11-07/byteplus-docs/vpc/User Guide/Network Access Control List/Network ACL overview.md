---
title: "Network ACL overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview"
---

## Overview

Network ACL (Network Access Control List) is used to control inbound and outbound traffic of subnets using a allowlist mechanism. Only traffic that matches the rules is allowed; all other traffic is blocked. A subnet can be associated with only one network ACL.

Network ACLs are often used together with security groups, where [security groups](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) control inbound and outbound traffic of network interfaces within the subnet. Traffic example diagram is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb683b1a66e10c83c78f46e03ce6f7f2.png)

> **tip**

> The following products deployed within a subnet are not affected by network ACLs:

* > Databases on the BytePlus , such as the MySQL edition of Cloud Database.

* > [Classic Load Balancer CLB](https://docs.byteplus.com/en/docs/clb/Product-Overview-01).

* > Network interfaces bound with a [Direct EIP](https://docs.byteplus.com/en/docs/eip/Set-up-EIP-Pass-through-Mode).

## Acl entry

* Network ACL is **Stateless**. Return traffic must be explicitly allowed by rules, meaning that both outbound and inbound directions must be explicitly permitted by the rules.

* Changes to Network ACL rules take effect immediately. Both existing persistent connections and subsequently newly established connections are controlled by the rules.

* It is recommended to cautiously allow common business ports such as SSH (22), Redis (6379), MemCached (11211), MySQL (3306), SMB (445), RDP (3389), and SQL Server (1433). For more information on common ports for ECSs, see [Common ports for ECSs](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances).

### Components

* **Parameter description**

   Network ACLs primarily consist of a triplet (Source/Destination Address, Protocol, Destination Port). The related parameters are as follows:

   |Parameters |Notes |Example |
   |---|---|---|
   |Direction |Divided into inbound rules and outbound rules.<br><br><br>* Inbound Rule: Control traffic from external resources accessing resources within the Network ACL.<br><br>* Outbound Rule: Control traffic from resources within the Network ACL accessing external resources. |Inbound |
   |Priority |For Network ACLs, priorities are numbered in ascending order starting from 1, meaning that a lower number (e.g., 1) indicates a higher priority. Dragging to adjust the order will automatically update the priority of Network ACL rules. `*` indicates the default priority, which is the lowest. |1 |
   |Policy |Allow or deny traffic. |Allow |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, ICMPv6, and GRE protocols. |TCP |
   |Source/destination address |* Source Address: This parameter only applies to inbound rules. It specifies the IP addresses allowed to access the cloud resources.<br><br>* Destination Address: This parameter only applies to outbound rules. It specifies the IP addresses that cloud resources within the subnet are allowed to access. |10.0.1.0/24 |
   |Destination port |* Inbound Rule: Define the ports that are allowed to access cloud resources within the subnet.<br><br>* Outbound Rule: Define the ports that cloud resources within the subnet can use to access external resources. |80\-81 |

* **Default rule**

   |Inbound/outbound |Priority |Policy |Agreement |Source/destination address |Destination port |Description |
   |---|---|---|---|---|---|---|
   |Inbound |1 |Allow |ALL |Source address: 0.0.0.0/0 |ALL |Allow all IPv4 traffic |
   |Inbound |2 |Allow |ALL |Source address: ::/0 |ALL |Allow all IPv6 traffic |
   |Inbound |\* |Deny |ALL |Source address: 0.0.0.0/0 |ALL |A rule to deny all IPv4 traffic exists with the lowest priority and cannot be deleted. |
   |Inbound |\* |Deny |ALL |Source address: ::/0 |ALL |A rule to deny all IPv6 traffic exists with the lowest priority and cannot be deleted |
   |Outbound |1 |Allow |ALL |Destination: 0.0.0.0/0 |ALL |Allow all IPv4 traffic |
   |Outbound |2 |Allow |ALL |Destination address: ::/0 |ALL |Allow all IPv6 traffic |
   |Outbound |\* |Deny |ALL |Destination address: 0.0.0.0/0 |ALL |A rule to deny all IPv4 traffic exists with the lowest priority and cannot be deleted. |
   |Outbound |\* |Deny |ALL |Destination address: ::/0 |ALL |A rule to deny all IPv6 traffic exists with the lowest priority and cannot be deleted |

   > **tip**

   > VPC's IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.

### Matching description

Rules are matched based on priority. Network ACL rule priorities are unique. The smaller the value, the higher the priority. `*` has the lowest priority.

## Differences between Network ACLs and security groups

|Comparison item |Network ACL |Security group |
|---|---|---|
|Scope of Effect |Subnet. Once a subnet is associated with a Network ACL, all resources within that subnet are subject to the restrictions of the Network ACL rules. |Network Interface. Once a network interface is added to a security group, it becomes subject to the restrictions of that security group's rules. |
|Stateless or stateful |Stateless. Return traffic must be explicitly allowed by rules, meaning that both outbound and inbound directions must be explicitly permitted by the rules. |Stateful. Return traffic is automatically allowed and is not affected by rules. This means: When a Network Interface initiates access, only the outbound rule needs to permit the traffic; the return data is not subject to inbound rules. When a Network Interface is accessed, only the inbound rule needs to permit the traffic; the return data is not subject to outbound rules. |
|Rule priority |Rule priorities are unique, and rules take effect based on their priority level. |Rule priority is not unique. When rule priorities differ, rules take effect based on their priority level. When rules have the same priority, deny policies take precedence over allow policies. |
|Instance Association Limitations |Only one Network ACL can be associated with a subnet. |Each network interface can be associated with up to 5 security groups by default. |

## Usage limits

For the quota items adjustable in the table below, if the default quotas are insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to request an increase.

|Limit item |Maximum |Support adjustment |
|---|---|---|
|Maximum number of Network ACLs creatable per VPC |200 |No |
|Maximum network ACLs attachable per subnet |1 |No |
|Maximum rules supportable per Network ACL |* Inbound rules: 20 IPv4 rules + 20 IPv6 rules<br><br>* Outbound rules: 20 IPv4 rules + 20 IPv6 rules |Yes |

## Configuration procedures

1. [Create Network ACL](https://docs.byteplus.com/en/docs/vpc/Creating-a-network-ACL)

2. [Add network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules)

3. [Attach subnet](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-subnet-with-a-network-ACL)

## Use cases

See [Network ACL use cases](https://docs.byteplus.com/en/docs/vpc/Network-ACL-use-cases)
