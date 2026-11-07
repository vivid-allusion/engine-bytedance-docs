---
title: "ModifyNatIpLimitRuleAttributes - Modifying a rate limiting rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ModifyNatIpLimitRuleAttributes"
---

Call the ModifyNatIpLimitRuleAttributes API to modify a rate limiting rule for a NAT gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Leaving optional parameters below unset means no modifications to them.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyNatIpLimitRuleAttributes&groupName=IP%E9%99%90%E9%80%9F&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|5fmZuT">必选</span> `Example: ModifyNatIpLimitRuleAttributes`

The action that you want to perform. Value: ModifyNatIpLimitRuleAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|SLuGk5">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 1000`

The maximum rate of establishing new connections. Value: 1\-150,000. Unit: connection per second (CPS).



**ConnectionLimit ** <span data-label="purple">string </span>`optional` `Example: 10000`

The maximum number of concurrent connections. Value range: 1–1,000,000. Unit: connections.​



**LimitRuleId ** <span data-label="purple">string </span><span data-api-tag="require|HfGayy">必选</span> `Example: iplimit-****`

The ID of the rate limiting rule.

You can call [DescribeNatIpLimitRules](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpLimitRules?lang=zh) to query the ID of the rate\-limiting rule.



**OutboundMbpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 10`

The maximum rate of the outbound bandwidth. Unit: Mbps. The maximum rate limiting value must not exceed the bandwidth cap of the NAT gateway instance.



**InboundMbpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 10`

The maximum rate of the inbound bandwidth. Unit: Mbps. The maximum rate\-limiting value must not exceed the bandwidth cap of the NAT gateway instance.



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
GET /?Action=ModifyNatIpLimitRuleAttributes&Version=2020-04-01&LimitRuleId=iplimit-**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing

```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250429195708148093100079663938",
    "Action": "ModifyNatIpLimitRuleAttributes",
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
|400 |LimitExceeded.BandwidthPerInternalIp |You've reached the limit on the bandwidth of internal ip that you can update. |The NAT IP bandwidth cap has been exceeded. |
|400 |InvalidIPAddress.Malformed |The specified IP address is malformed. |The specified IP is invalid. |
|400 |InvalidLimitRule.NotFound |The specified Limit Rule does not exist. |The specified IP rate limiting rule does not exist. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. |Inbound and outbound bandwidth limits are not specified. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support the current action. |
|403 |Forbidden |You are not authorized to use nat ip limit. |No permission to apply rate limiting for the NAT IP. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
