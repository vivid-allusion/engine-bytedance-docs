---
title: "DescribeSecurityGroups - Querying a security group list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups"
---

Call the DescribeSecurityGroups API to query security groups that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return security group entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all security groups belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSecurityGroups&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|TxMyE4">必选</span> `Example: DescribeSecurityGroups`

The interface name. The current API name is `DescribeSecurityGroups`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|J0MpY2">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp67acfmxazb4p****`

The ID of the VPC the security group belongs to.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**SecurityGroupIds.N ** <span data-label="purple">String </span>`optional` `Example: sg-bp67acfmxazb4p****`

List of security group IDs.


* Parameter \- N: Represents the serial number of the security group ID. The maximum number of entries per request is 100.

* Separate security group IDs with ampersands ( & ).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You must provide either the <code>SecurityGroupIds.N</code> or <code>SecurityGroupNames.N</code> parameter, but not both.</div>




**SecurityGroupNames.N ** <span data-label="purple">String </span>`optional` `Example: test-sg-1`

List of security group names.


* Parameter \- N: Represents the serial number of the security group name. The maximum number of entries per request is 100.

* Separate security group IDs with ampersands ( & ).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You must provide either the <code>SecurityGroupIds.N</code> or <code>SecurityGroupNames.N</code> parameter, but not both.</div>




**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The project to which the security group belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns security groups tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns security groups that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for security groups with an empty tag value.</div>




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

Total number of security groups that meet the conditions.

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



**SecurityGroups ** <span data-label="purple">Object[] </span>`Example: -`

Collection of security group information.


**AccountId ** <span data-label="purple">String </span>`Example: 2000****`

The main account to which the security group belongs.



**CreationTime ** <span data-label="purple">String </span>`Example: 2020-12-05T22:40:00+08:00`

Creation time of the security group.



**Description ** <span data-label="purple">String </span>`Example: TestDescription`

Description of the security group.



**SecurityGroupId ** <span data-label="purple">String </span>`Example: sg-bp67acfmxazb4p****`

Security group ID.



**SecurityGroupName ** <span data-label="purple">String </span>`Example: SGTestName`

Name of the security group.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp67acfmxazb4p****`

The VPC to which the security group belongs.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the security group.


* Available

* Creating



**Type ** <span data-label="purple">String </span>`Example: normal`

Type of the security group.


* default: Default security group.

* normal: Custom security group.

* VpnGW: VPN gateway security group.

* NatGW: NAT gateway security group.

* cidr_only: CIDR\-Only security group.



**ServiceManaged ** <span data-label="purple">Boolean </span>`Example: false`

Whether the security group is a managed security group.


* true: Yes

* false: No.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the security group belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the security group.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**UsedIpCount ** <span data-label="purple">Integer </span>`Example: 2000`

The number of configured IP addresses in the current security group.



**AvailableIpCount ** <span data-label="purple">Integer </span>`Example: 4000`

The number of remaining available IP addresses in the current security group.



**UsedNetworkInterfaceCount ** <span data-label="purple">Integer </span>`Example: 1500`

Number of associated ENIs.



**AvailableNetworkInterfaceCount ** <span data-label="purple">Integer </span>`Example: 14500`

The number of remaining available ENIs that can be associated with the security group.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeSecurityGroups&Version=2020-04-01&VpcId=vpc-bp67acfmxazb4p****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
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
        "Action": "DescribeSecurityGroups",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "SecurityGroups": [
            {
                "AccountId": "2000****",
                "VpcId": "vpc-2ff3bpyczwc1s5oxruwe8****",
                "SecurityGroupName": "Default",
                "Description": "default",
                "SecurityGroupId": "sg-2ff3bq4a38hz45oxruwc0****",
                "Status": "Available",
                "ProjectName": "default",
                "Type": "normal",
                "ServiceManaged": false,
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    },
                    {
                        "Key": "k2",
                        "Value": ""
                    }
                ],
                "CreationTime": "2021-07-23T16:15:45+08:00"
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
|400 |InvalidSecurityGroup.NotAuthorized |You are not authorized to operate invisible security group. |Hidden security groups cannot be operated without permissions. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.SecurityGroupIDs |You've reached the limit on the number of security group IDs that you can describe. |You have reached the maximum number of security group IDs that can be queried. |
|400 |LimitExceeded.SecurityGroupNames |You've reached the limit on the number of security group names that you can describe. |You have reached the maximum number of security group names that can be queried. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|409 |InvalidParameter.ParameterConflict |The parameters of security group id and security group name cannot be specified at the same time. |This request contains an invalid or unsupported parameter. You cannot specify both the security group ID and name at the same time. |
