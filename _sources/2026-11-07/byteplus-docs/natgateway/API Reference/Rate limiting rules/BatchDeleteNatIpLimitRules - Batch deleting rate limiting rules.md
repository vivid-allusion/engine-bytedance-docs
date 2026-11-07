---
title: "BatchDeleteNatIpLimitRules - Batch deleting rate limiting rules"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/BatchDeleteNatIpLimitRules"
---

Call the BatchDeleteNatIpLimitRules API to batch delete IP limit rules.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=BatchDeleteNatIpLimitRules&groupName=IP%E9%99%90%E9%80%9F&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|x3BaGJ">必选</span> `Example: BatchDeleteNatIpLimitRules`

The action that you want to perform. Value: BatchDeleteNatIpLimitRules.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OKJPPO">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|wRCh9N">必选</span> `Example: ngw-3tex2x1cwd4c6c0v****`

ID of the NAT gateway.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the ID of the NAT gateway.



**LimitRuleIds.N ** <span data-label="purple">string[] </span>`optional` `Example: iplimit-****`

ID of the rate limiting rule to be deleted.

You can call the [DescribeNatIpLimitRules](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpLimitRules) API to query the rate limiting rule ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=BatchDeleteNatIpLimitRules&Version=2020-04-01&NatGatewayId=d8rRAg&LimitRuleIds.1=rIHR2IyG HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
X-Date: 20251113T133524Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251113/cn-beijing/natgateway/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20251113213531057067222059C83528",
    "Action": "BatchDeleteNatIpLimitRules",
    "Version": "2020-04-01",
    "Service": "natgateway",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "2021062415303301022514515207C4****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidLimitRule.InvalidStatus |The specified Limit Rule is not in the correct status for the request. |The rate\-limiting rule of the specified NAT IP cannot respond to this request due to its status. |
|400 |InvalidLimitRule.NotFound |The specified Limit Rule does not exist. |The specified IP rate limiting rule does not exist. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidNatGateway.InvalidNatArch |The specified NAT gateway is not in the correct arch for the request. |The specified NAT gateway cannot respond to this request. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
