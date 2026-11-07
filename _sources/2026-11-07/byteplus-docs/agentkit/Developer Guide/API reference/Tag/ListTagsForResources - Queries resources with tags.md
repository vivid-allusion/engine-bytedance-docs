---
title: "ListTagsForResources - Queries resources with tags"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/ListTagsForResources_-_Queries_resources_with_tags"
---

You can call this operation to query resources associated with tags.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string   </span><span data-api-tag="require|t40SIG">必选</span>`Sample value: ListTagsForResources`

The action that you want to perform. Value: ListTagsForResources.



**Version ** <span data-label="purple">string   </span><span data-api-tag="require|saOSZ9">必选</span>`Sample value: 2025-10-30`

The version of the API. Value: 2025\-10\-30.



**MaxResults ** <span data-label="purple">integer </span>`Optional Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 100.

* Default value: 10.



**NextToken ** <span data-label="purple">string </span>`Optional Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**ResourceIds.N ** <span data-label="purple">string[]   </span><span data-api-tag="require|51M0Lh">必选</span>`Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

Resource ID.


* Parameter \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate multiple resources with ampersands (&).



**ResourceType ** <span data-label="purple">string   </span><span data-api-tag="require|g4anNE">必选</span>`Sample value: runtime`

The resource type. Valid values:


* runtime: Agent runtime.

* tool: Toolset.

* memory: Memory.

* mcpservice: MCP service.

* mcptoolset: MCP toolset.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with ampersands (&). Duplicate tag keys are not allowed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not pass in the parameter, all tags are queried.</div>


* <div data-tips="true" data-tips-type="tip">When an empty string is passed in, the error code InvalidTagFilterKey.Malformed is returned.</div>




**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Valid range: 1–10.

* The second N: specifies the serial number of a tag value. Valid range: 1–3.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, you need to pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in this parameter, all tag values under the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken ** <span data-label="purple">string </span>`Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The pagination token returned by this call. If this value is empty, the current page is the last page.



**TagResources ** <span data-label="purple">object[] </span>`Sample value: --`

This parameter consists of the information of the resources and associated tags.


**ResourceId ** <span data-label="purple">string </span>`Sample value: 8u0p77yseabkpak****`

Resource ID.



**ResourceType ** <span data-label="purple">string </span>`Sample value: runtime`

Resource type.



**TagKey ** <span data-label="purple">string </span>`Sample value: k1`

The key of the tag associated with the resource.



**TagValue ** <span data-label="purple">string </span>`Sample value: v1`

The value of the tag associated with the resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST https://agentkit.ap-southeast-1.byteplusapi.com.cn?Action=ListTagsForResources&Version=2025-10-30 HTTP/1.1
Content-Type: application/json; charset=UTF-8
{
  "MaxResults": 100,
  "NextToken": "NgkdBj6",
  "ResourceType": "CYUKDto",
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20251125162616245153035226AB92A8",
    "Action": "ListTagsForResources",
    "Version": "2025-10-30",
    "Service": "agentkit",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "NextToken": "vUEd",
    "TagResources": [
      {
        "ResourceId": "ZF3X094xW22",
        "ResourceType": "y",
        "TagKey": "UIEcR0OoBAv",
        "TagValue": "FzQ"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/agentkit/Common_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.ResourceIds |Resource Ids cannot be empty. |The ResourceIds cannot be empty. |
|400 |MissingParameter.ResourceType |The required parameter ResourceType is not supplied. |The ResourceType parameter cannot be empty. |
