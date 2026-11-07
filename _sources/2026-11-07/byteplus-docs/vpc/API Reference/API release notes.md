---
title: "API release notes"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/API-release-notes"
---

This topic introduces the API updates of Virtual Private Cloud (VPC).

## September 2026

|API |Modify |Associated feature |
|---|---|---|
|[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) |New error code: Forbidden.IpamPoolAllocationResourceDiscovery. |VPC |
|[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes)<br><br> |New error codes: InvalidCen.VpcPeeringConnectionActive, InvalidCoreNetwork.Conflict, InvalidCoreNetwork.NotExist, InvalidCoreNetwork.Repeated, and InvalidVpc.RoutePropagationModeConflict. ||
|[DeleteVpc](https://docs.byteplus.com/en/docs/vpc/DeleteVpc) |New error codes: InvalidRouteTable.InUse, InvalidVpc.InUse. ||
|[AssociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock) |* New request parameter: Ipv4IpamPoolId.<br><br>* New error codes: InvalidIpamPoolCidrAllocation.Malformed, Forbidden.IpamPoolAllocationResourceDiscovery. ||
|[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) |New error code: InvalidSpecificEgress.Mismatch. |Subnet |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes) |New error code: InvalidSpecificEgress.Mismatch. ||
|[DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet) |New error code: InvalidRouteCidr.Conflict. ||
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry)<br><br> |New error codes added: InvalidCidrBlock.Reserved, InvalidGroupItem.MissingDefault, Forbidden.RouteNextHopType. |Route table |
|[DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) |New request parameter: VpcId. ||
|[ModifyRouteEntry](https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry) |New rerror code: InvalidVpcPeeringConnection.InvalidStatus, InvalidRouteTable.NotFound. ||
|[CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface)<br><br> |* New request parameters: TcpEstablishedTimeout, TcpClosedAndTimeWaitTimeout, UdpTimeout.<br><br>* New error code: InvalidIp.Malformed. |Network interface |
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) |New request parameters: TcpEstablishedTimeout, TcpClosedAndTimeWaitTimeout, UdpTimeout. ||
|[DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) |New response parameters: TcpEstablishedTimeout, TcpClosedAndTimeWaitTimeout, UdpTimeout. ||
|[DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes) |* New response parameters: TcpEstablishedTimeout, TcpClosedAndTimeWaitTimeout, UdpTimeout.<br><br>* New error code: InvalidEniId.NotFound. ||
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |New request parameter: DeleteOnTermination. ||
|[AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses) |New error code: InvalidIp.Malformed. ||
|[AssignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses) |New error code: InvalidIp.Malformed. ||
|[CreateSecurityGroup](https://docs.byteplus.com/en/docs/vpc/CreateSecurityGroup) |New error code: Forbidden. |Security group |
|[DescribeSecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes) |New response parameter: SecurityGroupRuleId. ||
|[DescribePrefixListAssociations](https://docs.byteplus.com/en/docs/vpc/DescribePrefixListAssociations) |New error code: InvalidPrefixList.NotFound. |Prefix list |
|[DescribePrefixListEntries](https://docs.byteplus.com/en/docs/vpc/DescribePrefixListEntries) |New error code: InvalidPrefixList.NotFound. ||
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |New error codes: InvalidIp.Malformed, InvalidZoneId.NotFound. |HaVip |
|[CreateTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorSession)<br><br> |* New request parameter Enabled.<br><br>* New error codes: MainAccountNotSupportPaypal, MainAccountNotSupportPaypal, NotSupportPaypal. |Traffic mirror |
|[ModifyTrafficMirrorSessionAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorSessionAttributes) |New request parameter Enabled. ||
|[DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) |New response parameter Enabled. ||

## July 2026

|API |Modify |Associated feature |
|---|---|---|
|[AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/VirtualPrivateCloud/AuthorizeSecurityGroupIngress-Addinganinboundsecuritygrouprule) |New request parameters: SourcePortStart, SourcePortEnd, LocalCidrIp.<br><br> |Security group |
|[AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress) |||
|[ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress) |||
|[ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress) |||
|[RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress) |||
|[RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress) |||
|[DescribeSecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes) |New response parameters: SourcePortStart, SourcePortEnd, LocalCidrIp. ||

## March 2026

|API |Release note |Associated feature |
|---|---|---|
|[DeleteVpc](https://docs.byteplus.com/en/docs/vpc/DeleteVpc)<br><br> |New error code: InvalidRouteTable.InUse. |VPC instance |
|[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) |New error code: InvalidSpecificEgress.Mismatch |Subnet |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes) |New error code: InvalidSpecificEgress.Mismatch |Subnet |
|[DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups)<br><br> |New return values: UsedlpCount, AvailablelpCount, UsedNetworklnterfaceCount, AvailableNetworklnterfaceCount. |Security group |
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |New error code: InvalidZoneld.NotFound |HaVip |
|[DescribePrefixListAssociations](https://docs.byteplus.com/en/docs/vpc/DescribePrefixListAssociations) |Added new values TrRouteTable and TrRoutePolicyTable for the request parameter ResourceType. |Prefix list |

## November 2025

|API |Release note |Associated feature |
|---|---|---|
|[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) |Extended the mask range for the request parameter CidrBlock to /28 (previously up to /24). |VPC instance |
|[AssociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock) |Extended the mask range for the request parameter SecondaryCidrBlock to /28 (previously up to /24). ||
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |New error codes: InvalidIp.Malformed, Forbidden.TrafficMode, InvalidVpcEip.InUse. |Network interface<br><br> |
|[DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface) |New error code: InvalidVpcEip.InUse.<br><br> ||
|[UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses) |||
|[UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses) |||
|[CreateIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/CreateIpv4Gateway) |Added new APIs for managing IPv4 gateways to enable centralized control of IPv4 internet traffic. |IPv4 gateway |
|[DeleteIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/DeleteIpv4Gateway) |||
|[DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) |||
|[ModifyIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/ModifyIpv4Gateway) |||
|[AttachIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/AttachIpv4Gateway) |||
|[DetachIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/DetachIpv4Gateway) |||
|[EnableIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/EnableIpv4Gateway) |||
|[DisableIpv4Gateway](https://docs.byteplus.com/en/docs/vpc/DisableIpv4Gateway) |||

## September 2025

|API |Release note |Associated feature |
|---|---|---|
|[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc)<br><br> |New request parameter: DryRun. |VPC instance |
|[CreateRouteTable](https://docs.byteplus.com/en/docs/vpc/CreateRouteTable) |* New request parameter: AssociateType.<br><br>* New error code: InvalidRouteTableAssociateType.Malformed. |Route table |
|[DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) |New response parameters: AssociateType, Ipv4GatewayId, Ipv6GatewayId. ||
|[AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable) |* New request parameters: GatewayType, GatewayId.<br><br>* New error codes: InvalidGatewayType.Malformed, InvalidRouteTableAssociateGateway.Malformed, InvalidRouteTableGateway.VpcMismatch, Forbidden, InvalidIpv4Gateway.NotFound, InvalidIpv6Gateway.NotFound. ||
|[DisassociateRouteTable](https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable) |* New request parameters: GatewayType, GatewayId.<br><br>* New error codes: InvalidGatewayType.Malformed, InvalidRouteTable.GatewayMismatch, InvalidRouteTableAssociateType.Malformed. ||
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry)<br><br> |* New error codes: InvalidGatewayRouteTablePrefixList.Malformed, InvalidIpv4Gateway.NotFound ||
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes)<br><br> |New error codes: InvalidNetworkInterfaceTrafficMode.InvalidAvailabilityZone, InvalidSubnet.NotFound. |Network interface |
|[AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress) |* Added a new value gre for the request parameter Protocol, indicating the GRE protocol.<br><br>* Updated the Chinese and English descriptions for the error code InvalidSecurityRule.Malformed.<br><br><br> |Security group<br><br> |
|[AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress) |||
|[ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress) |||
|[ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress) |||
|[RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress) |||
|[RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress) |||
|[ModifySecurityGroupEgressRules](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupEgressRules) |Added new APIs for modifying inbound and outbound rules of security groups. ||
|[ModifySecurityGroupIngressRules](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupIngressRules) |||

## July 2025

|API |Release note |Associated feature |
|---|---|---|
|[DeleteVpc](https://docs.byteplus.com/en/docs/vpc/DeleteVpc) |New error code: InvalidClassicVpc.InUse.<br><br> |VPC instance |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes) |New error code: InvalidVpc.InvalidStatus. |Subnet |
|[AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses) |New error code: InvalidVpc.NotFound. |Network interface |
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |New error code: InvalidInstance.Malformed. ||
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) |||
|[CreateFlowLog](https://docs.byteplus.com/en/docs/vpc/CreateFlowLog) |New request parameter: EnableIndex. |Flow log |

## May 2025

|API |Release note |Associated feature |
|---|---|---|
|[AssignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses) |* New request parameter: ClientToken.<br><br>* New error codes: IdempotentParameterMismatch, InvalidParameter.ClientTokenMalformed, and IdempotentProcessing. |Network interface |
|[AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses) |||
|[UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses) |||
|[UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses) |||
|[ModifyRouteEntry](https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry) |* New request parameter: NextHopType.<br><br>* New error codes: Forbidden.RouteNextHopType, InvalidRouteEntry.PublishedToCen. |Route table |
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |New error codes: Forbidden.DualTunnelVpnGatewayRoute, InvalidEniId.NotFound. ||

## March 2025

|API |Release note |Associated feature |
|---|---|---|
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |Removed error code: Forbidden. |HaVip |
|[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet)<br><br> |* New request parameter: VpcIpv6CidrBlock, optional.<br><br>* New error codes: InvalidTransitRouter.InvalidStatus, InvalidVpcIPv6Cidr.Malformed. |Subnet |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes)<br><br> |* New request parameter VpcIpv6CidrBlock.<br><br>* New error codes: InvalidSubnetCidr.IPv6Conflict, InvalidVpcIPv6Cidr.Malformed. ||
|[AssociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/AssociateVpcCidrBlock) |* New request parameters:<br><br>   * Ipv6CidrBlock, optional.<br><br>   * Ipv6Isp, optional.<br><br>   * Ipv6MaskLen, optional.<br><br>* New response parameters: Ipv6CidrBlock, Ipv6Isp.<br><br>* New error codes: InsufficientIpv6Blocks, InvalidIpv6CidrBlock.NotReserved, InvalidParameter.EnableIpv6, InvalidParameter.MaskLength, InvalidParameter.SecondaryCidrAndIpv6Cidr, QuotaExceeded.VpcIpv6Cidr, Forbidden.Ipv6IspType. |VPC instance |
|[CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) |* New request parameters:<br><br>   * Ipv6Isp, optional.<br><br>   * Ipv6MaskLen, optional.<br><br>* New error codes: InvalidParameter.MaskLength, Forbidden.Ipv6IspType. ||
|[DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) |New response parameters: Ipv6CidrBlocks, Ipv6Isp. ||
|[DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) |New response parameters: Ipv6CidrBlock, Ipv6Isp. ||
|[DisassociateVpcCidrBlock](https://docs.byteplus.com/en/docs/vpc/DisassociateVpcCidrBlock) |* New request parameter: Ipv6CidrBlock.<br><br>* New error codes: InvalidIPv6CidrBlock.InUse, InvalidIPv6CidrBlock.NotFound, InvalidParameter.SecondaryCidrAndIpv6Cidr, QuotaExceeded.VpcIpv6Cidr. ||
|[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes)<br><br> |* New request parameters: Ipv6Isp, Ipv6MaskLen.<br><br>* New error codes: InsufficientIpv6Blocks, InvalidParameter.MaskLength, QuotaExceeded.VpcIpv6Cidr, Forbidden.Ipv6IspType, InvalidIpv6Pool.NotFound. ||

## January 2025

|API |Release note |Associated feature |
|---|---|---|
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |Removed error code `InvalidPrefixList.InvalidStatus`. |Route table |
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |New error code `InvalidTrafficMirrorSession.InvalidStatus`. |Network interface |
|[DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface) |Removed error codes `InvalidEip.InvalidStatus`, `InvalidPrefixList.InvalidStatus`, `InvalidSecurityGroup.InvalidStatus`, `InvalidFlowLog.NotFound`. ||
|* [AuthorizeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupEgress)<br><br>* [AuthorizeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress)<br><br>* [RevokeSecurityGroupEgress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupEgress)<br><br>* [RevokeSecurityGroupIngress](https://docs.byteplus.com/en/docs/vpc/RevokeSecurityGroupIngress) |* New error code `InvalidSecurityRule.InvalidSourceStatus`.<br><br>* Removed error code `InvalidPrefixList.InvalidStatus`. |Security group |
|* [ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress)<br><br>* [ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress) |New error code `InvalidSecurityRule.InvalidSourceStatus`. ||
|[DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) |New response parameters `TrafficMirrorFilters.CreatedAt`, `EgressFilterRules.CreatedAt`, `EgressFilterRules.UpdatedAt`, `IngressFilterRules.CreatedAt`, `IngressFilterRules.UpdatedAt`. |Traffic mirror |
|[DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) |New response parameters `TrafficMirrorSessions.CreatedAt` and `TrafficMirrorSessions.UpdatedAt`. ||
|[DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) |New response parameters `TrafficMirrorTargets.CreatedAt` and `TrafficMirrorTargets.UpdatedAt`. ||
|* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources)<br><br>* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources)<br><br>* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources) |New error code `InvalidResourceType.NotFound`. |Tag |

## October 2024

|API |Release note |Associated feature |
|---|---|---|
|[CreateTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorTarget) |* New request parameters `ProjectName`, `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`, `InvalidProject.NotFound`.<br><br>* Removed error code `Forbidden`. |Traffic mirror target |
|[ModifyTrafficMirrorTargetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorTargetAttributes) |Removed error code `Forbidden`. ||
|[DescribeTrafficMirrorTargets](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets) |* New request parameters `ProjectName`, `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameters `ProjectName` and `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`.<br><br>* Removed error code `Forbidden`. ||
|[DeleteTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorTarget) |Removed error code `Forbidden`. ||
|[CreateTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilter) |* New request parameters `ProjectName`, `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`, `InvalidProject.NotFound`.<br><br>* Removed error code `Forbidden`. |Traffic mirror filter |
|[ModifyTrafficMirrorFilterAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterAttributes) |Removed error code `Forbidden`. ||
|[DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) |* New request parameters `ProjectName`, `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameters `ProjectName` and `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`.<br><br>* Removed error code `Forbidden`. ||
|[DeleteTrafficMirrorFilter](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilter) |Removed error code `Forbidden`. ||
|[CreateTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorFilterRule) |Removed error code `Forbidden`. ||
|[ModifyTrafficMirrorFilterRuleAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterRuleAttributes) |Removed error code `Forbidden`. ||
|[DeleteTrafficMirrorFilterRule](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorFilterRule) |Removed error code `Forbidden`. ||
|[CreateTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/CreateTrafficMirrorSession) |* New request parameters `ProjectName`, `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`, `InvalidProject.NotFound`.<br><br>* Removed error code `Forbidden`. |Traffic mirror session |
|[ModifyTrafficMirrorSessionAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorSessionAttributes) |Removed error code `Forbidden`. ||
|[DescribeTrafficMirrorSessions](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions) |* New request parameters `ProjectName`, `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameters `ProjectName` and `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`.<br><br>* Removed error code `Forbidden`. ||
|[DeleteTrafficMirrorSession](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorSession) |Removed error code `Forbidden`. ||

## September 2024

|API |Release note |Associated feature |
|---|---|---|
|[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes) |New error code `QuotaExceeded.SystemRouteEntry`. |VPC |
|[CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) |New error code `QuotaExceeded.SystemRouteEntry`. |Subnet |
|[CreateRouteTable](https://docs.byteplus.com/en/docs/vpc/CreateRouteTable) |* New request parameters `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`. |Route table |
|[DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) |* New request parameters `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameter `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`. ||
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |New error codes`InvalidGroupResource.TypesInconsistent`, `InvalidRouteNextHop.IPv6Only`. ||
|[ModifyRouteEntry](https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry) |* New request parameter `NextHopId`.<br><br>* New error codes `InvalidRouteNextHop.Malformed`, `Forbidden`, and `Forbidden.RouteNextHopType`. ||
|[UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses) |Removed error code `InvalidEip.InvalidStatus`. |Network interface |
|[UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses) |Removed error code `InvalidEip.InvalidStatus`. ||
|[TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources) |* Added new values havip, routetable, and networkacl for the request parameter `ResourceType`.<br><br>* New error code `InvalidTagAccount.Malformed`. |Tag |
|[UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources) |Added new values havip, routetable, and networkacl for the request parameter `ResourceType`. ||
|[ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) |Added new values havip, routetable, and networkacl for the request parameter `ResourceType`. ||
|[CreateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/CreateNetworkAcl) |* New request parameters `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`. |Network ACL |
|[DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) |* New request parameters `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameter `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`. ||
|[DescribeNetworkAclAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAclAttributes) |New response parameter `Tags`. ||
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |* New request parameters `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`. |HaVip |
|[DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) |* New request parameters `TagFilters.N.Key`, `TagFilters.N.Values.N`.<br><br>* New response parameter `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`. ||
|[CreateFlowLog](https://docs.byteplus.com/en/docs/vpc/CreateFlowLog) |* New error code`InvalidVpnConnection.TlsAccessDenied`<br><br>* Removed error code`InvalidFlowLog.TlsAccessDenied`. |Flow log |

## July 2024

|API |Release note |Associated feature |
|---|---|---|
|[DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) |New request parameter `VpcOwnerId`. |VPC |
|[DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) |New request parameter `SubnetOwnerId`. |Subnet |
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |Added a new value GWLBEndpoint for the request parameter `NextHopType`. |Route table |
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) |Removed error code `Forbidden`. |Network interface |
|[AttachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface) |Removed error code `InvalidEip.InvalidStatus`. ||
|[DetachNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DetachNetworkInterface) |Removed error code `InvalidEip.InvalidStatus`. ||
|[UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses) |New error code `InvalidEip.InvalidStatus`. ||
|[CreateSecurityGroup](https://docs.byteplus.com/en/docs/vpc/CreateSecurityGroup) |New error code `InvalidVpc.InvalidStatus`. |Security group |
|[DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) |New response parameter `AccountId`. ||
|[DescribeSecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes) |* New response parameter `AccountId`.<br><br>* New error code `Forbidden`. ||
|[DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) |New response parameter `AccountId`. |Network ACL |
|[DescribeNetworkAclAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAclAttributes) |New response parameter `AccountId`. ||
|[CreateFlowLog](https://docs.byteplus.com/en/docs/vpc/CreateFlowLog) |* New request parameters `ProjectName`, `Tags.N.Key`, `Tags.N.Value`.<br><br>* New error codes `InvalidFlowLog.CloudProfileNotAvailable`, `InvalidTag.Disorder`, `InvalidTagKey.Malformed`, `InvalidTagValue.Malformed`, `LimitExceeded.Tags`, Forbidden`.PurchaseLimited`, `InvalidProject.NotFound`.<br><br>* Removed error code `Forbidden`. |Flow log |
|[ModifyFlowLogAttribute](https://docs.byteplus.com/en/docs/vpc/ModifyFlowLogAttribute) |Removed error code `Forbidden`. ||
|[DescribeFlowLogs](https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs) |* New request parameters `ProjectName`, `TagFilters.N.Key`, and `TagFilters.N.Values`.<br><br>* New response parameters `ProjectName` and `Tags`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`.<br><br>* Removed error code `Forbidden`. ||
|[ActiveFlowLog](https://docs.byteplus.com/en/docs/vpc/ActiveFlowLog) |Removed error code `Forbidden`. ||
|[DeactiveFlowLog](https://docs.byteplus.com/en/docs/vpc/DeactiveFlowLog) |Removed error code `Forbidden`. ||
|[DeleteFlowLog](https://docs.byteplus.com/en/docs/vpc/DeleteFlowLog) |Removed error code `Forbidden`. ||

## May 2024

|API |Release note |Associated feature |
|---|---|---|
|[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes) |Removed error code `InvalidVpc.EnableIpv6`. |VPC |
|[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes) |New error code`InvalidSubnet.InvalidStatus`. |Subnet |
|[DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet) |New error code`InvalidSubnet.InvalidStatus`. ||
|[CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry) |New error code `InvalidEni.InvalidStatus`. |Route table |
|[CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface) |New error codes `InvalidSecurityGroup.InvalidStatus` and `InvalidEni.InvalidStatus`. |Network interface |
|[DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface) |New error code `InvalidSecurityGroup.InvalidStatus`. ||
|[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) |New error code `InvalidSecurityGroup.InvalidStatus`. ||
|[CreatePrefixList](https://docs.byteplus.com/en/docs/vpc/CreatePrefixList) |New optional request parameters: `Tags.N.Key`, `Tags.N.Value`, and `ProjectName`. |Prefix list |
|[DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) |* New optional request parameters `TagFilters.N.Key` and `TagFilters.N.Values.N`.<br><br>* New response parameter `PrefixList.Tags.Key`, `PrefixList.Tags.Value`.<br><br>* New error codes `InvalidTagFilter.Disorder`, `InvalidTagFilterKey.Malformed`, `InvalidTagFilterValue.Malformed`, `LimitExceeded.TagFilterKey`, `LimitExceeded.TagFilterValue`. ||
|[ModifySecurityGroupAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupAttributes) |New error code `InvalidSecurityGroup.InvalidStatus`. |Security group |
|[ModifySecurityGroupRuleDescriptionsEgress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsEgress) |New error code `InvalidSecurityGroup.InvalidStatus`. ||
|[ModifySecurityGroupRuleDescriptionsIngress](https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupRuleDescriptionsIngress) |New error code `InvalidSecurityGroup.InvalidStatus`. ||
|[CreateHaVip](https://docs.byteplus.com/en/docs/vpc/CreateHaVip) |New error code `InvalidSubnet.InvalidStatus`. |HaVip |
|[AssociateHaVip](https://docs.byteplus.com/en/docs/vpc/AssociateHaVip) |New error code `InvalidEni.InvalidStatus`. ||
|[DisassociateHaVip](https://docs.byteplus.com/en/docs/vpc/DisassociateHaVip) |New error code `InvalidEni.InvalidStatus`. ||

## April 2024

|API |Release note |Associated feature |
|---|---|---|
|VPC |The first release of all OpenAPI of VPC. |All |
