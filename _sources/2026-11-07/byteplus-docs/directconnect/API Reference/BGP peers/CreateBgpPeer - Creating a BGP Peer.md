---
title: "CreateBgpPeer - Creating a BGP Peer"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateBgpPeer"
---

Call CreateBgpPeer to create a BGP Peer for a Direct Connect (DC) Virtual Interface using "BGP routes".

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateBgpPeer&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">String</span> <span data-api-tag="require|E3WqO3">必选</span> `Example: CreateBgpPeer`

The interface name. The current API name is `CreateBgpPeer`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|napvyy">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**BgpPeerName ** <span data-label="purple">String </span>`optional` `Example: test`

Name of the BGP Peer.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If this parameter is not specified or left empty, it defaults to the BGP connection instance ID​.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the BGP Peer.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**VirtualInterfaceId ** <span data-label="purple">String </span><span data-api-tag="require|eGHjha">必选</span> `Example: dcv-3tehy13n2l4c6c0v****`

ID of the DC Virtual interface where the BGP Peer is located. You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the DC Virtual Interface.



**RemoteAsn ** <span data-label="purple">Integer </span><span data-api-tag="require|WGLYzA">必选</span> `Example: 32500`

The ASN for the BGP Peer.

The valid ASN range is 1 to 4294960000. It must not be the same as BytePlus ASN (137718).



**AuthKey ** <span data-label="purple">String </span>`optional` `Example: testAuth`

The authentication key for the BGP Peer.


* Must be 6 to 80 characters in length.

* May include uppercase and lowercase letters, numbers and symbols (~ ` ! @ # $ % ^ \* ( ) \- _ = + [ ] { } | , . / ; :).



**IpVersion** <span data-label="purple">String</span> `optional` `Example: IPv4`

IP type of the BGP Peer.


* IPv4 (default)

* IPv6



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BgpPeerId ** <span data-label="purple">String </span>`Example: bgp-2752hz4teko3k7fap8u4c****`

The ID of the newly created BGP Peer.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateBgpPeer&Version=2020-04-01&BgpPeerName=test&Description=test&VirtualInterfaceId=dcv-3tehy13n2l4c6c0v****&RemoteAsn=32500&AuthKey=testA**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "CreateBgpPeer",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****",
        "BgpPeerId": "bgp-2752hz4teko3k7fap8u4c****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidBgpPeer.RemoteAsnMalformed |The specified remote ASN is malformed. Ensure that you've specified the remote ASN is not 137718. |The specified ASN is invalid. The ASN cannot be the same as BytePlus ASN. |
|400 |InvalidBgpPeer.VirtualInterfaceMalformed |The specified virtual interface does not support creating a BGP Peer. |The specified DC Virtual Interface does not support creating BGP Peers. |
|400 |InvalidBgpPeer.RemoteAsnMalformed |The specified BGP remote ASN is malformed. |The specified ASN is invalid. |
|400 |InvalidBgpPeer.AuthKeyMalformed |The specified BGP AuthKey is malformed. |The specified BGP authentication key is invalid. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidDirectConnectGateway.InvalidBusinessStatus |The specified direct connect gateway is not in the correct status for the request. The specified direct connect gateway is in freeze. |The specified DC Gateway cannot respond to this request due to its status. The current DC Gateway is frozen. |
|400 |InvalidBgpPeer.IpVersionMalformed |The specified IP version is malformed. |The specified IP version is invalid. |
|400 |InvalidBgpPeer.IpVersionMismatch |The specified direct connect virtual interface has no IPv6 address. |The specified DC Virtual Interface has no IPv6 address. |
|400 |InvalidDirectConnectVirtualInterface.InvalidStatus |The specified direct connect virtual interface is not in the correct status for the request. |The specified DC Virtual Interface cannot respond to this request due to its status. |
|400 |InvalidBgpPeer.RemoteAsnConflictBgpAsn |The specified ASN is invalid. The ASN cannot be the same as the ASN of direct connect gateway. |The specified BGP Peer ASN is invalid. It must not be the same as the DC Gateway ASN. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to operate IPv6. |
|403 |InvalidOperation.NotSupport |The operation is not supported. |This action is not supported. |
|404 |InvalidDirectConnectVirtualInterface.NotFound |The specified direct connect virtual interface does not exist. |The specified DC Virtual Interface does not exist. |
|409 |InvalidBgpPeer.Conflict |The specified BGP peer conflicts with another BGP peer. |The specified BGP Peer conflicts with another BGP Peer. |
