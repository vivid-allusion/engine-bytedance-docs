---
title: "What is Peering Connection"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/What-is-a-VPC-peering-connection"
---

## Overview

Peering Connection is a simple, low\-cost solution provided by BytePlus for interconnecting Virtual Private Clouds (VPCs) in the cloud. By establishing a direct network connection between two VPCs and performing simple route configuration, you can achieve private network access between VPCs, thereby meeting intra\-enterprise or cross\-enterprise interconnection requirements.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_412fb8924549c33e787608fbc0dc0511.png)

## Application scenarios

* Private network interconnection between two VPCs under the same account and in the same region. For example, a production VPC and a test VPC are isolated independently, but they can communicate via a peering connection for private network access. The test environment can interface with some production APIs and synchronize configuration data, achieving both security isolation and intranet communication.

* Private network interconnection among multiple VPCs under different accounts but in the same region. For example, different subsidiaries or business entities within a group each have their own independent cloud accounts and have built their own VPCs in the same region. Through cross\-account private network interconnection, business systems and internal platforms between subsidiaries can communicate over the intranet without going over the internet.

## Billing description

Peering connection is currently free of charge.

## Limits

* The CIDR blocks of the two VPCs to be interconnected must not overlap.

* Quotas are as follows:

   |Quota item |Quota notes |Default |Adjustable |Adjustable quota limit |
   |---|---|---|---|---|
   |vpc/peering/intra_region |Number of same\-region peering connections that can be created per VPC |10 |Yes |200 |
   |vpc/peering/cross_region |Number of cross\-region peering connections that can be created per VPC<br><br> |20 |Yes |200 |
   |peering/cross_border_bandwidth |Maximum cross\-border bandwidth supported by a single peering connection<br><br> |1G<br><br> |Yes<br><br> |100G |
   |peering/cross_region_bandwidth |Maximum non\-cross\-border cross\-region bandwidth supported by a single peering connection |1G |Yes<br><br> |100G |

## Peering Connection vs CEN

|Comparison item |Peering Connection |Cloud Enterprise Network (CEN) |
|---|---|---|
|Interconnection |Multiple VPCs can be freely combined for interconnection or isolation |Full mesh interconnection |
|Route configuration |Requires manual configuration of each route |Routes are automatically generated, no need to manually configure each route |
|Hybrid cloud support |Only interconnects VPCs; does not support connections to on\-premises data centers |Supports access to on\-premises IDCs via Direct Connect and VPN, perfectly suited for hybrid cloud |
|Advanced features |Does not support advanced features such as route summary and cloud service access |Supports advanced capabilities such as route summary and cloud service access |
|Application scenarios |Small\-scale simple networking with 2\-3 VPCs |Multi\-VPC clusters, hybrid cloud, complex large\-scale networking |
