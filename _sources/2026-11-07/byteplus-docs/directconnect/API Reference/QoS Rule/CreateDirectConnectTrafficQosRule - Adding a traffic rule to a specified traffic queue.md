---
title: "CreateDirectConnectTrafficQosRule - Adding a traffic rule to a specified traffic queue"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosRule"
---

Call CreateDirectConnectTrafficQosRule to add a traffic rule to a specified traffic queue.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

For more details and limits about traffic rules, see [QoS Policy overview](https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectTrafficQosRule&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|AH7NIR">必选</span> `Example: CreateDirectConnectTrafficQosRule`

The interface name. The current API name is `CreateDirectConnectTrafficQosRule`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|qHxOzQ">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|wI0L2D">必选</span> `Example: dcq-1234565`

The ID of the QoS policy that owns the traffic queue for the traffic rule will be associated. You can call [DescribeDirectConnectTrafficQosPolicies](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies) to query the QoS policy ID.



**DirectConnectTrafficQosQueueId** <span data-label="purple">String</span> <span data-api-tag="require|rGEflp">必选</span> `Example: dqq-1234565`

The ID of the traffic queue with which the traffic rule is to be associated.

You can call [DescribeDirectConnectTrafficQosQueues](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues) to query the traffic queue ID.



**Priority ** <span data-label="purple">Integer </span><span data-api-tag="require|Y0KLMP">必选</span> `Example: 1`

The priority of the traffic rule.


* Value range: **1\-10000**. A smaller number indicates higher priority.

* The priority values for traffic rules within the same QoS policy must be unique.



**Protocol ** <span data-label="purple">String </span>`optional` `Example: TCP`

Protocol type. Values:


* ICMP

* ICMPV6

* TCP

* UDP

* GRE

* ALL (default): Support all protocols


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Direct Connect IPv6 feature is in the beta stage. The protocol type can be set to <code>ICMPV6</code> only after the IPv6 feature is enabled. If needed, please contact your account manager.</div>




**SourceCidrBlock ** <span data-label="purple">String </span><span data-api-tag="require|eAyYGC">必选</span> `Example: 10.0.0.0/24`

Source IPv4 CIDR or IPv6 CIDR.


* When `Protocol` is TCP, UDP, GRE or ALL, IPv4 or IPv6 CIDR blocks can be provided.

* When `Protocol` is ICMP, only IPv4 CIDR blocks are supported.

* When `Protocol` is ICMPV6, only IPv6 CIDR blocks are supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>DestinationCidrBlock</code> must have the same IP type as <code>SourceCidrBlock</code>. That is, both are IPv4 CIDR blocks or IPv6 CIDR blocks.</div>




**DestinationCidrBlock ** <span data-label="purple">String </span><span data-api-tag="require|rROYU7">必选</span> `Example: 10.0.0.0/24`

Destination IPv4 CIDR or IPv6 CIDR.


* When `Protocol` is TCP, UDP, GRE or ALL, IPv4 or IPv6 CIDR blocks can be provided.

* When `Protocol` is ICMP, only IPv4 CIDR blocks are supported.

* When `Protocol` is ICMPV6, only IPv6 CIDR blocks are supported.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>DestinationCidrBlock</code> must have the same IP type as <code>SourceCidrBlock</code>. That is, both are IPv4 CIDR blocks or IPv6 CIDR blocks.</div>




**SourcePortStart ** <span data-label="purple">Integer </span><span data-api-tag="require|AakxOJ">必选</span> `Example: 1`

The start value of the source port number range.


* When `Protocol` is TCP, UDP, or ALL, the valid range is  **\-1** and **1\-65535**. \-1 indicates no port restriction.​

* When `Protocol` is ICMP, ICMPV6, or GRE, only "\-1" is supported, indicating no port restriction.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>SourcePortStart</code> must have the same value as <code>SourcePortEnd</code>.</div>




**SourcePortEnd ** <span data-label="purple">Integer </span><span data-api-tag="require|36Xqd4">必选</span> `Example: 1`

The end value of the source port number range.


* When `Protocol` is TCP, UDP, or ALL, the valid range is  **\-1**, **1\-65535**. \-1 indicates no port restriction.​

* When `Protocol` is ICMP, ICMPV6, or GRE, only "\-1" is supported, indicating no port restriction.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>SourcePortEnd</code> must have the same value as <code>SourcePortStart</code>.</div>




**DestinationPortStart ** <span data-label="purple">Integer </span><span data-api-tag="require|XPyYaA">必选</span> `Example: 1`

The start value of the destination port number range.


* When `Protocol` is TCP or UDP, the valid range is  **\-1** and **1\-65535**. \-1 indicates no port restriction.​

* When `Protocol` is ICMP, ICMPV6, GRE, or ALL, only "\-1" is supported, indicating no port restriction.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>DestinationPortStart</code> must have the same value as <code>DestinationPortEnd</code>.</div>




**DestinationPortEnd ** <span data-label="purple">Integer </span><span data-api-tag="require|WWDzA0">必选</span> `Example: 1`

The end value of the destination port number range.


* When `Protocol` is TCP or UDP, the valid range is  **\-1** and **1\-65535**. \-1 indicates no port restriction.​

* When `Protocol` is ICMP, ICMPV6, GRE, or ALL, only "\-1" is supported, indicating no port restriction.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>DestinationPortEnd</code> must have the same value as <code>DestinationPortStart</code>.</div>




**DirectConnectTrafficQosRuleName ** <span data-label="purple">String </span>`optional` `Example: dqr-name`

The name of the traffic rule.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left empty, this parameter defaults to the traffic rule ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: dqr-description`

The description of the traffic rule.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**MatchDscp** <span data-label="purple">Integer</span> `optional` `Example: 20`

The original DSCP value carried by traffic entering the DC gateway before. Value range: **0**\-**63.** 



**RemarkingDscp ** <span data-label="purple">Integer </span>`optional` `Example: 53`

The new DSCP value set for the traffic that matches the traffic rule is used to classify and mark the traffic entering DC gateway. Value range: **0\-63**. Use \-1 if not effective.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectTrafficQosRuleId ** <span data-label="purple">String </span>`Example: dqr-2fezs9g1xwy6859gp67ty****`

The ID of the traffic rule.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectTrafficQosRule&Version=2020-04-01&DirectConnectTrafficQosPolicyId=dcq-12aso41dvse8017q7y2m****&DirectConnectTrafficQosQueueId=dqq-in0gqqzwvi808gbssyj5****&Priority=51&Protocol=ALL&SourceCidrBlock=0.0.0.0/0&DestinationCidrBlock=0.0.0.0/0&SourcePortStart=-1&SourcePortEnd=-1&DestinationPortStart=-1&DestinationPortEnd=-1&MatchDscp=51&RemarkingDscp=-1 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202411071604527CCC8DCFE9DB825****",
        "Action": "CreateDirectConnectTrafficQosRule",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202411071604527CCC8DCFE9DB825****",
        "DirectConnectTrafficQosRuleId": "dqr-2fezs9g1xwy6859gp67ty****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.DefaultQueueTypeUnsupported |It is not supported to operate the direct connect traffic qos queue with default queue type. |Actions on the default\-type traffic queues are not supported. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidStatus |The specified direct connect traffic qos queue is not in the correct status for the request. |The specified QoS traffic queue cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosRule.CidrProtocolMismatch |The specified cidr of the direct connect traffic qos rule is invalid. The IP version of the source and destination cidr must match the specified network protocol. |The CIDR block specified for the traffic rule is invalid. The source and destination CIDR blocks must be the same IP version as the specified network. |
|400 |InvalidDirectConnectTrafficQosRule.CidrVersionMismatch |The specified cidr of the direct connect traffic qos rule is invalid. The source and destination cidr must both IPv4 or IPv6. |The CIDR block specified for the QoS traffic rule is invalid. The source and destination CIDR blocks must both be either IPv4 or IPv6. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidMatchDscp |The specified match dscp of the direct connect traffic qos rule is invalid. Match dscp only support \-1, 0~63. |The match DSCP of the specified traffic rule is invalid. It must be \-1 or an integer between 0 and 63. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidPort |The specified port range of the direct connect traffic qos rule is invalid with one of the start port is not equal with the end port. |The specified port number range is invalid. The start and end ports must be the same. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidPriority |The specified priority of the direct connect traffic qos rule is invalid. |The priority specified for the traffic rule is invalid. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidProtocol |The specified protocol of the direct connect traffic qos rule is invalid. |The network protocol specified for the QoS traffic rule is invalid. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidProtocolPort |The specified port range of the direct connect traffic qos rule is invalid with the protocol selected. |The specified port number range is invalid under the selected protocol for the current traffic rule. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidRemarkingDscp |The specified remarking dscp of the direct connect traffic qos rule is invalid. Remarking dscp only support \-1, 0~63. |The retagged DSCP of the specified QoS traffic rule is invalid. It must be \-1 or an integer between 0 and 63. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |QuotaExceeded.DcTrafficQosRule |You've reached the limit on the number of traffic qos rules that you can create. |You have reached the maximum number of QoS traffic rules that can be created. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to operate IPv6. |
|404 |InvalidDirectConnectTrafficQosPolicy.NotFound |The specified direct connect traffic qos policy does not exist. |The specified QoS policy does not exist. |
|404 |InvalidDirectConnectTrafficQosQueue.NotFound |The specified direct connect traffic qos queue does not exist. |The specified QoS traffic queue does not exist. |
|409 |InvalidDirectConnectTrafficQosRule.PriorityConflict |The specified priority of the direct connect traffic qos rule conflicts with another rule. |The specified QoS traffic rule priority conflicts with that of another rule. |
|409 |InvalidDirectConnectTrafficQosRule.RuleContentConflict |The specified content of the direct connect traffic qos rule conflicts with another rule. |The specified QoS traffic rule configuration conflicts with that of another rule. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
