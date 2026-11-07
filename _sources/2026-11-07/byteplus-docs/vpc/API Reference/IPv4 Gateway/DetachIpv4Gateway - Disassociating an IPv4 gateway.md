---
title: "DetachIpv4Gateway - Disassociating an IPv4 gateway"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DetachIpv4Gateway"
---

Call the DetachIpv4Gateway API to disassociate the IPv4 Gateway from the VPC.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DetachIpv4Gateway&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: DetachIpv4Gateway`

The interface name. The current API name is `DetachIpv4Gateway`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**Ipv4GatewayId ** String必选 `Example value: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the IPv4 Gateway ID.

**VpcId ** String必选 `Example value: vpc-bp15zkdt37pq72zv****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**PrivateMode ** Boolean`optional` `Example value: false`

The disassociation method.

* true: **Internet access consults the route table. ** After disassociation, resources in the VPC cannot communicate with the Internet. If Internet communication is required, the IPv4 gateway must be reassociated.

* false (default): **Internet access does not check the route table.**  After disassociation, resources in the VPC are no longer restricted by the IPv4 gateway. Elastic Compute Service (ECS) instances can access the Internet by binding an EIP.

> **tip**

> true can only be passed when the IPv4 gateway is in the active state. false can only be passed when the IPv4 gateway is in the inactive state.

**ClientToken ** String`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=DetachIpv4Gateway&Version=2020-04-01&DetachIpv4Gateway=ipv4gw-bp1fgnh68xyz9****&VpcId=vpc-bp15zkdt37pq72zv****&PrivateMode=true HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DetachIpv4Gateway",
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
|400 |InvalidIpv4Gateway.AssociateRouteTable |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is associated with a route table. |The specified IPv4 Gateway is in a state that cannot respond to the request. The specified IPv4 Gateway is already associated with a route table. |
|400 |InvalidIpv4Gateway.Enable |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is enabled. |The specified IPv4 gateway is in a state that cannot respond to this request. The specified IPv4 Gateway is enabled. |
|400 |InvalidIpv4Gateway.InvalidRoute |There is a route entry for the next hop to the IPv4 gateway. |A route entry exists with a next hop pointing to the IPv4 gateway. |
|400 |InvalidIpv4Gateway.InvalidStatus |The specified IPv4Gateway is not in the correct status for the request. |The specified IPv4 gateway is in a state that cannot process this request. |
|400 |InvalidIpv4Gateway.VpcMismatch |The specified IPv4 gateway is not attached to the specified VPC. |The specified IPv4 Gateway is not associated with the specified VPC. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpcIpv4Gateway.NotEnabled |The specified IPv4 gateway for the VPC is not enabled, so it cannot be detached in private mode. |The IPv4 gateway for the specified VPC is not enabled and therefore cannot be disassociated in private network mode. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 gateway does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
