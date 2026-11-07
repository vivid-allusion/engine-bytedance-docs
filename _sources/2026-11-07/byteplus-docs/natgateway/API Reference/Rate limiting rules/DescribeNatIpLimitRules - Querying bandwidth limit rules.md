---
title: "DescribeNatIpLimitRules - Querying bandwidth limit rules"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeNatIpLimitRules"
---

Call the DescribeNatIpLimitRules API to query bandwidth limit rules of a Network Address Translation (NAT) gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeNatIpLimitRules&groupName=IP%E9%99%90%E9%80%9F&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|nrBj01">必选</span> `Example: DescribeNatIpLimitRules`

The action that you want to perform. Value: DescribeNatIpLimitRules.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|ZdIAla">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LimitRuleIds.N ** <span data-label="purple">string[] </span>`optional` `Example: iplimit-93**`

The ID of the rate limiting rule.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|R0M1sl">必选</span> `Example: ngw-2feq5xhimd88w59gp686****`

ID of the NAT gateway.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways?lang=zh) API to query the ID of a NAT gateway.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NatIpLimitRules ** <span data-label="purple">object[] </span>`Example: -`

The details of rate limiting rules.


**LimitRuleId ** <span data-label="purple">string </span>`Example: iplimit-****`

The ID of the rate limiting rule.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

ID of the NAT gateway.



**InternalIp ** <span data-label="purple">string </span>`Example: 192.XX.XX.1`

The rate limiting IP address.



**OutboundMbpsLimit ** <span data-label="purple">string </span>`Example: 10`

The maximum rate of the outbound bandwidth. Unit: Mbps. The response value of "0" means no rate limit.



**InboundMbpsLimit ** <span data-label="purple">string </span>`Example: 10`

The maximum rate of the inbound bandwidth. Unit: Mbps. The response value of "0" means no rate limit.




**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The page number of the current pagination.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">integer </span>`Example: 33`

The total number of rate limiting rules that meet the conditions.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeNatIpLimitRules&Version=2020-04-01&NatGatewayId=ngw-2feq5xhimd88w59gp686****  HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeNatIpLimitRules",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 20,
        "NatBandwidthLimitRule": [
            {
                "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                "LimitRuleId": "iplimit-****",
                "InternalIp": "192.XX.XX.1",
                "OutboundMbpsLimit": 10,
                "InboundMbpsLimit": 10,
                "CreateTime": "2021-03-30T19:59:27+08:00",
                "UpdateTime": "2025-03-30T16:59:27+08:00"
            }
        ]   
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Explain |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |LimitExceeded.LimitRuleId |You've reached the limit on the number of LimitRule IDs that you can describe. |You have reached the maximum number of rate limiting rule IDs that can be queried. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
