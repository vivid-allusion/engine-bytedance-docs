---
title: "CreateNatIpLimitRule - Creating a rate limiting rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateNatIpLimitRule"
---

Call the CreateNatIpLimitRule API to create a rate limiting rule for a Network Address Translation (NAT) gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateNatIpLimitRule&groupName=IP%E9%99%90%E9%80%9F&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|JikkO5">必选</span> `Example: CreateNatIpLimitRule`

The action that you want to perform. Value: CreateNatIpLimitRule.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ohx1KG">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 1000`

The maximum rate of establishing new connections. Value: 1\-150,000. Unit: connection per second (CPS).



**ConnectionLimit ** <span data-label="purple">integer </span>`optional` `Example: 10000`

The maximum number of concurrent connections. Value range: 1–1,000,000. Unit: connections.​



**IsDefault ** <span data-label="purple">boolean </span>`optional` `Example: true`

Describe whether the type of rate limiting rule is default. Values:


* true: Default rate limiting rule.

* false: Custom rate limiting rule.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|QNYIzY">必选</span> `Example: ngw-1sm2t10buei****`

ID of the NAT gateway.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways?lang=zh) API to query the ID of a NAT gateway.



**InternalIp ** <span data-label="purple">string </span>`optional` `Example: 192.XX.XX.1`

The rate limiting IP address.

This parameter is not supported when IsDefault is "true".



**OutboundMbpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 10`

The maximum rate of the outbound bandwidth. Unit: Mbps.

The maximum rate limiting value must not exceed the bandwidth cap of the NAT gateway instance. Setting to "0" means no rate limit.



**InboundMbpsLimit ** <span data-label="purple">integer </span>`optional` `Example: 10`

The maximum rate of the inbound bandwidth. Unit: Mbps.

The maximum rate limiting value must not exceed the bandwidth cap of the NAT gateway instance. Setting to "0" means no rate limit.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**LimitRuleId ** <span data-label="purple">string </span>`Example: iplimit-93**`

The ID of the rate limiting rule.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateNatIpLimitRule&Version=2020-04-01&NatGatewayId=ngw-1sm2t10buei****&InternalIp=192.XX.XX.1&OutboundMbpsLimit=10&InboundMbpsLimit=0  HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021120316053701022513314307D5****",
        "Action": "CreateNatIpLimitRule",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021120316053701022513314307D5****",
        "LimitRuleId":"iplimit-93**"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |QuotaExceeded.LimitRule |You've reached the limit on the number of LimitRule that you can create. |You have reached the maximum number of IP rate limiting rules that can be created. |
|400 |InvalidIPAddress.Malformed |The specified IP address is malformed. |The specified IP is invalid. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. |Inbound and outbound bandwidth limits are not specified. |
|400 |InvalidLimitRule.InvalidStatus |The specified Limit Rule is not in the correct status for the request. |The rate limiting rule of the specified NAT IP cannot respond to this request due to its status. |
|400 |LimitExceeded.BandwidthPerInternalIp |You've reached the limit on the bandwidth of internal ip that you can update. |The NAT IP bandwidth cap has been exceeded. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support the current action. |
|400 |InvalidLimitRule.exists |The specified bandwidth limit rule with nat exists. |The rate limiting rule has been created for the specified NAT gateway. |
|400 |InvalidLimitRule.exists |The specified nat default limit rule exists. |The default rate limiting rule has been created for the specified NAT gateway. |
|400 |LimitExceeded.Connection |You've reached the limit on the connection that you can update. |You have exceeded the maximum number of NAT gateway's concurrent connections. |
|400 |LimitExceeded.Cps |You've reached the limit on the cps that you can update. |You have exceeded the maximum rate of establishing new connections for the NAT gateway. |
|400 |InvalidLimitRule.InternalIP |The specified default limit rule internal ip is invalid. |You do not need to specify an IP address for the default rate limiting rule of the specified NAT gateway. |
|403 |Forbidden |You are not authorized to use nat ip limit. |No permission to apply rate limiting for the NAT IP. |
|403 |Forbidden |You are not authorized to use nat default limit or cps and connection limit. |No permission to apply NAT gateway's default rate limiting rule, new connection limit or concurrent connection limit. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
