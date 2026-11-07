---
title: "AddZoneToVpcEndpoint - Adding an availability zone to endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/AddZoneToVpcEndpoint"
---

Call the AddZoneToVpcEndpoint API to add an Availability Zone to the specified endpoint. For operational instructions and precautions, see [Modifying an availability zone](https://docs.byteplus.com/en/docs/privatelink/Modifying-Availability-Zones).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddZoneToVpcEndpoint&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: AddZoneToVpcEndpoint`

Action to execute. Set the value to **AddZoneToVpcEndpoint**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**EndpointId ** String必选 `Example: ep-273yuq6q7bgn47fap8squ****`

The ID of the endpoint.

You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the ID of the endpoint.

**ZoneId ** String必选 `Example: cn-guangzhou-a`

The ID of the availability zone to which the endpoint network interface belongs. For more information, see [Regions and Availability Zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones).

**SubnetId ** String必选 `Example: subnet-1g0f7rju1txj48ibuxxob****`

The ID of the subnet to which the endpoint network interface belongs.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to obtain the subnet ID.

**PrivateIpAddress ** String`optional` `Example: 172.XX.XX.2`

The private IPv4 address of the endpoint network interface must fall within the IPv4 CIDR block of the subnet. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to get the CIDR block of the subnet.

**PrivateIpv6Address ** String`optional` `Example: 2408::153:3921:XX:XX:7b12:1c5f`

The private IPv6 address of the endpoint network interface must fall within the IPv6 CIDR block of the subnet. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to get the CIDR block of the subnet.

> **tip**

> This parameter is in the beta stage. If you need a trial, please contact your account manager.

## Response parameters

**RequestId ** String`optional` `Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

## Request examples

```JSON
GET /?Action=AddZoneToVpcEndpoint&Version=2020-04-01&EndpointId=ep-273yuq6q7bgn47fap8squ****&ZoneId=cn-guangzhou-a&SubnetId=subnet-1g0f7rju1txj48ibuxxob**** HTTP/1.1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AddZoneToVpcEndpoint",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidIP.Malformed |The specified IP is malformed. |The specified IP parameter format is invalid. |
|400 |EndpointZoneDuplicated |The specified zone is duplicated for the Endpoint. |The availability zones of the endpoint service are duplicated. |
|400 |InvalidEndpoint.InvalidStatus |The specified endpoint is not in the correct status for the request. |The specified endpoint is in a status that cannot respond to this request. |
|400 |ErrEndpointServiceNotSupportedZone |The specified endpoint service does not support the zone. |The specified endpoint service does not support the current Availability Zone. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InvalidEndpointIpAddressVersions.EndpointServiceMisMatch |The IpAddressVersions of associated EndpointService and Endpoint mismatch. |The IP address type of the endpoint does not match the associated endpoint service. |
|400 |InvalidEndpointService.InvalidLock |The operation is refused by the endpoint service. |This operation is not supported for the endpoint service. |
|400 |InvalidZone.Conflict |The specified zone is duplicated. |Duplicate Availability Zones specified. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the network interface has been reached. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The maximum number of security groups that can be bound to this network interface has been reached. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of network interfaces that can be associated with the security group has been reached |
|400 |QuotaExceeded.Eni |ENI number exceeded quota. |You have reached the maximum of network interfaces that you can create. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|400 |InvalidEndpointZoneIPVersion.AddressMismatch |The specified EndpointZone AddressIPVersion and address are not matched. |The specified availability zone address for the VPC endpoint does not match its IP address type. |
|400 |InvalidIPv6Address.Malformed |The specified IPv6Address is malformed. |The specified IPv6Address parameter format is invalid. |
|400 |InvalidPrivateDNSName.Conflict |The PrivateDNSName of associated EndpointService and Endpoint mismatch. |The DNS name of the endpoint does not match the associated endpoint service. |
|400 |InvalidPrivateDNS.UnsupportedOperation |The request on the specified PrivateDNS is denied due to the PrivateDNS is disabled. |The request was rejected because the Private DNS feature is not enabled. |
|400 |InvalidLocation.Intercepted |The specified action has been intercepted by location. |The specified operation has been intercepted by Location. |
|400 |InvalidEndpoint.ServiceDeleted |The specified endpoint's service has been deleted for the request. |The specified endpoint's associated endpoint service has been deleted, and the request cannot be processed. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidEndpoint.NotFound |The specified endpoint does not exist. |The specified endpoint does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidEndpointZone.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|404 |InvalidEndpointService.NotFound |The specified EndpointService does not exist. |The specified endpoint service does not exist. |
|409 |InvalidSecurityGroupId.Conflict |The specified security group is duplicated with another security group associated with the same elastic network interface. |The specified security group is already associated with this network interface and cannot be bound again. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
