---
title: "EnableIpv4Gateway - Enabling an IPv4 Gateway instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/EnableIpv4Gateway"
---

Call the EnableIpv4Gateway API to enable the IPv4 Gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Before enabling, the following conditions need to be met:

   * The IPv4 Gateway is associated with a VPC.

   * The route table associated with the subnet that requires Internet access has already been configured with a route entry pointing to the IPv4 gateway as the next hop.

* Once enabled, all inbound and outbound IPv4 internet traffic for the VPC will be restricted by the IPv4 gateway. Internet traffic traverses the subnet's route table.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnableIpv4Gateway&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|hM1YIL">必选</span> `Example value: EnableIpv4Gateway`

The interface name. The current API name is `EnableIpv4Gateway`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|jxClEr">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Ipv4GatewayId ** <span data-label="purple"> String  </span><span data-api-tag="require|jH1zWm">必选</span> `Example value: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the IPv4 Gateway ID.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=EnableIpv4Gateway&Version=2020-04-01&Ipv4GatewayId=ipv4gw-bp1fgnh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "EnableIpv4Gateway",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidIpv4Gateway.ConflictWithAnycastEip |The specified IPv4 gateway conflicts with that of the VPC which contains anycast EIP. |The specified IPv4 gateway conflicts with a VPC that contains an Anycast EIP. |
|400 |InvalidIpv4Gateway.ConflictWithDirectEip |The specified IPv4 gateway conflicts with that of the VPC which contains direct EIP. |The specified IPv4 gateway conflicts with a VPC that contains a directly accessible EIP. |
|400 |InvalidIpv4Gateway.ConflictWithNat |The specified IPv4 gateway conflicts with that of the VPC which contains NAT gateway. |The specified IPv4 gateway conflicts with a VPC that contains a NAT Gateway. |
|400 |InvalidIpv4Gateway.ConflictWithUserCidr |The specified IPv4 gateway conflicts with that of the VPC with user CIDR block configured. |The specified IPv4 gateway conflicts with a VPC configured with a custom CIDR block. |
|400 |InvalidIpv4Gateway.Enable |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is enabled. |The specified IPv4 gateway is in a state that cannot respond to this request. The specified IPv4 Gateway is enabled. |
|400 |InvalidIpv4Gateway.InvalidRoute |The route entry for the next hop to the IPv4 gateway is missing. |No route entry exists with a next hop pointing to the IPv4 gateway. |
|400 |InvalidIpv4Gateway.InvalidStatus |The specified IPv4Gateway is not in the correct status for the request. |The specified IPv4 Gateway is in a state that cannot respond to the request. |
|400 |InvalidIpv4Gateway.NotAttachVpc |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is not attached to a VPC. |The specified IPv4 Gateway is in a state that cannot respond to the request. The specified IPv4 Gateway is not associated with any VPC. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 gateway does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
