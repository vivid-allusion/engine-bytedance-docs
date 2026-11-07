---
title: "DescribeBgpPeers - Querying the list of BGP Peers"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers"
---

Call DescribeBgpPeers to query the details of BGP Peers that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If you do not provide the request parameter (`BgpPeerIds`), the system queries based on other parameters and returns all BGP Peers that meet conditions.

* If you do not provide any optional request parameters, the system queries based on the currently logged\-in account and returns all BGP Peers under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeBgpPeers&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|UMSWTX">必选</span> `Example: DescribeBgpPeers`

The interface name. The current API name is `DescribeBgpPeers`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|lNMpJa">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**BgpPeerIds.N ** <span data-label="purple">String </span>`optional` `Example: bgp-7qthudw0ll6jmc****`

ID of the BGP Peer.


* N represents the sequence number of a BGP Peer ID. You can call up to 100 IDs per request.

* Separate multiple BGP Peer IDs with ampersands (&).



**BgpPeerName ** <span data-label="purple">String </span>`optional` `Example: test`

Name of the BGP Peer.



**VirtualInterfaceId ** <span data-label="purple">String </span>`optional` `Example: dcv-3tehy13n2l4c6c0v****`

ID of the DC Virtual interface where the BGP Peer is located.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`optional` `Example: dcg-7qthudw0ll6jmc****`

ID of the DC Gateway to which the BGP Peer belongs.



**RemoteAsn ** <span data-label="purple">Integer </span>`optional` `Example: 32500`

Remote ASN of the BGP Peer.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 10`

Total number of BGP Peers meeting the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**BgpPeers ** <span data-label="purple">Object[] </span>`Example: -`

Details of the BGP Peer.


**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the BGP Peer.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**AuthKey ** <span data-label="purple">String </span>`Example: mypass***`

The authentication key for the BGP Peer.



**LocalAsn ** <span data-label="purple">Integer </span>`Example: 137718`

ASN on the BytePlus side.



**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the account to which the resource belongs.



**BgpPeerId ** <span data-label="purple">String </span>`Example: bgp-274oahfm8gjy87fap8tpn6n1c`

ID of the BGP Peer.



**IpVersion ** <span data-label="purple">String </span>`Example: IPv4`

IP type of the BGP Peer.


* IPv4

* IPv6



**RemoteAsn ** <span data-label="purple">Integer </span>`Example: 20031`

Remote ASN of the BGP Peer.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the BGP Peer is updated.



**BgpPeerName ** <span data-label="purple">String </span>`Example: test-bgp`

Name of the BGP Peer.



**Description ** <span data-label="purple">String </span>`Example: test bgp for idc`

Description of the BGP Peer.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the BGP Peer is created.



**SessionStatus ** <span data-label="purple">String </span>`Example: Up`

The status of the BGP connection.


* Up: Healthy

* Down: Faulty



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-2752hyf6****`

ID of the DC Virtual interface where the BGP Peer is located.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeBgpPeers&Version=2020-04-01&BgpPeerIds.1=bgp-2752hz4teko3k7f4c****&PageNumber=1&PageSize=20 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeBgpPeers",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "BgpPeers": [
            {
                "Status": "Available",
                "AuthKey": "mypass***",
                "LocalAsn": 137718,
                "AccountId": "20******57",
                "BgpPeerId": "bgp-274oahfm8gjy87fap8tpn6n1c",
                "IpVersion": "IPv4",
                "RemoteAsn": 20031,
                "UpdateTime": "2021-12-07T15:57:22+08:00",
                "BgpPeerName": "test-bgp",
                "Description": "test bgp for idc",
                "CreationTime": "2021-12-07T15:57:22+08:00",
                "SessionStatus": "Up",
                "VirtualInterfaceId": "dcv-2752hyf6****"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.BgpPeerId |You've reached the limit on the number of BGP peer IDs that you can describe. |You have reached the maximum number of BGP Peer IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
