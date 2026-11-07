---
title: "ModifyTrafficMirrorFilterRuleAttributes - Updating the filter rule attribute"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyTrafficMirrorFilterRuleAttributes"
---

Call the ModifyTrafficMirrorFilterRuleAttributes API to modify the filter rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If the following optional parameters are not configured, the existing configurations will be preserved.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTrafficMirrorFilterRuleAttributes&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|CLQfVU">必选</span> `Example value: ModifyTrafficMirrorFilterRuleAttributes`

The interface name. The current API name is `ModifyTrafficMirrorFilterRuleAttributes`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|9EPa6a">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TrafficMirrorFilterRuleId ** <span data-label="purple"> String </span><span data-api-tag="require|exYsGA">必选</span> `Example: tmr-j6cmls82xnc86vtpe****`

ID of the filter rule.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the ID of the filter rule within the traffic mirror filters.



**TrafficDirection** <span data-label="purple">String</span> `optional` `Example: ingress`

Direction of traffic. Valid values:


* ingress: Inbound.

* egress: Outbound.



**Priority ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The priority of the filter rule, ranging from 1 to 1000.


* A lower value indicates a higher priority. Default: 1, which is the highest priority.

* For the same Mirror Filter and the same direction (inbound/outbound), the priority must be unique.



**Policy ** <span data-label="purple"> String  </span>`optional` `Example value: accept`

Traffic collection policy. Valid values:


* accept: Allow. When traffic from the mirror site matches this rule, it is replicated to the mirror target for monitoring and analysis.

* Reject. When traffic from the mirror site matches this rule, it is not replicated, and monitoring/analysis for this traffic is denied.



**Protocol ** <span data-label="purple">String </span>`optional` `Example value: tcp`

Traffic protocol. Valid values:


* all: TCP, UDP, and ICMP protocols.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.



**SourceCidrBlock ** <span data-label="purple"> String  </span>`optional` `Example value: 100.100.0.0/16`

Traffic source CIDR block.



**SourcePortRange ** <span data-label="purple">String</span> `optional` `Example: -1/-1`

Traffic source port range.


* When `Protocol` is set to all or icmp, 

   * this parameter is not required.

   * Default: \-1/\-1, indicating no port restriction.

* When `Protocol` is set to tcp or udp, 

   * this parameter is required.

   * Value range: 1 to 65535.

   * Use a forward slash (/) to separate the start and end ports, e.g., 1/50, 80/80.



**DestinationCidrBlock ** <span data-label="purple"> String </span>`optional` `Example: 100.100.0.0/16`

Traffic destination CIDR block.



**DestinationPortRange ** <span data-label="purple"> String </span>`optional` `Example: -1/-1`

Traffic destination port range.


* When `Protocol` is set to all or icmp, 

   * this parameter is not required.

   * Default: \-1/\-1, indicating no port restriction.

* When `Protocol` is set to tcp or udp, 

   * this parameter is required.

   * Value range: 1 to 65535.

   * Use a forward slash (/) to separate the start and end ports, e.g., 1/50, 80/80.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: TM_FilterRule_1`

Description of the filter rule.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTrafficMirrorFilterRuleAttributes&Version=2020-04-01&TrafficMirrorFilterRuleId=tmr-j6cmls82xnc86vtpe****&Protocol=tcp HTTP/1.1
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
        "Action": "ModifyTrafficMirrorFilterRuleAttributes",
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


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDestinationCidrBlock.Malformed |The specified destination CIDR block is malformed. Currently only IPv4 is supported. |The specified destination CIDR block is invalid; currently only IPv4 is supported. |
|400 |InvalidDestinationPortRange.Malformed |The specified destination port range is malformed. |The specified destination port range is invalid. |
|400 |InvalidPolicy.Malformed |The specified policy is malformed. |The specified collection policy is invalid. |
|400 |InvalidPriority.Malformed |The specified priority is malformed. |The specified priority is invalid. |
|400 |InvalidProtocol.Malformed |The specified protocol is malformed. |The specified protocol is invalid. |
|400 |InvalidSourceCidrBlock.DestinationCidrBlockMismatch |The specified source and destination CIDR blocks are in different ether types. |The Ethernet types of the specified source and destination CIDR blocks do not match. |
|400 |InvalidSourceCidrBlock.Malformed |The specified source CIDR block is malformed. Currently only IPv4 is supported. |The specified source CIDR block is invalid; currently only IPv4 is supported. |
|400 |InvalidSourceCidrBlock.ProtocolMismatch |The specified source CIDR block and protocol are mismatch. |The specified source CIDR block does not match the protocol. |
|400 |InvalidSourcePortRange.Malformed |The specified source port range is malformed. |The specified source port range is invalid. |
|400 |InvalidTrafficDirection.Malformed |The specified traffic direction is malformed. |The specified traffic direction is invalid. |
|404 |InvalidTrafficMirrorFilterRule.NotFound |The specified traffic mirror filter rule does not exist. |The specified traffic mirror filter rule does not exist. |
|409 |InvalidTrafficMirrorFilterRule.Conflict |The specified rule conflicts with another in your traffic mirror filter. |The specified mirror traffic filter rule conflicts with another rule under the same mirror filter condition. |
|409 |InvalidTrafficMirrorFilterRulePriority.Conflict |The specified rule priority conflicts with another rule priority in your traffic mirror filter. |The specified Traffic Mirror Filter rule has a priority conflict with another rule under the same Traffic Mirror Filter. |
