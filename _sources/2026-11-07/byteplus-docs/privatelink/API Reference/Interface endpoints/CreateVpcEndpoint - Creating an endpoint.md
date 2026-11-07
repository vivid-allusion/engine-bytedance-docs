---
title: "CreateVpcEndpoint - Creating an endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint"
---

Call the CreateVpcEndpoint API to create an endpoint.

> When calling this API to create an endpoint, the state of the endpoint instance transitions as follows: Creating \> Available.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpcEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: CreateVpcEndpoint`

Action to execute. Set the value to **CreateVpcEndpoint**.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.

**VpcId ** String必选 `Example: vpc-bp15zkdt37pq72zv****`

The ID of the VPC to which the endpoint belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC ID.

**SecurityGroupIds.N ** String`optional` `Example: sg-bp67acfmxazb4p****`

The ID of the security group to be associated with the endpoint.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to obtain the Security Group ID.

* Parameter \-N: Represents the serial number of the security group ID, with a range of 1 to 5.

* Separate multiple security group IDs with ampersands ( & ).

**ServiceId ** String必选 `Example: epsvc-2fe630gurkl37k5gfuy33****`

The ID of the endpoint service to be associated.

You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get the ID of the endpoint service.

**Zones.N.SubnetId ** String`optional` `Example: subnet-bp15zckdt37pq72zv****`

The ID of the subnet to which the endpoint ENI to be created belongs.

You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to obtain the subnet ID.

* Parameter \-N: Indicates the serial number of the subnet ID, ranging from 1 to 10.

* Separate multiple subnet IDs with ampersands (&).

**Zones.N.ZoneId ** String`optional` `Example: cn-guangzhou-a`

The ID of the availability zone to which the endpoint ENI to be created belongs. For more information, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones).

* Parameter \-N: Indicates the serial number of the availability zone, ranging from 1 to 10.

* Separate multiple availability zone IDs with ampersands ( & ).

**EndpointName ** String`optional` `Example: endpoint-01`

Name of the endpoint.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If left blank, this defaults to the ID of the endpoint.

**ServiceName ** String`optional` `Example: com.volces.privatelink.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****`

The name of the endpoint service to be associated. Format: com.volces.privatelink. *<regionID\>* . *<endpointserviceID\>* .

**IpAddressVersions.N ** String`optional` `Example: ipv4`

The IP protocol type of the interface endpoint. The value can be **ipv4** or **ipv6**.

* The interface endpoint defaults to **IPv4**. If you only require **IPv4**, do not pass this parameter.

* If the interface endpoint is dual\-stack (**IPv4 & IPv6**), this parameter must be passed. Before passing the parameter, ensure the following conditions are met:

   * Your account has the IPv6 feature for the PrivateLink service enabled.

   * The subnet to which the interface endpoint belongs has the IPv6 CIDR block enabled.

   * The endpoint service associated with the interface endpoint is of the dual\-stack type.

* Parameter \- N: Represents the serial number of the IP protocol type for the interface endpoint. The value ranges from 1 to 2, and the serial numbers for the two IP protocol types are separated by &.

* Currently, specifying only IPv6 is not supported.

> **tip**

> The PrivateLink IPv6 feature is currently in Beta stage. For trial requests, contact your account manager.

**Zones.N.PrivateIpAddress ** String`optional` `Example: 172.XX.XX.2`

The private IPv4 address of the endpoint network interface must fall within the IPv4 CIDR block of the subnet. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to get the CIDR block of the subnet.

* Parameter \-N: Represents the serial number of the private IPv4 address, ranging from 1 to 10.

* Separate multiple private IPv4 addresses with ampersands ( & ).

**Zones.N.PrivateIpv6Address ** String`optional` `Example: 2408::153:3921:XX:XX:7b12:1c5f`

The private IPv6 address of the endpoint network interface must fall within the IPv6 CIDR block of the subnet. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to get the CIDR block of the subnet.

* Parameter \-N: Indicates the serial number of the private IPv6 address, ranging from 1 to 10.

* Separate multiple private IPv6 addresses with ampersands (&).

* If left blank, an IPv6 address will be randomly assigned from within the subnet IPv6 CIDR block by default.

**PrivateDNSEnabled** Boolean `optional` `Example: false`

Enable private DNS name.

* false (default): Disable.

* true: Enabled.

> **tip**

* > The private DNS name of the VPC endpoint service must have a verification status of Verified before it can be enabled. You can call the [DescribeVpcEndpointServiceAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServiceAttributes) API to check the private DNS name verification status of the endpoint service.

* > When enabled, the private DNS name of the endpoint defaults to the private DNS name of its associated endpoint service.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

The Client Token that is used to ensure the request idempotency.

* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.

**Description ** String`optional` `Example: Endpoint`

The description of the endpoint. The default value is an empty string.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

**ProjectName ** String`optional` `Example: default`

Name of the project to which the endpoint belongs.

**Tags.N.Key ** String`optional` `Example: k1`

The tag key of the endpoint user tag.

* The length limit is 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: v1`

The tag value of the endpoint user tag.

* The length limit is 0 to 256 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**ServiceRegion ** String必选 `Example: cn-beijing`

The region to which the endpoint service belongs. For region IDs, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones).

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**Endpoint ID** String `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

## Request examples

```json
GET /?Action=CreateVpcEndpoint&Version=2020-04-01&VpcId=vpc-bp15zkdt37pq72zv****&SecurityGroupIds.1=sg-bp67acfmxazb4p****&SecurityGroupIds.2=sg-bp1gxw6bznjjvhu3****&ServiceId=epsvc-2fe630gurkl37k5gfuy33****&Zones.1.SubnetId=subnet-bp15zckdt37pq72zv****&Zones.2.SubnetId=subnet-1g0f7rju1txj48ibuxxob****&Zones.1.ZoneId=cn-guangzhou-a&Zones.2.ZoneId=cn-guangzhou-b HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateVpcEndpoint",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "EndpointId": "ep-273yuq6q7bgn47fap8squ****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |EndpointServiceNotAuthorized |The specified endpoint service is not authorized to user. |The endpoint service is not authorized for the user. |
|400 |EndpointZoneDuplicated |The specified zone is duplicated for the Endpoint. |The availability zones of the endpoint service are duplicated. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The specified Description parameter format is invalid. |
|400 |InvalidIP.Malformed |The specified IP is malformed. |The specified IP parameter format is invalid. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |IdempotentParameterMismatch |The request uses the same ClientToken as a previous, but non\-identical request. Do not reuse a ClientToken with different requests, unless the requests are identical. |Do not reuse the same ClientToken across different requests, as this request uses a ClientToken identical to another request. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidPrivateDNS.UnsupportedOperation |The request on the specified PrivateDNS is denied due to the PrivateDNS is disabled. |The request was rejected because the Private DNS feature is not enabled. |
|400 |LimitExceed.SecurityGroupNumber |You've reached the limit on the number of security groups that you can operate. |You have reached the maximum number of security groups that can be operated on in a single request. |
|400 |LimitExceed.ZoneNumber |You've reached the limit on the number of zones that you can operate. |You have reached the maximum number of availability zones that can be operated on in a single request. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the network interface has been reached. |
|400 |InvalidSecurityGroup.Conflict |The specified security group is duplicated. |The specified security groups are duplicated. |
|400 |InvalidZone.Conflict |The specified zone is duplicated. |Duplicate Availability Zones specified. |
|400 |InvalidZone.Disorder |The specified zone index orders are malformed. |The specified availability zone entry serial number is invalid. |
|400 |ServiceLinkRoleNotAuthorized |The service role for Private Link has not been authorized. |Please first authorize the service\-associated role for PrivateLink. |
|400 |ErrEndpointServiceNotSupportedZone |The specified endpoint service does not support the zone. |The specified endpoint service does not support the current Availability Zone. |
|400 |QuotaExceed.EndpointNumber |You've reached the limit on the number of endpoint instances that you can create. |The quota limit for the number of endpoints that can be created has been reached. |
|400 |QuotaExceed.EndpointEachVpc |You've reached the limit on the number of endpoint instances that you can create in the specified VPC. |The quota limit for the number of endpoints that can be created in the specified VPC has been reached. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The maximum number of security groups that can be bound to this network interface has been reached. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of network interfaces that can be associated with the security group has been reached |
|400 |QuotaExceeded.Eni |ENI number exceeded quota. |You have reached the maximum of network interfaces that you can create. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified security group and endpoint are not in the same VPC. |The specified security group and endpoint are not in the same VPC. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |OrderError.OrderInOneStep |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |ErrPrivateZoneExisted |The vpc and the private dns have created the private zone. |Private DNS resolution has already been configured for this VPC and DNS domain. |
|400 |InvalidEndpointZoneIPVersion.AddressMismatch |The specified EndpointZone AddressIPVersion and address are not matched. |The specified availability zone address for the VPC endpoint does not match its IP address type. |
|400 |InvalidIpAddressVersions.Conflict |The specified IpAddressVersions parameter is duplicated. |The specified IpAddressVersions is duplicated. |
|400 |InvalidIpAddressVersions.Malformed |The specified IpAddressVersions is malformed. |The specified IpAddressVersions parameter format is invalid. |
|400 |InvalidEndpointIpAddressVersions.EndpointServiceMisMatch |The IpAddressVersions of associated EndpointService and Endpoint mismatch. |The IP address type of the endpoint does not match the associated endpoint service. |
|400 |InvalidIPv6Address.Malformed |The specified IPv6Address is malformed. |The specified IPv6Address parameter format is invalid. |
|400 |InvalidAccount.SecurityGroupMisMatch |The specified account and security group don't match. |The specified account and security group do not match. |
|400 |InvalidEndpoint.ServiceMisMatch |The specified endpoint and service don't match. |The specified endpoint and endpoint service do not match. |
|400 |InvalidVpcAccount.Mismatched |The specified VPC and account don't match. |The specified VPC and account do not match. |
|400 |InvalidLocation.Intercepted |The specified action has been intercepted by location. |The current account does not have operation permissions in the specified region. Please request to be added to the allowlist. |
|400 |InvalidServiceManaged.Conflict |The specified endpoint is not service\-managed. |Only managed endpoints support binding to managed security groups. |
|400 |PrivateDNSNameConflictwithPrivateZone |The specified private DNS name already exists private zone in the VPC. |The specified private DNS name already exists for PrivateZone within this VPC. |
|400 |InvalidEndpointZoneIPVersion.SubnetMismatch |The specified EndpointZone Subnet and Endpoint IPAddressVersion are not matched. |The specified availability zone subnet for the VPC endpoint does not match its IP address type. |
|403 |Forbidden.ServiceManagedEndpoint |You are not authorized to perform operations on the service managed endpoint. |You do not have permission to perform operations on the service\-managed endpoint. |
|403 |Forbidden.ServiceManagedEndpointService |You are not authorized to perform operations on the service managed endpoint service. |You do not have permission to perform operations on the service\-managed endpoint service. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidVpc.NotFound |The specified vpc does not exist. |The specified VPC does not exist. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
|409 |InvalidVpcPrivateDNSName.Conflict |The specified PrivateDNSName in single vpc and single endpoint service already exists. |The specified private DNS name already exists under the same VPC and the same endpoint service. |
|412 |IdempotentProcessing |The request uses the same ClientToken as a previous one that is still in process. |The idempotent request is in progress. |
|500 |NetworkInterfaceCreateFailed |The network interface create failed. |Failed to create the network interface in the availability zone. |
|500 |PrivateZoneCreateFailed |The private zone create failed. |PrivateZone creation failed. |
|500 |PrivateZoneQueryFailed |Failed to query private zone. |Failed to query PrivateZone. |
