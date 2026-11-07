---
title: "ListTagsForResources - Querying the tag list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified criteria.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|iF5OAA">必选</span> `Example value: ListTagsForResources`

The interface name. The current API name is `ListTagsForResources`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|h1i5WN">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Resource type ** <span data-label="purple"> String </span><span data-api-tag="require|8FjZ-p">必选</span>`Example value: vpc`

The resource type. Values:


* vpc: Virtual Private Cloud.

* subnet: Subnet.

* eni: Network Interface.

* securitygroup: Security group.

* havip: High\-Availability Virtual IP Address.

* routetable: Route table.

* networkacl: Network ACL.

* flowlog: Flow Log.

* trafficmirrortarget: Traffic Mirror Target.

* trafficmirrorfilter: Traffic Mirror Filter.

* trafficmirrorsession: Traffic Mirror Session.

* eip: EIP.

* bandwidthpackage: Bandwidth Package.

* ngw: NAT Gateway.

* vpngateway: VPN gateway.

* directconnectconnection: Direct Connect Connection.

* directconnectgateway: Direct Connect Gateway.

* directconnectvirtualinterface: Direct Connect Virtual Interface.



**ResourceIds.N ** <span data-label="purple">String</span> `optional` `Example value: vpc-273w3e33y2y9s7fap8u2j****`

The resource ID.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per call.

* Separate multiple resource IDs with ampersands (&).



**TagType ** <span data-label="purple"> String  </span>`optional` `Example value: custom`

Tag type. Valid values:


* custom: Custom tag

* system: System tag.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If this parameter is not provided or is passed empty, tags of all types are queried.</div>




**TagFilters.N.Key ** <span data-label="purple"> String </span>`optional` `Example value: k1`

The tag key of the tag.


* N specifies the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). Multiple tag keys have a logical AND relationship. The query returns resources tagged with all the specified keys.

* The tag key must be unique.



**TagFilters.N.Values.N ** <span data-label="purple"> String  </span>`optional` `Example value: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To provide this parameter, provide <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="default">Passing an empty string queries for resources with an empty tag value.</div>




**NextToken ** <span data-label="purple"> String  </span>`optional` `Example value: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.



**MaxResults ** <span data-label="purple"> Integer </span>`optional` `Example value: 50`

The number of results to return per query. Default: 10, Maximum: 100.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



**NextToken ** <span data-label="purple"> String  </span>`optional` `Example value: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**ResourceTags ** <span data-label="purple"> Object[]  </span>`optional` `Example value: -`

The tag information attached to the resource.


**ResourceType ** <span data-label="purple"> String </span>`optional` `Example value: vpc`

The resource type.



**ResourceId ** <span data-label="purple"> String </span>`optional` `Example value: vpc-273w3e33y2y9s7fap8u2j****`

The resource ID.



**TagKey ** <span data-label="purple"> String </span>`optional` `Example value: k1`

The key of a tag attached to the resource.



**Tag value ** <span data-label="purple"> String </span>`optional` `Example value: v1`

The value of a tag attached to the resource.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=vpc&ResourceIds.1=vpc-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vpc-bp15zckdt37pq72zv**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "ResourceTags": [
            {
                "ResourceType": "vpc",
                "ResourceId": "vpc-273w3e33y2y9s7fap8u2j****",
                "TagKey": "k1",
                "TagValue": "v1"
            },
            {
                "ResourceType": "vpc",
                "ResourceId": "vpc-bp15zckdt37pq72zv****",
                "TagKey": "k2",
                "TagValue": "v2"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |Querying NextToken is invalid. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |InvalidTagType.Malformed |The specified parameter tag type is invalid. |The tag type is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
