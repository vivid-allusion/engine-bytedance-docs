---
title: "DescribeNetworkAclAttributes - Querying Network ACL details"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAclAttributes"
---

Call the DescribeNetworkAclAttributes API to view details of the specified Network Access Control List.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkAclAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeNetworkAclAttributes`

The interface name. The current API name is `DescribeNetworkAclAttributes`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**NetworkAclId ** String必选 `Example: nacl-bp1fg655nh68xyz9****`

The ID of the network ACL to be viewed.

You can call the [DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) API to query the Network Access Control List ID.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `example value: 2021062415303301022514515207C4****`

Request ID.

**NetworkAclAttribute ** Object`Optional` `Example: -`

Details of the Network Access Control List.

**AccountId ** String`Optional` `Example: 2000****`

Main account ID to which the network ACL belongs.

**NetworkAclId ** String`Optional` `Example: nacl-bp1fg655nh68xyz9****`

ID of the Network Access Control List.

**NetworkAclName ** String`optional` `example value: test-acl`

Name of the Network Access Control List.

**Description ** String`optional` `Example value: TestDescription`

Description of Network Access Control List.

**VpcId ** String`Optional` `Example value: vpc-bp67acfmxazb4p****`

The VPC to which the Network Access Control List belongs.

**Status ** String`Optional` `Example: Available`

The state of the Network Access Control List.

* Available

* Creating

**CreationTime ** String`optional` `Example: 2017-12-05T22:40:00+08:00`

Creation time of the network ACL.

**UpdateTime ** String`Optional` `Example: 2017-12-05T22:40:00+08:00`

Modified time of the Network ACL.

**ProjectName ** String`optional` `example value: default`

Name of the project to which the Network Access Control List belongs.

**Tags ** Object[]`optional` `Example value: -`

Tag information of the Network ACL.

**Key ** String`Optional` `Example: k1`

The tag key of the tag.

**Value ** String`optional` `example: v1`

The tag value.

**IngressAclEntries ** Object[]`optional` `Example value: -`

Details of the Network ACL inbound rule.

If multiple inbound rules exist, the returned results are sorted in descending order of rule priority.

**NetworkAclEntryId ** String`optional` `example: nae-a2dk86arlydmezasw****`

ID of the inbound rule.

**NetworkAclEntryName ** String`Optional` `Example value: test-acl-1`

Name of the inbound rule.

**Description ** String`Optional` `Example: This is IngressAclEntries.`

Description of the inbound rule.

**Policy ** String`Optional` `Example value: accept`

Authorization policy of inbound rule.

* accept: Allow access.

* drop: Deny access. No explicit "access denied" message is returned; only symptoms like request timeouts or connection failures are visible to the initiator.

**SourceCidrIp ** String`Optional` `Example: 10.XX.XX.0/24`

The CIDR block of the source address for the inbound rule.

**Protocol ** String`optional` `example: all`

Protocol type.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.

**Priority ** Integer`optional` `Example: 1`

Inbound rule priority: A lower number indicates a higher priority.

* Value range: 1\-100

* Default: 1

**Port ** String`Optional` `Example: -1/-1`

Destination port range of the inbound rule.

* When the `Protocol` of an inbound rule is `all`, `icmp`, or `gre`, the port range is \-1/\-1, indicating no port restrictions.

* When the `Protocol` of an inbound rule is `tcp` or `udp`, the port range is 1~65535. Formats like 1/200 or 80/80 represent ports 1 through 200 and port 80, respectively.

**EgressAclEntries ** Object[]`Optional` `Example value: -`

Details of the Network ACL outbound rule.

If multiple outbound rules exist, the returned results are sorted in descending order of rule priority.

**NetworkAclEntryId ** String`Optional` `Example: nae-a2d447uw4tillfvgb****`

ID of the outbound rule.

**NetworkAclEntryName ** String`Optional` `Example value: test-acl-1`

Name of the outbound rule.

**Description ** String`optional` `Example value: This is EgressAclEntries.`

Description of outbound rules.

**Policy ** String`Optional` `Example value: accept`

Authorization policy.

* accept: Allow access.

* drop: Deny access. No explicit "access denied" message is returned; only symptoms like request timeouts or connection failures are visible to the initiator.

**DestinationCidrIp ** String`optional` `Example value: 10.XX.XX.0/24`

CIDR block of the destination address.

**Protocol ** String`optional` `example: all`

Protocol type.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.

**Priority ** Integer`optional` `Example: 1`

Outbound rule priority: A lower number indicates a higher priority.

* Value range: 1\-100

* Default: 1

**Port ** String`Optional` `Example: -1/-1`

Destination port range of the outbound rule.

* When the `Protocol` of an outbound rule is `all`, `icmp`, or `gre`, the port range is \-1/\-1, indicating no port restrictions.

* When the `Protocol` of an outbound rule is `tcp` or `udp`, the port range is 1~65535. Formats like 1/200 or 80/80 represent ports 1 through 200 and port 80, respectively.

**Resources ** Object[]`Optional` `Example value: -`

Details of the resource associated with the Network ACL.

**ResourceId ** String`Optional` `Example value: subnet-bp1de348lntdwcdf****`

The ID of the resource associated with the Network ACL.

**Status ** String`Optional` `Example: BINDED`

The status of the resource associated with the network ACL.

* BINDED: Associated.

* BINDING: Associating.

* UNBINDING: Disassociating.

## Request examples

```JSON
GET /?Action=DescribeNetworkAclAttributes&Version=2020-04-01&NetworkAclId=nacl-bp1fg655nh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNetworkAclAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkAclAttribute": {
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
        },
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|404 |InvalidNetworkAcl.NotFound |The specified Network ACL does not exist. |The specified Network ACL does not exist. |
