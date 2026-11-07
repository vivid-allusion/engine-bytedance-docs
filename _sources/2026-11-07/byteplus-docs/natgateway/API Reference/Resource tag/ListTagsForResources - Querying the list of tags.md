---
title: "ListTagsForResources - Querying the list of tags"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ListTagsForResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|4f8MbK">必选</span>`Example: ListTagsForResources`

The action that you want to perform. Value: ListTagsForResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|dJIbbe">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**TagType ** <span data-label="purple">string </span>`optional` `Example: custom`

The tag type. Values:


* custom: Custom tag

* system: System tag.

> If you omit this parameter or set it to an empty string, tags of all types are queried.



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|HeOP4I">必选</span>`Example: ngw`

The type of the tagged resource. Currently only "ngw" (NAT gateway instance) is supported.



**NextToken ** <span data-label="purple">string </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.



**ResourceIds.N ** <span data-label="purple">string[] </span>`optional` `Example: ngw-273w3e33y2y9s7fap8u2j****`

ID of the NAT gateway.


* N represents the sequence number of a resource ID. You can specify a maximum of 50 IDs per call.

* Separate multiple resource IDs with ampersands (&).



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). The relationship between multiple tag keys is a logical "AND". That is, the query returns resources that have all specified tags.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).

> Description

> * To provide this parameter, provide TagFilters.N.Key first.

> * Passing an empty string queries for resources with an empty tag value.



**MaxResults ** <span data-label="purple">integer </span>`optional` `Example: 50`

The number of results per query. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NextToken ** <span data-label="purple">string </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple">object[] </span>`Example: -`

Information about the tag attached to the resource.


**ResourceType ** <span data-label="purple">string </span>`Example: ngw`

The resource type.

ngw: NAT gateway.



**ResourceId ** <span data-label="purple">string </span>`Example: ngw-2feq5xhimd88w59gp686****`

The resource ID.



**TagKey ** <span data-label="purple">string </span>`Example: k1`

The key of the tag attached to the resource.



**TagValue ** <span data-label="purple">string </span>`Example: v1`

The value of the tag attached to the resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ListTagsForResources&Version=2020-04-01&TagType=custom&ResourceType=ngw&ResourceIds.1=ngw-273w3e33y2y9s7fap8u2j**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
X-Date: 20251113T125259Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251113/cn-beijing/natgateway/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202511132054182290370111475D3BB8",
    "Action": "ListTagsForResources",
    "Version": "2020-04-01",
    "Service": "natgateway",
    "Region": "cn-beijing"
  },
  "Result": {
    "RequestId": "2021062415303301022514515207C4****",
    "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
    "ResourceTags": [
      {
        "ResourceType": "ngw",
        "ResourceId": "ngw-2feq5xhimd88w59gp686****",
        "TagKey": "k1",
        "TagValue": "v1"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTagType.Malformed |The specified parameter tag type is invalid. |The tag type is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken queried is invalid. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
