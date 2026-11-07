---
title: "UpdateNetworkAclEntries - Updating an outbound/inbound ACL rule"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/UpdateNetworkAclEntries"
---

Call the UpdateNetworkAclEntries API to update the network ACL outbound and inbound rules.

## Instructions

* Update inbound rules: When `UpdateIngressAclEntries` is set to true and new inbound rule parameters are provided, the system will first delete the current inbound rules and then create new ones based on the incoming parameters.

* Update outbound rules: When `UpdateEgressAclEntries` is set to true and new outbound rule parameters are provided, the system will first delete the current outbound rules and then create new ones based on the incoming parameters.

* Parameter \- N: Represents the serial number of the rule information. The maximum number of entries per request is 20. Separate rule information with ampersands ( & ).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateNetworkAclEntries&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: UpdateNetworkAclEntries`

The interface name. The current API name is `UpdateNetworkAclEntries`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**NetworkAclId ** String必选 `Example: nacl-bp1fg655nh68xyz9****`

ID of the Network ACL.

You can call the [DescribeNetworkAcls](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkAcls) API to query the Network ACL ID.

**UpdateIngressAclEntries ** Boolean`optional` `Example value: false`

**Whether to update the inbound rule:**

**Type the enumerated values strictly in the case form as follows. Do not set other values.**

* **true: Update.**

* **false (default): Do not update.**

**IngressAclEntries.N.NetworkAclEntryId ** String`optional` `Example: nae-2zepn32de59j8m4****`

The ID of the network ACL inbound rule.

If you provide the ID of an existing inbound rule, the new rule will continue to use that ID.

**IngressAclEntries.N.NetworkAclEntryName ** String`optional` `Example: acl-3****`

Name of the network ACL inbound rule.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, this parameter defaults to an empty string.

**IngressAclEntries.N.Description ** String`optional` `Example: ThisIsIngressAclEntries`

Description of the network ACL inbound rule.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, this defaults to an empty string.

**IngressAclEntries.N.Policy ** String`optional` `Example value: accept`

The authorization policy for a network ACL inbound rule. It refers to external resources accessing resources within the subnet. Valid values:

* accept (Default): Allow access.

* drop: Deny access.

**IngressAclEntries.N.SourceCidrIp ** String`optional` `Example: 10.XX.XX.0/24`

The source CIDR block for a network ACL inbound rule.

> **tip**

> This parameter is required when the parameter `UpdateIngressAclEntries` is set to "true".

**IngressAclEntries.N.Protocol ** String`optional` `Example: all`

The protocol type of the network ACL inbound rule. Valid values:

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all (default): Support all protocols.

**IngressAclEntries.N.Port** String `optional` `Example value: 22/22`

The destination port range for a network ACL inbound rule.

* When `IngressAclEntries.N.Protocol` is set to all, icmp, icmpv6, or gre,

   * this parameter is not required.

   * Default: \-1/\-1, indicating no port restriction.

* When `IngressAclEntries.N.Protocol` is set to tcp or udp,

   *  this parameter is required.

   * Value range: 1\-65535.

   * Use a forward slash (/) to separate the start and end ports, e.g., 1/50, 80/80.

**UpdateEgressAclEntries ** Boolean`optional` `Example: false`

**Whether to update the outbound rule.**

**Type the enumerated values strictly in the case form as follows. Do not set other values.**

* **true: Update.**

* **false (default): Do not update.**

**EgressAclEntries.N.NetworkAclEntryId ** String`optional` `Example: nae-2zecs97e0brcge46****`

ID of the Network ACL outbound rule.

If you provide the ID of an existing outbound rule, the new rule will continue to use that ID.

**EgressAclEntries.N.NetworkAclEntryName ** String`optional` `Example: acl-01`

The name of the network ACL outbound rule.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, this parameter defaults to an empty string.

**EgressAclEntries.N.Description** String `optional` `Example value: ThisIsEgressAclEntries`

Description of the network ACL outbound rule.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, this defaults to an empty string.

**EgressAclEntries.N.Policy ** String`optional` `Example: accept`

The authorization policy for a network ACL outbound rule. It refers resources within the subnet accessing external resources. Valid values:

* accept (Default): Allow access.

* drop: Deny access.

**EgressAclEntries.N.DestinationCidrIp ** String`optional` `Example: 10.XX.XX.0/24`

The destination CIDR block for a network ACL outbound rule.

> **tip**

> This parameter is required when the parameter `UpdateEgressAclEntries` is set to "true".

**EgressAclEntries.N.Protocol ** String`optional` `Example: all`

The protocol type of the network ACL outbound rule. Valid values:

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.

* icmpv6: ICMPv6 protocol.

* gre: GRE protocol.

* all (default): Support all protocols.

**EgressAclEntries.N.Port ** String`optional` `Example: -1/-1`

The destination port range for a network ACL outbound rule.

* When `EgressAclEntries.N.Protocol` is set to all, icmp, icmpv6, or gre,

   *  this parameter is not required.

   * Default: \-1/\-1, indicating no port restriction.

* When `EgressAclEntries.N.Protocol` is set to tcp or udp,

   * this parameter is required.

   * Value range: 1\-65535.

   * Use a forward slash (/) to separate the start and end ports, e.g., 1/50, 80/80.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=UpdateNetworkAclEntries&Version=2020-04-01&NetworkAclId=nacl-bp1fg655nh68xyz9**** HTTP/1.1 
Host: vpc.cn-beijing.byteplusapi.com.cn 
X-Date: 20250804T033538Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```

Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateNetworkAclEntries",
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

|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.AddressMismatch |The network types of the specified source and destination CIDRs are different. |The source and destination CIDR blocks must be of the same type. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCidr.ProtocolMismatch |The specified cidr block mismatch the protocol type. |The specified CIDR block format does not match the protocol type. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidNetworkAcl.InvalidStatus |The specified Network ACL is not in the correct status for the request. |The specified Network ACL is in a state that cannot respond to this request. |
|400 |InvalidNetworkAclEntry.Disorder |The specified Network ACL entry index orders are malformed. |The specified serial number for the network ACL rule entry is invalid. |
|400 |InvalidNetworkAclEntryPolicy.Malformed |The specified Network ACL entry policy is malformed. |The specified network ACL rule authorization policy is invalid. |
|400 |InvalidNetworkAclEntryPort.Malformed |The specified Network ACL entry port is malformed. |The specified network ACL rule port is invalid. |
|400 |InvalidNetworkAclEntryProtocol.Malformed |The specified Network ACL entry protocol is malformed. |The specified Acl Entry protocol is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |QuotaExceeded.NetworkAclEntryEgress |Network ACL egress entry number exceeded quota. |The maximum number of inbound rules allowed for a single network ACL has been reached. |
|400 |QuotaExceeded.NetworkAclEntryIngress |Network ACL ingress entry number exceeded quota. |The maximum number of outbound rules allowed for a single network ACL has been reached. |
|404 |InvalidNetworkAcl.NotFound |The specified Network ACL does not exist. |The specified network ACL does not exist. |
|404 |InvalidNetworkAclEntryId.NotFound |The specified Network ACL entry does not exist. |The specified network ACL rule ID does not exist. |
|409 |InvalidNetworkAclEntryId.Conflict |The specified Network ACL has duplicated entry id. |The specified network ACL contains duplicate rule IDs. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
