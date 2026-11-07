---
title: "DescribeNetworkAcls - Querying a network ACL list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls"
---

Call the DescribeNetworkAcls API to query network ACLs that meet specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkAcls&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeNetworkAcls`

The interface name. The current API name is `DescribeNetworkAcls`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**VpcId ** String`optional` `Example: vpc-bp1opxu1zkhn00gzv****`

The ID of the VPC to which the network ACL belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**NetworkAclIds.N ** String`optional` `Example: acl-bp1fg655nh68xyz9****`

ID of the Network ACL.

* Parameter \- N: Indicates the serial number of the Network ACL ID, with a maximum of 100 per call.

* Separate multiple IDs with ampersands (&).

**SubnetId ** String`optional` `Example: subnet-087k1y0owv0x57ku****`

ID of the subnet associated with the Network ACL.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**NetworkAclName ** String`optional` `Example: test-acl`

Name of the Network Access Control List.

**ProjectName ** String`optional` `Example: default`

Project to which the Network Access Control List belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns Network ACLs tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns Network ACLs that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > If this parameter is passed in, `TagFilters.N.Key` must be passed in first.

* > Passing an empty string queries for Network ACLs with an empty tag value.

**PageNumber ** Integer`optional` `Example: 1`

Page number of the list. Default: 1.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for pagination queries.

**PageSize ** Integer`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for pagination queries.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**TotalCount ** Integer`Example: 2`

Total number of Network ACLs that meet the criteria.

> **tip**

> This parameter is scheduled for deprecation. It becomes meaningless when using `NextToken` and `MaxResults` for paginated queries.

**PageNumber ** Integer`Example: 1`

The current page number.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for pagination queries.

**PageSize ** Integer`Example: 10`

The count of entries per page in the current pagination.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for pagination queries.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**NetworkAcls ** Object[]`Example: -`

Details of the Network ACL.

**AccountId ** String`Example: 2000****`

Main account ID to which the network ACL belongs.

**NetworkAclId ** String`Example: nacl-bp1fg655nh68xyz9****`

ID of the Network ACL.

**NetworkAclName ** String`Example: test-acl`

Name of the network ACL.

**Description ** String`Example: TestDescription`

Network ACL description.

**VpcId ** String`Example: vpc-bp67acfmxazb4p****`

VPC to which the Network ACL belongs.

**Status ** String`Example: Available`

The state of the Network ACL.

* Available

* Creating

**CreationTime ** String`Example: 2017-12-05T22:40:00+08:00`

Creation time of the network ACL.

**UpdateTime ** String`Example: 2017-12-05T22:40:00+08:00`

Modified time of the Network ACL.

**ProjectName ** String`Example: default`

The name of the project to which the network ACL belongs.

**Tags ** Object[]`Example: -`

Tag information of the Network ACL.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

**IngressAclEntries ** Object[]`Example: -`

Details of the Network ACL inbound rule.

If multiple inbound rules exist, the returned results are sorted in descending order of rule priority.

**NetworkAclEntryId ** String`Example: nae-a2dk86arlydmezasw****`

ID of the inbound rule.

**NetworkAclEntryName ** String`Example: test-acl-1`

Name of the inbound rule.

**Description ** String`Example: This is IngressAclEntries.`

Description of the inbound rule.

**Policy ** String`Example: accept`

Authorization policy of inbound rule.

* accept: Allow access.

* drop: Deny access. No explicit "access denied" message is returned; only symptoms like request timeouts or connection failures are visible to the initiator.

**SourceCidrIp ** String`Example: 10.XX.XX.0/24`

The CIDR block of the source address for the inbound rule.

**Protocol ** String`Example: all`

Protocol type.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.

**Priority ** Integer`Example: 1`

Inbound rule priority: A lower number indicates a higher priority.

* Value range: 1\-100

* Default: 1

**Port ** String`Example: -1/-1`

Destination port range of the inbound rule.

* When the `Protocol` of an inbound rule is `all`, `icmp`, or `gre`, the port range is \-1/\-1, indicating no port restrictions.

* When the `Protocol` of an inbound rule is `tcp` or `udp`, the port range is 1~65535. Formats like 1/200 or 80/80 represent ports 1 through 200 and port 80, respectively.

**EgressAclEntries ** Object[]`Example: -`

Details of the Network ACL outbound rule.

If multiple outbound rules exist, the returned results are sorted in descending order of rule priority.

**NetworkAclEntryId ** String`Example: nae-a2d447uw4tillfvgb****`

ID of the outbound rule.

**NetworkAclEntryName ** String`Example: test-acl-1`

Name of the outbound rule.

**Description ** String`Example: This is EgressAclEntries.`

Description of the outbound rule.

**Policy ** String`Example: accept`

Authorization policy.

* accept: Allow access.

* drop: Deny access. No explicit "access denied" message is returned; only symptoms like request timeouts or connection failures are visible to the initiator.

**DestinationCidrIp ** String`Example: 10.XX.XX.0/24`

CIDR block of the destination address.

**Protocol ** String`Example: all`

Protocol type.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.

**Priority ** Integer`Example: 1`

Outbound rule priority: A lower number indicates a higher priority.

* Value range: 1\-100

* Default: 1

**Port ** String`Example: -1/-1`

Destination port range of the outbound rule.

* When the `Protocol` of an outbound rule is `all`, `icmp`, or `gre`, the port range is \-1/\-1, indicating no port restrictions.

* When the `Protocol` of an outbound rule is `tcp` or `udp`, the port range is 1~65535. Formats like 1/200 or 80/80 represent ports 1 through 200 and port 80, respectively.

**Resources ** Object[]`Example: -`

Details of the resource associated with the Network ACL.

**ResourceId ** String`Example: subnet-bp1de348lntdwcdf****`

ID of the resource associated with the Network ACL.

**Status ** String`Example: BINDED`

The status of the resource associated with the network ACL.

* BINDED: Associated.

* BINDING: Associating.

* UNBINDING: Disassociating.

## Request examples

```json
GET /?Action=DescribeNetworkAcls&Version=2020-04-01&VpcId=vpc-bp1opxu1zkhn00gzv****PageNumber=1&PageSize=20 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNetworkAcls",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkAcls": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-bp67acfmxazb4p****",
                "Status": "Available",
                "AccountId": "2000****",
                "Resources": [
                    {
                        "Status": "BINDED",
                        "ResourceId": "subnet-bp1de348lntdwcdf****"
                    }
                ],
                "UpdateTime": "2017-12-05T22:40:00+08:00",
                "Description": "TestDescription",
                "ProjectName": "default",
                "CreationTime": "2017-12-05T22:40:00+08:00",
                "NetworkAclId": "nacl-bp1fg655nh68xyz9****",
                "NetworkAclName": "test-acl",
                "EgressAclEntries": [
                    {
                        "Port": "-1/-1",
                        "Policy": "accept",
                        "Priority": 1,
                        "Protocol": "all",
                        "Description": "This is EgressAclEntries.",
                        "DestinationCidrIp": "10.XX.XX.0/24",
                        "NetworkAclEntryId": "nae-a2d447uw4tillfvgb****",
                        "NetworkAclEntryName": "test-acl-1"
                    }
                ],
                "IngressAclEntries": [
                    {
                        "Port": "-1/-1",
                        "Policy": "accept",
                        "Priority": 1,
                        "Protocol": "all",
                        "Description": "This is IngressAclEntries.",
                        "SourceCidrIp": "10.XX.XX.0/24",
                        "NetworkAclEntryId": "nae-a2dk86arlydmezasw****",
                        "NetworkAclEntryName": "test-acl-1"
                    }
                ]
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
|400 |LimitExceeded.NetworkAcl |You've reached the limit on the number of Network ACL IDs that you can describe. |The maximum allowed number of Network ACL IDs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
