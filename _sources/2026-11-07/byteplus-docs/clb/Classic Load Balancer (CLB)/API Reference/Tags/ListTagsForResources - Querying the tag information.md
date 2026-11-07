---
title: "ListTagsForResources - Querying the tag information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified criteria.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|AHNJgE">必选</span> `Example: ListTagsForResources`

Action to execute. Set the value to **ListTagsForResources**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|6D4LP9">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ResourceType ** <span data-label="purple">String </span><span data-api-tag="require|Uco2JR">必选</span> `Example: clb`

The resource type. Values:


* clb: CLB instance.

* listener

* servergroup: Backend server group.

* acl: Access control.

* certificate



**ResourceIds.N ** <span data-label="purple">String </span>`optional` `Example: clb-273sdsdsxxxxxp8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

* You can call the following API to obtain the resource ID:

   * [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers)

   * [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners)

   * [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups)

   * [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls)

   * [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates)



**TagType ** <span data-label="purple">String </span>`optional` `Example: custom`

The tag type. Values:


* custom: Custom tag

* system: System tag.

* Leaving this parameter unset means querying all types of tags.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns resources tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the sequence number of a tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for resources with an empty tag value.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of results per query. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple">Object[] </span>`Example: -`

Resource and its associated tag information.


**ResourceType ** <span data-label="purple">String </span>`Example: CLB`

The resource type.



**ResourceId ** <span data-label="purple">String </span>`Example: clb-2fe6fszjgeznk5oxruv0u****`

The resource ID.



**TagKey ** <span data-label="purple">String </span>`Example: k1`

The key of the tag attached to the resource.



**TagValue ** <span data-label="purple">String </span>`Example: v1`

The value of the tag attached to the resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=clb&ResourceIds.1=clb-273sdsdsxxxxxp8u2j****&TagType=custom&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "ResourceTags": [
            {
                "TagKey": "k1",
                "TagValue": "v1",
                "ResourceId": "clb-2fe6fszjgeznk5oxruv0u****",
                "ResourceType": "CLB"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Explain |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagType.Malformed |The specified TagType is malformed. |The specified TagType parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceType'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ResourceType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
