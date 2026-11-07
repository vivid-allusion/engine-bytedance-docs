---
title: "DescribeSubnets - Querying a subnet list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeSubnets"
---

Call the DescribeSubnets API to query subnets that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return subnet entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all subnets belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSubnets&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|JPfuQQ">必选</span> `Example: DescribeSubnets`

The interface name. The current API name is `DescribeSubnets`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|krILNI">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



o**ZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-beijing-a`

ID of the availability zone to which the subnet belongs.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1b1xjllp3ve5yze****`

ID of the VPC to which the subnet belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**SubnetIds.N ** <span data-label="purple">String </span>`optional` `Example: subnet-23`

ID of the subnet.


* Parameter \- N: Represents the serial number of the subnet ID. The maximum number of entries per request is 100.

* Separate multiple IDs with ampersands (&).



**SubnetName ** <span data-label="purple">String </span>`optional` `Example: subnet-1323sadadda****`

Name of the subnet.



**SubnetOwnerId ** <span data-label="purple">String </span>`optional` `Example: 2000****`

Main account ID of the subnet owner.



**RouteTableId ** <span data-label="purple">String </span>`optional` `Example: vrt-bp145q7glnuzdv****`

Account ID of the subnet owner.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Name of the project to which the VPC instance (containing the subnet) belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns subnets tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns subnets that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for subnets with an empty tag value.</div>




**IsDefault ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Whether the subnet is a default subnet. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Default subnet, indicating the subnet was automatically created by the system when an ECS instance was launched.

* false: Non\-default subnet, indicating the subnet was manually created by the user.



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

Total number of subnets that match the criteria.

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



**Subnets ** <span data-label="purple">Object[] </span>`Example: -`

Detailed information of the subnet.


**AccountId ** <span data-label="purple">String </span>`Example: 200000****`

Account ID of the subnet owner.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-25bcdxs7pv1****`

ID of the subnet.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-257gcdcdq64****`

ID of the VPC to which the subnet belongs.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of subnet.


* Pending: Configuring.

* Available



**CidrBlock ** <span data-label="purple">String </span>`Example: 172.XX.XX.0/24`

IPv4 CIDR block of the subnet.



**Ipv6CidrBlock ** <span data-label="purple">String </span>`Example: 2408:XXXX:0:a600::/64`

IPv6 CIDR block of subnet.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IPv6 feature is currently in beta stage. If you need a trial, please contact your account manager.</div>




**ZoneId ** <span data-label="purple">String </span>`Example: cn-beijing-a`

The availability zone of the subnet.



**AvailableIpAddressCount ** <span data-label="purple">Integer </span>`Example: 1`

Count of available IP addresses within the subnet.



**Description ** <span data-label="purple">String </span>`Example: Description`

Description of the subnet.



**SubnetName ** <span data-label="purple">String </span>`Example: subnet-1`

Name of the subnet.



**CreationTime ** <span data-label="purple">String </span>`Example: 2018-01-18T12:43:57+08:00`

Creation time of subnet.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2019-01-18T11:23:55+08:00`

Update time of the subnet.



**TotalIpv4Count ** <span data-label="purple">Integer </span>`Example: 253`

Total number of available IPs in the subnet.



**NetworkAclId ** <span data-label="purple">String </span>`Example: acl-bp1fg655nh68xyz9****`

ID of the network ACL associated with the subnet.



**IsDefault ** <span data-label="purple">Boolean </span>`Example: false`

Whether the subnet is a default subnet.


* true: Default subnet, indicating the subnet was automatically created by the system when an ECS instance was launched.

* false: Non\-default subnet, indicating the subnet was manually created by the user.



**RouteTable ** <span data-label="purple">Object </span>`Example: -`

Route table information.


**RouteTableId ** <span data-label="purple">String </span>`Example: vrt-bp145q7glnuzdv****`

ID of the route table associated with the subnet.



**RouteTableType ** <span data-label="purple">String </span>`Example: System`

Type of the route table associated with the subnet.


* System: System route table.

* Custom: Custom route table.




**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the subnet belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the subnet.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeSubnets&Version=2020-04-01&ZoneId=cn-beijing-a&VpcId=vpc-bp1b1xjllp3ve5yze****NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSubnets",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "Subnets": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-257gcdcdq64****",
                "Status": "Available",
                "ZoneId": "cn-beijing-a",
                "SubnetId": "subnet-25bcdxs7pv1****",
                "AccountId": "200000****",
                "CidrBlock": "172.XX.XX.0/24",
                "IsDefault": true,
                "RouteTable": {
                    "RouteTableId": "vrt-bp145q7glnuzdv****",
                    "RouteTableType": "System"
                },
                "SubnetName": "subnet-1",
                "UpdateTime": "2019-01-18T11:23:55+08:00",
                "Description": "Description",
                "ProjectName": "default",
                "CreationTime": "2018-01-18T12:43:57+08:00",
                "NetworkAclId": "acl-bp1fg655nh68xyz9****",
                "Ipv6CidrBlock": "2408:XXXX:0:a600::/64",
                "TotalIpv4Count": 253,
                "AvailableIpAddressCount": 1
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
|400 |LimitExceeded.SubnetId |You've reached the limit on the number of subnet IDs that you can describe. |The maximum allowed number of subnet IDs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
