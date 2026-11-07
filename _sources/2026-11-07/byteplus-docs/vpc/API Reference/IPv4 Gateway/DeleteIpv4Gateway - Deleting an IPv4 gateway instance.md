---
title: "DeleteIpv4Gateway - Deleting an IPv4 gateway instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteIpv4Gateway"
---

Call the DeleteIpv4Gateway API to delete the IPv4 Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteIpv4Gateway&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|VSFhu-">必选</span> `Example value: DeleteIpv4Gateway`

The interface name. The current API name is `DeleteIpv4Gateway`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Agomiv">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Ipv4GatewayId ** <span data-label="purple"> String  </span><span data-api-tag="require|-jBdPP">必选</span> `Example value: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

You can call the [DescribeIpv4Gateways](https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways) API to query the IPv4 Gateway ID.



**ClientToken ** <span data-label="purple"> String  </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteIpv4Gateway&Version=2020-04-01&Ipv4GatewayId=ipv4gw-bp1fgnh68xyz9**** HTTP/1.1
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
        "Action": "DeleteIpv4Gateway",
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
|400 |InvalidIpv4Gateway.AssociateRouteTable |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is associated with a route table. |The specified IPv4 gateway is in a state that cannot process this request. The specified IPv4 Gateway is already associated with a route table. |
|400 |InvalidIpv4Gateway.AttachVpc |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is attached to a VPC. |The specified IPv4 gateway is in a state that cannot process this request. The specified IPv4 Gateway is already associated with a VPC. |
|400 |InvalidIpv4Gateway.Enable |The specified IPv4 gateway is not in the correct status for the request. The specified IPv4 gateway is enabled. |The specified IPv4 gateway is in a state that cannot respond to this request. The specified IPv4 Gateway is enabled. |
|400 |InvalidIpv4Gateway.InvalidRoute |There is a route entry for the next hop to the IPv4 gateway. |A route entry exists with a next hop pointing to the IPv4 gateway. |
|400 |InvalidIpv4Gateway.InvalidStatus |The specified IPv4Gateway is not in the correct status for the request. |The specified IPv4 Gateway is in a state that cannot respond to the request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 gateway does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
