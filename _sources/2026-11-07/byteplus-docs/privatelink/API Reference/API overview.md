---
title: "API overview"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/API-overview"
---

This topic introduces the API actions available for PrivateLink.

<span id="endpoint-services"></span>
## Endpoint services


|Action |Description |
|---|---|
|[CreateVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService) |Creates an endpoint service. |
|[DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) |Queries the endpoint services that meet specified conditions. |
|[DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) |Queries the details of an endpoint service. |
|[ModifyVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointServiceAttributes) |Modifies the attributes of an endpoint service. |
|[DeleteVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcEndpointService) |Deletes an endpoint service. |
|[VerifyVpcEndpointServicePrivateDNS](https://docs.byteplus.com/en/docs/privatelink/VerifyVpcEndpointServicePrivateDNS) |Verifies the DNS name of an endpoint service. |


<span id="service-resources"></span>
## Service resources


|Action |Description |
|---|---|
|[AttachResourceToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AttachResourceToVpcEndpointService) |Attaches service resources to an endpoint service. |
|[DescribeVpcEndpointServiceResources](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceResources) |Queries service resources attached to an endpoint service. |
|[DetachResourceFromVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/DetachResourceFromVpcEndpointService) |Detaches service resources from an endpoint service. |


<span id="service-accounts-in-the-allowlist"></span>
## Service accounts in the allowlist


|Action |Description |
|---|---|
|[AddPermissionToVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/AddPermissionToVpcEndpointService) |Adds service accounts to the allowlist of an endpoint service. |
|[DescribeVpcEndpointServicePermissions](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicePermissions) |Queries the IDs of service accounts in the allowlist of an endpoint service. |
|[RemovePermissionFromVpcEndpointService](https://docs.byteplus.com/en/docs/privatelink/RemovePermissionFromVpcEndpointService) |Removes service accounts from the allowlist of an endpoint service. |


<span id="interface-endpoints"></span>
## Interface endpoints


|Action |Description |
|---|---|
|[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint) |Creates an interface endpoint. |
|[DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) |Queries interface endpoints that meet specified conditions. |
|[DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes) |Queries detailed information about an interface endpoint. |
|[DescribeVpcEndpointServicesByEndUser](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServicesByEndUser) |Queries the VPC endpoints that meet specified conditions under the current account. |
|[ModifyVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcEndpointAttributes) |Modifies the attributes of an interface endpoint. |
|[DeleteVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcEndpoint) |Deletes an interface endpoint. |


<span id="gateway-endpoints"></span>
## Gateway endpoints


|Action |Description |
|---|---|
|[CreateVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcGatewayEndpoint) |Creates a gateway endpoint. |
|[DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) |Queries gateway endpoints that meet specified conditions. |
|[DescribeVpcGatewayEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpointAttributes) |Queries detailed information about a gateway endpoint. |
|[ModifyVpcGatewayEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/ModifyVpcGatewayEndpointAttributes) |Modifies the attributes of a gateway endpoint. |
|[DeleteVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/DeleteVpcGatewayEndpoint) |Deletes a gateway endpoint. |
|[DescribeVpcGatewayEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpointServices) |Queries gateway endpoint services that meet specified conditions. |


<span id="availability-zones-of-interface-endpoints"></span>
## Availability Zones of interface endpoints


|Action |Description |
|---|---|
|[AddZoneToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint) |Adds an Availability Zone to a VPC endpoint. |
|[DescribePrivateLinkAvailableZones](https://docs.byteplus.com/en/docs/privatelink/DescribePrivateLinkAvailableZones) |Queries Availability Zones for PrivateLink. |
|[DescribeVpcEndpointZones](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointZones) |Queries Availability Zones for VPC endpoints that meet specified conditions. |
|[RemoveZoneFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/RemoveZoneFromVpcEndpoint) |Removes an Availability Zone from a VPC endpoint. |


<span id="security-groups-of-interface-endpoints"></span>
## Security groups of interface endpoints


|Action |Description |
|---|---|
|[AttachSecurityGroupToVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/AttachSecurityGroupToVpcEndpoint) |Attaches a security group to a VPC endpoint. |
|[DescribeVpcEndpointSecurityGroups](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointSecurityGroups) |Queries the security groups for VPC endpoints that meet specified conditions. |
|[DetachSecurityGroupFromVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/DetachSecurityGroupFromVpcEndpoint) |Detaches a security group from a VPC endpoint. |


<span id="endpoint-connections"></span>
## Endpoint connections


|Action |Description |
|---|---|
|[EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) |Enables an endpoint connection. |
|[DescribeVpcEndpointConnections](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointConnections) |Queries endpoint connections that meet specified conditions. |
|[DisableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/DisableVpcEndpointConnection) |Disables an endpoint connection. |


<span id="tags"></span>
## Tags


|Action |Description |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/privatelink/TagResources) |Adds a user tag to a resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/privatelink/UntagResources) |Deletes a user tag from a resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/privatelink/ListTagsForResources) |Queries tags that meet specified conditions. |
