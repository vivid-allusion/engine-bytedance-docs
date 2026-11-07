---
title: "AssignIpv6Addresses - Allocating the private IPv6 address"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses"
---

Call the AssignIpv6Addresses API to assign private IPv6 addresses to a specified (primary or secondary) network interface (ENI).

> **tip**

> IPv6 is currently in the invite\-only Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssignIpv6Addresses&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: AssignIpv6Addresses`

API name. The current API name is `AssignIpv6Addresses`.

**Version ** String必选`Example: 2020-04-01`

The API version. The current API version is `2020-04-01`.

**NetworkInterfaceId ** String必选 `Example: eni-bp1fg655nh68xyz9****`

ENI ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ENI ID.

**Ipv6AddressCount ** Integer`optional` `Example: 2`

The number of private IPv6 addresses to assign to the ENI. If this parameter is provided, the system will automatically allocate the specified number of available IP addresses from the ENI's subnet as its private IPv6 addresses.

> **tip**

> You must provide either the `Ipv6Address.N` parameter or the `Ipv6AddressCount` parameter, but not both.

**Ipv6Address.N ** String`optional` `Example: 2408:4008:55b:XXXX:XXXX:922:96c4:e0`

Assign a private IPv6 address to the network interface.

* N: Indicates the serial number of the private IPv6 address, and its range of values is determined by the ENI status.

   * When the ENI is in the Available (unattached) state, the value range is 1 to 10.

   * When the ENI is in the InUse (attached) state, the value range for N is constrained by the instance type specifications. For more details, please see the [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* Separate multiple private IPv6 addresses with ampersands ( & ).

* The specified private IPv6 addresses must be available addresses within the ENI's subnet.

> **tip**

> You must provide either the `Ipv6Address.N` parameter or the `Ipv6AddressCount` parameter, but not both.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**NetworkInterfaceId ** String`Example: eni-bp1fg655nh68xyz9****`

ENI ID.

**Ipv6Set ** String[]`Example: 2408:4008:55b:XXXX:XXXX:922:96c4:e0`

IPv6 address list.

## Request example

```json
GET /?Action=AssignIpv6Addresses&Version=2020-04-01&NetworkInterfaceId=eni-bp1fg655nh68xyz9****&Ipv6AddressCount=2 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AssignIpv6Addresses",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv6Set": [
            ""
        ],
        "NetworkInterfaceId": "eni-bp1fg655nh68xyz9****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of ENI cannot process this request. |
|400 |InvalidEniIp.Malformed |The specified elastic network interface ip is malformed. If you are specifying an IP of an elastic network interface, ensure it must fall into the range of the CIDR block of the subnet to which the elastic network interface belongs to. |The specified ENI IP is invalid. Please ensure the ENI IP falls within the CIDR range of its subnet. |
|400 |InvalidEniIpPrefix.Malformed |The specified elastic network interface IP prefix is malformed. ensure it must fall into the range of the CIDR block of the subnet. |The specified ENI IP prefix is invalid. Please ensure the ENI IP prefix falls within the CIDR range of its subnet. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS instance is in a state that cannot process this request. |
|400 |InvalidIp.Malformed |The specified ip is malformed. |The specified IP is invalid. |
|400 |InvalidIpv6.Malformed |The specified IPv6 address is malformed. |The specified IPv6 address is invalid. |
|400 |InvalidIpv6Prefix.Malformed |The specified ipv6 prefix is malformed. |The specified IPv6 prefix is invalid. |
|400 |InvalidParameter.EnableIpv6 |The EnableIpv6 parameter is currently not supported. |The EnableIpv6 request parameter is not currently supported. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |InvalidSubnet.DisableIpv6 |Specified subnet disable IPv6 |This subnet does not have IPv6 enabled. |
|400 |LimitExceeded.Ipv6AddressesPerEni |You've reached the limit on the number of IPv6 addresses per ENI that you can assign. |The maximum number of assignable IPv6 addresses for the ENI has been reached. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the ENI has been reached. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|403 |Forbidden.IpPrefix |You are not authorized to allocate ip prefix. |You do not have permission to assign ENI prefixes. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The owner of the specified elastic network interface is not in sharing. |No permission to perform actions on the specified ENI. The specified ENI is not owned by a user in the sharing list. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified ENI. The specified ENI is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|409 |InvalidIPv4Prefix.Conflict |The specified IPv4 prefix is in use. |The specified IPv4 prefix is in use. |
|409 |InvalidIPv6Prefix.Conflict |The specified IPv6 prefix is in use. |The specified IPv6 prefix is currently in use. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
|409 |InvalidIpPrefix.Conflict |The parameters for IP prefix number and IP prefixes cannot be specified at the same time. |The request cannot include both an IP prefix count and specific IP prefixes simultaneously. |
|409 |InvalidParameter.ParameterConflict |The parameters for IP address number and IP addresses cannot be specified at the same time. |The request cannot include both an IP address count and specific IP addresses simultaneously. |
