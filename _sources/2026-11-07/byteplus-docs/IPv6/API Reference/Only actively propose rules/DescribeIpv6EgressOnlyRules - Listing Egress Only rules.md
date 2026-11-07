---
title: "DescribeIpv6EgressOnlyRules - Listing Egress Only rules"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6EgressOnlyRules"
---

Call the DescribeIpv6EgressOnlyRules API to query Egress Only rules that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query returns IPv6 Internet bandwidths that match all specified conditions. If no matching entry is found, an empty result is returned.

* If none of the optional request parameters are provided, the query is scoped to the current account and returns all IPv6 Internet bandwidths belonging to it.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|uHc1FE">必选</span> `Example: DescribeIpv6EgressOnlyRules`

The action to perform. Value: **DescribeIpv6EgressOnlyRules**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|HFMzjM">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6GatewayId ** <span data-label="purple">String </span><span data-api-tag="require|KbyV73">必选</span> `Example: ipv6gw-hp3rwmtmfhgis****`

The ID of the IPv6 Gateway.

You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to query the ID of IPv6 Gateway.



**InstanceId ** <span data-label="purple">String </span>`optional` `Example: eip-hp3nxjkfxn5pnhgl5****`

The IPv6 Internet bandwidth ID associated with the Egress Only rule.



**Ipv6Address ** <span data-label="purple">String </span>`optional` `Example: 2408:XXXX:153:3921:851c:c435:7b12:1c5f`

The IPv6 address to which the Egress Only rule applies.



**Ipv6EgressOnlyRuleIds.N ** <span data-label="purple">String </span>`optional` `Example: ipv6py-fhjshfsfweryew****`

The ID of the Egress Only rule.


* N represents the serial number of an Egress Only rule ID. The value ranges from 1 to 100, meaning a maximum of 100 Egress Only rule IDs can be specified in a single query.

* Separate multiple IDs of Egress Only rules with ampersands (&).



**Name ** <span data-label="purple">String </span>`optional` `Example: rulename`

The name of the Egress Only rule.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a paginated query. Maximum: 100. Default: 20.



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.


* If left blank, the query starts from the beginning.

* Provide `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202106241530330102251****`

The request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of Egress Only rules that meet the conditions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. It is meaningless when using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of entries per page in the current pagination.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty result indicates no more pages.



**Ipv6EgressRules ** <span data-label="purple">Object[] </span>`Example: -`

The details of Egress Only rules that meet the conditions.


**Ipv6EgressOnlyRuleId ** <span data-label="purple">String </span>`Example: ipv6py-fhjshfsfweryew***`

The ID of the Egress Only rule.



**Name ** <span data-label="purple">String </span>`Example: test-name`

The name of the Egress Only rule.



**Description ** <span data-label="purple">String </span>`Example: test-desc`

The description of the Egress Only rule.



**InstanceId ** <span data-label="purple">String </span>`Example: eip-fufuewsdgb***`

The IPv6 Internet bandwidth ID to add an Egress Only rule.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the IPv6 Egress Only rule.


* Creating

* Available




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeIpv6EgressOnlyRules&Version=2020-04-01&Ipv6GatewayId=ipv6gw-hp3rwmtmfhgis**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202106241530330102251****",
        "Action": "DescribeIpv6EgressOnlyRules",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    }, 
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount":2,
        "PageNumber": 1,
        "PageSize": 20,
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "Ipv6EgressRules": [
            {
                "Ipv6EgressOnlyRuleId": "ipv6py-fhjshfsfweryew***",
                "Name": "rulename",
                "Description": "",
                "InstanceId": "eip-hp3nxjkfxn5pnhgl5****",
                "Status": "Available"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken value is invalid. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.Ipv6EgressOnlyRule |You've reached the limit on the number of Ipv6EgressOnlyRule IDs that you can describe. |You have reached the maximum number of IPv6 Egress Only rule IDs that can be queried. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
