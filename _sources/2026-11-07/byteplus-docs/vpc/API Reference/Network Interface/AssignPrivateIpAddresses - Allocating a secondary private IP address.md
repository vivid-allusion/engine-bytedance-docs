---
title: "AssignPrivateIpAddresses - Allocating a secondary private IP address"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses"
---

Call the AssignPrivateIpAddresses API to allocate secondary private IPv4 addresses to (primary/secondary) network interfaces (ENI).

## Instructions

* [BytePlus Official service network interfaces](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview#.572R5Y2h57G75Z6L) do not support allocating secondary private IPv4 addresses.

* Only secondary network interfaces in `Available` or `InUse` status can be allocated secondary private IPv4 addresses.

* When allocating secondary private IPv4 addresses from a primary ENI, the instance to which the primary ENI belongs must be in the `RUNNING` or `STOPPED` state.

* When a secondary ENI is in the `Available` state, it can be assigned up to 49 secondary private IPv4 addresses. When a secondary ENI is in the `InUse` (attached) state, the number of assignable secondary private IPv4 addresses is limited by the specifications of the instance it is attached to.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssignPrivateIpAddresses&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选`Example: AssignPrivateIpAddresses`

The interface name. The current API name is `AssignPrivateIpAddresses`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**NetworkInterfaceId ** String必选 `Example: eni-bp67acfmxazb4p****`

ENI ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ENI ID.

**PrivateIpAddress.N ** String`optional` `Example: 192.168.XX.10`

Specify the IP addresses and the quantity of private IP addresses for the ENI.

* N: Indicates the serial number of the private IPv4 address, and its range of values is determined by the network interface status.

   * When the ENI is in the Available (unattached) state, the value range is 1 to 49.

   * When the ENI is in the InUse (attached) state, the value range for N is constrained by the instance type specifications. For more details, please see the [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* Separate multiple private IPv4 addresses with ampersands (&).

* The specified private IPv4 addresses must be available addresses within the ENI's subnet.

> **tip**

> You must provide either the `PrivateIpAddress.N` parameter or the `SecondaryPrivateIpAddressCount` parameter, but not both.

**SecondaryPrivateIpAddressCount ** Integer`optional` `Example: 1`

The number of secondary private IPv4 addresses to assign to the ENI. If this parameter is provided, the system will automatically allocate the corresponding number of available IP addresses from the ENI's subnet as its secondary private IPv4 addresses.

> **tip**

> You must provide either the `PrivateIpAddress.N` parameter or the `SecondaryPrivateIpAddressCount` parameter, but not both.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**Ipv4Prefix.N ** String`optional` `Example: ["192.168.1.32/28"]`

Assign the /28 IPv4 CIDR block to the ENI.

> **tip**

> This parameter cannot be specified together with any of the following parameters

* > Ipv4PrefixCount

* > PrivateIpAddress.N

* > SecondaryPrivateIpAddressCount

* > This parameter is currently in the invite\-only Beta stage. For trial requests, contact your account manager.

**Ipv4PrefixCount ** Integer`optional` `Example: 1`

Specify the number of /28 IPv4 CIDR blocks to be automatically assigned by the system.

> **tip**

> This parameter cannot be specified together with any of the following parameters

* > Ipv4Prefix.N

* > PrivateIpAddress.N

* > SecondaryPrivateIpAddressCount

* > This parameter is currently in the invite\-only Beta stage. For trial requests, contact your account manager.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 473469C7-AA6F-4DC5-B3DB-A3DC0DE3****`

The request ID.

**NetworkInterfaceId ** String`Example: eni-bp125p95hhdhn3ot****`

ENI ID.

**PrivateIpSet ** String[]`Example: 192.168.XX.10`

The collection of secondary private IPv4 addresses for the ENI.

## Request example

```json
GET /?Action=AssignPrivateIpAddresses&Version=2020-04-01&NetworkInterfaceId=eni-bp67acfmxazb4p****&PrivateIpAddress.1=192.168.XX.10&PrivateIpAddress.2=192.168.XX.12 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AssignPrivateIpAddresses",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkInterfaceId": "eni-bp125p95hhdhn3ot****",
        "PrivateIpSet": [
            ""
        ],
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |InvalidEni.IPv4Disabled |IPv4 has been disabled for the specified ENI. |IPv4 has been disabled for the specified ENI. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of ENI cannot process this request. |
|400 |InvalidEniIp.Malformed |The specified elastic network interface ip is malformed. If you are specifying an IP of an elastic network interface, ensure it must fall into the range of the CIDR block of the subnet to which the elastic network interface belongs to. |The specified ENI IP is invalid. Please ensure the ENI IP falls within the CIDR range of its subnet. |
|400 |InvalidEniIpPrefix.Malformed |The specified elastic network interface IP prefix is malformed. ensure it must fall into the range of the CIDR block of the subnet. |The specified ENI IP prefix is invalid. Please ensure the ENI IP prefix falls within the CIDR range of its subnet. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS instance is in a state that cannot process this request. |
|400 |InvalidIp.Malformed |The specified ip is malformed. |The specified IP is invalid. |
|400 |InvalidIpPrefix.Malformed |The specified ipv4 prefix is malformed. |The specified IPv4 prefix is invalid. |
|400 |InvalidIpv6.Malformed |The specified IPv6 address is malformed. |The specified IPv6 address is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |LimitExceeded.Ipv6AddressesPerEni |You've reached the limit on the number of IPv6 addresses per ENI that you can assign. |The maximum number of assignable IPv6 addresses for the ENI has been reached. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the ENI has been reached. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|403 |Forbidden.IpPrefix |You are not authorized to allocate ip prefix. |You do not have permission to assign ENI prefixes. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The owner of the specified elastic network interface is not in sharing. |No permission to perform actions on the specified ENI. The specified ENI is not owned by a user in the sharing list. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified ENI. The specified ENI is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|409 |InvalidIPv4Prefix.Conflict |The specified IPv4 prefix is in use. |The specified IPv4 prefix is currently in use. |
|409 |InvalidIPv6Prefix.Conflict |The specified IPv6 prefix is in use. |The specified IPv6 prefix is in use. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
|409 |InvalidIpPrefix.Conflict |The parameters for IP prefix number and IP prefixes cannot be specified at the same time. |The request cannot include both an IP prefix count and specific IP prefixes simultaneously. |
|409 |InvalidParameter.ParameterConflict |The parameters for IP address number and IP addresses cannot be specified at the same time. |The request cannot include both an IP address count and specific IP addresses simultaneously. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
