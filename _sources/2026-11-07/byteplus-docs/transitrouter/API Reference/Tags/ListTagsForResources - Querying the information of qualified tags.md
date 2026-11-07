---
title: "ListTagsForResources - Querying the information of qualified tags"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|iba1uo">必选</span> `Example value: ListTagsForResources`

The interface name. The current API name is `ListTagsForResources`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|S298Sj">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType** <span data-label="purple">String</span> <span data-api-tag="require|wcxoHX">必选</span>`Example value: transitrouter`

The resource type. Values:


* transitrouter: TR instance.

* transitrouterroutetable: TR route table.

* transitrouterattachment: Attachment, including network instance attachments (VPC, VPN, or DC Gateway) and inter\-region attachments.

* transitrouterbandwidthpackage: TR bandwidth package.



**TagType ** <span data-label="purple"> String  </span>`optional` `Example: custom`

Tag type. Values:


* custom: Custom tag

* system: System tag

* Leaving this parameter unset means querying all types of tags.



**NextToken ** <span data-label="purple"> String  </span>`optional` `example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**MaxResults ** <span data-label="purple"> Integer </span>`Optional` `Example: 50`

The maximum number of entries to return in this query. Default: 10. Maximum: 100.



**ResourceIds.N ** <span data-label="purple"> String </span>`Optional` `Example: tr-273sdsdsxxxxxp8u2j****`

The resource ID.


* N represents the serial number of the resource ID, ranging from 1 to 50.

* Separate multiple resource IDs with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters">DescribeTransitRouters</a> API to get the ID of the “transitrouter” resource.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables">DescribeTransitRouterRouteTables</a> API to get the ID of the “transitrouterroutetable” resource.</div>


* <div data-tips="true" data-tips-type="default">Based on the type of the resource to be tagged, you can call <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments">DescribeTransitRouterVpcAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments">DescribeTransitRouterVpnAttachments</a>, <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments">DescribeTransitRouterDirectConnectGatewayAttachments</a>, or <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments">DescribeTransitRouterPeerAttachments</a> to get the ID of the “transitrouterattachment” resource.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages">DescribeTransitRouterBandwidthPackages</a> API to get the ID of the “transitrouterbandwidthpackage” resource.</div>




**TagFilters.N.Key** <span data-label="purple">String</span> `Optional` `Example value: k1`

The specified tag key when querying resources based on tags.


* N represents the serial number of the tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the resources that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple"> String  </span>`Optional` `Example value: v1`

Tag value of a resource.


* The first N represents the serial number of the tag key, ranging from 1 to 10.

* The second N represents the serial number of the tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To provide this parameter, you must first provide TagFilters.N.Key.</div>


* <div data-tips="true" data-tips-type="default">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple"> String  </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple"> Object[]  </span>`Example value: --`

Resource and its associated tag information.


**ResourceId ** <span data-label="purple"> String  </span>`example: tr-2fe6fszjgeznk5oxruv0u****`

The resource ID.



**TagKey ** <span data-label="purple"> String </span>`Example: k1`

The key of the tag associated with the resource.



**TagValue ** <span data-label="purple"> String  </span>`Example: v1`

The key of the tag associated with the resource.



**Resource type ** <span data-label="purple"> String </span>`Example: transitrouter`

The resource type.


* transitrouter: TR instance.

* transitrouterroutetable: TR route table.

* transitrouterattachment: Attachment, including network instance attachments (VPC, VPN, or DC Gateway) and inter\-region attachments.

* transitrouterbandwidthpackage: TR bandwidth package.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=transitrouter HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T040802Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815120805184193062099730FCA",
    "Action": "ListTagsForResources",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
    "ResourceTags": [
      {
        "ResourceId": "tr-2fe6fszjgeznk5oxruv0u****",
        "TagKey": "k1",
        "TagValue": "v1",
        "ResourceType": "transitrouter"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken queried is invalid. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag key for filtering is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag value for filtering is invalid. |
|400 |InvalidTagType.Malformed |The specified parameter tag type is invalid. |The tag type is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
