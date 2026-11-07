---
title: "API overview"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/API-overview-1"
---

This document introduces the APIs and their features involved in using a Virtual Private Cloud (VPC).

<span id=".56eB5pyJ572R57uc"></span>
## Virtual Private Cloud (VPC) 


|API |Functionality |
|---|---|
|[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) |Create a VPC. |
|[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes) |Modify the name and description of the VPC and other information. |
|[DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) |Query VPCs that meet specified criteria. |
|[DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) |View details of the specified VPC. |
|[DeleteVpc](https://docs.byteplus.com/en/docs/vpc/DeleteVpc) |Delete a specified VPC. |
|[AssociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock) |Add a secondary CIDR block to a specified VPC. |
|[DisassociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/DisassociateVpcCidrBlock) |Delete a secondary CIDR block from a specified VPC. |


<span id=".5a2Q572R"></span>
## Subnet 


|API |Functionality |
|---|---|
|[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) |Create a subnet. |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes) |Modify the name and description of the subnet. |
|[DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) |Query subnets that meet specified conditions. |
|[DescribeSubnetAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSubnetAttributes) |View specified subnet details. |
|[DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet) |Delete the specified subnet. |


<span id=".6Lev55Sx6KGo"></span>
## Route tables


|API |Functionality |
|---|---|
|[CreateRouteTable](https://docs.byteplus.com/en/docs/vpc/CreateRouteTable) |Create a route table. |
|[ModifyRouteTableAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyRouteTableAttributes) |Modify the name or description of a specified route table. |
|[DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) |Describe the route tables that meet specified conditions. |
|[AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable) |Associate a subnet with a specified custom route table. |
|[DisassociateRouteTable](https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable) |Disassociate the route table from the subnet. |
|[DeleteRouteTable](https://docs.byteplus.com/en/docs/vpc/DeleteRouteTable) |Delete a route table. |
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |Add a custom route entry to the route table. |
|[ModifyRouteEntry](https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry) |Modify the name and description of a custom route entry. |
|[DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) |Query static route entries that meet specified conditions. |
|[DeleteRouteEntry](https://docs.byteplus.com/en/docs/vpc/DeleteRouteEntry) |Delete a route entry. |


<span id=".572R5Y2h"></span>
## Network interface 


|API |Functionality |
|---|---|
|[CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface) |Create a secondary network interface. |
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes) |Modify network interface name, description, security group, source/destination address check, delete with cloud server instance, etc. |
|[DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) |Query network interfaces that meet the criteria. |
|[DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) |View the details of the specified network interface. |
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |Attach a secondary network interface to an ECS instance. |
|[DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface) |Detach a secondary network interface from an ECS instance. |
|[DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface) |Delete a specified secondary network interface. |
|[AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses) |Assign a secondary private IP address to a specified network interface, which can be a primary network interface or a secondary network interface. |
|[UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses) |Delete a secondary private IP address from the specified network interface. |
|[AssignIPv6Addresses](https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses) |Assign a secondary private IPv6 address to a specified network interface, which can be a primary network interface or a secondary network interface. |
|[UnassignIPv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses) |Delete the IPv6 private address for a specified network interface. |


<span id=".5a6J5YWo57uE"></span>
## Security group 


|API |Functionality |
|---|---|
|[CreateSecurityGroup](https://docs.byteplus.com/en/docs/vpc/CreateSecurityGroup) |Create a security group. |
|[ModifySecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupAttributes) |Modify the name and description of the security group. |
|[DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) |Query the security groups that meet the specified conditions. |
|[DeleteSecurityGroup](https://docs.byteplus.com/en/docs/vpc/DeleteSecurityGroup) |Delete a specified security group. |
|[AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress) |Add an inbound rule to a security group. |
|[AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress) |Add an outbound rule to a security group. |
|[ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress) |Modify the description of an outbound rule in a security group. |
|[ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress) |Modify the description of an inbound rule in a security group. |
|[DescribeSecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes) |Query security group rules in the security group that meet specified conditions. |
|[RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress) |Delete an inbound rule from a security group. |
|[RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress) |Delete an outbound Security Group Egress. |


<span id=".5YmN57yA5YiX6KGo"></span>
## Prefix List


|API |Functionality |
|---|---|
|[CreatePrefixList](https://docs.byteplus.com/en/docs/vpc/CreatePrefixList) |Create a prefix list. |
|[ModifyPrefixList](https://docs.byteplus.com/en/docs/vpc/ModifyPrefixList) |Modify a prefix list. |
|[DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) |Query the prefix lists that meet the specified conditions. |
|[DescribePrefixListAssociations](https://docs.byteplus.com/en/docs/vpc/DescribePrefixListAssociations) |Query resources associated with a specified prefix list. |
|[DescribePrefixListEntries](https://docs.byteplus.com/en/docs/vpc/DescribePrefixListEntries) |View the prefix entries of a specified prefix list. |
|[DeletePrefixList](https://docs.byteplus.com/en/docs/vpc/DeletePrefixList) |Delete a prefix list. |


<span id=".6auY5Y-v55So6Jma5oufSVA="></span>
## HAVIP


|API |Functionality |
|---|---|
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |Create an HAVIP. |
|[ModifyHaVipAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyHaVipAttributes) |Modify the name and description of a specified high availability virtual IP (HAVIP). |
|[DeleteHaVip](https://docs.byteplus.com/en/docs/vpc/DeleteHaVip) |Delete a specified HAVIP. |
|[AssociateHaVip](https://docs.byteplus.com/en/docs/vpc/AssociateHaVip) |Bind an HAVIP to an ECS instance or a network interface. |
|[DisassociateHaVip](https://docs.byteplus.com/en/docs/vpc/DisassociateHaVip) |Unbind an HAVIP from an ECS instance or a network interface. |
|[DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) |Query the high availability virtual IPs (HAVIPs) in a specified Region. |


<span id=".572R57ucQUNM"></span>
## Network ACL


|API |Functionality |
|---|---|
|[CreateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/CreateNetworkAcl) |Create a network ACL. |
|[ModifyNetworkAclAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkAclAttributes) |Modify the Basic information of a Network ACL. |
|[DeleteNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkAcl) |Delete a network ACL. |
|[DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) |Query information of Network Access Control Lists that meet specified conditions. |
|[DescribeNetworkAclAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAclAttributes) |Query the specified Network Access Control List. |
|[UpdateNetworkAclEntries](https://docs.byteplus.com/en/docs/vpc/UpdateNetworkAclEntries) |Update an inbound or outbound network ACL entry. |
|[AssociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/AssociateNetworkAcl) |Associate a resource with a specified network ACL. |
|[DisassociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DisassociateNetworkAcl) |Disassociate a resource from a specified network ACL. |


<span id=".5rWB5pel5b-X"></span>
## Flow logs


|API |Functionality |
|---|---|
|[CreateFlowLog](https://docs.byteplus.com/en/docs/vpc/CreateFlowLog) |Create a flow log. |
|[ModifyFlowLogAttribute](https://docs.byteplus.com/en/docs/vpc/ModifyFlowLogAttribute) |Modify a flow log. |
|[DescribeFlowLogs](https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs) |Query the flow logs that meet the specified conditions. |
|[ActiveFlowLog](https://docs.byteplus.com/en/docs/vpc/ActiveFlowLog) |Start a flow log. |
|[DeactiveFlowLog](https://docs.byteplus.com/en/docs/vpc/DeactiveFlowLog) |Stop a flow log. |
|[DeleteFlowLog](https://docs.byteplus.com/en/docs/vpc/DeleteFlowLog) |Delete a flow log. |


<span id=".5rWB6YeP6ZWc5YOP"></span>
## Traffic Mirror


|API |Functionality |
|---|---|
|[CreateTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorTarget) |Create a traffic mirror target. |
|[ModifyTrafficMirrorTargetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorTargetAttributes) |Modify the name and description of a traffic mirror target. |
|[DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) |Query traffic mirror target that meets the specified condition. |
|[DeleteTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorTarget) |Delete a traffic mirror target. |
|[CreateTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilter) |Create a traffic mirror filter. |
|[ModifyTrafficMirrorFilterAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterAttributes) |Modify a traffic mirror filter. |
|[DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) |Query traffic mirror filter that meets specified conditions. |
|[DeleteTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilter) |Delete a traffic mirror filter. |
|[CreateTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilterRule) |Create a traffic mirror filter rule. |
|[ModifyTrafficMirrorFilterRuleAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterRuleAttributes) |Modify a traffic mirror filter rule. |
|[DeleteTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilterRule) |Delete a traffic mirror filter rule. |
|[CreateTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorSession) |Create a traffic mirror session. |
|[ModifyTrafficMirrorSessionAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorSessionAttributes) |Modify a traffic mirror session. |
|[DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) |Query traffic mirror sessions that meet specified conditions. |
|[DeleteTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorSession) |Delete a traffic mirror session. |


<span id=".5qCH562-"></span>
## Tag


|API |Functionality |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources) |Add a user tag to a resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources) |Unbind a user tag from a resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) |Query tags that meet specified criteria. |
