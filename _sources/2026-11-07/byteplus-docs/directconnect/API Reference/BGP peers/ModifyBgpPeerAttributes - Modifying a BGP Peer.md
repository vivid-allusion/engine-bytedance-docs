---
title: "ModifyBgpPeerAttributes - Modifying a BGP Peer"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyBgpPeerAttributes"
---

Call ModifyBgpPeerAttributes to modify the information of a specified BGP Peer.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBgpPeerAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|JbzAd6">必选</span> `Example: ModifyBgpPeerAttributes`

The interface name. The current API name is `ModifyBgpPeerAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|pAydB0">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**BgpPeerId ** <span data-label="purple">String </span><span data-api-tag="require|MbyFmI">必选</span> `Example: bgp-2752hz4teko3k7f4c****`

ID of the BGP Peer to be modified. You can call [DescribeBgpPeers](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers) to query the BGP Peer ID.



**BgpPeerName ** <span data-label="purple">String </span>`optional` `Example: test`

Name of the BGP Peer.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the name of the BGP Peer.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the BGP Peer.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the description of the BGP Peer.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyBgpPeerAttributes&Version=2020-04-01&BgpPeerId=bgp-2752hz4teko3k7f4c****&BgpPeerName=test&Description=test HTTP/1.1
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
        "Action": "ModifyBgpPeerAttributes",
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

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|404 |InvalidBgpPeer.NotFound |The specified BGP peer does not exist. |The BGP Peer you specified does not exist. |
