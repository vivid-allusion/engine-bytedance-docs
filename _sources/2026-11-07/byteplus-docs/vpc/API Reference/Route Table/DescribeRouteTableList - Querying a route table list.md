---
title: "DescribeRouteTableList - Querying a route table list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList"
---

Call the DescribeRouteTableList API to query route tables that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* When multiple request parameters are passed in, the system queries based on these parameters and returns route tables that match all conditions. If no matching route tables are found, an empty value is returned.

* If no optional parameters are passed in, the system queries based on the currently logged\-in account and returns all route tables under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRouteTableList&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|AwzIBR">必选</span> `Example: DescribeRouteTableList`

The interface name. The current API name is `DescribeRouteTableList`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|lbLz09">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-2fdz8g5nruzuo5oxru****`

ID of the VPC to which the route table belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**RouteTableId ** <span data-label="purple">String </span>`optional` `Example: vtb-2fdzao4h726f45******`

The ID of the route table to query.



**AssociateType ** <span data-label="purple">String </span>`optional` `Example: Subnet`

Type of route table. Valid values:


* Subnet: Subnet route table.

* Gateway: Gateway route table.



**RouteTableName ** <span data-label="purple">String </span>`optional` `Example: test-route-table`

The name of the route table to query.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Name of the project to which the route table belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys are combined using a logical AND operation, meaning the query returns route tables that have all the specified tag keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns route tables that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string will return route tables with empty tag values.</div>




**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.


* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of matching route tables.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. It becomes meaningless when using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The count of entries per page in the current pagination.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.



**RouterTableList ** <span data-label="purple">Object[] </span>`Example: -`

Detailed information of the route table.


**AccountId ** <span data-label="purple">String </span>`Example: 200000****`

The ID of the account to which the route table belongs.



**AssociateType ** <span data-label="purple">String </span>`Example: Subnet`

Type of route table.



**Ipv4GatewayId ** <span data-label="purple">String </span>`Example: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.



**Ipv6GatewayId ** <span data-label="purple">String </span>`Example: ipv6gw-fadfgegg******`

IPv6 Gateway ID.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-2fdz8g5nruzuo5oxru****`

ID of VPC to which the route table belongs.



**VpcName ** <span data-label="purple">String </span>`Example: test`

Name of the VPC.



**RouteTableId ** <span data-label="purple">String </span>`Example: vtb-2fdzao4h726f45******`

Route table ID.



**RouteTableName ** <span data-label="purple">String </span>`Example: Test-route-table`

Route table name.



**Description ** <span data-label="purple">String </span>`Example: Test route table`

Description of the route table.



**RouteTableType ** <span data-label="purple">String </span>`Example: Custom`

Type of route table.


* Custom: Custom route table.

* System: System route table.



**SubnetIds ** <span data-label="purple">String[] </span>`Example: subnet-2fdzbgudy248w5o****`

List of subnets associated with the route table.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the route table belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the route table.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreationTime ** <span data-label="purple">String </span>`Example: 2021-09-01T19:38:31+08:00`

Creation time of the route table.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-09-01T19:38:31+08:00`

Update time of route table.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeRouteTableList&Version=2020-04-01&VpcId=vpc-2fdz8g5nruzuo5oxru****&PageSize=20&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeRouteTableList",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RouterTableList": [
            {
                "RouteTableId": "vtb-2ff3bq0c10e0w5oxruvx6****",
                "RouteTableName": "test",
                "RouteTableType": "System",
                "VpcId": "vpc-2ff3bpyczwc1s5oxruwe8****",
                "SubnetIds": [
                    "subnet-1g0esbs70pfr48ibuxwpu****"
                ],
                "VpcName": "test",
                "CreationTime": "2021-09-01T19:38:31+08:00",
                "UpdateTime": "2021-09-01T19:38:31+08:00",
                "AccountId": "200000****",
                "Description": "system route table created by vpc",
                "ProjectName": "default",
                "Tags": [
                    {
                        "Key":"k1",
                        "Value":"v1"
                    }
                 ]   
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|Status code |Error codes |Error message |Explain |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
