---
title: "TagResources - Adding a custom tag"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/TagResources"
---

Call the TagResources API to add custom tags to a resource.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

​​If multiple tags with the same key are applied to a resource, the most recent value overwrites any previous ones.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|JZnau9">必选</span> Example: `TagResources`

The action that you want to perform. Value: TagResources.



**Version ** `String` <span data-api-tag="require|HeD9LP">必选</span> Example: `2020-04-01`

The API version.



**ResourceType ** `String` <span data-api-tag="require|-1Xmz8">必选</span> Example: `vpngateway`

The resource type. Values:


* vpngateway: VPN gateway

* customergateway: Customer gateway

* vpnconnection: IPsec\-VPN connection

* sslvpnserver: SSL VPN server

* sslvpnclientcert: SSL client certificate



**ResourceIds.N ** `String` <span data-api-tag="require|r1y8K6">必选</span> Example: `vgw-273w3e33y2y9s7fap8u2j****`

The resource ID.


* N represents the sequence number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).



**Tags.N.Key ** `String` <span data-api-tag="require|ElhCRK">必选</span> Example: `k1`

The key of the custom tag.


* N represents the sequence number of a tag key. Valid range: 1\-20.

* Separate multiple tag keys with ampersands (&).

* Must not start with volc: or sys: in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


> Duplicate tag keys are not allowed for the same resource.



**Tags.N.Value ** `String` `optional` Example: `v1`

The value of the custom tag.


* N represents the sequence number of a tag value. Valid range: 1\-20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with spaces, the system automatically deletes the space.


> To provide this parameter, provide Tags.N.Key first.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=TagResources&Version=2020-04-01&ResourceType=vpngateway&ResourceIds.1=vgw-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vgw-bp15zckdt37pq72zv****&Tags.1.Key=k1&Tags.2.Key=k2&Tags.1.Value=v1&Tags.2.Value=v2 HTTP/1.1
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
        "Action": "TagResources",
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
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
|400 |QuotaExceeded.ResourceTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that can be created per resource. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagAccount.Malformed |The specified parameter tag account is invalid. Account ID cannot be 1. |The tag user is invalid. User ID cannot be 1. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
