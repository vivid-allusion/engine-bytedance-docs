---
title: "ModifySecurityGroupEgressRules - Modifying an outbound security group rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifySecurityGroupEgressRules"
---

Call the ModifySecurityGroupEgressRules API to modify outbound security group rules.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Parameter \- N: Represents the serial number of the rule information. The maximum number of entries per request is 10. Separate rule information with ampersands ( & ).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySecurityGroupEgressRules&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|__wNZ4">必选</span> `Example value: ModifySecurityGroupEgressRules`

The interface name. The current API name is `ModifySecurityGroupEgressRules`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|ieMJ5F">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**SecurityGroupId ** <span data-label="purple"> String  </span><span data-api-tag="require|rQysTL">必选</span> `Sample value: sg-bp1fg655nh68xyz9****`

Security group ID.



**SecurityGroupRules.N.OriginPermission.Protocol ** <span data-label="purple"> String  </span>`optional` `Sample value: tcp`

Transport layer protocol before modification. Valid values:


* tcp: TCP protocol.

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.



**SecurityGroupRules.N.OriginPermission.PortStart ** <span data-label="purple"> Integer </span>`optional` `Example value: 22`

Port range start value before modification.


* When Protocol is set to tcp or udp, the value range is 1\-65535.

* When Protocol is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).



**SecurityGroupRules.N.OriginPermission.PortEnd ** <span data-label="purple"> Integer </span>`optional` `Example value: 22`

End value of the port range before modification.


* When Protocol is set to tcp or udp, the value range is 1\-65535.

* When Protocol is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).



**SecurityGroupRules.N.OriginPermission.CidrIp ** <span data-label="purple"> String  </span>`optional` `example: 10.XX.XX.0/8`

Destination IPv4 CIDR or IPv6 CIDR before modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.OriginPermission.CidrIp</code>, <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code>, and <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.OriginPermission.CidrIp</code> \> <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.OriginPermission.PrefixListId** <span data-label="purple">String</span> `optional` `Example value: pl-bp1fg655nh68xyz9****`

ID of the prefix list before modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.OriginPermission.CidrIp</code>, <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code>, and <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.OriginPermission.CidrIp</code> \> <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.OriginPermission.SourceGroupId ** <span data-label="purple"> String </span>`optional` `Example value: sg-bp67acfmxazb4p****`

Source security group ID before modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.OriginPermission.CidrIp</code>, <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code>, or <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.OriginPermission.CidrIp</code> \> <code>SecurityGroupRules.N.OriginPermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.OriginPermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.OriginPermission.Policy ** <span data-label="purple"> String </span>`optional` `Example value: accept`

Access policy before modification. Valid values:


* accept: Allow.

* drop: Deny.



**SecurityGroupRules.N.OriginPermission.Priority ** <span data-label="purple"> Integer </span>`optional` `Example value: 1`

Priority of the security group rules before modification.

Value range: 1\-100. Default: 1.



**SecurityGroupRules.N.OriginPermission.Description ** <span data-label="purple"> String  </span>`optional` `Sample value: OriginPermissionDescription`

Description of the security group rules before modification.



**SecurityGroupRules.N.UpdatePermission.Protocol ** <span data-label="purple"> String  </span>`optional` `example: tcp`

Transport layer protocol after modification. Valid values:


* tcp: TCP protocol.

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all: All protocols.



**SecurityGroupRules.N.UpdatePermission.PortStart** <span data-label="purple">Integer</span> `optional` `Example value: 22`

Start value of the port range after modification.


* When Protocol is set to tcp or udp, the value range is 1\-65535.

* When Protocol is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).



**SecurityGroupRules.N.UpdatePermission.PortEnd ** <span data-label="purple"> Integer </span>`optional` `Example value: 22`

End value of the port range after modification.


* When Protocol is set to tcp or udp, the value range is 1\-65535.

* When Protocol is set to icmp, icmpv6, or all, the port must be set to \-1 (indicating no port restrictions).



**SecurityGroupRules.N.UpdatePermission.CidrIp ** <span data-label="purple"> String </span>`optional` `Example value: 10.XX.XX.0/16`

Destination IPv4 CIDR or IPv6 CIDR after modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code>, <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code>, and <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code> \> <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.UpdatePermission.SourceGroupId ** <span data-label="purple"> String  </span>`optional` `Example value: sg-bp67acfmxazb4p****`

Destination Security Group ID after modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code>, <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code>, and <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code> \> <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.UpdatePermission.PrefixListId ** <span data-label="purple"> String </span>`optional` `Example value: pl-bp1fg655nh68xyz9****`

Prefix list ID after modification.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">At least one of the parameters <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code>, <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code>, and <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code> must be provided. If multiple parameters are provided, only one takes effect with the following priority: <code>SecurityGroupRules.N.UpdatePermission.CidrIp</code> \> <code>SecurityGroupRules.N.UpdatePermission.SourceGroupId</code> \> <code>SecurityGroupRules.N.UpdatePermission.PrefixListId</code>.</div>




**SecurityGroupRules.N.UpdatePermission.Policy** <span data-label="purple">String</span> `optional` `example: accept`

The modified access policy takes the following values:


* accept: Allow.

* drop: Deny.



**SecurityGroupRules.N.UpdatePermission.Priority ** <span data-label="purple"> Integer  </span>`optional` `Example: 2`

Priority of Security Group rules.

Value range: 1\-100. Default: 1.



**SecurityGroupRules.N.UpdatePermission.Description ** <span data-label="purple"> String  </span>`optional` `Example value: UpdatePermissionDescription`

Description of the security group rule.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifySecurityGroupEgressRules&Version=2020-04-01&SecurityGroupId=sg-bp1fg655nh68xyz9****&SecurityGroupRules.1.OriginPermission.Protocol=tcp&SecurityGroupRules.1.OriginPermission.PortStart=22&SecurityGroupRules.1.OriginPermission.PortEnd=22&SecurityGroupRules.1.OriginPermission.CidrIp=10.XX.XX.0/8&SecurityGroupRules.1.OriginPermission.Policy=accept&SecurityGroupRules.1.OriginPermission.Priority=1&SecurityGroupRules.1.UpdatePermission.Protocol=tcp&SecurityGroupRules.1.UpdatePermission.PortStart=22&SecurityGroupRules.1.UpdatePermission.PortEnd=22&SecurityGroupRules.1.UpdatePermission.CidrIp=10.XX.XX.0/16&SecurityGroupRules.1.UpdatePermission.Policy=accept&SecurityGroupRules.1.UpdatePermission.Priority=2 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifySecurityGroupEgressRules",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.ProtocolMismatch |The specified cidr block mismatch the protocol type. |The specified CIDR block format does not match the protocol type. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to the request. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified source security group is not in the specified VPC. |The referenced security group is not in the specified VPC. |
|400 |InvalidSecurityGroupType.Malformed |The type of specified security group is invalid. |The specified type value is invalid. |
|400 |InvalidSecurityRule.InvalidStatus |The specified security rule is not in the correct status for the request. |The specified security group rule in a state that cannot respond to this request. |
|400 |InvalidSecurityRule.Malformed |The source address of specified security group rule is invalid. CIDR\-only security group does not support security group as source address. |The source address of the security group rule is invalid. CIDR\-based security groups do not support security groups as source addresses. |
|400 |InvalidSecurityRule.Malformed |The source address of specified security group rule is invalid. CIDR\-only security group is not supported as source address. |The source address of the specified security group rule is invalid. CIDR\-based security groups do not support being used as source addresses. |
|400 |InvalidSecurityRule.Repeated |There are duplicate rules in the specified rules. |Duplicate rules exist in the specified rules. |
|400 |InvalidSecurityRulePolicy.Malformed |The specified security rule policy is malformed. |The action of specified security group rule is invalid. |
|400 |InvalidSecurityRulePort.Malformed |The specified security rule port is malformed. |The port of specified security group rule is invalid. |
|400 |InvalidSecurityRulePriority.Malformed |The specified security rule priority is malformed. |The specified security group rule priority is invalid. |
|400 |InvalidSecurityRuleProtocol.Malformed |The specified security rule protocol is malformed. |The protocol of the specified security group rules is invalid. |
|400 |LimitExceeded.SecurityGroupIDs |You've reached the limit on the number of security group IDs that you can describe. |You have reached the maximum number of security group IDs that can be queried. |
|400 |QuotaExceeded.PrefixListAssociation |The number of resources a prefix list can be referenced by exceeded quota. |The number of resources associated with the prefix list has exceeded the quota limit. |
|400 |QuotaExceeded.SecurityGroupRule |You've reached the limit on the number of egress security rules that you can create. |The quota for the maximum number of outbound rules that can be created for the security group has been reached. |
|400 |QuotaExceeded.SecurityGroupRule |You've reached the limit on the number of ingress security rules that you can create. |The quota for the maximum number of inbound rules that can be created for the security group has been reached. |
|400 |QuotaExceeded.SecurityGroupSecurityGroup |The number of security groups bound to the security group exceeded quota. |The specified security group has reached the maximum number of allowed source security group associations. |
|400 |QuotaExceeded.Vpc |VPC number exceeded quota. |Reached the maximum VPCs that you can create. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No sufficient permissions to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidSecurityRule.NotFound |The specified security rule does not exist. |The specified security group rule does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
