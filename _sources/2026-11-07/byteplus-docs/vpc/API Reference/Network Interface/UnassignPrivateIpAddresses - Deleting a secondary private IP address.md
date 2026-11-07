---
title: "UnassignPrivateIpAddresses - Deleting a secondary private IP address"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses"
---

Call the UnassignPrivateIpAddresses API to release the private IPv4 address from the specified network interface.

## Instructions

* The primary network interface can release secondary private IPv4 addresses only when its status is RUNNING or STOPPED.

* The secondary network interface can release secondary private IPv4 addresses only when its status is Available or InUse.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UnassignPrivateIpAddresses&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: UnassignPrivateIpAddresses`

The interface name. The current API name is `UnassignPrivateIpAddresses`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**NetworkInterfaceId**String必选`Example value: eni-bp67acfmxazb4p****`

Network Interface ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the network interface ID.

**PrivateIpAddress.N ** String必选 `Example value: 192.168.XX.10`

Secondary private IPv4 address of the network interface to be released.

* N: Indicates the serial number of the secondary private IPv4 address.

* Separate multiple secondary private IPv4 addresses with ampersands ( & ).

**ClientToken ** String`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example value: 473469C7-AA6F-4DC5-B3DB-A3DC0DE3****`

Request ID.

## Request examples

```JSON
GET /?Action=UnassignPrivateIpAddresses&Version=2020-04-01&NetworkInterfaceId=eni-bp67acfmxazb4ph****&PrivateIpAddress.1=192.168.XX.10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UnassignPrivateIpAddresses",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3****"
    }
}
```

## Error codes

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidAnycastEip.InvalidStatus |The specified anycast elastic IP address is not in the correct status for the request. |The specified Anycast EIP is in a status that cannot respond to this request. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of elastic network interface cannot process this request. |
|400 |InvalidIpPrefix.Malformed |The specified ipv4 prefix is malformed. |The specified IPv4 prefix is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |InvalidVpcEip.InUse |The specified vpc eip is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The owner of the specified elastic network interface is not in sharing. |No permission to perform actions on the specified elastic network interface. The specified Elastic Network Interface (ENI) is not owned by a user in the sharing list. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified elastic network interface does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
