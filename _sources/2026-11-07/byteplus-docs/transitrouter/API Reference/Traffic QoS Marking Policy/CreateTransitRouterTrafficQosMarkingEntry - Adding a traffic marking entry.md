---
title: "CreateTransitRouterTrafficQosMarkingEntry - Adding a traffic marking entry"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingEntry"
---

Call the CreateTransitRouterTrafficQosMarkingEntry API to add entries to a traffic marking policy.

<span id=".5L2_55So6K-05piO"></span>
## Notes

A traffic marking policy supports a maximum of 100 entries by default.​ If the quota is insufficient, [create a quota modification application](https://docs.byteplus.com/en/docs/6837/129542) to request a quota increase.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Traffic marking may be impacted by adding traffic marking entries. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterTrafficQosMarkingEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|cOkMiP">必选</span> `Example: CreateTransitRouterTrafficQosMarkingEntry`

The interface name. The current API name is `CreateTransitRouterTrafficQosMarkingEntry`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|KtAiFL">必选</span>`Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple"> String  </span><span data-api-tag="require|xvjuFd">必选</span> `Example: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



**TransitRouterTrafficQosMarkingEntryName ** <span data-label="purple"> String </span>` optional` `Example: tme-02`

Name of the marking entry.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**Priority ** <span data-label="purple"> integer </span><span data-api-tag="require|Ehr9_6">必选</span>`Example: 100`

The priority of the marking entry. Value: 1\-10000 Priority values for different marking entries must be unique.



**Protocol ** <span data-label="purple"> String  </span>`optional` `Example: udp`

Protocol type.


* tcp: Transmission Control Protocol

* udp: User Datagram Protocol

* gre: Generic Routing Encapsulation​​

* icmp: Internet Control Message Protocol

* icmpv6: Internet Control Message Protocol version 6

* all (default): All protocols.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="default">You can set it to ICMPv6 only after enabling the TR IPv6 feature.</div>




**SourceCidrBlock ** <span data-label="purple"> String  </span><span data-api-tag="require|zrhjoE">必选</span> `Example: 192.168.XX.XX/24`

The CIDR block of the source IP address, supporting IPv4 and IPv6.


* When `Protocol` is set to tcp, udp, gre, or all, this parameter accepts IPv4/IPv6 CIDR blocks.

* When `Protocol` is set to icmp, this parameter only supports IPv4 CIDR blocks.

* When `Protocol` is set to icmpv6, this parameter only supports IPv6 CIDR blocks.



**DestinationCidrBlock ** <span data-label="purple"> String  </span><span data-api-tag="require|WpVdSm">必选</span> `Example: 192.168.XX.XX/24`

The CIDR block of the destination IP address, supporting IPv4 and IPv6.


* When `Protocol` is set to tcp, udp, gre, or all, this parameter accepts IPv4/IPv6 CIDR blocks.

* When `Protocol` is set to icmp, this parameter only supports IPv4 CIDR blocks.

* When `Protocol` is set to icmpv6, this parameter only supports IPv6 CIDR blocks.

* The IP CIDR block type of this parameter should match that of `SourceCidrBlock`, both IPv4 CIDR blocks or both IPv6 CIDR blocks.



**SourcePortStart ** <span data-label="purple"> Integer </span><span data-api-tag="require|Qyzetb">必选</span> `Example: 1`

Start value of the source port range. Value range: \-1, 1 to 65535.


* \-1 indicates no port restriction.​

* The value must be \-1 when `Protocol` is set to icmp, icmpv6, or gre.



**SourcePortEnd ** <span data-label="purple"> Integer </span><span data-api-tag="require|wey7hN">必选</span> `Example: 1`

End value of the source port range. Value range: \-1, 1 to 65535.


* \-1 indicates no port restriction.​

* The value must be \-1 when `Protocol` is set to icmp, icmpv6, or gre.



**DestinationPortStart ** <span data-label="purple"> Integer </span> `Example: 1`

Start value of the destination port range. Value range: \-1, 1 to 65535.


* \-1 indicates no port restriction.​

* The value must be \-1 when `Protocol` is set to icmp, icmpv6, gre, or all.



**DestinationPortEnd ** <span data-label="purple"> Integer </span><span data-api-tag="require|0uAi_o">必选</span>`Example: 1`

End value of the destination port range. Value range: \-1, 1 to 65535.


* \-1 indicates no port restriction.​

* The value must be \-1 when `Protocol` is set to icmp, icmpv6, gre, or all.



**MatchDscp ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

The DSCP is carried in the traffic packet. Value range: \-1, 0 to 63. The default value is \-1, meaning the packet's DSCP value can be any value to match this marking entry.



**RemarkingDscp ** <span data-label="purple"> Integer </span><span data-api-tag="require|xhDjw2">必选</span> `Example: 1`

This parameter specifies the DSCP value to apply to target traffic packets. Value range: 0\-63. Once target traffic successfully matches this marking entry, the DSCP of the traffic packets will be replaced with the value specified by this parameter.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: This traffic qos marking entry is used for test.`

The description of the marking entry.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

The Client Token that is used to ensure the request idempotency.


* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterTrafficQosMarkingEntryId ** <span data-label="purple"> String </span>`Example: tr-tme-1i5i8khf9m58gae5kcx6****`

ID of the marking entry.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateTransitRouterTrafficQosMarkingEntry&Version=2020-04-01&TransitRouterTrafficQosMarkingPolicyId=tr-tmp-hy13n2l4c6c0v****&Priority=100&SourceCidrBlock=192.168.XX.XX%2F24&DestinationCidrBlock=192.168.XX.XX%2F24&SourcePortStart=1&SourcePortEnd=1&DestinationPortStart=1&DestinationPortEnd=1&RemarkingDscp=1 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T083802Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202507311638051041080960773AC806",
    "Action": "CreateTransitRouterTrafficQosMarkingEntry",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterTrafficQosMarkingEntryId": "tr-tme-1i5i8khf9m58gae5kcx6****"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.TooLong |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action is unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.CidrProtocolMismatch |The specified cidr of the Transit Router traffic qos marking entry is invalid. The IP version of the source and destination cidr must match the specified network protocol. |The CIDR block of the specified marking entry is invalid. The source and destination CIDR blocks must be the same IP version as the specified network. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.CidrVersionMismatch |The specified cidr of the Transit Router traffic qos marking entry is invalid. The source and destination cidr must both IPv4 or IPv6. |The CIDR block of the specified marking entry is invalid. The source and destination CIDR blocks must both be IPv4 or both be IPv6. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.EndPortSmallerThanStart |The specified port range of the traffic qos marking entry is invalid with end port smaller than start port. |The specified port range is invalid. The end port must not be smaller than the start port. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidMatchDscp |The specified match dscp of the Transit Router traffic qos marking entry is invalid. Match dscp only support \-1, 0~63. |The match DSCP of the specified marking entry is invalid. It must be \-1 or an integer between 0 and 63. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidPriority |The specified priority of the Transit Router traffic qos marking entry is invalid. |The priority of the specified marking entry is invalid. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidProtocol |The specified protocol of the Transit Router traffic qos marking entry is invalid. |The network protocol for the specified marking entry is invalid. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidProtocolPort |The specified port range of the traffic qos marking entry is invalid with the protocol selected. |The specified port range is invalid under the selected protocol for the current traffic marking entry. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.InvalidRemarkingDscp |The specified remarking dscp of the Transit Router traffic qos marking entry is invalid. Remarking dscp only support 0~63. |The remarking DSCP of the specified marking entry is invalid. It must be an integer between 0 and 63. |
|400 |InvalidTransitRouterTrafficQosMarkingEntry.StartEndPortInconsistent |The specified port range of the traffic qos marking entry is invalid with one of the start/end port is "\-1", and the other is not. |The specified port range is invalid. If either the start or end port is set to "\-1", the other must also be set to "\-1", representing no port restriction. |
|400 |QuotaExceeded.TransitRouterTrafficQosMarkingEntry |You've reached the limit on the number of traffic qos marking entries that you can create on one traffic qos marking policy. |You have reached the maximum number of marking entries for a single traffic marking policy. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. Action unsupported. |
|404 |InvalidTransitRouterTrafficQosMarkingPolicy.NotFound |The specified Transit Router traffic qos marking policy does not exist. |The specified traffic marking policy does not exist. |
|409 |InvalidTransitRouterTrafficQosMarkingEntry.PriorityConflict |The specified priority of the traffic qos marking entry conflicts with another entry. |The priority of the specified marking entry conflicts with that of another entry. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
