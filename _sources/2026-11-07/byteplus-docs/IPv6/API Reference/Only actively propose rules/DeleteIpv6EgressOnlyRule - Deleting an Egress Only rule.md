---
title: "DeleteIpv6EgressOnlyRule - Deleting an Egress Only rule"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DeleteIpv6EgressOnlyRule"
---

Call the DeleteIpv6EgressOnlyRule API to delete a specified Egress Only rule.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|MeuKib">必选</span> `Example: DeleteIpv6EgressOnlyRule`

The action to perform. Value: **DeleteIpv6EgressOnlyRule**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|mysSeb">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6EgressOnlyRuleId ** <span data-label="purple">String </span><span data-api-tag="require|KPqrrr">必选</span> `Example: ipv6py-fhjshfsfweryew****`

The ID of the Egress Only rule.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DeleteIpv6EgressOnlyRule&Version=2020-04-01&Ipv6EgressOnlyRuleId=ipv6py-fhjshfsfweryew**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteIpv6EgressOnlyRule",
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

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified Elastic IP Address (EIP) is being processed by another request. Try again later. |
|400 |InvalidIpv6.InUse |The specified IPv6 address bandwidth is being operated by another request. |The specified IPv6 Internet bandwidth is being processed by another request. Try again later. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|404 |InvalidIpv6EgressOnlyRule.NotFound |The specified Ipv6EgressOnlyRule does not exist. |The specified IPv6 Egress Only rule does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
