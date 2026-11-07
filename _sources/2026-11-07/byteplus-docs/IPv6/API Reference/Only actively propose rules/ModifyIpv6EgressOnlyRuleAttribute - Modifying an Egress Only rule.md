---
title: "ModifyIpv6EgressOnlyRuleAttribute - Modifying an Egress Only rule"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/ModifyIpv6EgressOnlyRuleAttribute"
---

Call the ModifyIpv6EgressOnlyRuleAttribute API to modify the name of a specified Egress Only rule.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Z5NCMg">必选</span> `Example: ModifyIpv6EgressOnlyRuleAttribute`

The action to perform. Value: **ModifyIpv6EgressOnlyRuleAttribute**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ZbHAeJ">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6EgressOnlyRuleId ** <span data-label="purple">String </span><span data-api-tag="require|DqMNtl">必选</span> `Example: ipv6py-fhjshfsfweryew****`

The ID of the Egress Only rule.



**Name ** <span data-label="purple">String </span>`optional` `Example: rulename`

The name of the Egress Only rule.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=ModifyIpv6EgressOnlyRuleAttribute&Version=2020-04-01&Ipv6EgressOnlyRuleId=ipv6py-fhjshfsfweryew****&Name=rule-1 HTTP/1.1
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
        "Action": "ModifyIpv6EgressOnlyRuleAttribute",
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
|400 |InvalidIpv6EgressOnlyRule.InvalidStatus |The specified Ipv6EgressOnlyRule is not in the correct status for the request. |The specified IPv6 Egress Only rule cannot respond to this request due to its status. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|404 |InvalidIpv6EgressOnlyRule.NotFound |The specified Ipv6EgressOnlyRule does not exist. |The specified IPv6 Egress Only rule does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
