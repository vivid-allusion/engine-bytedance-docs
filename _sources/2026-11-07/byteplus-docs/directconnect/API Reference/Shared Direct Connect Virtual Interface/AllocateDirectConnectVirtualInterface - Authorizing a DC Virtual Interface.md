---
title: "AllocateDirectConnectVirtualInterface - Authorizing a DC Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/AllocateDirectConnectVirtualInterface"
---

Call AllocateDirectConnectVirtualInterface to create a Shared Virtual Interface for another account.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You have acquired the ID of BytePlus account that requires a Shared Virtual Interface.

* You cannot enable **Network Quality Analyzer (NQA)**  and **Bidirectional Forwarding Detection (BFD)**  simultaneously.

* The NQA feature is currently in the beta stage. If you need a trial, please contact your account manager. If you do not enable NQA, avoid providing `EnableNqa`, `NqaDetectInterval`, or `NqaDetectMultiplier` during the call.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Shared Virtual Interface is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AllocateDirectConnectVirtualInterface&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|PW7iyk">必选</span> `Example: AllocateDirectConnectVirtualInterface`

The interface name. The current API name is `AllocateDirectConnectVirtualInterface`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|cNibLE">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|oAJxPm">必选</span> `Example: dcc-2fe3zsmkshs59g****`

ID of the DC Connection associated with the Shared Virtual Interface.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.



**LocalIp ** <span data-label="purple">String </span><span data-api-tag="require|1hyEFA">必选</span> `Example: 192.XX.XX.10/24`

Cloud gateway peer IP for the Shared Virtual Interface.



**OwnerAccountId ** <span data-label="purple">String </span><span data-api-tag="require|HBgxIU">必选</span> `Example: 2100052****`

ID of the BytePlus account that uses the Shared Virtual Interface.



**PeerIp ** <span data-label="purple">String </span><span data-api-tag="require|4PNvPs">必选</span> `Example: 192.XX.XX.20/24`

Your gateway peer IP for the Shared Virtual Interface.



**VlanId ** <span data-label="purple">Integer </span><span data-api-tag="require|whALB3">必选</span> `Example: 2000`

A VLAN ID for connecting to the on\-premises data center. Confirm that this VLAN ID is unoccupied. Range: 0–2999.


* 0: The DC Connection's switch port operates in Layer 3 routing mode with no VLAN configured. This mode supports only a single untagged Shared Virtual Interface per DC Connection.

* 1–2999: The DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate Virtual Interface. This mode supports multiple Shared Virtual Interfaces per DC Connection.



`**VirtualInterfaceName ** <span data-label="purple">String </span>`optional` `Example: Share-dcv`

Name of the Shared Virtual Interface.


* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it empty, it defaults to the instance ID of the Shared Virtual Interface.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the Shared Virtual Interface.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Limited bandwidth of the Shared Virtual Interface. Unit: Mbps.


* \-1 (default): No rate limiting.

* Must not exceed the bandwidth of the associated DC Connection.

* If a DC Virtual Interface is associated with a Shared Line, it inherits the bandwidth of the Shared Line, which is unchangeable.



**RouteType ** <span data-label="purple">String </span>`optional` `Example: Static`

Route types for Shared Virtual Interface. Values:


* BGP: BGP dynamic routing

* Static: Static routing



**EnableBfd ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable BFD. Type in the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enabled

* false (default): Do not enable



**BfdDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

The time interval for detection. Unit: ms. Range: 200–1000. Default: 1000. Avoid providing this parameter if you do not enable BFD.



**BfdDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 3`

The number of BFD detection attempts. Valid range: 3–10. Default: 3. Avoid providing this parameter if you do not enable BFD.



**EnableNqa ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Specify whether to enable NQA. Values:


* true: Enable

* false (default): Disable

> Description

> NQA is available only when `RouteType` is `Static`.



**NqaDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 3000`

The time interval for NQA to send consecutive packets. Unit: ms. Range: 1000–5000. Default: 2000. Avoid passing this parameter if you do not enable NQA.



**NqaDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 8`

The number of NQA detection attempts. If consecutive failure count reaches the set value for the detect multiplier, the system declares a faulty line. Valid range: 3–8. Default: 5. Avoid providing this parameter if you do not enable NQA.

> Explain

> If the line traffic nearly reaches the maximum bandwidth after enabling NQA, we recommend setting Detect multiplier to `8`.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

Key of the Shared Virtual Interface tag.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag keys with ampersands (&).

* Cannot start with `volc:` or `sys:` in any case form. `volc:` and `sys:` prefixes are reserved for system tags. You cannot create tags starting with these prefixes.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).



**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the Shared Virtual Interface.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive. Must not start or end with a space.

> Explain

> To provide `Tags.N.Value`, you must provide `Tags.N.Key`.



**EnableBfdEcho ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable BFD echo packet. Values:


* true: Enabled

* false (default): Not enabled



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-7qthudw0ll6jmc****`

ID of the newly created Shared Virtual Interface.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AllocateDirectConnectVirtualInterface&Version=2020-04-01&DirectConnectConnectionId=dcc-2fe3zsmkshs59g****&LocalIp=192.XX.XX.10/24&OwnerAccountId=2100052****&PeerIp=192.XX.XX.20/24&VlanId=2000&VirtualInterfaceName=Share-dcv&Description=This is a sample description&Bandwidth=100&RouteType=Static&EnableBfd=false&BfdDetectInterval=1000&BfdDetectMultiplier=3&EnableNqa=true&NqaDetectInterval=3000&NqaDetectMultiplier=8&Tags.1.Key=key1&Tags.1.Value=value1&EnableBfdEcho=false HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202405101632430CEFC9A53DA1A20FD8B9",
        "Action": "AllocateDirectConnectVirtualInterface",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202405101632430CEFC9A53DA1A20F****",
        "VirtualInterfaceId": "dcv-12al2nocyjcw017q7y2g0****"
    }
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthExceeded |The specified bandwidth of virtual interface exceeds the bandwidth of physical connection. |The specified bandwidth for the DC Virtual Interface exceeds the bandwidth of the DC Connection. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMismatch |The specified bandwidth of virtual interface is inconsistent with the bandwidth of the shared connection. |The specified bandwidth for the DC Virtual Interface does not match that of the Shared Line. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectIntervalMalformed |The specified bfd detect interval is malformed. It can only be set when bfd is enabled, and the value should be between 200 and 1000. |The specified Detect interval for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 200 to 1000. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectMultiplierMalformed |The specified bfd detect multiplier is malformed. It can only be set when bfd is enabled, and the value should be between 3 and 10. |The specified detect multiplier for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 3 to 10. |
|400 |InvalidDirectConnectVirtualInterface.ConnectionIsExclusive |The specified virtual interface connection is exclusive. You can not create another virtual interface. |The Direct Connect of the specified DC Virtual Interface is exclusive. You cannot create any new DC Virtual Interfaces. |
|400 |InvalidDirectConnectVirtualInterface.ConnectionIsShared |The specified virtual interface connection is shared. You can not create a new virtual interface which Vlan ID is 0. |The Direct Connect of the specified DC Virtual Interface is shared. You cannot create a new DC Virtual Interface with a VLAN ID of 0. |
|400 |InvalidDirectConnectVirtualInterface.EnableBfdMismatch |The specified virtual interface route type does not support enable bfd. |The specified route type of the DC Virtual Interface does not support enabling BFD. |
|400 |InvalidDirectConnectVirtualInterface.EnableNqaMismatch |The specified virtual interface route type does not support enable nqa. |The specified route type of the DC Virtual Interface does not support enabling NQA. |
|400 |InvalidDirectConnectVirtualInterface.LocalIpMalformed |The specified virtual interface local IP is malformed. |The specified Cloud gateway peer IP of the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.NqaBfdBothEnabled |The specified virtual interface does not support enabling bfd and nqa at the same time. |The specified DC Virtual Interface does not support enabling BFD and NQA simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectIntervalMalformed |The specified nqa detect interval is malformed. It can only be set when nqa is enabled, and the value should be between 1000 and 5000. |The specified Detect interval for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 1000 to 5000. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectMultiplierMalformed |The specified nqa detect multiplier is malformed. It can only be set when nqa is enabled, and the value should be between 3 and 8. |The specified detect multiplier for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 3 to 8. |
|400 |InvalidDirectConnectVirtualInterface.OwnerAccountIdMalformed |The specified virtual interface owner account ID is malformed. |The owner account ID of the specified DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpMalformed |The specified virtual interface peer IP is malformed. |The specified Your gateway peer IP for the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpMismatch |The specified virtual interface Peer IP and Local IP are not in the same subnet. |The specified Your gateway peer IP for the DC Virtual Interface is not within the same subnet as Cloud gateway peer IP. |
|400 |InvalidDirectConnectVirtualInterface.RouteTypeMalformed |The specified virtual interface route type is malformed. |The specified route type for the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.VlanIdMalformed |The specified virtual interface Vlan ID is malformed. |The specified VLAN ID for the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.VlanIdMismatch |The specified Vlan ID of virtual interface is inconsistent with the Vlan ID of the shared connection. |The specified VLAN ID of the DC Virtual Interface does not match that of the Shared Line. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |QuotaExceeded.VirtualInterfacePerConnection |You've reached the limit on the number of virtual interfaces per direct connect connection that you can create. |You have reached the maximum number of DC Virtual Interfaces that can be created per DC Connection. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |You have reached the maximum bandwidth allocable to the DC Connection. |
|400 |InvalidDirectConnectTrafficQosPolicy.DirectConnectConnectionWithSharedVif |It is not supported to associate the qos policy for direct connect connection associated with shared direct connect virtual interfaces. |The DC Connection associated with a Shared Virtual Interface does not support associating QoS policies. |
|403 |Forbidden |You are not authorized to perform nqa operations on the specified virtual interface. |No permission to perform NQA on the specified DC Virtual Interface. |
|403 |InvalidDirectConnectVirtualInterface.CrossAccountForbidden |You are not authorized to allocate the specified virtual interface to other account. |No permission to share the specified DC Virtual Interface to another account. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|409 |InvalidDirectConnectVirtualInterface.LocalIpConflict |The specified virtual interface local IP already exists. |The specified Cloud gateway peer IP for the DC Virtual Interface exists. |
|409 |InvalidDirectConnectVirtualInterface.OwnerAccountIdConflict |The specified owner account ID is equal to current user. |The specified Virtual Interface owner account ID is the same as the current account ID. |
|409 |InvalidDirectConnectVirtualInterface.PeerIpConflict |The specified virtual interface peer IP conflicts with its local IP. |The specified Your gateway peer IP for the DC Virtual Interface conflicts with the Cloud gateway peer IP. |
|409 |InvalidDirectConnectVirtualInterface.VlanIdConflict |The specified virtual interface Vlan ID already exists. |The specified VLAN ID for the DC Virtual Interface exists. |
