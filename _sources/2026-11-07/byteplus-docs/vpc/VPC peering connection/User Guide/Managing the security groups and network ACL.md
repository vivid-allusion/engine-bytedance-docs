---
title: "Managing the security groups and network ACL"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-routes-security-groups-and-network-ACLs"
---

To enable resource communication between the requester VPC and the acceptor VPC, both the security groups and network ACLs of the two VPCs must allow the communication traffic required for mutual access.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07e93692c58acc563396134b706cd757.png) </span>

<span id="UHXlDMc2"></span>
### Security group

The network ACL associated with the subnet to which the resource belongs must be configured as follows to allow traffic.


|Rule direction |Priority |Policy |Protocol type |Destination port |Source/destination address |Description |
|---|---|---|---|---|---|---|
|Inbound |Set priority (e.g. 100) |Allow |ALL |ALL |Source address: CIDR block of the peer VPC (if only specific subnets need to communicate, enter the subnet CIDR block) |Allow inbound traffic from the peer VPC to the local VPC |
|Outbound |Set priority (e.g. 100) |Allow |ALL |ALL |Destination address: CIDR block of the peer VPC (if only specific subnets need to communicate, enter the subnet CIDR block) |Allow traffic destined for the peer VPC to leave the local VPC |


For actions, see [Adding a security group rule](https://docs.byteplus.com/en/docs/vpc/Managing-security-group-rules).

<span id="9KFIRyGt"></span>
### Network ACL

The network ACL associated with the resource's subnet must be configured as follows to allow traffic:


|Direction |Priority |Policy |Protocol type |Destination port |Source/destination address |Description |
|---|---|---|---|---|---|---|
|Inbound |Set priority (e.g. 1) |Allow |ALL |ALL |Source address: CIDR block of the peer VPC (if only specific subnets need to communicate, enter the subnet CIDR block) |Allow inbound traffic from the peer VPC to the local VPC |
|Outbound |Set priority (e.g. 1) |Allow |ALL |ALL |Destination address: CIDR block of the peer VPC (if only specific subnets need to communicate, enter the subnet CIDR block) |Allow traffic destined for the peer VPC to leave the local VPC |


For actions, see [Adding a Network ACL rule](https://docs.byteplus.com/en/docs/vpc/Managing-network-ACL-rules).
