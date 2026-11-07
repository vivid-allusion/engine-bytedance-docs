---
title: "Traffic Mirror Overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview"
---

## Introduction​

Through traffic mirroring, you can replicate the traffic of a network interface based on custom Mirror Filters and privately forward the replicated traffic to a target service for monitoring and analysis.

> **tip**

> Replicated traffic consumes the network bandwidth of the Elastic Compute Service (ECS) instance where the network interface resides. Sufficient network bandwidth is required to ensure that traffic mirrors do not impact business traffic. Proceed with caution.

## Application scenarios

* **Security audit**

   Replicate business traffic and forward it to an auditing platform for security auditing, providing clues and evidence for cybersecurity incidents, and enabling timely detection of potential cybersecurity threats.

* **Intrusion detection**

   When network intrusions maliciously exploit computing and network resources, traffic monitoring software can analyze the traffic replicated by traffic mirror to promptly address security vulnerabilities.

* **Troubleshooting**

   During abnormal network traffic conditions, the traffic replicated by traffic mirrors can be analyzed to more efficiently pinpoint ECSs causing network anomalies.

## Compositions

### Mirror site

The mirror site refers to the network interface whose traffic needs to be replicated.

### Mirror Filter

Mirror Filters are composed of filtering rules. The parameters of the filtering rules are described as follows:

|Parameter |Description |Example |
|---|---|---|
|Direction |Select to replicate either the outbound or inbound traffic of the Network Interface. |Inbound |
|Priority |The priority of Mirror Filters ranges from 1 to 1000. A smaller value indicates higher priority. The value 1 indicates the highest priority. For the same Mirror Filter and the same direction (inbound/outbound), the priority must be unique. |1 |
|Strategy |Set to allow or deny. Allow means traffic will be replicated, while Reject means it will not be replicated. |Allow |
|Agreement |Select the traffic protocol. Supported protocols include ALL, TCP, UDP, and ICMP. |TCP |
|Source address and port |Set the source address and port for the network interface traffic. |192.168.0.0/12 80 |
|Destination address and port |Set the destination port of the Network Interface traffic. |192.168.0.66/32 80 |

Example of an inbound rule: Traffic from resources within the 192.168.0.0/12 range accessing port 80 of 192.168.0.66 via the TCP protocol (excluding return traffic) will be replicated and forwarded to the Mirror Target.

### Mirror Target

The Traffic Mirror Target is a Network Interface or Classic Load Balancer (CLB) that collects traffic.

The traffic mirror data packets received by the Mirror Target are encapsulated using the VXLAN protocol, as shown in the figure below.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5513e7e622b3bedec8377263a2c7bf6f.png)

Key parameters in the VXLAN encapsulation are as follows:

* IP\-UDP:

   * Source IP: The primary IP address of the mirror site.

   * Destination IP: The primary IP address of the Mirror Target.

   * Source port: The system settings have no special meaning.

   * Destination port: The fixed port 4789 used by the VXLAN protocol.

* VNI in the VXLAN header: The ID of the Mirror Session, specified by the user when creating the mirror session. If not specified, it is randomly assigned. For details, see [Create Traffic Mirror Session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session).

For more information about the VXLAN protocol, see [RFC 7348](https://tools.ietf.org/html/rfc7348).

### Traffic Mirror Session

The mirror session associates the mirror site, mirror target, and Mirror Filters, enabling the privately forwarded replication of traffic from the mirror site to the mirror target. It serves as the carrier for traffic mirrors.

#### Traffic path

The traffic path is shown in the following diagram:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a5466ad0822a161bb5539fa3c2263c57.png)

After filtering the business traffic data of the site network interface, traffic meeting the Mirror Filters is replicated, encapsulated using VXLAN, and privately forwarded to the mirror target network interface. Through the traffic monitoring software deployed on the ECS at the mirror target, the VXLAN\-encapsulated data packets are decapsulated to obtain the original traffic data, which is then monitored and analyzed.

> **tip**

> The traffic monitoring software deployed on the ECS must support decapsulation of VXLAN\-encapsulated data packets.

#### Rule matching explanation

When the mirror site has multiple mirror sessions and multiple filter rules, the matching process for inbound traffic (similarly for outbound traffic) follows these steps:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2a39fbc85fb930dcabb7babdb91c18c9.png)

1. All mirror sessions are sorted from highest to lowest priority.

2. Inbound filter rules within a mirror session are sorted from highest to lowest priority.

3. Network Interface's traffic is matched against rules sequentially based on policy, protocol, source address and port, and destination address and port. If traffic matches a rule, it is either replicated or not replicated based on the rule, and the matching process ends. If traffic does not match any filter rule, it is not replicated.

## Limits

**Feature limitations**

### Mirror site

* The mirror site must be the primary network interface of an ECS or a secondary network interface attached to an ECS.

* IPv4 and IPv6 traffic from the mirror site can be replicated.

* The security group and network ACL of the mirror site must allow outbound traffic on UDP port 4789.

* The route table entries of the mirror site must support private network access from the mirror site to the mirror target.

* The following traffic from the mirror site will not be mirrored:

   * Traffic rejected by network ACLs, security groups; Flow log traffic.

   * Traffic between the Network Interface and DNS server.

   * ARP traffic.

   * DHCP traffic.

   * NTP traffic.

   * Traffic related to instance metadata.

* Replicated traffic consumes the network bandwidth of the ECS instance where the mirror site network interface resides.

* Only the primary or secondary network interfaces of ECSs with the following specifications can serve as mirror sites:

|**Specification** |**Description** |
|---|---|
|[General](https://docs.byteplus.com/en/docs/ecs/General-purpose) |g1ie, g3il, g3al, g3i, g3a |
|[Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Computing-optimized) |c1ie, c3il, c3al, c3i, c3a |
|[Memory-optimized](https://docs.byteplus.com/en/docs/ecs/Memory-optimized) |r1ie, r3il, r3al, r3i, r3a |
|[Local SSD type](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based) |i2, i2g, i3s |
|[Big data type](https://docs.byteplus.com/en/docs/ecs/Big-data-based) |d2, d2c, d2s |
|[Burstable instance](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances) |t2 |
|[Shared](https://docs.byteplus.com/en/docs/ecs/Shared) |s2 |

### Mirror Target

* The mirror target must be a network interface within the same VPC (primary or attached secondary network interface of an ECS) or a Classic Load Balancer (CLB), and must belong to the same account as the mirror site.

* The security group and network ACL of the mirror target must allow inbound traffic on UDP port 4789.

* If the mirror target is a CLB, a UDP listener must be configured to allow traffic on port 4789.

* The ECS associated with the mirror target must have traffic monitoring software installed that supports VXLAN decapsulation to monitor and analyze the mirrored traffic.

* The mirror target cannot be the same Network Interface as the mirror site, and it cannot serve as the mirror site for another mirror session.

### Others

The traffic packets replicated from the mirror site undergo VXLAN encapsulation. To ensure these packets are not truncated, it is recommended to configure the MTU value of the Network Interface according to the following relationship:

The MTU of the mirror site ≤ the packet size set in the mirror session ≤ the MTU of the Mirror Target \- 50, and the packet size set in the mirror session must be ≤ 1450. For details, see[Modifying network interface MTU](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface).

**Quota limitations**

**Traffic Mirror Session**

|**Limits** |**Maximum** |**Adjustable** |
|---|---|---|
|Maximum number of Traffic Mirror Sessions creatable per account per region |20000 |No |
|Maximum number of mirror sites associable with a single mirror session |1 |No |
|Maximum number of mirror targets associable with a single mirror session |1 |No |
|Maximum number of filter rules associable with a single mirror session |1 |No |

**Mirror Filter**

|**Limits** |**Maximum** |**Adjustable** |
|---|---|---|
|Maximum number of filter rules creatable per account per region |10000 |No |
|Number of mirror sessions associable with a mirror filter rule |2000 |No |
|Maximum filter rules per traffic direction under a single Mirror Filter |10 |No |

**Mirror site**

|**Limits** |**Maximum** |**Adjustable** |
|---|---|---|
|Maximum number of mirror sessions associable with a single mirror site |3 |No |

**Mirror Target**

|**Limits** |**Maximum** |**Adjustable** |
|---|---|---|
|Maximum number of traffic mirror targets supported per account per region |10000 |No |
|Maximum number of mirror sessions associable with a single mirror target |10 |No |
|Maximum number of mirror sites associable with a single traffic mirror target |100 |No |

## Configuration procedures

The configuration procedure is shown in the following diagram:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aea4685b9b07017a51e897e5dff4dd57.png)

1. [Create Traffic Mirror Target](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-target)

2. [Create Traffic Mirror Filter](https://docs.byteplus.com/en/docs/vpc/Managing-traffic-mirror-filter)

3. [Create Traffic Mirror Session](https://docs.byteplus.com/en/docs/vpc/Managing-a-Traffic-Mirror-session)
