---
title: "ListTagsForResources - Querying the list of tags"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

In a parameter in the format of a.N.b, the "N" represents the sequence number of a tag when querying resources by tags. It must be assigned a value in strict numerical order, starting from 1 up to 10. Separate multiple tags with ampersands (&).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|zeZvxR">必选</span> Example: `ListTagsForResources`

The action to perform. Value: ListTagsForResources.



**Version ** `String` <span data-api-tag="require|Wz_Uvc">必选</span> Example: `2020-04-01`

The API version.



**ResourceType ** `String` <span data-api-tag="require|4WI4DE">必选</span> Example: `vpngateway`

The resource type. Values:


* vpngateway: VPN gateway

* customergateway: Customer gateway

* vpnconnection: IPsec\-VPN connection

* sslvpnserver: SSL VPN server

* sslvpnclientcert: SSL client certificate



**ResourceIds.N ** `String` `optional` Example: `vgw-273w3e33y2y9s7fap8u2j****`

The resource ID.


* N represents the sequence number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).



**TagType ** `String` `optional` Example: `custom`

The tag type. Values:


* custom: Custom tag

* system: System tag.


> If this parameter is not provided or is passed empty, tags of all types are queried.



**TagFilters.N.Key ** `String` `optional` Example: `k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. The relationship between multiple tag keys is a logical "AND". That is, the query returns resources that have all specified tags.



**TagFilters.N.Values.M ** `String` `optional` Example: `v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid range: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).


> Description


> * If this parameter is passed in, TagFilters.N.Key must be passed in first.

> * Passing an empty string queries for resources with an empty tag value.



**NextToken ** `String` `optional` Example: `caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.



**MaxResults ** `Integer` `optional` Example: `50`

The number of results per query. Default: 10. Maximum: 100.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `2021062415303301022514515207C4****`

Request ID.



**ResourceTags ** `Object[]` `optional` Example: `-`

Information about tags associated with the resource **.** 


**Resource type** `String` `optional` Example: `vpngateway`

The resource type.



**ResourceId ** `String` `optional` Example: `vgw-273w3e33y2y9s7fap8u2j****`

The resource ID.



**TagKey ** `String` `optional` Example: `k1`

The key of the tag attached to the resource.



**TagValue ** `String` `optional` Example: `v1`

The value of the tag associated with the resource.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=vpngateway&ResourceIds.1=vgw-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vgw-bp15zckdt37pq72zv**** HTTP/1.1
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
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "ResourceTags": [
            {
                "ResourceType": "vpngateway",
                "ResourceId": "vgw-273w3e33y2y9s7fap8u2j****",
                "TagKey": "k1",
                "TagValue": "v1"
            },
            {
                "ResourceType": "vpngateway",
                "ResourceId": "vgw-bp15zckdt37pq72zv****",
                "TagKey": "k2",
                "TagValue": "v2"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
|400 |InvalidTagType.Malformed |The specified parameter tag type is invalid. |The tag type is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken queried is invalid. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
