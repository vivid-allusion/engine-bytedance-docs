---
title: "GetSmartCCConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/GetSmartCCConfig"
---

Retrieve the currently effective intelligent CC protection configuration for the specified domain.

<span id="d0f8YMlM"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=GetSmartCCConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Kp7PrU">必选</span> `Sample value: GetSmartCCConfig`

API name. The current API name is `GetSmartCCConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|sZNx5U">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the current resource with a project. Only projects with permissions under the current identity can be associated. 



**Domain ** <span data-label="purple"> String  </span>`Optional` `Sample value: example.volcwaf001.com`

To retrieve the currently effective intelligent CC protection configuration, specify the domain.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Action ** <span data-label="purple"> String  </span>`Sample value: block`

The action for the intelligent CC protection configuration. Supported values are as follows.


* `observe`: Observe;

* `block`: Block.



**CreateAt ** <span data-label="purple"> Integer  </span>`Sample value: 1672531200`

Configuration creation time, represented as a Unix timestamp.



**Domain ** <span data-label="purple"> String  </span>`Sample value: example.volcwaf001.com`

The domain corresponding to the currently effective intelligent CC protection configuration.



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The enable switch for the intelligent CC protection configuration. Supported values are as follows.


* `0`: Disabled;

* `1`: Enabled.



**Level ** <span data-label="purple"> String  </span>`Sample value: default`

The protection level of intelligent CC protection. Supported values are as follows.


* `loose`: Relaxed;

* `default`: Standard;

* `strict`: Strict.



**Region ** <span data-label="purple"> String  </span>`Sample value: cn-beijing`

The region where the cloud WAF instance is located.


* Asia Pacific (Johor)：ap\-southeast\-1

* Asia Pacific (Jakarta)：ap\-southeast\-3

* China (Hong Kong)：cn\-hongkong

* Edge：byteplus\-global



**UpdateAt ** <span data-label="purple"> Integer  </span>`Sample value: 1719000000`

Configuration update time, in Unix timestamp format.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
