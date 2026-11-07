---
title: "Security group overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Security-group-overview"
---

## Overview

Security groups use an allowlist mechanism, consist of multiple rules, and are used to control inbound and outbound traffic of network interfaces. Only traffic that matches the rules is allowed; all other traffic is blocked. **Every network interface must be added to a security group**.

For example, if an ECS instance provides external services on port 80, the security groups associated with its ENI must have an inbound rule allowing traffic on port 80 to ensure the service is accessible.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b137755dc7755fdfd23801bc5c834605.png)

Security groups are often used in conjunction with Network ACLs, which control the inbound and outbound traffic at the subnet level. [Learn more](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview)

## Category

|Category ||Operation permission |Notes |
|---|---|---|---|
|Default Security Group ||The user has all permissions except Create and Delete |The Default Security Group acts as a safety net, ensuring every ENI is associated with at least one security group. It is created with the VPC and deleted with the VPC. |
|Custom Security Group |Normal Security Group |User has full permissions |Users are responsible for their own planning and management. |
||CIDR\-Only Security Group |User has full permissions |To meet scenarios requiring a **single security group to associate with a vast number of IPs**, **CIDR\-Only Security Groups** are introduced as an extension of **Common security groups**. For a comparison, see [Common security group VS CIDR-Only security group](https://docs.byteplus.com/en/docs/vpc/Common-security-group-VS-CIDR-Only-security-group?lang=en). |
|Managed Security Group ||User has view\-only permission, modification is not allowed |They are created only alongside cloud services (e.g., NAT Gateway, VPN Gateway) and deleted only when those services are deleted. |

## Security group rule

### Precautions

* Security groups are **Stateful**. Return traffic is automatically allowed (with a connection aging time of 900 seconds for TCP and 30 seconds for ICMP). In other words, for outbound traffic initiated by the ENI, only the outbound rules need to permit it. For inbound traffic received by the ENI, only the inbound rules need to permit it.

* Security group rule changes take effect immediately. Both existing persistent connections and newly established connections are controlled by the updated rules.

* An inbound rule with itself as the source ensures communication between ENIs within the group. If deleted, private communication within the group is broken.

* It is recommended to exercise caution when allowing traffic on commonly used service ports such as SSH (22), Redis (6379), MemCached (11211), MySQL (3306), SMB (445), RDP (3389), and SQL Server (1433). [Learn more](https://docs.byteplus.com/en/docs/ecs/Common_ports_for_ECS_instances)

### Rule Composition

* **Parameter description**

   To add rules to a security group to allow traffic, the parameters for security group rules are described below:

   |Parameters |Notes |
   |---|---|
   |Inbound/outbound |Direction of traffic.<br><br><br>* Inbound: Traffic entering the network interface.<br><br>* Outbound: Traffic leaving the network interface. |
   |Priority |Priority of Security Group rules.<br><br><br>* Priority values can be identical.<br><br>* Priority range is 1\-100, where the default value 1 represents the highest precedence.​​ |
   |Policy |Policy of traffic. When priorities are equal, deny policy takes precedence over allow policy.<br><br><br>* Allow: Permits the traffic to pass.<br><br>* Deny: Rejects the traffic to pass. Use Case: This is applicable for scenarios where you need to permit traffic from a large CIDR block but explicitly deny traffic from specific IP addresses within that block. |
   |Protocol type |Supports ALL, TCP, UDP, ICMP, ICMPV6,GRE. |
   |Port range |Define the **Destination port** range according to different protocol types. |
   |Source/destination address |* Source address: Configurable for inbound rules only.<br><br>* Destination address: Configurable for outbound rules only. |

* **Matching description**

   After an ENI is associated with one or more security groups, when traffic passes through, the rule matching process is as follows (using inbound traffic as an example; the logic is similar for outbound traffic):

   1. **Priority sorting**: All inbound rules from all associated security groups are aggregated and sorted by priority from highest to lowest.

      > **tip**

      * > A lower priority value indicates a higher precedence.

      * > For rules with equal priority​​, deny policies take precedence over allow policies.

      * > If no rules are configured in any associated security group, all inbound and outbound traffic for the network interface is denied by default.

   2. **Matching**: Traffic matches rules sequentially from top to bottom​​. If matched: ​​Allow/Deny​​ based on the rule's policy, ​​matching​​ terminates. If no match: ​​Implicitly deny​​ the traffic.

## Usage limits

For the quota items adjustable in the table below, if the default quotas are insufficient, you can go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to request an increase.

|Limit item |Maximum |Adjustable |
|---|---|---|
|Maximum private IP addresses (IPv4/IPv6) associable with a single security group |6000<br><br>> CIDR\-Only security groups do not have this restriction. |No |
|Maximum number of Security Groups attachable per Network Interface |5 |No |
|Maximum rules addable per security group |* Inbound rules: 200 IPv4 rules + 200 IPv6 rules<br><br>* Outbound rules: 200 IPv4 rules + 200 IPv6 rules |Yes |
|Maximum number of Security Group IDs referenceable by a single security group |10 |No |
|Maximum number of security groups creatable per account per region (including default security groups) |300 |Yes |
|Maximum custom tags addable to a single security group |50 |No |

## Configuration procedures

1. [Create Security Group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group)

2. [Associated Network Interface](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-a-network-interface#.5YWz6IGU572R5Y2h)

3. [Add Security Group Rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules)

## Best Practices

* For security group planning, see [How to plan security groups](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups).

* For application examples, see [Security group use cases](https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases).

* After allowing an IP address and port in the security group rules, please verify that the ECS instance's firewall also allows traffic. If the firewall is not configured to permit it, the traffic will still be blocked.
