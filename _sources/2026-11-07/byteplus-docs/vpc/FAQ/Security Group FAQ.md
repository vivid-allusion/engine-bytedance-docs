---
title: "Security Group FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Security-group-FAQ"
---

|Issue category |Issue |
|---|---|
|Billing |[Is there a charge for the Security Group service?](https://docs.byteplus.com/en/docs/47/4634#.5a6J5YWo57uE5pyN5Yqh5aaC5L2V6K6h6LS577yf) |
|Limits |[How many Security Groups can an account own? How many Security Group rules are allowed? How many security groups can an ECS be associated with?​​](https://docs.byteplus.com/en/docs/47/4634#.5LiA5Liq6LSm5Y-36IO95oul5pyJ5aSa5bCR5Liq5a6J5YWo57uE77yf5aSa5bCR5p2h5a6J5YWo57uE6KeE5YiZ77yf5LqR5pyN5Yqh5Zmo5Y-v5Lul6YCJ5oup5YWz6IGU5aSa5bCR5Liq5a6J5YWo57uE77yf) |
|Feature |* [How is the priority of security group rules defined?](https://docs.byteplus.com/en/docs/47/4634#.5a6J5YWo57uE6KeE5YiZ55qE5LyY5YWI57qn5piv5aaC5L2V5a6a5LmJ55qE77yf)<br><br>* [When a network interface is associated with multiple security groups, how is traffic matched?](https://docs.byteplus.com/en/docs/47/4634#.5b2T572R5Y2h5YWz6IGU5aSa5Liq5a6J5YWo57uE5pe277yM5YW25rWB6YeP5aaC5L2V5Yy56YWN77yf)<br><br>* [How to troubleshoot inaccessible public cloud ports?](https://docs.byteplus.com/en/docs/47/4634#.5peg5rOV6K6_6Zeu5YWs5pyJ5LqR5p-Q5Lqb56uv5Y-j5pe25oCO5LmI5Yqe77yf)<br><br>* [How to allow or deny specific IPs and ports in a security group?​​](https://docs.byteplus.com/en/docs/47/4634#.5a6J5YWo57uE5aaC5L2V5pS-6YCa5oiW5ouS57ud5oyH5a6a55qESVDlj4rnq6_lj6PvvJ8=)<br><br>* [Why do batch security group rule imports fail?](https://docs.byteplus.com/en/docs/47/4634#.5om56YeP5a-85YWl5a6J5YWo57uE6KeE5YiZ5aSx6LSl5piv5LuA5LmI5Y6f5Zug77yf)<br><br>* [Do changes to security group rules take effect immediately?](https://docs.byteplus.com/en/docs/47/4634#.5Y-Y5pu05a6J5YWo57uE6KeE5YiZ5piv5ZCm5a-55Y6f5pyJ5rWB6YeP5a6e5pe255Sf5pWI77yf) |
|Comparison |* [Can security groups and iptables be used simultaneously?](https://docs.byteplus.com/en/docs/47/4634#.5L2_55So5LqG5a6J5YWo57uE5piv5ZCm5oSP5ZGz552A5LiN5Y-v5Lul5L2_55SoaXB0YWJsZXPvvJ8=)<br><br>* [Which has higher priority between security groups and network ACLs?](https://docs.byteplus.com/en/docs/47/4634#.5a6J5YWo57uE5ZKM572R57ucQUNM5ZOq5Liq5LyY5YWI57qn5pu06auY77yf) |
|Others |* [Why are security group rules configured for ECS's network interface not taking effect?​​](https://docs.byteplus.com/en/docs/47/4634#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo572R5Y2h6YWN572u55qE5a6J5YWo57uE6KeE5YiZ5pyq55Sf5pWI77yf)<br><br>* [Why can't a security group be deleted even after all ECSs are removed?​​](https://docs.byteplus.com/en/docs/47/4634#.5LqR5pyN5Yqh5Zmo5bey57uP5YWo6YOo56e75Ye677yM5Li65LuA5LmI5a6J5YWo57uE5peg5rOV5Yig6Zmk77yf)<br><br>* [Why did ECS previously receive TCP data from a peer resource but now cannot?​​](https://docs.byteplus.com/en/docs/47/4634#.5Li65LuA5LmI5LqR5pyN5Yqh5Zmo5LmL5YmN5Y-v5Lul5o6l5pS25a-556uv6LWE5rqQ55qEVENQ5pWw5o2u77yM546w5Zyo5Y205peg5rOV5o6l5pS25LqG77yf)<br><br>* [After an ECS is added to a security group, can the security group be changed?](https://docs.byteplus.com/en/docs/47/4634#.5LqR5pyN5Yqh5Zmo5Yqg5YWl5a6J5YWo57uE5ZCO77yM5Y-v5Lul5Y-Y5pu05a6J5YWo57uE5ZCX77yf) |

## Is there a charge for the Security Group service?

Currently, no charges apply for using Security Groups.

## How many Security Groups can an account own? How many Security Group rules are allowed? How many security groups can an ECS be associated with?

* By default, 300 per account per region. This can be increased to 10,000 via the Quota Center.

* Default rule capacity per security group:

   * Inbound: 200 IPv4 rules, 200 IPv6 rules;

   * Outbound: 200 IPv4 rules, 200 IPv6 rules;

   * If the default quota does not meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to apply for a quota increase.

* Each network interface of an ECS can be associated with up to 5 security groups.

## How is the priority of security group rules defined?

The priority value range for security group rules is currently 1 to 100, where a lower number indicates higher priority.

When adding security group rules, the default priority is 1 (highest priority). If rules share the same priority level, "Deny" policies take precedence over "Allow" policies.

## When a network interface is associated with multiple security groups, how is traffic matched?

Security groups consist of a set of rules, where the group itself has no priority, but each rule has a priority.

The matching process is as follows (using inbound traffic as an example; outbound follows the same logic):​​

1. Aggregate all inbound rules​​ from all associated security groups. Sort rules by priority​​ in descending order.

   > **tip**

   * > A lower priority value indicates a higher precedence.

   * > For rules with equal priority​​, deny policies take precedence over allow policies.

2. Traffic matches rules sequentially from top to bottom​​. If matched: ​​Allow/Deny​​ based on the rule's policy, ​​matching​​ terminates. If no match: ​​Implicitly deny​​ the traffic.

## How to troubleshoot inaccessible public cloud ports?

**Symptom:**  Specific ports on your public cloud instance are inaccessible from certain regions or carriers, while other ports function normally.

**Analysis:**  Some carriers flag ports in the following table as high\-risk ports and block them by default:

|Agreement |Port |
|---|---|
|TCP |42 135 137 138 139 444 445 593 1025 1068 1434 3127 3128 3129 3130 4444 4789 5554 5800 5900 9996 |
|UDP |135~139 1026 1027 1028 1068 1433 1434 4789 5554 9996 |

**Solution:**  Change sensitive ports to non\-high\-risk alternatives for your services.

## Do changes to security group rules take effect immediately?

Yes. Security group rule modifications are applied instantly.

## Can security groups and iptables be used simultaneously?

No. Your traffic undergoes dual\-layer filtering with the following traversal paths:

* Outbound: Instance process \> iptables \> Security Group.

* Inbound: Security Group \> iptables \> Instance process.

## Which has higher priority between security groups and network ACLs?

Security Groups and Network ACLs operate at different security layers and cannot be directly compared in terms of priority.

Security Groups operate at the ECS instance's network interface level, while Network ACLs function at the subnet level. Before inbound traffic reaches an ECS instance, it must first pass through the Network ACL rules associated with the instance's subnet, followed by Security Group rules. If the Network ACL inbound rules deny traffic from a specific CIDR block, that traffic will be blocked—even if Security Group inbound rules explicitly allow it. Consequently, no traffic from that CIDR block will reach the ECS instance.

For more information about the differences between security groups and network ACLs, see [Network ACL and Security Group differences](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview#.572R57ucQUNM5LiO5a6J5YWo57uE5beu5byC).

## How to allow or deny specific IPs and ports in a security group?​​

You can [add a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) based on the following example.

* **Allow specified IP**

   Example: Allow ECSs within the security group to access 10.10.10.10 via port 80.​​

   |Direction |Priority |Strategy |Protocol type |Port range |Source |
   |---|---|---|---|---|---|
   |Outbound |1 |Allow |TCP |80 |10.10.10.10/32 |

* **Deny specified IP**

   For example: Deny access from 10.10.10.10 to port 80 on ECSs within the security group.​​

   |Direction |Priority |Strategy |Protocol type |Port range |Source |
   |---|---|---|---|---|---|
   |Inbound |1 |Deny |TCP |80 |10.10.10.10/32 |

## Why do batch security group rule imports fail?​​

The import file may have the following issues:

* Incorrect parameter format. For parameter format details, see [Download and complete the template](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules#.5LiL6L295bm25aGr5YaZ5qih5p2_).

* Duplicate security groups. Rules in the file either duplicate existing rules or contain internal repetitions.

* Incorrect file format. Only .csv, .xls, and .xlsx files are supported.

* Incompatible encoding format. If garbled characters appear, modify the encoding format and retry.

## Why are security group rules configured for ECS's network interface not taking effect?​​

Check the security group configuration for errors in the following areas:

* Incorrect rule direction​​: For example, inbound rules mistakenly applied to outbound rules.

* Verify if the selected protocol matches the service.

* Verify if high\-risk port usage exists. Some carriers block high\-risk ports. Switch to non\-restricted ports.

* The allowed port isn't enabled on the ECS.

* When an ECS instance is bound to multiple security groups with conflicting rules. For example, if Security Group 1 allows access to a specific port, but Security Group 2 has a higher\-priority rule denying access to that port—the port will become inaccessible.

* If ECS has other access controls configured (e.g., host\-based firewalls), these may block access to the port.

## Why did ECS previously receive TCP data from a peer resource but now cannot?​​

First, verify the status of the peer resource and related components. If no anomalies exist, confirm whether the TCP connection timed out and disconnected.

Security groups are ​​stateful​​. Return traffic from the peer resource is automatically allowed within the TCP connection aging period (900 seconds on BytePlus). However, if the security group’s inbound rules do not explicitly allow traffic from the peer, the TCP connection is initially permitted but will be blocked after the 900\-second timeout when the connection drops.

For example​​: Two BytePlus ECSs establish a TCP connection, each with primary Network Interfaces in different security groups. To ensure uninterrupted data flow beyond the TCP aging limit, use one of these solutions:

* Solution 1: If both ECSs reside in the same VPC, place their primary Network Interfaces in the same security group with intra\-group communication rules enabled.

* Solution 2: Configure outbound and inbound rules in both security groups to explicitly allow mutual access.

* Solution 3: Enable TCP keepalive on the local ECS to maintain connection activity

## After an ECS is added to a security group, can the security group be changed?

Yes. Changing the security group for an ECS essentially means replacing the security group associated with the network interface bound to the ECS. You may refer to the process for [updating network interface's security group](https://docs.byteplus.com/en/docs/vpc/Updating-the-security-group-of-a-network-interface) to complete this operation.

## Why can't a security group be deleted even after all ECSs are removed?​​

* When creating a VPC, the BytePlus platform automatically generates a ​​default security group​​, which ​​cannot be deleted​​.

* Security groups support associations with resources like ECSs, Classic Load Balancers (CLB), and secondary network interfaces. Before deletion, ensure the target security group has been ​​disassociated from all instances. If any instances remain associated, remove them first before deleting the security group.
