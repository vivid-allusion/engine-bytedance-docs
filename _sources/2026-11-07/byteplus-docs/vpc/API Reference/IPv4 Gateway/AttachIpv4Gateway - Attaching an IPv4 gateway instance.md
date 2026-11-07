---
title: "AttachIpv4Gateway - Attaching an IPv4 gateway instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AttachIpv4Gateway"
---

Call the AttachIpv4Gateway API to associate the IPv4 Gateway with the VPC.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AttachIpv4Gateway&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: AttachIpv4Gateway`

The interface name. The current API name is `AttachIpv4Gateway`.

**Version ** String必选 ` Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**Ipv4GatewayId ** String必选 `Example value: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the ID of IPv4 Gateway.

**VpcId ** String必选 `Example value: vpc-bp15zkdt37pq72zv****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**ClientToken ** String`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=AttachIpv4Gateway&Version=2020-04-01&Ipv4GatewayId=ipv4gw-bp1fgnh68xyz9****&VpcId=vpc-bp15zkdt37pq72zv****  HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AttachIpv4Gateway",
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

|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidIpv4Gateway.InvalidStatus |The specified IPv4Gateway is not in the correct status for the request. |The specified IPv4 Gateway is in a state that cannot respond to the request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
|400 |LimitExceeded.VpcAttachIpv4Gateway |You've reached the limit on the number of IPv4 gateways that you can attach a VPC with. |Maximum number of IPv4 gateways per VPC has been reached. A VPC can only be associated with one IPv4 gateway. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 gateway does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
