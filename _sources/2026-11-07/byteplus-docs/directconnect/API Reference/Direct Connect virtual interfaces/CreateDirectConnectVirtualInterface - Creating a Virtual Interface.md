---
title: "CreateDirectConnectVirtualInterface - Creating a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectVirtualInterface"
---

Call CreateDirectConnectVirtualInterface to create a Virtual Interface.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You cannot enable **Network Quality Analyzer (NQA)**  and **Bidirectional Forwarding Detection (BFD)**  simultaneously.

* The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. If you do not enable NQA, avoid providing `EnableNqa`, `NqaDetectInterval`, or `NqaDetectMultiplier` during the call.

* For configuration limits on Virtual Interface interconnect IP, see [Virtual Interface FAQs](https://docs.byteplus.com/en/docs/directconnect/Virtual-interface#.5Yib5bu66Jma5ouf5o6l5Y-j5pe25pys56uvSVDjgIHlr7nnq69JUOaYr-WQpuaciemZkOWItu-8nw==).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectVirtualInterface&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Z7lxCq">必选</span> `Example: CreateDirectConnectVirtualInterface`

The interface name. The current API name is `CreateDirectConnectVirtualInterface`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Zlbq7W">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VirtualInterfaceName ** <span data-label="purple">String </span>`optional` `Example: test`

The name for the Virtual Interface.


* Must start with a letter or Chinese character. May include digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it empty, it defaults to the instance ID of the Virtual Interface.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

The description for the Virtual Interface.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|0CVVDS">必选</span> `Example: dcc-2fe3zsmkshs59g****`

The ID of the Direct Connect (DC) Connection associated with the Virtual Interface.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`optional` `Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway associated with the Virtual Interface.

You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the DC Gateway ID.



**VlanId ** <span data-label="purple">Integer </span><span data-api-tag="require|pOxugj">必选</span> `Example: 2000`

A VLAN ID for connecting to the on\-premises data center. Confirm that this VLAN ID is unoccupied. Range: 0–2999.


* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged virtual interface per DC Connection.

* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate virtual interface. This mode supports multiple virtual interfaces per DC Connection.



**LocalIp ** <span data-label="purple">String </span><span data-api-tag="require|7qQcbP">必选</span> `Example: 192.XX.XX.10/24`

Cloud gateway peer IP for the Virtual Interface.



**PeerIp ** <span data-label="purple">String </span><span data-api-tag="require|yiaKqs">必选</span> `Example: 192.XX.XX.20/24`

Your gateway peer IP of the Virtual Interface



**LocalIpv6Ip ** <span data-label="purple">String </span>`optional` `Example: fe80:XX::1/120`

The IPv6 address of Cloud gateway peer IP for the Virtual Interface.



**PeerIpv6Ip ** <span data-label="purple">String </span>`optional` `Example: fe80:XX::2/120`

The IPv6 address of Your gateway peer IP for the Virtual Interface.



**RouteType ** <span data-label="purple">String </span>`optional` `Example: Static`

The route type for the Virtual Interface. Values:


* BGP: BGP dynamic routing

* Static: Static routing



**EnableBfd ** <span data-label="purple">Boolean </span>`Optional` `Example: false`

Specify whether to enable BFD control packet. Values:


* true: Enable

* false (default): Disable



**EnableBfdEcho ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable BFD echo packet. Values:


* true: Enable

* false (default): Disable



**BfdDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

The time interval for detection. Unit: ms. Range: 200–1000. Default: 1000. Avoid providing this parameter if you do not enable BFD.



**BfdDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 3`

The number of BFD detection attempts. Valid range: 3–10. Default: 3. Avoid providing this parameter if you do not enable BFD.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Limited bandwidth for the Virtual Interface. Unit: Mbps.


* \-1 (default): No rate limiting.

* 1–100000: The maximum bandwidth on the outbound and inbound directions of the Virtual Interface. It cannot exceed the bandwidth of the DC Connection associated with the Virtual Interface. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the details of the DC Connection.

* If a Virtual Interface is associated with a Shared Line, it inherits the bandwidth of the Shared Line. You do not need to specify this parameter. If you need to specify this parameter, ensure that the value is consistent with the bandwidth of the Shared Line associated with the Virtual Interface. You can call [DescribeSharedDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeSharedDirectConnectConnections) to query Shared Line information. (The Shared Line feature is currently in the beta stage. Only accounts with this feature enabled can use it and access the related documentation. To request a trial, please contact your account manager.)



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key for the Virtual Interface.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:`, regardless of case.​ `volc:` and `sys:` prefixes are reserved for system tags. You cannot create tags starting with these prefixes.

* Must be 1 to 128 characters. May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).



**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value for the Virtual Interface.


* N represents the sequence number of a tag value. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive. Must not start or end with a space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide <code>Tags.N.Value</code>, you must provide <code>Tags.N.Key</code>.</div>




**EnableNqa ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Specify whether to enable NQA. Values:


* true: Enable

* false (default): Disable


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">NQA is available only when <code>RouteType</code> is <code>Static</code>.</div>




**NqaDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 3000`

The time interval for NQA to send consecutive packets. Unit: ms. Range: 1000–5000. Default: 2000. Avoid providing this parameter if you do not enable NQA.



**NqaDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 8`

The number of NQA detection attempts. If consecutive failure count reaches the set value for the detect multiplier, the system declares a faulty line. Valid range: 3–8. Default: 5. Avoid providing this parameter if you do not enable NQA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the line traffic nearly reaches the maximum bandwidth after enabling NQA, we recommend setting Detect multiplier to <code>8</code>.</div>




**GatewayType ** <span data-label="purple">String </span>`Optional` `Example: DCGW`

The gateway type associated with the Virtual Interface. Values:


* DCGW (default): Direct Connect Gateway.

* DXGW: Global Direct Exchange Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-7qthudw0ll6jmc****`

The ID of the newly created Virtual Interface.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=CreateDirectConnectVirtualInterface&Version=2020-04-01&VirtualInterfaceName=test&Description=This is a sample description&DirectConnectConnectionId=dcc-2fe3zsmkshs59g****&DirectConnectGatewayId=dcg-7qthudw0ll6jmc****&VlanId=2000&LocalIp=192.XX.XX.10/24&PeerIp=192.XX.XX.20/24&LocalIpv6Ip=fe80:XX::1/120&PeerIpv6Ip=fe80:XX::2/120&RouteType=Static&EnableBfd=false&EnableBfdEcho=false&BfdDetectInterval=1000&BfdDetectMultiplier=3&Bandwidth=100&Tags.1.Key=key1&Tags.1.Value=value1&EnableNqa=true&NqaDetectInterval=3000&NqaDetectMultiplier=8&GatewayType=DCGW HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateDirectConnectVirtualInterface",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "VirtualInterfaceId": "dcv-7qthudw0ll6jmc****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.VirtualInterfacePerGateway |You've reached the limit on the number of virtual interfaces per direct connect gateway that you can create. |You have reached the maximum number of Virtual Interfaces that can be created per DC Gateway. |
|400 |QuotaExceeded.VirtualInterfacePerConnection |You've reached the limit on the number of virtual interfaces per direct connect connection that you can create. |You have reached the maximum number of Virtual Interfaces that can be created per DC Connection. |
|400 |InvalidDirectConnectVirtualInterface.LocalIpMalformed |The specified virtual interface local IP is malformed. |The specified Cloud gateway peer IP for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpMalformed |The specified virtual interface peer IP is malformed. |The specified Your gateway peer IP for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpMismatch |The specified virtual interface Peer IP and Local IP are not in the same subnet. |The specified Your gateway peer IP for the Virtual Interface is not within the same subnet as Cloud gateway peer IP. |
|400 |InvalidDirectConnectVirtualInterface.VlanIdMalformed |The specified virtual interface Vlan ID is malformed. |The specified VLAN ID for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.RouteTypeMalformed |The specified virtual interface route type is malformed. |The specified route type for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.ConnectionIsShared |The specified virtual interface connection is shared. You can not create a new virtual interface which Vlan ID is 0. |The Direct Connect of the specified Virtual Interface is shared. You cannot create a new Virtual Interface with a VLAN ID of 0. |
|400 |InvalidDirectConnectVirtualInterface.ConnectionIsExclusive |The specified virtual interface connection is exclusive. You can not create another virtual interface. |The Direct Connect of the specified Virtual Interface is dedicated. You cannot create any new Virtual Interfaces. |
|400 |InvalidDirectConnectVirtualInterface.DirectConnectGatewayMismatch |The specified direct connect gateway and connection are in different switches. |The specified DC Gateway and DC Connection are not on the same access switch. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMismatch |The specified bandwidth of virtual interface is inconsistent with the bandwidth of the shared connection. |The specified bandwidth for the Virtual Interface does not match that of the Shared Line. |
|400 |InvalidDirectConnectVirtualInterface.BfdBfdEchoBothEnabled |The specified virtual interface does not support enabling bfd and bfd echo at the same time. |The specified Virtual Interface does not support enabling BFD control packet and echo packet simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.VlanIdMismatch |TThe specified Vlan ID of virtual interface is inconsistent with the Vlan ID of the shared connection. |The specified VLAN ID of the Virtual Interface does not match that of the Shared Line. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthExceeded |The specified bandwidth of virtual interface exceeds the bandwidth of physical connection. |The specified bandwidth for the Virtual Interface exceeds that of the DC Connection. |
|400 |InvalidDirectConnectVirtualInterface.EnableBfdMismatch |The specified virtual interface route type does not support enable bfd. |The specified route type of the Virtual Interface does not support enabling BFD. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectIntervalMalformed |The specified bfd detect interval is malformed. It can only be set when bfd is enabled, and the value should be between 200 and 1000. |The specified detect interval for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 200 to 1000. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectMultiplierMalformed |The specified bfd detect multiplier is malformed. It can only be set when bfd is enabled, and the value should be between 3 and 10. |The specified detect multiplier for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 3 to 10. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectVirtualInterface.EnableNqaMismatch |The specified virtual interface route type does not support enable nqa. |The specified route type of the Virtual Interface does not support enabling NQA. |
|400 |InvalidDirectConnectVirtualInterface.NqaBfdEchoBothEnabled |The specified virtual interface does not support enabling bfd echo and nqa at the same time. |The specified Virtual Interface does not support enabling BFD and NQA simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectIntervalMalformed |The specified nqa detect interval is malformed. It can only be set when nqa is enabled, and the value should be between 1000 and 5000. |The specified Detect interval for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 1,000 to 5,000. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectMultiplierMalformed |The specified nqa detect multiplier is malformed. It can only be set when nqa is enabled, and the value should be between 3 and 8. |The specified detect multiplier for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 3 to 8. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidDirectConnectGateway.InvalidBusinessStatus |The specified direct connect gateway is not in the correct status for the request. The specified direct connect gateway is in freeze. |The specified DC Gateway cannot respond to this request due to its status. The current DC Gateway is frozen. |
|400 |InvalidDirectConnectVirtualInterface.GatewayIpv6NotEnable |The specified direct connect gateway does not enable IPv6. |The specified DC Gateway does not have IPv6 enabled. |
|400 |InvalidDirectConnectVirtualInterface.Ipv6IpMissing |The specified virtual interface local IPv6 IP or peer IPv6 IP is missing, they must either both be configured or not configured at all. |The specified Virtual Interface must have IPv6 addresses for both your gateway and cloud gateway specified simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.LocalIpv6IpMalformed |The specified virtual interface local IPv6 address is malformed. |The specified Cloud gateway peer IPv6 for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpv6IpMalformed |The specified virtual interface peer IPv6 address is malformed. |The specified Your gateway peer IPv6 for the Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpv6IPMismatch |The specified virtual interface Peer IPv6 IP and Local IPv6 IP are not in the same subnet. |The specified Your gateway peer IPv6 for the Virtual Interface is not within the same subnet as the Cloud gateway peer IPv6. |
|400 |InvalidDirectConnectVirtualInterface.NqaBfdBothEnabled |The specified virtual interface does not support enabling bfd and nqa at the same time. |The specified Virtual Interface does not support enabling BFD and NQA simultaneously. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |You have reached the maximum bandwidth allocable to the DC Connection. |
|400 |InvalidDirectConnectTrafficQosPolicy.DirectConnectConnectionWithDifferentQos |In the direct connect gateway with multiple direct connect connections scene, it is not supported to associate with different qos policy in all direct connect connections. |When multiple DC Connections are associated with the same DC Gateway, all DC Connections must have the same QoS Policy. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to perform IPv6 actions. |
|403 |Forbidden |You are not authorized to perform nqa operations on the specified virtual interface. |No permission to perform NQA on the specified Virtual Interface. |
|403 |InvalidDirectConnectVirtualInterface.BfdEchoForbidden |You are not authorized to perform bfd echo operations on the specified virtual interface. |No permission to perform BFD echo on the specified Virtual Interface. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
|409 |InvalidDirectConnectVirtualInterface.PeerIpConflict |The specified virtual interface peer IP conflicts with its local IP. |The specified Your gateway peer IP for the Virtual Interface conflicts with the Cloud gateway peer IP. |
|409 |InvalidDirectConnectVirtualInterface.VlanIdConflict |The specified virtual interface Vlan ID already exists. |The specified VLAN ID for the Virtual Interface already exists. |
|409 |InvalidDirectConnectVirtualInterface.LocalIpConflict |The specified virtual interface local IP already exists. |The specified Cloud gateway peer IP for the Virtual Interface already exists. |
|409 |InvalidDirectConnectVirtualInterface.PeerIpv6IpConflict |The specified virtual interface peer IPv6 IP conflicts with its local IPv6 IP. |The specified Your gateway peer IPv6 for the Virtual Interface conflicts with Cloud gateway peer IPv6. |
|409 |InvalidDirectConnectVirtualInterface.LocalIpv6IpConflict |The subnet of the specified virtual interface local IPv6 IP overlaps with another virtual interface. |The subnet of the specified Cloud gateway peer IPv6 for the Virtual Interface overlaps with the subnet of another Virtual Interface. |
