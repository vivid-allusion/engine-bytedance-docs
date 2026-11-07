---
title: "DescribeHaVips - Querying a HAVIP"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeHaVips"
---

Call the DescribeHaVips API to query high availability virtual IP addresses (HAVIP) that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return HAVIP entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all HAVIPs belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeHaVips&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|WTqOfG">必选</span> `Example: DescribeHaVips`

The interface name. The current API name is `DescribeHaVips`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Mx6a7V">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1s5fnvk4gn2tws03****`

ID of the VPC to which the HAVIP belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**SubnetId ** <span data-label="purple">String </span>`optional` `Example: subnet-bp1s5fnvk4gn2tws03****`

ID of the subnet to which the HAVIP belongs.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.



**IpAddress ** <span data-label="purple">String </span>`optional` `Example: 192.XX.XX.10`

IP address of the HAVIP.



**HaVipIds.N ** <span data-label="purple">String </span>`optional` `Example: havip-2zeo05qre24nhrqpy****`

HAVIP ID.


* Parameter \- N: Indicates the serial number of the HAVIP ID, with a maximum of 100 per call.

* Separate multiple HAVIP IDs with the ampersand (&).



**HaVipName ** <span data-label="purple">String </span>`optional` `Example: havip-test-name`

The name of the HAVIP.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

The status of the HAVIP.


* Available

* Creating

* InUse: In use

* Deleting



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project-1`

Name of the HAVIP project.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns HAVIPs tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns HAVIPs that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for HAVIPs with an empty tag value.</div>




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

The total number of HAVIPs that meet the criteria.

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



**HaVips ** <span data-label="purple">Object[] </span>`Example: -`

Details of HAVIP.


**CreatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Creation time of HAVIP.



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:48:55+08:00`

Update time of HAVIP.



**AccountId ** <span data-label="purple">String </span>`Example: 200000****`

The ID of the account to which the HAVIP belongs.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the HAVIP.



**Description ** <span data-label="purple">String </span>`Example: test havip`

The description of the HAVIP.



**HaVipId ** <span data-label="purple">String </span>`Example: havip-273whz6qg3k7fap8tw****`

HAVIP ID.



**HaVipName ** <span data-label="purple">String </span>`Example: havip-test-name`

The name of the HAVIP.



**MasterInstanceId ** <span data-label="purple">String </span>`Example: i-sad5kl1we****`

ID of the primary instance bound to HAVIP.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-274dzjk74o0e87fap8u****`

ID of the VPC to which the HAVIP belongs.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-274dzk7vi0o3k7fap8sp****`

ID of the subnet to which the HAVIP belongs.



**AssociatedInstanceType ** <span data-label="purple">String </span>`Example: EcsInstance`

The type of instance bound to the HAVIP.


* EcsInstance: Elastic Compute Service instance

* NetworkInterface: Elastic network interface



**AssociatedInstanceIds ** <span data-label="purple">String[] </span>`Example: i-sad5kl1we****`

List of instance IDs bound to HAVIP.



**AssociatedEipId ** <span data-label="purple">String </span>`Example: eip-2ziwb7ujxscd*****`

ID of the EIP bound to HAVIP.



**AssociatedEipAddress ** <span data-label="purple">String </span>`Example: 132.XX.XX.45`

The IP address of the HAVIP\-bound EIP.



**ProjectName ** <span data-label="purple">String </span>`Example: Project-1`

Name of the HAVIP project.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of HAVIP.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeHaVips&Version=2020-04-01&VpcId=vpc-bp1s5fnvk4gn2tws03****&SubnetId=subnet-bp1s5fnvk4gn2tws03****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "33E480C5-B46F-4CA5-B6FD-D77C746E****",
        "Action": "DescribeHaVips",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "HaVips": [
            {
                "CreatedAt": "2021-08-05T21:46:55+08:00",
                "UpdatedAt": "2021-08-05T21:48:55+08:00",
                "AccountId": "200000****",
                "Status": "Available",
                "Description": "test havip",
                "HaVipId": "havip-273whz6qg3k7fap8tw****",
                "HaVipName": "havip-test-name",
                "IpAddress": "10.XX.XX.20",
                "MasterInstanceId": "eni-273whz8pqai2o7fap8t6****",
                "VpcId": "vpc-274dzjk74o0e87fap8ul****",
                "SubnetId": "subnet-274dzk7vi0o3k7fap8sp****",
                "AssociatedInstanceType": "EcsInstance",
                "AssociatedInstanceIds": [
                    "i-sad5kl1we*****",
                    "i-pua1ksl2e*****"
                ],
                "AssociatedEipId": "eip-2ziwb7ujxscd*****",
                "AssociatedEipAddress": "132.XX.XX.45",
                "ProjectName": "Project-1",
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.HaVipId |You've reached the limit on the number of HaVip IDs that you can describe. |The maximum allowed number of HAVIP IDs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
