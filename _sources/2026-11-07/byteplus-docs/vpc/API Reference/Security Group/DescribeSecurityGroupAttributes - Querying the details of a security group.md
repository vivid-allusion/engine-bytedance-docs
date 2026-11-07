---
title: "DescribeSecurityGroupAttributes - Querying the details of a security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroupAttributes"
---

Call the DescribeSecurityGroupAttributes API to query security group rules that meet specified conditions within a given security group.

## Instructions

* When multiple request parameters are provided, the query returns security group rules that match all the specified conditions. If no rule matches, the basic information of the specified security group is returned.

* If no optional request parameters are provided, all rules in the specified security group rules are returned.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSecurityGroupAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeSecurityGroupAttributes`

Interface name. The current API name is `DescribeSecurityGroupAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**SecurityGroupId ** String必选 `Example: sg-bp1gxw6bznjjvhu3****`

ID of the security group the rule belongs to.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group ID.

**Direction ** String`optional` `Example: egress`

Authorization direction. Valid values:

* egress: The outbound direction of the security group

* ingress: The inbound direction of the security group

**Protocol ** String`optional` `Example: all`

Protocol type. Valid values:

* tcp: TCP protocol.

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* all: Support all protocols.

**CidrIp ** String`optional` `Example: 10.XX.XX.1/8`

The CIDR block used for authorizing traffic in inbound (ingress) or outbound (egress) security group rules. Its meaning varies depending on the value of the `Direction` parameter.

* When `Direction` is "egress", it represents the destination CIDR block.

* When `Direction` is "ingress", it represents the source CIDR block.

> **tip**

> When the parameters `CidrIp`, `SourceGroupId, PrefixListId` are all provided, only one takes effect. The order of priority is: `CidrIp` \> `SourceGroupId` \> `PrefixListId`.

**SourceGroupId ** String`optional` `Example: sg-bp67acfmxazb4p****`

ID of the source or destination address security group.

> **tip**

> When the parameters `CidrIp`, `SourceGroupId, PrefixListId` are provided, only one takes effect. The priority order is `CidrIp` \> `SourceGroupId` \> `PrefixListId`

**PrefixListId ** String`optional` `Example: pl-bp1fg655nh68xyz9****`

ID of the prefix list.

> **tip**

> When the parameters `CidrIp`, `SourceGroupId, PrefixListId` are all provided, only one takes effect. The order of priority is: `CidrIp` \> `SourceGroupId` \> `PrefixListId`.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**AccountId ** String`Example: 2000****`

The root user to which the security group belongs.

**VpcId ** String`Example: vpc-bp1opxu1zkhn00gzv****`

The VPC ID.

**SecurityGroupId ** String`Example: sg-bp1gxw6bznjjvhu3****`

ID of the target security group.

**SecurityGroupName ** String`Example: testSecurityGroupName2`

Name of the target security group.

**Description ** String`Example: sg_1`

Description of the security group.

**Type ** String`Example: normal`

The type of the security group.

* default: Default security group.

* normal: Custom security group.

* VpnGW: VPN gateway security group.

* NatGW: NAT Gateway security group.

**ServiceManaged ** Boolean`Example: true`

Whether the security group is a managed security group.

* true: Yes.

* false: No.

**Status ** String`Example: Available`

Status of the security group.

* Available

* Creating

**Permissions ** Object[]`Example: -`

Collection of security group rules.

**SourceGroupId ** String`Example: sg-bp1gxw6bznjjvhu3****`

Security group ID.

**Direction ** String`Example: egress`

Authorization direction.

**Priority ** Integer`Example: 1`

Rule priority.

**Policy ** String`Example: accept`

Access policy.

* accept: Allow access.

* drop: Deny access.

**Protocol ** String`Example: TCP`

Protocol type.

**PortStart ** Integer`Example: 80`

Start port.

**PortEnd ** Integer`Example: 80`

End port.

**CidrIp ** String`Example: 10.XX.XX.1/8`

The CIDR block used for authorizing traffic in inbound (ingress) or outbound (egress) security group rules. Its meaning depends on the value of the returned `Direction` field:

* When `Direction` is "egress", it represents the destination CIDR block.

* When `Direction` is "ingress", it represents the source CIDR block.

**PrefixListId ** String`Example: pl-bp1fg655nh68xyz9****`

ID of the prefix list.

**PrefixListCidrs ** String[]`Example: 8.XX.XX.0/16`

CIDR block of the prefix list.

**Description ** String`Example: sg rule for default`

Description of the security group rule.

**CreationTime ** String`Example: 2021-12-12T07:28:38+08:00`

Creation time of the security group rule.

**UpdateTime ** String`Example: 2021-2-10T07:28:30+08:00`

The time when the security group rule was last updated.

**SecurityGroupRuleId ** String`Example: sgr-bp12kc4rqohaf2js****`

Security group rule ID.

**ProjectName ** String`Example: default`

Name of the project to which the security group belongs.

**Tags ** Object[]`Example: -`

Tag information of the security group.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

**CreationTime ** String`Example: 2021-07-12T07:28:20+08:00`

Creation time of security group.

**UpdateTime ** String`Example: 2021-08-12T07:30:38+08:00`

Update time of security group.

## Request example

```json
GET /?Action=DescribeSecurityGroupAttributes&Version=2020-04-01&SecurityGroupId=sg-bp1gxw6bznjjvhu3**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSecurityGroupAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "2000****",
        "CreationTime": "2021-07-12T07:28:20+08:00",
        "Description": "sg_1",
        "Permissions": [
            {
                "CidrIp": "10.XX.XX.1/8",
                "Policy": "accept",
                "PortEnd": 80,
                "Priority": 1,
                "Protocol": "TCP",
                "Direction": "egress",
                "PortStart": 80,
                "UpdateTime": "2021-2-10T07:28:30+08:00",
                "Description": "sg rule for default",
                "CreationTime": "2021-12-12T07:28:38+08:00",
                "PrefixListId": "pl-bp1fg655nh68xyz9****",
                "SourceGroupId": "sg-bp1gxw6bznjjvhu3****",
                "PrefixListCidrs": [
                    ""
                ],
                "SecurityGroupRuleId": "sgr-bp12kc4rqohaf2js****"
            }
        ],
        "ProjectName": "default",
        "RequestId": "2021062415303301022514515207C4****",
        "SecurityGroupId": "sg-bp1gxw6bznjjvhu3****",
        "SecurityGroupName": "testSecurityGroupName2",
        "ServiceManaged": true,
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "Type": "normal",
        "UpdateTime": "2021-08-12T07:30:38+08:00",
        "VpcId": "vpc-bp1opxu1zkhn00gzv****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
