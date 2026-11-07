---
title: "ListTagsForResources - Querying the tag list"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|kq2cS-">必选</span> `Example: ListTagsForResources`

The interface name. The current API name is `ListTagsForResources`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|mtmkkS">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType ** <span data-label="purple"> String </span><span data-api-tag="require|H0qaTh">必选</span>`Example: directconnectconnection`

The resource type to query tags for. Values:


* directconnectconnection: Direct Connect Connection

* directconnectgateway: Direct Connect Gateway

* directconnectvirtualinterface: Direct Connect Virtual Interface



**ResourceIds.N ** <span data-label="purple"> String </span>`optional` `Example: dcc-lhn2cx0an18****`

Target resource ID.


* N represents the sequence number of a resource ID. You can specify a maximum of 50 IDs per call.

* Separate multiple resource IDs with ampersands (&).



**TagType ** <span data-label="purple"> String  </span>`optional` `Example: custom`

The tag type. Values:


* custom: Custom tag

* system: System tag.


> If this parameter is not provided or is passed empty, tags of all types are queried.



**TagFilters.N.Key ** <span data-label="purple"> String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (&). Multiple tag keys have a logical AND relationship. The query returns resources tagged with all the specified keys.



**TagFilters.N.Values.M ** <span data-label="purple">string </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).


> Note


> * To provide this parameter, provide TagFilters.N.Key first.

> * If you provide an empty string, the system will query resources whose tag value is an empty string.



**NextToken ** <span data-label="purple"> String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.



**MaxResults ** <span data-label="purple"> Integer  </span>`optional` `Example: 50`

The number of results to return per query. Default: 10, Maximum: 100.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple">String</span> `Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple"> Object[]  </span>`Example: -`

Information about the tag attached to the resource.


**TagKey ** <span data-label="purple"> String </span>`Example: key`

The key of a tag attached to the resource.



**TagValue ** <span data-label="purple"> String </span>`Example: value`

The value of a tag attached to the resource.



**ResourceId ** <span data-label="purple"> String </span>`Example: dcc-lhn2cx0an18****`

The resource ID.



**ResourceType ** <span data-label="purple"> String </span>`Example: directconnectconnection`

The resource type.


* directconnectconnection: Direct Connect Connection

* directconnectgateway: Direct Connect Gateway

* directconnectvirtualinterface: Direct Connect Virtual Interface




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=directconnectconnection&ResourceIds.1=dcc-lhn2cx0an18****&TagType=custom&TagFilters.1.Key=k1&TagFilters.1.Values.M=v1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "ResourceTags": [
            {
                "TagKey": "key",
                "TagValue": "value",
                "ResourceId": "dcc-lhn2cx0an18****",
                "ResourceType": "directconnectconnection"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
