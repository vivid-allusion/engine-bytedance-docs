---
title: "ModifyVpcAttributes - Modifying the VPC information"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes"
---

Call the ModifyVpcAttributes API to modify the Virtual Private Cloud (VPC) information.

> **tip**

> IPv6 is currently in the invite\-only Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

## Instructions

* If the following optional parameters are not configured, the existing configurations will be preserved.

* ModifyVpcAttributes is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) API to check the VPC status. `Pending` means configuring, and `Available` means configuration is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpcAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifyVpcAttributes`

The API name. The current API name is `ModifyVpcAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current API version is `2020-04-01`.

**VpcId ** String必选 `Example: vpc-bp15zct37pq72zv****`

The ID of the VPC for which to modify information.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**VpcName ** String`optional` `Example: Vpc-1`

Name of the VPC.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).

* Cannot start with `http://` or `https://`.

**Description ** String`optional` `Example: This is my VPC.`

Description of the VPC.

* Length limit: 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include English commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Cannot start with `http://` or `https://`.

**DnsServers.N ** String`optional` `Example: 12.XX.XX.5`

DnsServers of the VPC.

* Parameter \- N: Represents the serial number of a DNS server address. A maximum of 5 addresses can be specified per single API call. Each DnsServer must be provided as a valid IP address.

* Separate multiple IP addresses with ampersands ( & ).

**EnableIpv6 ** Boolean`optional` `Example: true`

Enable or disable IPv6.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Enable.

* false: Disable. This value can only be configured when all subnets under the VPC have IPv6 disabled and the VPC is not associated with an IPv6 gateway.

**Ipv6Isp ** String`optional` `Example: ChinaMobile`

ISP. Valid values:

* BGP: BGP (multi\-line).

* ChinaMobile: China Mobile static single\-ISP.

* ChinaTelecom: China Telecom static single\-ISP.

* ChinaUnicom: China Unicom static single\-ISP.

* ChinaMobile_Value: The static preferential single ISP provided by China Mobile.

* ChinaUnicom_Value: The static preferential single ISP provided by China Unicom.

* ChinaTelecom_Value: The static preferential single ISP provided by China Telecom.

> **tip**

> Except for BGP (multi\-line), all other ISPs are only supported in the China (Shanghai) region.

**Ipv6MaskLen ** Integer`optional` `Example: 62`

Mask length of the IPv6 CIDR block.

* When Ipv6Isp is set to BGP, only a prefix length of /56 is supported. Otherwise, this parameter supports /62 to /64.

* After the parameter Ipv6CidrBlock is provided, this parameter does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

**Ipv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/56`

IPv6 CIDR block of the VPC.

* When this parameter is provided, the Ipv6MaskLen parameter does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

* If the Ipv6Isp parameter is not provided or is set to BGP, and this parameter is not provided, the system will automatically assign an IPv6 CIDR block.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=ModifyVpcAttributes&Version=2020-04-01&VpcId=vpc-bp15zct37pq72zv****&VpcName=vpc-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyVpcAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InsufficientIpv6Blocks |The specified pool does not contain enough free IPv6 blocks to fulfill your request. |The IPv6 pool has insufficient IPv6 address range resources. |
|400 |InvalidCen.VpcPeeringConnectionActive |The specified VPC peering connection has been created. |The specified VPC has already established a peering connection and does not support association with a Cloud Enterprise Network (CEN). |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCoreNetwork.Conflict |The added core network IDs is conflict with current IDs. |The core network ID to be added conflicts with an existing one. |
|400 |InvalidCoreNetwork.NotExist |The removed core network IDs does not exist in current IDs. |The core network ID to be removed does not exist in the existing IDs. |
|400 |InvalidCoreNetwork.Repeated |The core network IDs in the parameter is repeated. |There are duplicate core network IDs in the parameters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|400 |InvalidEnableIpv6 |Repeat enable vpc IPv6 |The VPC already has IPv6 enabled and cannot be re\-enabled. |
|400 |InvalidIpv6CidrBlock.NotReserved |The specified IPv6 CIDR block is not reserved. |The specified IPv6 address range is not reserved. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.EnableIpv6 |The EnableIpv6 parameter is currently not supported. |The EnableIpv6 request parameter is not currently supported. |
|400 |InvalidParameter.MaskLength |The IPv6 mask length in this request is invalid. |The IPv6 mask length in this request is invalid. |
|400 |InvalidTransitRouter.Repeated |The transit router IDs in the parameter is repeated. |Duplicate transit router IDs were found in the parameters. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of an IPv6 route entry. |The specified VPC contains IPv6 routes and cannot be modified. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of an IPv6\-enabled subnet. |The specified VPC contains subnets with IPv6 enabled and cannot be modified. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of an Ipv6Gateway. |The specified VPC contains an IPv6 gateway and cannot be deleted. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |InvalidVpc.RoutePropagationModeConflict |The specified route propagation mode conflicts with the current VPC route propagation mode. |The specified route propagation mode conflicts with the route propagation mode of the current VPC. |
|400 |InvalidVpcDnsServerIpAddress.Malformed |The specified DNS server IP address is malformed. |The specified DNS server IP address format is invalid. |
|400 |LimitExceeded.VpcDnsServerNumber |You've reached the limit on the number of DNS servers that you can add. |Reached the maximum DNS servers that you can add. |
|400 |QuotaExceeded.SystemRouteEntry |You've reached the limit on the number of system route entries per route table. |The maximum number of system routes that you can create has been reached. |
|400 |QuotaExceeded.VpcIpv6Cidr |You've reached the limit on the number of IPv6 CIDR blocks per VPC that you can create. |The maximum number of IPv6 CIDR blocks allowed for the specified VPC has been reached. |
|403 |Forbidden.Ipv6IspType |You are not authorized to create this type IPv6 CIDR. |You do not have permission to create an IPv6 CIDR block for the specified ISP type. |
|404 |InvalidIpv6Pool.NotFound |The specified IPv6 pool does not exist. |The specified IPv6 pool does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
