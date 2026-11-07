---
title: "ListTagsForNLBResources - Querying the qualified tag information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ListNLBTagsForResources"
---

Call ListTagsForNLBResources API to query tag information that meets the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForNLBResources&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|S36zyR">必选</span>`Example: ListTagsForNLBResources`

Action to execute. Set the value to ListTagsForNLBResources.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Eq7csm">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**ResourceType ** <span data-label="purple">String </span><span data-api-tag="require|5Ng4z6">必选</span> `Example: nlb`

The resource type. Valid values:


* nlb: NLB instance.

* nlb_listener: Listener.

* nlb_servergroup: Server group.

* nlb_security_policy: TLS custom security policy.



**ResourceIds.N ** <span data-label="purple">String </span>`optional` `Example: nlb-273sdsdswrfdp8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of the resource ID, ranging from 1 to 20.

* Separate multiple resource IDs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers">DescribeNetworkLoadBalancers</a> API to query the ID of the NLB instance.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners">DescribeNLBListeners</a> API to query the ID of the listener.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups">DescribeNLBServerGroups</a> API to query the ID of the server group.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies">DescribeNLBSecurityPolicies</a> API to query the ID of the custom TLS security policy.</div>




**TagType ** <span data-label="purple">String </span>`optional` `Example: custom`

Tag type. Valid values:


* custom: Custom tag

* system: System tag.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The specified tag key when querying resources by tag.


* N: Represents the serial number of the tag key, valid value ranges from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the resources that contain all specified tag keys.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the specified <code>TagFilters.N.Key</code> does not exist, an empty string is returned.</div>




**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

Tag value of a resource.


* The first N indicates the serial number of the tag key, ranging from 1 to 10.

* The second N represents the serial number of the tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide <code>TagFilters.N.Key</code>.</div>


* <div data-tips="true" data-tips-type="tip">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of results per query. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId** <span data-label="purple">String</span> `Example: 2024062415303301022514515207C4****`

Request ID.



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple">Object[] </span>`Example: --`

Resource and its associated tag information.


**ResourceType ** <span data-label="purple">String </span>`Example: nlb`

The resource type.



**ResourceId ** <span data-label="purple">String </span>`Example: nlb-rrq1hytw2u4gv0x58c31xxx`

The resource ID.



**TagKey ** <span data-label="purple">String </span>`Example: key`

The key of the tag attached to the resource.



**TagValue ** <span data-label="purple">String </span>`Example: value`

The value of the tag attached to the resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ListTagsForNLBResources&Version=2020-04-01&ResourceType=nlb&ResourceIds.1=nlb-273sdsdswrfdp8u2j****&TagType=custom&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListTagsForNLBResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2024062415303301022514515207C4****",
        "ResourceTags": [
            {
                "TagKey": "key",
                "TagValue": "value",
                "ResourceId": "nlb-rrq1hytw2u4gv0x58c31xxx",
                "ResourceType": "nlb"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagType.Malformed |The specified TagType is malformed. |The specified TagType parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceType'. |This request is missing a required parameter. Please ensure your API request includes all required parameters, such as ResourceType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
