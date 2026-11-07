---
title: "SetSmartCCConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/SetSmartCCConfig"
---

Configure the intelligent rate limiting switch, level, and action settings for the specified domain.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=SetSmartCCConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API, as well as some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|s9zTCn">必选</span> `Sample value: SetSmartCCConfig`

API name. The current API name is `SetSmartCCConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|XA4fVp">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the current resource with a project. Only projects with permissions under the current identity can be associated. To obtain the project name, refer to the `ListProjectResources` API (to get the project resource list), or call the `CreateProject` API to create a new project. The default value is `default`.



**Action ** <span data-label="purple"> String  </span>`Optional` `Sample value: block`

Enumeration values for the action to be taken. Supported values are as follows. No default value.


* `observe`: Observe;

* `block`: Block.



**CreateAt ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1717248000`

Configuration creation time, in Unix timestamp format.



**Domain ** <span data-label="purple"> String  </span>`Optional` `Sample value: example.volcwaf001.com`

The target domain for which to configure the intelligent rate limiting switch, level, and action settings.



**Enable ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The enable switch for intelligent rate limiting. Supported values are as follows.


* `0`: Disabled;

* `1`: Enabled.



**Level ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The level of intelligent rate limiting. No default value. Supported values are as follows.


* `loose`: Loose;

* `default`: Standard;

* `strict`: Strict.



**Region ** <span data-label="purple"> String  </span>`Optional` `Sample value: cn-beijing`

The region where the cloud WAF instance is located.


* Asia Pacific (Johor)：ap\-southeast\-1

* Asia Pacific (Jakarta)：ap\-southeast\-3

* China (Hong Kong)：cn\-hongkong

* Edge：byteplus\-global



**UpdateAt ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1719000000`

Configuration update time, in Unix timestamp format. Not required, no default value.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
