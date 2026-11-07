---
title: "DescribeBgpPeerAttributes - Querying a BGP Peer"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeerAttributes"
---

Call DescribeBgpPeerAttributes to query the details of a specified BGP Peer.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBgpPeerAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|36Y0oo">必选</span> `Example: DescribeBgpPeerAttributes`

The interface name. The current API name is `DescribeBgpPeerAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|AXStrf">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**BgpPeerId ** <span data-label="purple">String </span><span data-api-tag="require|Qn9kAR">必选</span>`Example: bgp-2752hz4teko3k7f4c****`

ID of the BGP Peer to be queried.

You can call [DescribeBgpPeers](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers) to query the BGP Peer ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

ID of the account to which the BGP Peer belongs.



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-7qthudw0ll6jmc****`

ID of the DC Virtual interface where the BGP Peer is located.



**BgpPeerId ** <span data-label="purple">String </span>`Example: bgp-2752hz4teko3k7f4c****`

ID of the BGP Peer.



**BgpPeerName ** <span data-label="purple">String </span>`Example: test`

Name of the BGP Peer.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

Description of the BGP Peer.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the BGP Peer is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the BGP Peer is updated.



**RemoteAsn ** <span data-label="purple">Integer </span>`Example: 32000`

Remote ASN of the BGP Peer.



**AuthKey ** <span data-label="purple">String </span>`Example: testAu****`

The authentication key for the BGP Peer.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the BGP Peer.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**SessionStatus ** <span data-label="purple">String </span>`Example: Up`

The session status of the BGP Peer.


* Up: Healthy

* Down: Faulty



**IpVersion ** <span data-label="purple">String </span>`Example: IPv4`

IP type of the BGP Peer.


* IPv4

* IPv6



**LocalAsn ** <span data-label="purple">Integer </span>`Example: 137718`

ASN on the BytePlus side.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeBgpPeerAttributes&Version=2020-04-01&BgpPeerId=bgp-2752hz4teko3k7f4c**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021111616110801021214619****",
        "Action": "DescribeBgpPeerAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021111616110801021214619****",
        "AccountId": "210000****",
        "BgpPeerId": "bgp-2752hz4teko3k7f4c****",
        "VirtualInterfaceId": "dcv-7qthudw0ll6jmc****",
        "BgpPeerName": "test",
        "Description": "test",
        "RemoteAsn": 32000,
        "AuthKey": "testAuth",
        "Status": "Available",
        "CreationTime": "2021-12-15T17:05:42+08:00",
        "UpdateTime": "2021-12-17T11:50:30+08:00",
        "IpVersion": "IPv4",
        "LocalAsn": 137718,
        "SessionStatus": "Up"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidBgpPeer.NotFound |The specified BGP peer does not exist. |The BGP Peer you specified does not exist. |
