---
title: "UntagResources - Disassociating a custom tag"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/UntagResources"
---

Call the UntagResources API to disassociate a custom tag from a resource.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Tags exist only in association with a resource. When a tag is disassociated from all its bound resources, it is automatically deleted.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|bve5YW">必选</span> Example: `UntagResources`

The action to perform. Value: UntagResources.



**Version ** `String` <span data-api-tag="require|WcSLy-">必选</span> Example: `2020-04-01`

The API version.



**ResourceType ** `String` <span data-api-tag="require|n54wTz">必选</span> Example: `vpngateway`

The resource type. Values:


* vpngateway: VPN gateway

* customergateway: Customer gateway

* vpnconnection: IPsec\-VPN connection

* sslvpnserver: SSL VPN server

* sslvpnclientcert: SSL client certificate



**ResourceIds.N ** `String` <span data-api-tag="require|4OY-64">必选</span> Example: `vgw-273w3e33y2y9s7fap8u2j****`

The resource ID.


* N represents the sequence number of a resource ID. A maximum of 50 IDs can be specified per call.

* Separate multiple resource IDs with ampersands (&).



**TagKeys.N ** `String` <span data-api-tag="require|iMQeDv">必选</span> Example: `k1`

The key of the custom tag to be deleted.


* N represents the sequence number of a tag key. A maximum of 20 keys can be speicified per call.

* Separate multiple tag keys with ampersands (&).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=vpngateway&ResourceIds.1=vgw-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vgw-bp15zckdt37pq72zv****&TagKeys.1=k1&TagKeys.2=k2 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
   "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
