---
title: "CreateVpcEndpointService - Creating an endpoint service"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpointService"
---

Call the CreateVpcEndpointService API to create an endpoint service.

## Instructions

A single endpoint service supports adding a default maximum of 100 service resources per Availability Zone.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpcEndpointService&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: CreateVpcEndpointService`

Action to execute. Set the value to **CreateVpcEndpointService**.

**Version ** String必选 `Example: 2020-04-01`

Current API version is **2020\-04\-01**.

**ServiceType ** String`optional` `Example: Interface`

Endpoint service type.

* Interface: Interface endpoint service.

**ServiceNameSuffix ** String`optional` `Example: tos`

Name suffix of the endpoint service.

After setting the name suffix, the system generates the endpoint service name in the format **com.volces.privatelink.<RegionID\>.<name suffix\>** .

> **tip**

> This parameter is currently in the invite\-only Beta stage. If you need to use different name suffixes to distinguish services, contact your account manager.

**IpAddressVersions.N ** String`optional` `Example: ipv4`

The IP protocol type of the endpoint service. The value can be **ipv4** or **ipv6**.

* The endpoint service defaults to **ipv4**. If you only require **ipv4**, do not pass this parameter.

* If the endpoint service is dual\-stack (**ipv4&ipv6**), this parameter is required. Before passing the parameter, ensure the following conditions are met:

   * The IPv6 functionality for the PrivateLink service has been activated.

   * The specified service resource supports dual\-stack.

* Parameter \- N: Indicates the serial number of the IP protocol type for the endpoint service, with a value range of 1 to 2. The two IP protocol type sequence numbers are separated by ampersands (&).

* Currently, specifying only IPv6 is not supported.

> **tip**

> The PrivateLink IPv6 feature is currently in the invite\-only Beta stage. For trial requests, contact your account manager.

**ServiceResourceType ** String`optional` `Example: CLB`

Service resource type. Valid values:

* CLB: Classic Load Balancer.

* ALB: Application Load Balancer.

* NLB：Network Load Balancer.

> **tip**

> The ALB and NLB service resource support for PrivateLink is in the invite\-only Beta stage. For trial requests, contact your account manager.

**Resources.N.ResourceId ** String必选 `Example: clb-bp1o94dp5i6ea****`

The ID of the service resource to be added to the endpoint service.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to obtain the CLB instance ID.

* N: Indicates the serial number of the service resource. The valid range is 1 to 20.

* Separate multiple service resources with ampersands (&).

**Resources.N.ZoneIds.N ** String`optional` `Example: cn-guangzhou-a`

The availability zones where the CLB provides services.

* This parameter is required when ServiceResourceType is set to **ALB**.

   * The first N indicates the serial number of the resource, ranging from 1 to 20.

   * The second N: Indicates the serial number of the availability zone where the resource provides services, with a value range of 1 to the maximum number of availability zones supported by the service.

* When ServiceResourceType is set to **CLB**, this parameter does not need to be filled, and the primary availability zone of the CLB instance is used by default.

**AutoAcceptEnabled ** Boolean`optional` `Example: false`

Auto\-accept endpoint connection. Valid values:

* true: The endpoint service automatically accepts endpoint connection requests.

* false (default): The endpoint service does not automatically accept endpoint connections; you need to manually accept them by calling the [EnableVpcEndpointConnection](https://docs.byteplus.com/en/docs/privatelink/EnableVpcEndpointConnection) API.

**PrivateDNSEnabled ** Boolean`optional` `Example: false`

Whether to enable private DNS name for the VPC endpoint service.

* false (default): Disable.

* true: Enable.

**PrivateDNSType ** String`optional` `Example: public`

Domain type of the private DNS name.

* public (default): Internet.

> **tip**

> This parameter takes effect when `PrivateDNSEnabled` is set to **true**.

**PrivateDNSName ** String`optional` `Example: www.example.com`

Private DNS name refers to the custom domain name you wish to use when accessing the service via PrivateLink, and it only supports internet domain names.

Internet domain names cannot be set to those already configured for internal (global) resolution, nor to domain names used for PrivateLink (including endpoint service domain names and endpoint domain names).

> **tip**

* > This parameter must be specified when the `PrivateDNSEnabled` parameter is set to **true**.

* > If a wildcard domain such as `*.www.example.com` is provided, both the wildcard domain and its root domain `www.example.com` support resolution.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* This parameter value is auto\-generated by the client to ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If this parameter is not specified, idempotence validation will not be performed.

**Description ** String`optional` `Example: EndpointService`

The description of the endpoint service, with the default value being an empty string.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Length limit: 0 to 255 characters.

**ProjectName ** String`optional` `Example: default`

The name of the project to which the endpoint service belongs.

**Tags.N.Key ** String`optional` `Example: k1`

The tag key for the endpoint service user.

* Length limit: 1 to 128 characters.

* Case\-sensitive and cannot start with `volc:` or `sys:` in any case sensitivity.

* Cannot start or end with a space.

* The tag value can contain letters, numbers, space characters, and the following special characters: _ . : / = + \- @.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: v1`

The tag value for the endpoint service user.

* The length limit: 0 to 255 characters.

* Case\-sensitive. Cannot start or end with a space.

* The tag value can contain letters, numbers, space characters, and the following special characters: _ . : / = + \- @.

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**SupportedRegions.N ** String`optional` `Example: cn-beijing`

Select the service publish region ID.

* Parameter \-N: Indicates the serial number of the region ID. The value range of N is 1 to 20.

* Separate multiple region IDs with ampersands (&).

* The system automatically determines whether the region initiating the request is passed in; if not, it automatically adds it.

* You can see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones) to get the region ID.

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**ServiceId ** String`Example: epsvc-2fe630gurkl37k5gfuy33****`

ID of the endpoint service.

## Request example

```json
GET /?Action=CreateVpcEndpointService&Version=2020-04-01&ServiceType=Interface&ServiceNameSuffix=tos&IpAddressVersions.1=ipv4&IpAddressVersions.2=ipv6&ServiceResourceType=CLB&Resources.1.ResourceId=clb-bp1o94dp5i6ea****&Resources.2.ResourceId=clb-bp1b6c719dfa08ex****&Resources.1.ZoneIds.1=cn-guangzhou-a&Resources.1.ZoneIds.2=cn-guangzhou-b&AutoAcceptEnabled=false&PrivateDNSEnabled=false&PrivateDNSType=public&PrivateDNSName=www.example.com&ClientToken=123e4567-e89b-12d3-a456-42665544****&Description=EndpointService&ProjectName=default&Tags.1.Key=k1&Tags.2.Key=k2&Tags.1.Value=v1&Tags.2.Value=v2 HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn 
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateVpcEndpointService",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain the required parameter. Ensure that all required parameters are provided in the request, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidResource.Disorder |The specified resource index orders are malformed. |The serial number of the specified resource entry is invalid. |
|400 |InvalidServiceResource.Malformed |The specified ServiceResource is malformed. |The specified ServiceResource parameter format is invalid. |
|400 |InvalidServiceResourceType.Malformed |The specified ServiceResourceType is malformed. |The specified ServiceResourceType parameter format is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|400 |IdempotentParameterMismatch |The request uses the same ClientToken as a previous, but non\-identical request. Do not reuse a ClientToken with different requests, unless the requests are identical. |Do not reuse the same ClientToken across different requests, as this request uses a ClientToken identical to another request. |
|400 |InvalidResource.Conflict |The specified resource is duplicated. |The specified resource is duplicated. |
|400 |ErrPrivateLinkServiceNotSupportedZone |The PrivateLink service does not support the zone. |The VPC endpoint service does not support adding service resources from this Availability Zone. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the network interface has been reached. |
|400 |LimitExceed.ServiceResourceNumber |You've reached the limit on the number of service resources that you can operate. |The maximum number of service resources that can be operated on in a single request has been reached. |
|400 |QuotaExceed.EndpointServiceNumber |You've reached the limit on the number of endpoint service instances that you can create. |The quota for the number of endpoint service instances that can be created has been reached. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The maximum number of security groups that can be bound to this network interface has been reached. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of network interfaces that can be associated with the security group has been reached |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|400 |QuotaExceed.ServiceResourceEachZone |You've reached the limit on the number of service resources in the zone that you can create. |The quota limit for the number of service resources that can be created in a single Availability Zone has been reached. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue format is invalid. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |InvalidAccountServiceNameMapping.InvalidStatus |The specified account service name mapping is not in the correct status for the request. |The specified service name mapping is in a status that cannot respond to the request. |
|400 |InvalidPrivateDNSEnabled.PrivateDNSNameMismatch |The specified PrivateDNSEnabled and PrivateDNSName are mismatched. |The specified parameter for whether private DNS is enabled does not match the provided private DNS name. |
|400 |InvalidPrivateDNSName.Malformed |The specified PrivateDNSName is malformed. |The specified PrivateDNSName parameter format is invalid. |
|400 |InvalidServiceNameSuffix.Malformed |The specified ServiceNameSuffix is malformed. |The specified ServiceNameSuffix parameter format is invalid. |
|400 |ServiceNameSuffixExist |The specified service name suffix already exists. |The specified service name suffix already exists. |
|400 |InvalidPrivateDNSEnabled.PrivateDNSTypeMismatch |The specified PrivateDNSEnabled and PrivateDNSType are mismatched. |The specified parameter PrivateDNSEnabled does not match the PrivateDNSType. |
|400 |InvalidPrivateDNSType.Malformed |The specified PrivateDNSType is malformed. |The specified PrivateDNSType parameter format is invalid. |
|400 |InvalidIpAddressVersions.Conflict |The specified IpAddressVersions parameter is duplicated. |The specified IpAddressVersions is duplicated. |
|400 |InvalidServiceResourceStatus.IPVersionMismatch |The specified service resource can not support the EndpointService ipAddressVersion that you want. |The current service resource does not support the specified endpoint service IP address type. |
|400 |InvalidIpAddressVersions.Malformed |The specified IpAddressVersions is malformed. |The specified IpAddressVersions parameter format is invalid. |
|400 |ServiceLinkRoleNotAuthorized |The service role for PrivateLink has not been authorized. |Please first authorize the service\-associated role for PrivateLink. |
|400 |InvalidLocation.Intercepted |The specified action has been intercepted by location. |The current account does not have operation permissions in the specified region. Please request to be added to the allowlist. |
|400 |InvalidApplicationLoadBalancer.InvalidZoneInfo |The specified Application LoadBalancer zone attributes is invalid. |The specified Availability Zone information for the ALB is invalid. |
|400 |InvalidZoneforALB.conflict |The application load balancer does not support the zone. |The specified ALB instance does not support this Availability Zone. |
|400 |InvalidPrivateDNSType.ServiceOwnerMismatch |The specified service owner can not support the EndpointService PrivateDNS type that you want. |The specified private DNS type is not supported by the current service owner. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |No permission to perform this operation on the specified service. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|404 |InvalidServiceNameSuffix.NotFound |The specified ServiceNameSuffix does not exist. |The specified service name suffix does not exist. |
|412 |IdempotentProcessing |The request uses the same ClientToken as a previous one that is still in process. |The idempotent request is in process. |
