---
title: "DescribeIpv6AddressBandwidths - Listing IPv6 Internet bandwidths"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6AddressBandwidths"
---

Call the DescribeIpv6AddressBandwidths API to query IPv6 Internet bandwidths that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query returns IPv6 Internet bandwidths that match all specified conditions. If no matching entry is found, an empty result is returned.

* If none of the optional request parameters are provided, the query is scoped to the current account and returns all IPv6 Internet bandwidths belonging to it.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Il0Ewr">必选</span> `Example: DescribeIpv6AddressBandwidths`

The action to perform. Value: **DescribeIpv6AddressBandwidths**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|v8yrrG">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1opxu1zkhn00gzv****`

The VPC ID.



**AllocationIds.N ** <span data-label="purple">String </span>`optional` `Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.


* N represents the sequence number of an IPv6 Internet bandwidth ID. The value ranges from 1 to 100, indicating that a maximum of 100 IDs can be specified for a query.

* Separate multiple IPv6 Internet bandwidth IDs with ampersands (&).



**Ipv6Addresses.N ** <span data-label="purple">String </span>`optional` `Example: 2408::153:3921:XX:XX:7b12:1c5f`

The IPv6 address.


* N represents the sequence number of an IPv6 address pending IPv6 Internet bandwidth activation. The value ranges from 1 to 100, indicating that a maximum of 100 addresses can be specified for a query.

* Separate multiple IPv6 addresses with ampersands (&).



**ISP ** <span data-label="purple">String </span>`optional` `Example: BGP`

The ISP of the IPv6 Internet bandwidth.


* BGP (Multi\-ISP).



**AssociatedInstanceType ** <span data-label="purple">String </span>`optional` `Example: EcsInstance`

The instance type associated with the IPv6 Internet bandwidth.


* EcsInstance: Elastic Compute Service (ECS) instance.



**AssociatedInstanceId ** <span data-label="purple">String </span>`optional` `Example: i-3tm18xqalm4e8i4q****`

The instance ID associated with the IPv6 Internet bandwidth.



**NetworkType ** <span data-label="purple">String </span>`optional` `Example: Public`

The communication type of the IPv6 address to be queried.


* Private: Private network communication.

* Public: Public network communication.



**BandwidthPackageId ** <span data-label="purple">String </span>`optional` `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the IPv6 Bandwidth Package.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (&). Multiple tag keys are combined with a logical "AND". The query returns IPv6 Internet bandwidth entries tagged with all the specified keys.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a paginated query. Maximum: 100. Default: 20.



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in a paginated query.


* If left blank, the query starts from the beginning.

* Provide `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid range: 1\-3. Multiple tag values under the same tag key are combined with a logical "OR". The query returns IPv6 Internet bandwidth entries tagged with any one of those values under the specified key.

* Separate multiple tag values with ampersands (&).

> Description

> * To provide this parameter, provide TagFilters.N.Key first.

> * If you provide an empty string, the system queries IPv6 Internet bandwidth with an empty tag value.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

The request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of IPv6 Internet bandwidth entries that meet the query conditions.

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



**Ipv6AddressBandwidths ** <span data-label="purple">Object[] </span>`Example: -`

The details of the IPv6 Internet bandwidth entries that meet the query conditions.


**Ipv6GatewayId ** <span data-label="purple">String </span>`Example: ipv6gw-hp3y0l3ln89j8cdvf****`

The ID of the IPv6 Gateway.



**IsBlocked ** <span data-label="purple">Boolean </span>`Example: true`

Describe whether the instance is blocked.


* true: Yes.

* false: No.



**AllocationId ** <span data-label="purple">String </span>`Example: eip-2zaiwb7ujxscd****`

The ID of the IPv6 Internet bandwidth.

> This parameter is returned only when IPv6 Internet bandwidth is enabled for IPv6 addresses.



**UpdateTime** <span data-label="purple">String</span> `Example: 2019-04-29T01:37:38+08:00`

The time when the IPv6 Internet bandwidth is updated.



**CreationTime ** <span data-label="purple">String </span>`Example: 2019-04-29T01:37:38+08:00`

The time when the IPv6 Internet bandwidth is enabled.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-05-07 01:00:00`

The time when IPv6 Internet bandwidth is suspended due to overdue payment.



**DeleteTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when the IPv6 Internet bandwidth is deleted.



**Bandwidth** <span data-label="purple">Integer</span> `Example: 5`

The bandwidth cap of the IPv6 Internet bandwidth. Unit: Mbps.



**BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

The ID of the IPv6 Bandwidth Package.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the IPv6 Internet bandwidth.


* Creating

* Available



**ISP ** <span data-label="purple">String </span>`Example: BGP`

The ISP of the IPv6 Internet bandwidth.



**InstanceId ** <span data-label="purple">String </span>`Example: i-3tm18xqalm4e8i4q****`

The instance ID associated with the IPv6 Internet bandwidth.



**InstanceType ** <span data-label="purple">String </span>`Example: EcsInstance`

The instance type associated with the IPv6 Internet bandwidth.



**Ipv6Address ** <span data-label="purple">String </span>`Example: 2408::153:3921:XX:XX:7b12:1c5f`

The IPv6 address.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

Describe whether the IPv6 Internet bandwidth is locked.


* Normal

* FinancialLocked: Being locked.



**NetworkType ** <span data-label="purple">String </span>`Example: Public`

The communication type of the IPv6 address.



**LockReason ** <span data-label="purple">String </span>`Example: Financial`

The reason for the IPv6 Internet bandwidth being locked.

This parameter is returned only when the IPv6 Internet bandwidth is in the `FinancialLocked` status.


* Financial: Being locked due to arrears.

* Security: Being locked due to security.



**BillingType ** <span data-label="purple">Integer </span>`Example: 3`

The metering method of the IPv6 Internet bandwidth.


* 2: Pay\-by\-bandwidth\-cap.

* 3: Pay\-by\-data\-transfer.



**ProjectName ** <span data-label="purple">String </span>`Example: project_01`

The name of the project to which the IPv6 Internet bandwidth belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the IPv6 Internet bandwidth.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeIpv6AddressBandwidths&Version=2020-04-01&VpcId=vpc-bp1opxu1zkhn00gzv**** HTTP/1.1
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
        "Action": "DescribeIpv6AddressBandwidths",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv6AddressBandwidths": [
            {
                "ISP": "BGP",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Available",
                "Bandwidth": 5,
                "IsBlocked": true,
                "DeleteTime": "2021-05-07 23:23:23",
                "InstanceId": "i-3tm18xqalm4e8i4q****",
                "LockReason": "Financial",
                "UpdateTime": "2019-04-29T01:37:38+08:00",
                "BillingType": 3,
                "Ipv6Address": "2408::153:3921:XX:XX:7b12:1c5f",
                "NetworkType": "Public",
                "OverdueTime": "2021-05-07 01:00:00",
                "ProjectName": "project_01",
                "AllocationId": "eip-2zaiwb7ujxscd****",
                "CreationTime": "2019-04-29T01:37:38+08:00",
                "InstanceType": "EcsInstance",
                "Ipv6GatewayId": "ipv6gw-hp3y0l3ln89j8cdvf****",
                "BusinessStatus": "Normal",
                "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****"
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
|400 |LimitExceeded.AllocationId |You've reached the limit on the number of allocation IDs that you can describe. |You have reached the maximum number of Allocation IDs that can be queried. |
|400 |LimitExceeded.Ipv6Address |You've reached the limit on the number of IPv6 addresses that you can describe. |You have reached the maximum number of IPv6 addresses that can be queried. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain the required parameter. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
