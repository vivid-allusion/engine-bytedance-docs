---
title: "NLB Instance Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Instance-Overview"
---

<span id=".566A5LuL"></span>
## Overview

NLB instances serve as the implementation vehicle for Network Load Balancer service. They receive client access requests and forward them to backend servers according to listener rules and the scheduling algorithm.

Before using the NLB service, users need to first create an NLB instance and then configure corresponding listeners and server groups.

<span id=".5a6e5L6L6K6_6Zeu5o6n5Yi2"></span>
## Security groups and Network Access Control List (ACL)

Traffic routing to the NLB instance is controlled by security groups and Network Access Control Lists (NACLs), as specified below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4de9fbd65629587c169337ea35a45ac2.png) </span>

<span id=".5a6J5YWo57uE"></span>
### Security group 

Security groups attached to an NLB instance are divided into entrusted security groups and non\-entrusted security groups. You can view all security groups attached to the NLB instance in the security group tab on the instance details page. [Learn more](https://docs.byteplus.com/en/docs/vpc/Security-group-overview)


* **Entrusted security group**: When creating an NLB instance, the system automatically creates and attaches it to the NLB instance. Its lifecycle remains consistent with the NLB instance. Modifications, deletions, and detachments are not supported. The entrusted security group is deleted when the NLB instance is deleted.

* **Non\-entrusted security group**: Security groups manually attached to the NLB instance by users, including the default and custom security groups. For unmanaged security groups associated with the NLB instance, both outbound and inbound rules must allow traffic to/from NLB. For detailed configuration steps, please refer to [Configuring Instance Security Groups](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB).


<span id=".572R57ucQUNM"></span>
### Network ACL

When the subnet containing the NLB instance associated with a [Network Access Control List (ACL)](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview), the traffic passing through the NLB instance is also subject to the Network ACL rules. You must configure both outbound and inbound rules in this Network ACL to allow traffic to/from the NLB instance. For detailed configuration steps, please refer to [Configuring Instance Network ACLs](https://docs.byteplus.com/en/docs/clb/Configuring-security-group-and-Network-ACL-for-NLB).

<span id=".6Leo5Y-v55So5Yy66L2s5Y-R"></span>
## Forwarding across all zones

NLB instances have forwarding across all zones enabled by default. After the instance is created, users can disable forwarding across all zones as needed.


* When the instance enables forwarding across all zones, the NLB forwards the client access traffic to all backend servers based on the scheduling algorithm. For example, the NLB in AZ A can forward access traffic to backend servers in both AZ A and AZ B.

* When forwarding across all zones is disabled, the NLB forwards the client access traffic only to backend servers in the same Availability Zone based on the scheduling algorithm. For example, the NLB in Availability Zone A can only forward access traffic to backend servers in Availability Zone A.


Taking the weighted round\-robin algorithm as an example, let us introduce the all zones forwarding feature of NLB. As shown in the figure below, the NLB instance supports both Availability Zone A and Availability Zone B simultaneously, with 2 backend servers in Availability Zone A and 3 backend servers in Availability Zone B, all with equal weights.

Client access traffic is distributed across 2 Availability Zones using a weighted round\-robin algorithm. Within each Availability Zone, the NLB uses the weighted round\-robin algorithm. Subsequently, the traffic is then routed to backend servers for processing based on across all zones configuration.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a191bf61acc49dd16c80affcb42652d7.png) </span>

&nbsp;
