---
title: "Flow log overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Flow-log-overview"
---

## Overview

After the flow log aggregates and processes the log data of outbound and inbound traffic for network interfaces as needed, it delivers the data to the TLS for storage and search analysis. You can analyze flow logs to monitor network traffic, troubleshoot network issues, and optimize network architecture.

## Application scenarios

When you need to monitor network traffic or troubleshoot network problems, you can review the traffic data recorded in the flow logs. Below is a brief introduction to common application scenarios. For details, see [Usage example](https://docs.byteplus.com/en/docs/vpc/Use-cases).

|Category |Scenarios |Related product documentation |
|---|---|---|
|On\-Cloud Public Network |View traffic between ECS instances and the Internet via EIP addresses |[EIP](https://docs.byteplus.com/en/docs/eip/What-is-EIP) |
||View ECS instances with high traffic through the Internet NAT Gateway |[NAT](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway) |
||View traffic accessing ECSs through a CLB via the Internet |[Classic Load Balancer](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) |
||View traffic accessing ECSs through a NLB via the Internet |[Network Load Balancer](https://docs.byteplus.com/en/docs/clb/What-is-Network-Load-Balancer) |
|On\-Cloud Private Network |View traffic between ECSs within the same VPC |\- |
||View traffic between different VPCs |[CEN](https://docs.byteplus.com/en/docs/cen/Product-Overview-01), [Transit Router](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-01), [VPN](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network) |
||View traffic through PrivateLink connection endpoints |[PL](https://docs.byteplus.com/en/docs/privatelink/Product-Overview-01) |
|Hybrid cloud |View traffic between the on\-cloud VPC and on\-premises IDC |[Direct Connect](https://docs.byteplus.com/en/docs/directconnect/What-is-Direct-Connect), [VPN](https://docs.byteplus.com/en/docs/vpn/What-is-Virtual-Private-Network) |
|Rejected traffic |View traffic rejected by security groups and network ACLs |[Security Group](https://docs.byteplus.com/en/docs/vpc/Security-group-overview), [Network ACL](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) |

## Terms

|Term |Notes |
|---|---|
|Torch Log Service |The Torch Log Service (TLS) collects and stores log data, and provides search and analysis, monitoring and alerting, and visualization. The VPC service integrates with the TLS via SDK to deliver the traffic data of network interfaces within the VPC to the TLS. The TLS then stores, retrieves, and analyzes this traffic data. |
|Log project |The fundamental resource management unit in the Torch Log Service (TLS), used for log resource isolation and Identity and Access Management (IAM). |
|Log Topic |The basic unit for log management (such as log collection, storage, query, and analysis) in TLS. |
|[Sampling interval](https://docs.byteplus.com/en/docs/vpc/Creating-a-flow-log) |The time interval at which the VPC delivers flow log data to the TLS. For connections with continuous data packets, this also represents the maximum aggregation time for traffic data to be aggregated into a single log entry. |
|[Flow log fields](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview#.5rWB5pel5b-X5a2X5q61) |Fields that record network interface traffic data. The Virtual Private Cloud (VPC) delivers flow log data to the TLS in the format of flow log fields. The TLS then stores, retrieves, and analyzes network interface traffic data according to the flow log field format. |

## Flow log fields

**The fields recorded in flow logs stored in the Torch Log Service (TLS) are as follows:**

`<version> <account-id> <networkinterface-id> <srcaddr> <dstaddr> <srcport> <dstport> <protocol> <packets> <bytes> <start> <end> <action> <log-status>`

> **tip**

> Flow log keeps iterating, higher versions are backward compatible with all fields from lower versions and add new fields on top of them.

|Field |Field type |Notes |Example |
|---|---|---|---|
|version |long |Version of the VPC flow log. Supports 1, 2, 3, and 4. Higher version numbers support fields that are added on top of those in earlier versions. |1 |
|account\-id |text |The ID of the main account. |210011\*\*\*\* |
|networkinterface\-id |text |Network Interface ID. |eni\-bp1fgnh68xyz9\*\*\*\* |
|srcaddr |text |Source IP address. |192.168.XX.12 |
|dstaddr |text |Destination IP address. |221.100.XX.55 |
|srcport |text |Source port. |33 |
|dstport |text |Destination port. |55 |
|protocol |text |IANA protocol number. For example, TCP protocol number is 6, and UDP protocol number is 17. For more information, see [IANA protocol number](http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml). |6 |
|packets |long |Total number of packets transmitted within the collection window. |100 |
|bytes |long |Total number of bytes transmitted within the collection window. |105 |
|start |long |The start time of the traffic data sampling window, expressed in Unix timestamp format.<br><br>> **tip**<br><br><br>> Unix Time: The total number of seconds elapsed since January 1, 1970, 00:00:00 Coordinated Universal Time (UTC). For example, August 1, 2023, 00:00:00 converts to a Unix time of 1690819200.<br> |1690819200 |
|end |long |The end time of the traffic data sampling window, expressed in Unix timestamp format. |1690819800 |
|action |text |Traffic policy.<br><br><br>* ACCEPT: The traffic has been accepted. In other words, traffic is allowed by a security group or a Network ACL and recorded.<br><br>* REJECT: The traffic has been rejected. In other words, traffic is denied by a security group or a Network ACL and not recorded. |ACCEPT |
|log\-status |text |Flow Log recording status.<br><br><br>* OK: Normal, successfully recorded in flow logs.<br><br>* NODATA: Indicates no incoming or outgoing network traffic within the collection window; in this case, the **packets** and **bytes** fields are both \-1.<br><br>* SKIPDATA: Indicates that some flow log records were skipped during the collection window. This may be caused by internal capacity constraints or internal errors. |OK |
|direction |text |Direction of traffic.<br><br><br>* in: Direction of traffic entering the network interface.<br><br>*  out: Direction of traffic leaving the network interface. |in |

## Limits

* A single account in a single region can create up to 10 flow logs.

* Only one flow log can be created for the same resource. This means that only one flow log can be created for a single network interface, subnet, or Virtual Private Cloud (VPC).

   > **tip**

   > If a flow log is created for a network interface, another for the subnet it resides in, and yet another for the VPC it belongs to, the traffic data of that network interface will be recorded by all three flow logs.

* Traffic from the primary or secondary network interfaces of instance types such as d1s, g1, c1, r1, and i1 is not supported for collection.

* The following types of traffic cannot be recorded by flow logs:

   * Traffic between a network interface and public DNS servers (if a custom DNS server is used, the traffic will be recorded).

   * DHCP traffic.

   * Traffic from Windows instances for activating the Windows operating system.

   * NTP traffic.

   * Traffic related to instance metadata.

   * Traffic generated by Traffic Mirror.

> **tip**

> Flow logs do not consume your network bandwidth. Please proceed with confidence.

## Configuration and Usage Process

1. [Create Flow Log](https://docs.byteplus.com/en/docs/vpc/Creating-a-flow-log)

2. [Analyze Flow Log](https://docs.byteplus.com/en/docs/vpc/Analyzing-a-flow-log)
