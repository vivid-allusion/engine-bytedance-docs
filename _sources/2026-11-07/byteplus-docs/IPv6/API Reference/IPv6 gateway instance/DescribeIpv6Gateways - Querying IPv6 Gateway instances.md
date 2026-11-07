---
title: "DescribeIpv6Gateways - Querying IPv6 Gateway instances"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways"
---

Call the DescribeIpv6Gateways API to query IPv6 Gateways that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query returns IPv6 Gateways that match all specified conditions. If no matching entry is found, an empty result is returned.

* If none of the optional request parameters are provided, the query is scoped to the current account and returns all IPv6 Gateways belonging to it.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|fvex0d">必选</span> `Example: DescribeIpv6Gateways`

The action to perform. Value: **DescribeIpv6Gateways**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|dSK8wR">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Ipv6GatewayIds.N ** <span data-label="purple">String </span>`optional` `Example: ipv6gw-hp3rwmtmfhgis****`

The ID of the IPv6 Gateway instance.


* N represents the sequence number of an IPv6 Gateway ID. The value ranges from 1 to 100, meaning a maximum of 100 instance IDs can be specified in a single query.

* Separate multiple IPv6 Gateway IDs with ampersands (&).



**VpcIds.N ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1opxu1zkhn00gzv****`

The VPC ID associated with the IPv6 Gateway instance.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.


* N represents the sequence number of a VPC ID. The value ranges from 1 to 100, meaning a maximum of 100 instance IDs can be specified in a single query.

* Separate multiple VPC IDs with ampersands (&).



**Name ** <span data-label="purple">String </span>`optional` `Example: ipv6GW-01`

The name of the IPv6 Gateway instance.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The name of the project to which the IPv6 Gateway belongs.


* If this parameter is not passed or is passed as empty, the query returns all IPv6 Gateway instances.

* If this parameter is passed as non\-empty, the query returns the IPv6 Gateway instances that belong to the specified project.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a paginated query. Maximum: 100. Default: 20.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.


* If left blank, the query starts from the beginning.

* Provide `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of IPv6 Gateways that match the conditions.

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



**Ipv6Gateways ** <span data-label="purple">Object[] </span>`Example: -`

The details of IPv6 Gateway instances that meet the conditions.


**CreationTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

The time when the IPv6 Gateway instance is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

The time when the IPv6 Gateway instance is modified.



**Status ** <span data-label="purple">String </span>`Example: Available`

The running status of the IPv6 Gateway instance. Values:


* Creating

* Deleting

* Available



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp67acfmxazb4p****`

The VPC ID associated with the IPv6 Gateway instance.



**Description ** <span data-label="purple">String </span>`Example: descriptionforIPv6GW`

The description of the IPv6 Gateway instance.



**Ipv6GatewayId ** <span data-label="purple">String </span>`Example: ipv6gw-hp3rwmtmfhgis****`

The ID of the IPv6 Gateway instance.



**RouteTableId ** <span data-label="purple">String </span>`Example: rt-3tbe3o0tn849ovie****`

The route table ID associated with the IPv6 Gateway instance.



**Name ** <span data-label="purple">String </span>`Example: ipv6GW-01`

The name of the IPv6 Gateway instance.



**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The name of the project to which the IPv6 Gateway belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the IPv6 Gateway.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeIpv6Gateways&Version=2020-04-01&Ipv6GatewayIds.1=ipv6gw-hp3rwmtmfhgis****&Ipv6GatewayIds.2=ipv6gw-hp3y0l3ln89j8**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: vpc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeIpv6Gateways",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv6Gateways": [
            {
                "Name": "ipv6GW-01",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-bp67acfmxazb4p****",
                "Status": "Available",
                "UpdateTime": "2017-12-05T22:40:00+08:00",
                "Description": "descriptionforIPv6GW",
                "ProjectName": "Project_1",
                "CreationTime": "2017-12-05T22:40:00+08:00",
                "RouteTableId": "rt-3tbe3o0tn849ovie****",
                "Ipv6GatewayId": "ipv6gw-hp3rwmtmfhgis****"
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/IPv6/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken value is invalid. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.Ipv6GatewayId |You've reached the limit on the number of Ipv6Gateway IDs that you can describe. |You have reached the maximum number of IPv6 Gateway IDs that can be queried. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
|400 |LimitExceeded.VpcId |You've reached the limit on the number of VPC IDs that you can describe. |You have reached the maximum number of VPC IDs that can be queried. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
