---
title: "ModifyDirectConnectVirtualInterfaceAttributes - Modifying information for a DC Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectVirtualInterfaceAttributes"
---

Call ModifyDirectConnectVirtualInterfaceAttributes to modify the name, description, and configurations of the specified DC Virtual Interface.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The Network Quality Analyzer (NQA) feature is currently in the beta stage. If you need a trial, please contact your account manager. If you do not enable NQA, avoid providing `EnableNqa`, `NqaDetectInterval`, or `NqaDetectMultiplier` during the call.

* You can call ModifyDirectConnectVirtualInterfaceAttributes to add IPv6 addresses for Cloud gateway peer IP and Your gateway peer IP of a DC Virtual Interface, subject to the following limits:

   * Only support adding new IPv6 addresses. Modifying or deleting existing IPv6 addresses is unsupported.

   * Only support simultaneously adding IPv6 addresses for Cloud gateway peer IP and Your gateway peer IP. Adding either side separately is unsupported.

* You cannot enable Network Quality Analyzer (NQA) and Bidirectional Forwarding Detection (BFD) simultaneously.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectVirtualInterfaceAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|c6mgXv">必选</span> `Example: ModifyDirectConnectVirtualInterfaceAttributes`

The interface name. The current API name is `ModifyDirectConnectVirtualInterfaceAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|kKkOZ7">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VirtualInterfaceId ** <span data-label="purple">String </span><span data-api-tag="require|Y5K5rn">必选</span> `Example: dcv-7qthudw0ll6jmc****`

The ID of the DC Virtual Interface to be modified.

You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the DC Virtual Interface.



**VirtualInterfaceName ** <span data-label="purple">String </span>`optional` `Example: test`

Name of the DC Virtual interface.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the name of the DC Virtual Interface.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the DC Virtual Interface.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the name of the DC Virtual Interface.



**EnableBfd ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable BFD control packet. Values:


* true: Enable

* false: Disable.


You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query `RouteType`.



**EnableBfdEcho ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable BFD echo packet. Values:


* true: Enable

* false: Disable.


You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query `EnableBfdEcho`.



**BfdDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 1000`

The time interval for detection. Unit: ms. Range: 200–1000. Default: 1000. Avoid providing this parameter if you do not enable BFD.



**BfdDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 3`

The number of BFD detection attempts. Valid range: 3–10. Default: 3. Avoid providing this parameter if you do not enable BFD.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 100`

Bandwidth of the DC Virtual Interface. Unit: Mbps.


* \-1: No rate limiting.

* 1–100000: The maximum bandwidth on the outbound and inbound directions of the DC Virtual Interface. It cannot exceed the bandwidth of the DC Connection associated with the DC Virtual Interface. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the details of the DC Connection.

* If a DC Virtual Interface is associated with a Shared Line, it inherits the bandwidth of the Shared Line. You do not need to specify this parameter. If you need to specify this parameter, ensure that the value is consistent with the bandwidth of the Shared Line associated with the DC Virtual Interface. You can call [DescribeSharedDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeSharedDirectConnectConnections) to query Shared Line information. (The Shared Line feature is currently in the beta stage. Only accounts with this feature enabled can use it and access the related documentation. If you need a trial, please contact your account manager.)

* If left blank, the current configuration remains.



**EnableNqa ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Specify whether to enable NQA. Values:


* true: Enable

* false (default): Disable


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">NQA is available only when <code>RouteType</code> is <code>Static</code>.</div>


* <div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces">DescribeDirectConnectVirtualInterfaces</a> to query <code>RouteType</code>.</div>




**NqaDetectInterval ** <span data-label="purple">Integer </span>`optional` `Example: 3000`

The time interval for NQA to send consecutive packets. Unit: ms. Range: 1000–5000. Default: 2000. Avoid passing this parameter if you do not enable NQA.



**NqaDetectMultiplier ** <span data-label="purple">Integer </span>`optional` `Example: 8`

The number of NQA detection attempts. If consecutive failure count reaches the set value for the detect multiplier, the system declares a faulty line. Valid range: 3–8. Default: 5. Avoid providing this parameter if you do not enable NQA.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the line traffic nearly reaches the maximum bandwidth after enabling NQA, we recommend setting Detect multiplier to <code>8</code>.</div>




**LocalIpv6Ip ** <span data-label="purple">String </span>`optional` `Example: fe80:XX::1/120`

IPv6 address of Cloud gateway peer IP for the DC Virtual Interface.



**PeerIpv6Ip ** <span data-label="purple">String </span>`optional` `Example: fe80:XX::2/120`

IPv6 address of Your gateway peer IP for the DC Virtual Interface.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectVirtualInterfaceAttributes&Version=2020-04-01&VirtualInterfaceId=dcv-7qthudw0ll6jmc****&VirtualInterfaceName=test&Description=This is a sample description&EnableBfd=false&EnableBfdEcho=false&BfdDetectInterval=1000&BfdDetectMultiplier=3&Bandwidth=100&EnableNqa=true&NqaDetectInterval=3000&NqaDetectMultiplier=8&LocalIpv6Ip=fe80:XX::1/120&PeerIpv6Ip=fe80:XX::2/120 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "ModifyDirectConnectVirtualInterfaceAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMismatch |The specified bandwidth of virtual interface is inconsistent with the bandwidth of the shared connection. |The specified bandwidth for the DC Virtual Interface does not match that of the Shared Line. |
|400 |InvalidDirectConnectVirtualInterface.BfdBfdEchoBothEnabled |The specified virtual interface does not support enabling bfd and bfd echo at the same time. |The specified DC Virtual Interface does not support enabling BFD control packet and echo packet simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthMalformed |The specified bandwidth is malformed. |The specified bandwidth is invalid. |
|400 |InvalidDirectConnectVirtualInterface.BandwidthExceeded |The specified bandwidth of virtual interface exceeds the bandwidth of physical connection. |The specified bandwidth for the DC Virtual Interface exceeds the bandwidth of the DC Connection. |
|400 |InvalidDirectConnectVirtualInterface.EnableBfdMismatch |The specified virtual interface route type does not support enable bfd. |The specified route type of the DC Virtual Interface does not support enabling BFD. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectIntervalMalformed |The specified bfd detect interval is malformed. It can only be set when bfd is enabled, and the value should be between 200 and 1000. |The specified Detect interval for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 200 to 1000. |
|400 |InvalidDirectConnectVirtualInterface.BfdDetectMultiplierMalformed |The specified bfd detect multiplier is malformed. It can only be set when bfd is enabled, and the value should be between 3 and 10. |The specified detect multiplier for BFD is invalid. You can set this parameter only when you enable BFD, with a valid value from 3 to 10. |
|400 |InvalidDirectConnectVirtualInterface.EnableNqaMismatch |The specified virtual interface route type does not support enable nqa. |The specified route type of the DC Virtual Interface does not support enabling NQA. |
|400 |InvalidDirectConnectVirtualInterface.NqaBfdEchoBothEnabled |The specified virtual interface does not support enabling bfd echo and nqa at the same time. |The specified DC Virtual Interface does not support enabling BFD and NQA simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectIntervalMalformed |The specified nqa detect interval is malformed. It can only be set when nqa is enabled, and the value should be between 1000 and 5000. |The specified Detect interval for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 1000 to 5000. |
|400 |InvalidDirectConnectVirtualInterface.NqaDetectMultiplierMalformed |The specified nqa detect multiplier is malformed. It can only be set when nqa is enabled, and the value should be between 3 and 8. |The specified detect multiplier for NQA is invalid. You can set this parameter only when you enable NQA, with a valid value from 3 to 8. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidDirectConnectGateway.InvalidBusinessStatus |The specified direct connect gateway is not in the correct status for the request. The specified direct connect gateway is in freeze. |The specified DC Gateway cannot respond to this request due to its status. The current DC Gateway is frozen. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectVirtualInterface.Ipv6IpChange |It is unsupported changing local IPv6 IP or peer IPv6 IP. |The IPv6 addresses of both Your gateway and Cloud gateway for the DC Virtual Interface are unchangeable. |
|400 |InvalidDirectConnectVirtualInterface.GatewayIpv6NotEnable |The specified direct connect gateway does not enable IPv6. |The specified DC Gateway does not have IPv6 enabled. |
|400 |InvalidDirectConnectVirtualInterface.Ipv6IpMissing |The specified virtual interface local IPv6 IP or peer IPv6 IP is missing, they must either both be configured or not configured at all. |The specified DC Virtual Interface must have IPv6 addresses for both Your gateway and Cloud gateway specified simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.LocalIpv6IpMalformed |The specified virtual interface local IPv6 address is malformed. |The specified Cloud gateway peer IPv6 for the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpv6IpMalformed |The specified virtual interface peer IPv6 address is malformed. |The specified Your gateway peer IPv6 for the DC Virtual Interface is invalid. |
|400 |InvalidDirectConnectVirtualInterface.PeerIpv6IPMismatch |The specified virtual interface Peer IPv6 IP and Local IPv6 IP are not in the same subnet. |The specified Your gateway peer IPv6 for the DC Virtual Interface is not within the same subnet as the Cloud gateway peer IPv6. |
|400 |InvalidDirectConnectVirtualInterface.NqaBfdBothEnabled |The specified virtual interface does not support enabling bfd and nqa at the same time. |The specified DC Virtual Interface does not support enabling BFD and NQA simultaneously. |
|400 |InvalidDirectConnectVirtualInterface.InvalidStatus |The specified direct connect virtual interface is not in the correct status for the request. |The specified DC Virtual Interface cannot respond to this request due to its status. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |The maximum bandwidth allocable of the DC Connection has been reached. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to operate IPv6. |
|403 |Forbidden |You are not authorized to perform nqa operations on the specified virtual interface. |No permission to perform NQA on the specified DC Virtual Interface. |
|403 |InvalidDirectConnectVirtualInterface.BfdEchoForbidden |You are not authorized to perform bfd echo operations on the specified virtual interface. |No permission to perform BFD echo on the specified DC Virtual Interface. |
|403 |InvalidDirectConnectVirtualInterface.IPv6Forbidden |You are not authorized to perform IPv6 operations on the specified virtual interface. |No permission to apply IPv6 to the specified DC Virtual Interface. |
|403 |InvalidDirectConnectVirtualInterface.OperationForbidden |You are not authorized to perform operations on the specified virtual interface. |No permission to operate the specified DC Virtual Interface. |
|404 |InvalidDirectConnectVirtualInterface.NotFound |The specified direct connect virtual interface does not exist. |The specified DC Virtual Interface does not exist. |
|409 |InvalidDirectConnectVirtualInterface.PeerIpv6IpConflict |The specified virtual interface peer IPv6 IP conflicts with its local IPv6 IP. |The specified Your gateway peer IPv6 for the DC Virtual Interface conflicts with Cloud gateway peer IPv6. |
|409 |InvalidDirectConnectVirtualInterface.LocalIpv6IpConflict |The subnet of the specified virtual interface local IPv6 IP overlaps with another virtual interface. |The subnet of the specified Cloud gateway peer IPv6 for the DC Virtual Interface overlaps with the subnet of another DC Virtual Interface. |
