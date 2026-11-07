---
title: "What's New"
product: "Virtual Private Cloud"
product_code: "vpc"
section: "Document"
source: "https://docs.byteplus.com/en/docs/vpc/Whats-New"
---

This topic tracks the feature release updates for Virtual Private Cloud (VPC). New features will be rolled out across regions gradually. We welcome you to try them out.

> **tip**

* > Products or features in beta stage are not yet available to all users. To help users understand the product, documentation for some beta products/features is open to all users, while documentation for others is visible only to users who have the corresponding product capability enabled. To request access to a beta product or feature, please contact your account manager to apply.

* > Available regions may vary by product or feature. Please refer to the actual regions displayed in the console for confirmation.

* > To view past release records, see the [Historical What's New](https://docs.byteplus.com/en/docs/vpc/Historical-Whats-New).

## July 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Security group |Supports batch export of security group rules for multiple security groups. |GA |[Batch import/export security group rules](https://docs.byteplus.com/en/docs/vpc/Batch-importing-or-exporting-security-group-rules) |

## May 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Traffic Mirror |Support replicating IPv6 traffic from mirrored sources in traffic mirroring. |GA |[Traffic Mirror Overview](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview) |
|2 |Route Table |Support routing IPv6 traffic to Gateway Load Balancer endpoints. |Invite\-only Beta |[Managing a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry) |
|3 |Security group |Support batch deletion of security groups. |GA |[Deleting a security group](https://docs.byteplus.com/en/docs/vpc/Deleting-a-security-group) |

## March 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Add IP prefix delegation to network interfaces |To simplify multi\-IP allocation and improve expansion efficiency, you can configure IP prefix delegation for the network interface to reserve a dedicated subnet in advance for that interface. |Invite\-only Beta |[Add/Remove IP prefix delegation](https://docs.byteplus.com/en/docs/vpc/Adding_or_removing_an_IP_prefix_delegation) |
|2 |Prefix list |Allow route entries and routing policies of a transit router to be configured using prefix lists. |Invite\-only Beta |[Prefix list overview](https://docs.byteplus.com/en/docs/vpc/Prefix-list-overview) |

## February 2026

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |VPC CIDR block |Support secondary CIDR blocks for a VPC that belong to a different major segment from the primary CIDR block. |Invite\-only Beta |[Add/Delete secondary CIDR block](https://docs.byteplus.com/en/docs/vpc/Managing-secondary-CIDR-blocks) |

## November 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |VPC CIDR |The optional IPv4 CIDR mask range for VPCs has been extended to /28 (previously the maximum was /24). |GA |[What is Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) |
|2 |IPv4 gateway |IPv4 Gateway manages the inbound and outbound IPv4 internet traffic of a private network, enabling centralized control and fine\-grained management of such traffic. |Invite\-only Beta |[IPv4 Gateway Overview](https://docs.byteplus.com/en/docs/vpc/IPv4-Gateway-Overview) |
|3 |Gateway route table |The gateway route table associates with an IPv4 gateway to forward inbound IPv4 internet traffic to a firewall or gateway node for security protection. ||[Route table overview](https://docs.byteplus.com/en/docs/vpc/Route-table-overview) |

## October 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Security group |Security groups support the GRE protocol. |GA |[Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) |
|2 |Security group |CIDR\-Only security groups now support referencing prefix lists. ||[Add Security Group Rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules) |

## August 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Flow Log |Flow Logs now support automatic index creation. |GA |[Create Flow Log](https://docs.byteplus.com/en/docs/vpc/Creating-a-flow-log) |
|2 |Shared VPC |The Shared VPC feature is officially GA. ||[Shared VPC Overview](https://docs.byteplus.com/en/docs/vpc/Shared-VPC-Overview) |

## June 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |CIDR\-Only Security Group |CIDR\-Only security group is now generally available (GA). |GA |[Security Group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) |
|2 |Modify the next hop of the route entry |Route entry supports modifying the Next Hop. ||[Modify route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry) |

## April 2025

|Serial number |Feature |Description |Stage |Documentation |
|---|---|---|---|---|
|1 |Traffic Mirror |Provides you with Traffic Mirror analysis examples. |GA |[Traffic Mirror analysis example](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-analysis-example) |
|2 |HAVIP |High\-Availability Virtual IP (HAVIP) is now GA. ||[High-Availability Virtual IP Address Overview](https://docs.byteplus.com/en/docs/vpc/HAVIP-overview) |
|3 |Prefix list |When adding entries to a prefix list, multiple CIDR blocks are now supported as input. ||[Add/Delete prefix list entry](https://docs.byteplus.com/en/docs/vpc/Managing-entries-in-the-prefix-list) |
