---
title: "AdjustCCRulePriority"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/AdjustCCRulePriority"
---

Adjust the priority of rate limiting rules or advanced condition groups under the specified domain.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=AdjustCCRulePriority&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|1rg-FR">必选</span> `Sample value: AdjustCCRulePriority`

API name. The name of the current API is `AdjustCCRulePriority`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|tepwe_">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the resources corresponding to the current operation with a project. Only projects with permissions under the current identity can be associated. The project name can be obtained via the `ListProjectResources` (get project resource list) API, or you can create a new project using the `CreateProject` (create project) API. The default value is `default`.



**AccurateGroupPriority ** <span data-label="purple"> Integer  </span><span data-api-tag="require|VF342R">必选</span> `Sample value: 1`

The priority adjustment target for the advanced condition group. The value range is `0` to `9`. If not adjusted, the original value must be provided. Only one of this field or the `RulePriority` field can be adjusted at a time.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|rn4A6_">必选</span> `Sample value: example.volcwaf001.com`

Specify the target domain whose rate limiting rule priority needs to be adjusted.



**RuleId ** <span data-label="purple"> Integer  </span><span data-api-tag="require|QteIF2">必选</span> `Sample value: 1`

The ID of the protection rule whose priority needs to be adjusted.



**RulePriority ** <span data-label="purple"> Integer  </span><span data-api-tag="require|mdtEUD">必选</span> `Sample value: 1`

The priority adjustment target for the rate limiting rule. The value range is `0` to `9`. If not adjusted, the original value must be provided. Only one of this field or the `AccurateGroupPriority` field can be adjusted at a time.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
