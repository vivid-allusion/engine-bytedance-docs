---
title: "CreateIpv4Gateway - Creating an IPv4 gateway instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateIpv4Gateway"
---

Call the CreateIpv4Gateway API to create an IPv4 Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateIpv4Gateway&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|B-ZAJk">必选</span> `Example value: CreateIpv4Gateway`

The interface name. The current API name is `CreateIpv4Gateway`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|3mSt9I">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Ipv4GatewayName ** <span data-label="purple"> String  </span>`optional` `Example value: ipv4-gw-1`

IPv4 Gateway name.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, this defaults to the ID of the IPv4 gateway.



**Description ** <span data-label="purple"> String  </span>`optional` `Example value: ipv4-gw-master`

Description of the IPv4 Gateway.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, this defaults to an empty string.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



**Ipv4GatewayId ** <span data-label="purple"> String  </span>`optional` `Example value: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateIpv4Gateway&Version=2020-04-01&Ipv4GatewayName=ipv4-gw-1 HTTP/1.1
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
        "Action": "CreateIpv4Gateway",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv4GatewayId": "ipv4gw-bp1fgnh68xyz9****",
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
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
|400 |LimitExceeded.VpcAttachIpv4Gateway |You've reached the limit on the number of IPv4 gateways that you can attach a VPC with. |Maximum number of IPv4 gateways per VPC has been reached. A VPC can only be associated with one IPv4 gateway. |
|403 |Forbidden.IPv4Gateway |You are not authorized to perform operations on the specified IPv4 gateway. |No sufficient permissions to perform this operation on the specified IPv4 gateway. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
