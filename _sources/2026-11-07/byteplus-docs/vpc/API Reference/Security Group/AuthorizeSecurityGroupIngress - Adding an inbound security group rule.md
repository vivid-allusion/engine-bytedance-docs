---
title: "AuthorizeSecurityGroupIngress - Adding an inbound security group rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AuthorizeSecurityGroupIngress"
---

Call the AuthorizeSecurityGroupIngress API to add an inbound rule to the security group.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AuthorizeSecurityGroupIngress&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: AuthorizeSecurityGroupIngress`

The interface name. The current API name is `AuthorizeSecurityGroupIngress`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**SecurityGroupId ** String必选 `Example: sg-bp67acfmxazb4p****`

Security group ID.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group ID.

**Protocol ** String必选 `Example: all`

Protocol type. Valid values:

* tcp: TCP protocol.

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.

**PortStart ** Integer必选 `Example: 22`

Start value of the destination port range.

* When `Protocol` is set to tcp or udp, the value range is 1\-65535.

* When `Protocol` is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).

**PortEnd ** Integer必选 `Example: 22`

End value of the destination port range.

* When `Protocol` is set to tcp or udp, the value range is 1\-65535.

* When `Protocol` is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).

**CidrIp ** String`optional` `Example: 10.XX.XX.0/8`

Source IPv4 CIDR or IPv6 CIDR.

> **tip**

> At least one of the parameters `CidrIp`, `SourceGroupId`, or `PrefixListId` must be provided. If multiple parameters are provided, only one takes effect with the following priority: `CidrIp` \> `SourceGroupId` \> `PrefixListId`.

**SourceGroupId ** String`optional` `Example: sg-bp67acfmxazb4p****`

Source Security Group ID. This means the IP addresses of all Network Interfaces within this security group are used as the source addresses.

> **tip**

> At least one of the parameters `CidrIp`, `SourceGroupId`, or `PrefixListId` must be provided. If multiple parameters are provided, only one takes effect with the following priority: `CidrIp` \> `SourceGroupId` \> `PrefixListId`.

**PrefixListId** String `optional` `Example: pl-bp1fg655nh68xyz9****`

ID of the source address prefix list. This means all CIDR blocks in the prefix list are treated as source addresses.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the Prefix List ID.

> **tip**

* > The number of inbound security group rules that can still be added to the current security group is not less than the maximum number of entries in the prefix list.

* > At least one of the parameters `CidrIp`, `SourceGroupId`, or `PrefixListId` must be provided. If multiple parameters are provided, only one takes effect with the following priority: `CidrIp` \> `SourceGroupId` \> `PrefixListId`.

**Policy ** String`optional` `Example: accept`

Access policy. Resources specified by `CidrIp`, `SourceGroupId`, or `PrefixListId` can access Network Interfaces within the security group. Valid values:

* accept (default): Allow.

* drop: Deny.

**Priority ** Integer`optional` `Example: 1`

Security group rule priority: A lower number indicates a higher priority.

* Value range: 1\-100.

* Default: 1

**Description ** String`optional` `Example: SG-Ingress-1`

Description of the security group rule.

* Must start with a letter, Chinese character, or digit. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Length limit is 1 to 255 characters.

* If left blank, this parameter defaults to an empty string.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

**SourcePortStart ** Integer`optional` `Example: 22`

The start value of the source port number range.

* When `Protocol` is set to tcp or udp, the value range is 1\-65535.

* When `Protocol` is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).

> **tip**

> The five\-tuple security group is currently in invite\-only Beta. For trial requests, please contact your account manager.

**SourcePortEnd ** Integer`optional` `Example: 22`

The end value of the source port number range.

* When `Protocol` is set to tcp or udp, the value range is 1\-65535.

* When `Protocol` is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).

> **tip**

> The five\-tuple security group is currently in invite\-only Beta. For trial requests, please contact your account manager.

**LocalCidrIp ** String`optional` `Example: 192.169.1.0/28`

Destination IPv4 CIDR or IPv6 CIDR.

> **tip**

> The five\-tuple security group is currently in invite\-only Beta. For trial requests, please contact your account manager.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=AuthorizeSecurityGroupIngress&Version=2020-04-01&SecurityGroupId=sg-bp67acfmxazb4p****&Protocol=tcp&PortStart=22&PortEnd=22&CidrIp=10.XX.XX.0/8&Policy=accept&Priority=1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "AuthorizeSecurityGroupIngress",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.AddressMismatch |The network types of the specified source and destination CIDRs are different. |The source and destination CIDR blocks must be of the same type. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCidr.ProtocolMismatch |The specified cidr block mismatch the protocol type. |The specified CIDR block format does not match the protocol type. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified source security group is not in the specified VPC. |The referenced security group is not in the specified VPC. |
|400 |InvalidSecurityRule.InvalidSourceStatus |The specified source security group is not in the correct status for the request. |The source security group associated with the specified security group rule is in a state that cannot process this request. |
|400 |InvalidSecurityRule.Malformed |The source address of specified security group rule is invalid. CIDR\-only security group does not support security group as source address. |The source address of the security group rule is invalid. CIDR\-based security groups do not support security groups as source addresses. |
|400 |InvalidSecurityRule.Malformed |The source address of specified security group rule is invalid. CIDR\-only security group is not supported as source address. |The source address of the specified security group rule is invalid. CIDR\-based security groups do not support being used as source addresses. |
|400 |InvalidSecurityRulePolicy.Malformed |The specified security rule policy is malformed. |The action of specified security group rule is invalid. |
|400 |InvalidSecurityRulePort.Malformed |The specified security rule port is malformed. |The port of specified security group rule is invalid. |
|400 |InvalidSecurityRulePriority.Malformed |The specified security rule priority is malformed. |The specified security group rule priority is invalid. |
|400 |InvalidSecurityRuleProtocol.Malformed |The specified security rule protocol is malformed. |The protocol of the specified security group rules is invalid. |
|400 |QuotaExceeded.PrefixListAssociation |The number of resources a prefix list can be referenced by exceeded quota. |The number of resources associated with the prefix list has exceeded the quota limit. |
|400 |QuotaExceeded.SecurityGroupRule |You've reached the limit on the number of ingress security rules that you can create. |The quota for the maximum number of inbound rules that can be created for the security group has been reached. |
|400 |QuotaExceeded.SecurityGroupSecurityGroup |The number of security groups bound to the security group exceeded quota. |The specified security group has reached the maximum number of allowed source security group associations. |
|403 |Forbidden |You are not authorized to operate five tuple rule on the specified security group. |You do not have permission to execute operations on Five\-tuple rules for the specified security group. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No sufficient permissions to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|409 |InvalidSecurityRule.Conflict |The specified security rule conflicts with that of another security rule in your security group. |The specified security group rule conflicts with another rule within the same security group. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
