---
title: "API release notes"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/API-release-notes"
---

This article introduces the API change dynamics of Private Link.

<span id="Ug0oKNhF"></span>
## November 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Added error code: InsufficientIpInSubnet. |Interface Endpoint<br><br> |
|[ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes) |||
|[DescribeVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointConnections) |* Modified response parameter: ReplaceResourceId changed to ReplacedResourceId, indicating the service resource ID after seamless replacement.<br><br>* New response parameters:<br><br>   * ReplacedNetworkInterfaceId, indicating the new ENI ID of the endpoint after replacing the service resource.<br><br>   * ReplacedNetworkInterfaceIp, indicating the new endpoint ENI’s IPv4 address after replacing the service resource.<br><br>   * ReplacedNetworkInterfaceIpv6, indicating the new endpoint ENI’s IPv6 address after replacing the service resource.<br><br>   * ReplacingResource, indicating whether seamless replacement is in progress. |Endpoint connection<br><br> |
|[DisableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/DisableVpcEndpointConnection) |Added error code: InvalidReplaceResource.Deleted. ||
|[EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) |Added error code: UnsupportedOperation.ReplaceResourceConflict. ||
|[ModifyVpcEndpointZoneConnectionResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceResourceAttributes)<br><br> |Added new error codes: InsufficientIpInSubnet, InvalidEndpointZoneIPVersion.AddressMismatch, InvalidFusionClusterEndpoint.ResourceNotMatch, InvalidServiceResourceType.Malformed, InvalidServiceType.Malformed, InvalidSubnet.VpcMisMatch, InvalidSubnet.ZoneMisMatch, Forbidden, InvalidSubnet.NotFound, NetworkInterfaceCreateFailed. ||
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Added new error codes: InsufficientIpInSubnet, InvalidEndpointIpAddressVersions.EndpointServiceMisMatch, and Forbidden. |Endpoint availability zone |
|[DescribeVpcEndpointZones](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointZones)<br><br> |New response parameters:<br><br><br>* ReplacedNetworkInterfaceId indicates the new endpoint ENI ID after replacing the service resource.<br><br>* ReplacedNetworkInterfaceIp indicates the new endpoint ENI's IPv4 address after replacing the service resource.<br><br>* ReplacedNetworkInterfaceIpv6 indicates the new endpoint ENI's IPv6 address after replacing the service resource. ||
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |Added error code: Forbidden. |Service Resource |


<span id="Ug0oKNhF"></span>
## September 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[DescribeVpcEndpointServiceResources](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceResources) |Add response parameter: ResourceAutoAllocated structure. |Service Resource |
|[DetachResourceFromVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DetachResourceFromVpcEndpointService) |Added error code: UnsupportedOperation.LastAutoAllocatedResource. ||
|[ModifyVpcEndpointServiceResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceResourceAttributes) |* Added request parameters: ResourceAutoAllocated.N.AutoAllocatedEnabled.<br><br><br>ResourceAutoAllocated.N.ZoneId。<br><br><br>* Modify request parameters: ZoneIds.N changed from required to optional.<br><br>* Added new error codes: ErrServiceResourceNotSupportedMultipleZone, InvalidIncorrectOrder.Malformed, UnsupportedOperation.LastAutoAllocatedResource. ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## July 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Modify request parameters: change PrivateDNSEnabled type from String to Boolean. |Endpoint |
|[ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes) |* Modified request parameters: EndpointName changed from required to optional; PrivateDNSEnabled parameter type changed from String to Boolean.<br><br>* Removed error code: InvalidEndpointZoneIPVersion.AddressMismatch.<br><br>* Added new error codes: InvalidEndpointZoneIPVersion.AddressMismatch, Forbidden.IPv6EndpointToOthers, Forbidden.ToIPv6Endpoint. ||
|[ModifyVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointConnections) |Modify request parameters: change Bps and Cps from String to Integer.<br><br> |Endpoint connection |
|[ModifyVpcGatewayEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcGatewayEndpointAttributes) |Modify request parameters: change EndpointName from required to optional. |Gateway Endpoint |
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |* Modify request parameters: rename ZoneIds to ZoneIds.N.<br><br>* Delete error code: InvalidServiceResource.InvalidStatus |Service Resource |
|[ModifyVpcEndpointServiceResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceResourceAttributes) |Deleted error code: InvalidServiceResource.InvalidStatus.<br><br> ||
|[CreateUniqueResourceTypeVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateUniqueResourceTypeVpcEndpointService) ||Endpoint Service<br><br> |
|[ModifyUniqueResourceTypeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyUniqueResourceTypeVpcEndpointServiceAttributes) |* Added error codes: InvalidModifyConnectedEpsvcIPVersion.Conflict and MissingParameter.<br><br>* Deleted error code: InvalidServiceResource.InvalidStatus. ||
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |* Modify request parameters: change PrivateDNSEnabled parameter type from String to Boolean.<br><br>* Added error code: InvalidPrivateDNSType.ServiceOwnerMismatch.<br><br>* Deleted error code: InvalidServiceResource.InvalidStatus. ||
|[ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes) |* Modified request parameter: changed PrivateDNSEnabled type from String to Boolean.<br><br>* Added new error codes: InvalidModifyConnectedEpsvcIPVersion.Conflict, InvalidPrivateDNSType.ServiceOwnerMismatch, and InvalidServiceResource.NotFound.<br><br>* Deleted an error code: InvalidServiceResource.InvalidStatus. ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## May 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) |* Added request parameter: ZoneId.<br><br>* Added error code: InvalidEndpointZone.InvalidStatus. |Endpoint connection |
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Delete error code: QuotaExceed.EndpointZoneEachInstance.<br><br> |Interface Endpoint |
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint)<br><br> ||Endpoint Availability Zone |
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |Removed error code: QuotaExceed.ServiceZoneEachInstance. |Service Resource<br><br>&nbsp;<br><br> |
|[ModifyVpcEndpointServiceResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceResourceAttributes) |||
|[CreateUniqueResourceTypeVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateUniqueResourceTypeVpcEndpointService) ||Endpoint Service |
|[ModifyUniqueResourceTypeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyUniqueResourceTypeVpcEndpointServiceAttributes) |||
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |||


<span id=".MjAyNOW5tDEx5pyI"></span>
## March 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Modify the Chinese descriptions of error codes: InvalidLocation.Intercepted and InvalidServiceManaged.Conflict. |Interface Endpoint |
|[AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint) |Modified the Chinese description of error code InvalidServiceManaged.Conflict. |Endpoint Security Group |
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Modified the Chinese description of the error code InvalidLocation.Intercepted. |Endpoint availability zone |
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |* Add request parameter: Resources.N.ZoneIds.N.<br><br>* Modify request parameters: Add new value field ALB to ServiceResourceType.<br><br>* Add new error codes: InvalidApplicationLoadBalancer.InvalidZoneInfo, InvalidZoneforALB.conflict, InvalidResource.NotFound.<br><br>* Modify the Chinese description of the error code InvalidLocation.Intercepted. |Endpoint Service |
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |* Modify request parameters: update ZoneIds validation logic; this parameter must be provided for ALB resources.<br><br>* Added new error codes: ServiceLinkRoleNotAuthorized, InvalidApplicationLoadBalancer.InvalidZoneInfo, InvalidZoneforALB.conflict, and InvalidResource.NotFound.<br><br>* Modified the Chinese description of the error code InvalidLocation.Intercepted. |Service Resource |
|[ModifyVpcEndpointServiceResourceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceResourceAttributes) |Added an interface to modify ALB service resources. ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## January 2025


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes) |Add response parameters: Bps, EndpointZoneNums. |Interface Endpoint |
|[DescribeVpcEndpointServicesByEndUser](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicesByEndUser) |Added new error codes: InvalidParameter.BatchQueryForFuzzySearch, LimitExceed.EndpointServices, and Forbidden. ||
|[ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes) |||
|[DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) |* Add request parameter: ConnectionStatus.<br><br>* Add response parameters: Bps, EndpointZoneNums. ||
|[DescribeVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointConnections) ||Endpoint connection |
|[ModifyVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointConnections) |||
|[AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint) |Added new error codes: InvalidEndpoint.ServiceDeleted and ServiceLinkRoleNotAuthorized. |Endpoint security group |
|[DetachSecurityGroupFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DetachSecurityGroupFromVpcEndpoint) |Added new error code: InvalidEndpoint.ServiceDeleted. ||
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Added new error codes: InvalidEndpoint.ServiceDeleted, ServiceLinkRoleNotAuthorized. |Endpoint availability zone |
|[RemoveZoneFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/RemoveZoneFromVpcEndpoint) |Add error code: InvalidEndpoint.ServiceDeleted. ||
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |* Modified request parameter: Resources.N.ZoneIds changed to Resources.N.ZoneIds.N.<br><br>* Added a new request parameter: ServiceType. |Endpoint Service |
|[DeleteVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcEndpointService) |* Removed error code: InvalidEndpoint.InUse.<br><br>* Added new error codes: InvalidEndpoint.InvalidStatus and InvalidEndpoint.IsConnected. ||
|[DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) |Add new response parameter: DeletedTime. ||
|[DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) |||


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |Add error code `InvalidLocation.Intercepted`. |Endpoint Service |
|[DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) |Add response parameter `ServiceNameManaged`; add error code `Forbidden`. ||
|[DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) |||
|[CreateUniqueResourceTypeVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateUniqueResourceTypeVpcEndpointService) |Added error code `InvalidLocation.Intercepted`. ||
|[ModifyUniqueResourceTypeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyUniqueResourceTypeVpcEndpointServiceAttributes) |||
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) ||Service Resource |
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Add error codes `InvalidServiceManaged.Conflict`, `Forbidden.ServiceManagedEndpoint`, `Forbidden.ServiceManagedEndpointService`, `InvalidLocation.Intercepted`; remove error code `Forbidden.SpecifiedSecurityGroup`. |Interface Endpoint |
|[DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes) |Added response parameter `ServiceManaged`; added error code `Forbidden`. ||
|[DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) |||
|[DescribeVpcEndpointServicesByEndUser](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicesByEndUser) |Added response parameter `ServiceNameManaged`. ||
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Added new error code `InvalidLocation.Intercepted`. |endpoint availability zone |
|[AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint) |Add error codes `InvalidServiceManaged.Conflict` and `Forbidden.ServiceManagedEndpoint`; remove error code `Forbidden.SpecifiedSecurityGroup`. |Endpoint security group |


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |Added request parameter `IpAddressVersions.N`; added error codes `ServiceLinkRoleNotAuthorized`, `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, and `InvalidServiceResourceStatus.IPVersionMismatch`. |Endpoint Service |
|[CreateUniqueResourceTypeVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateUniqueResourceTypeVpcEndpointService) |Added new request parameter `IpAddressVersions.N`; added new error codes `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, `InvalidServiceResourceStatus.IPVersionMismatch`, and `Forbidden`. ||
|[ModifyUniqueResourceTypeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyUniqueResourceTypeVpcEndpointServiceAttributes) |Added request parameter `IpAddressVersions.N`; added error codes `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, `InvalidModifyConnectedDualStackEpsvcIPVersion.Conflict`, `InvalidServiceResourceStatus.IPVersionMismatch`, `Forbidden`. ||
|[DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) |Added response parameter `IpAddressVersions`. ||
|[DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) |||
|[ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes) |Added request parameter `IpAddressVersions.N`; added error codes `ErrPrivateLinkServiceNotSupportedZone`, `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, `InvalidModifyConnectedDualStackEpsvcIPVersion.Conflict`, `InvalidServiceResource.InvalidStatus`, `InvalidServiceResource.Malformed`, and `InvalidServiceResourceStatus.IPVersionMismatch`. ||
|[DescribeVpcEndpointServiceResources](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceResources) |Added error code `InvalidZoneID.Malformed`. |Service Resource |
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |Added new error code `InvalidServiceResourceStatus.IPVersionMismatch`. ||
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Add request parameters `IpAddressVersions.N` and `Zones.N.PrivateIpv6Address`; add error codes `InvalidEndpointZoneIPVersion.AddressMismatch`, `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, `InvalidIPVersion.Conflict`, and `InvalidIPv6Address.Malformed`. |Interface Endpoint |
|[DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes) |Added response parameter `IpAddressVersions`. ||
|[DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) |||
|[DescribeVpcEndpointServicesByEndUser](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicesByEndUser) |||
|[ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes) |Added new request parameter `IpAddressVersions.N`; added new error codes `InvalidEndpointZoneIPVersion.AddressMismatch`, `InvalidIPAddressVersion.Conflict`, `InvalidIPAddressVersionsParameter.Malformed`, `InvalidIPVersion.Conflict`, `AssignIPv6AddressFailed`, `InvalidSubnet.VpcMisMatch`, `InvalidSubnet.ZoneMisMatch`, `UnsupportedOperation.AccountArrears`, `InvalidSubnet.NotFound`. ||
|[CreateVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcGatewayEndpoint) |Added new error codes `InvalidEndpoint.ServiceMisMatch`, `InvalidPolicy.Condition.Malformed`, `InvalidPolicy.ConditionKey.Malformed`, `InvalidPolicy.ConditionOperator.Malformed`, and `InvalidPolicy.ConditionValue.Malformed`. |Gateway Endpoint |
|[ModifyVpcGatewayEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcGatewayEndpointAttributes) |Add error codes `InvalidPolicy.Condition.Malformed`, `InvalidPolicy.ConditionKey.Malformed`, `InvalidPolicy.ConditionOperator.Malformed`, `InvalidPolicy.ConditionValue.Malformed`. ||
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Add request parameter `PrivateIpv6Address`; add error codes `InvalidPrivateDNS.UnsupportedOperation`, `InvalidEndpointZoneIPVersion.AddressMismatch`, `InvalidIPv6Address.Malformed`. |Endpoint availability zone |
|[DescribeVpcEndpointZones](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointZones) |Add request parameters `Ipv6ServiceStatus` and `NetworkInterfaceIpv6`. ||
|[DescribeVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointConnections) |Added response parameter `NetworkInterfaceIpv6`. |Endpoint connection |
|[EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) |Add error code `InvalidIPVersion.Conflict`. ||


<span id="Et7tNOQu"></span>
## Aug\-24


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) |Add response parameters `Payer`, `BillingType`, and `BusinessStatus`. |Endpoint Service |
|[DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) |Added request parameter `ServiceType`; added response parameters `Payer`, `BillingType`, and `BusinessStatus`. ||
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Added error codes `InvalidAccount.SecurityGroupMisMatch`, `InvalidEndpoint.ServiceMisMatch`, `InvalidVpcAccount.Mismatched`. |Interface Endpoint |
|[DescribeVpcEndpointServicesByEndUser](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicesByEndUser) |Add response parameters `Payer`, `BillingType`, and `BusinessStatus`. ||
|[DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) |Added response parameter `Payer`. ||
|[DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes) |||
|[CreateVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcGatewayEndpoint) |Added error code `InvalidVpcAccount.Mismatched`. |Gateway Endpoint |
|[AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint) |Added new error codes `InvalidAccount.SecurityGroupMisMatch` and `InvalidEndpointService.NotFound`. |Endpoint Security group |
|[DetachSecurityGroupFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DetachSecurityGroupFromVpcEndpoint) |Added a new error code `InvalidEndpointService.NotFound`. ||
|[RemoveZoneFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/RemoveZoneFromVpcEndpoint) ||Status of the endpoint availability zone. |
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Added new error code `InvalidPrivateDNSName.Conflict`. ||
|[EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) |Added error codes `InvalidPrivateDNS.UnsupportedOperation` and `InvalidPrivateDNSName.Conflict`. |Endpoint connection |


<span id="baMuqWbP"></span>
## May 2024


|**API** |**Release note** |**Associated features** |
|---|---|---|
|All Interfaces |Private Link OpenAPI interface launched for the first time. |\-\- |


&nbsp;

&nbsp;
