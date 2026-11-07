---
title: "DescribeVpcs - Querying a VPC list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeVpcs"
---

Call the DescribeVpcs API to query VPCs that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return VPC entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all VPCs belonging to this account.

* When using a tag to filter VPC instances, you can query up to 1,000 instances associated with the specified tag. If a specified tag is associated with more than 1000 VPC instances, only the first 1000 instances will be returned. At this point, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) API to query.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpcs&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DE7pQy">必选</span> `Example: DescribeVpcs`

The interface name. The current API name is `DescribeVpcs`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ioULPt">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**VpcIds.N ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1b1p3ve5yze****`

VPC ID.


* Parameter \- N: Represents the serial number of the VPC ID. The maximum number of entries per request is 100.

* Separate multiple VPC IDs with ampersands ( & ).



**VpcName ** <span data-label="purple">String </span>`optional` `Example: Vpc-1`

Name of the VPC.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Name of the project to which the VPC belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns VPCs tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns VPCs that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for VPCs with an empty tag value.</div>




**IsDefault ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Whether the VPC is the Default VPC.

Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Default VPC, indicating the VPC was automatically created by the system when an ECS instance was launched.

* false: Non\-default VPC, indicating the VPC was manually created by the user.



**VpcOwnerId ** <span data-label="purple">String </span>`optional` `Example: 210367****`

The main account ID to which the VPC belongs.



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

* If you provide the `NextToken` returned from a previous API call, the query continues from that position.​



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of VPCs that meet the criteria.

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



**Vpcs ** <span data-label="purple">Object[] </span>`Example: -`

Details of the VPC.


**AccountId ** <span data-label="purple">String </span>`Example: 21000****`

The ID of the account to which the VPC belongs.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp1qpo0kug3a20qqe****`

VPC ID.



**VpcName ** <span data-label="purple">String </span>`Example: vpc1`

Name of the VPC.



**Description ** <span data-label="purple">String </span>`Example: This is my VPC.`

Description of the VPC.



**CidrBlock ** <span data-label="purple">String </span>`Example: 10.XX.XX.0/8`

IPv4 CIDR block of the VPC.



**Ipv6CidrBlock ** <span data-label="purple">String </span>`Example: 2408:XXXX:0:a600::/56`

IPv6 CIDR block of the VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IPv6 feature is currently in beta stage. If you need a trial, please contact your account manager.</div>




**Ipv6CidrBlocks ** <span data-label="purple">Object[] </span>`Example: -`

The IPv6 CIDR block information of the VPC.


**Ipv6CidrBlock ** <span data-label="purple">String </span>`Example: 2408:XXXX:0:a600::/56`

IPv6 CIDR block of the VPC.



**Ipv6Isp ** <span data-label="purple">String </span>`Example: ChinaMobile`

Internet Service Provider (ISP)


* BGP (Multi\-ISP).

* ChinaMobile: Static single\-ISP provided by China Mobile.

* ChinaTelecom: Static single\-ISP provided by China Telecom.

* ChinaUnicom: Static single\-ISP provided by China Unicom.

* ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.

* ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.

* ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Except for BGP (Multi\-ISP), all other line types are only supported in the China (Shanghai) region.</div>





**SecondaryCidrBlocks ** <span data-label="purple">String[] </span>`Example: ["10.XX.XX.0/16"]`

Secondary CIDR block of the VPC.



**UserCidrBlocks ** <span data-label="purple">String[] </span>`Example: ["72.XX.XX.0/24"]`

The user CIDR block of the VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The user CIDR block of the VPC is currently in beta stage. If you need a trial, please contact your account manager.</div>




**SubnetIds ** <span data-label="purple">String[] </span>`Example: ["subnet-2fe74yvngdukg5oxruwgq****"]`

Subnet list of the VPC.



**RouteTableIds ** <span data-label="purple">String[] </span>`Example: ["vtb-bp1krxxzp0c29fmon****"]`

The route table ID associated with the VPC.



**NetworkAclNum ** <span data-label="purple">String </span>`Example: 5`

The number of network ACLs in the VPC.



**SecurityGroupIds ** <span data-label="purple">String[] </span>`Example: ["securitygroup178ftwt45bg****"]`

The list of security groups in the VPC.



**NatGatewayIds ** <span data-label="purple">String[] </span>`Example: ["ngw-3tjx9odz8q3vj0x1****"]`

The ID of the NAT gateway created in the VPC.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is not returned if no NAT gateway has been created in the VPC.</div>




**AssociateCens ** <span data-label="purple">Object[] </span>`Example: -`

The CEN information associated with the VPC.


**CenId ** <span data-label="purple">String </span>`Example: cen-23887d****`

The ID of the CEN.



**CenOwnerId ** <span data-label="purple">String </span>`Example: 12223****`

User ID of the CEN.



**CenStatus ** <span data-label="purple">String </span>`Example: Attached`

The status of the VPC in the CEN.


* Attaching

* Attached




**IsDefault ** <span data-label="purple">Boolean </span>`Example: false`

Whether the VPC is the Default VPC.


* true: Default VPC, indicating the VPC was automatically created by the system when an ECS instance was launched.

* false: Non\-default VPC, indicating the VPC was manually created by the user.



**DnsServers ** <span data-label="purple">String[] </span>`Example: ["100.96.0.2"]`

DNS server.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the VPC.


* Creating

* Pending: In the configuring process.

* Available



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the VPC belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

VPC tag information.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreationTime ** <span data-label="purple">String </span>`Example: 2018-04-18T15:02:37+08:00`

Creation time of the VPC.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2019-04-25T01:37:38+08:00`

Update time of VPC.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpcs&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
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
        "Action": "DescribeVpcs",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2,
        "Vpcs": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-bp1qpo0kug3a20qqe****",
                "Status": "Available",
                "VpcName": "vpc1",
                "AccountId": "21000****",
                "CidrBlock": "10.XX.XX.0/8",
                "IsDefault": true,
                "SubnetIds": [
                    "subnet-2fe74yvngdukg5oxruwgq****"
                ],
                "DnsServers": [
                    "100.96.0.2"
                ],
                "UpdateTime": "2019-04-25T01:37:38+08:00",
                "Description": "This is my VPC.",
                "ProjectName": "default",
                "CreationTime": "2018-04-18T15:02:37+08:00",
                "AssociateCens": [
                    {
                        "CenId": "cen-23887d****",
                        "CenStatus": "Attached",
                        "CenOwnerId": "12223****"
                    }
                ],
                "Ipv6CidrBlock": "2408:XXXX:0:a600::/56",
                "NatGatewayIds": [
                    "ngw-3tjx9odz8q3vj0x1****"
                ],
                "NetworkAclNum": "5",
                "RouteTableIds": [
                    "vtb-bp1krxxzp0c29fmon****"
                ],
                "Ipv6CidrBlocks": [
                    {
                        "Ipv6Isp": "ChinaMobile",
                        "Ipv6CidrBlock": "2408:XXXX:0:a600::/56"
                    }
                ],
                "UserCidrBlocks": [
                    "72.XX.XX.0/24"
                ],
                "SecurityGroupIds": [
                    "securitygroup178ftwt45bg****"
                ],
                "SecondaryCidrBlocks": [
                    "10.XX.XX.0/16"
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
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |The maximum number of filter tag values that can be specified in a single request has been reached. |
|400 |LimitExceeded.VpcId |You've reached the limit on the number of VPC IDs that you can describe. |You have reached the maximum number of VPC IDs that can be queried. |
