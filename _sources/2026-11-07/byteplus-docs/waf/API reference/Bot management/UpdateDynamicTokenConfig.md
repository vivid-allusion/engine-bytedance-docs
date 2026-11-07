---
title: "UpdateDynamicTokenConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateDynamicTokenConfig"
---

Update the dynamic token configuration for the specified domain.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateDynamicTokenConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|RpDcF4">必选</span> `Sample value: UpdateDynamicTokenConfig`

API name. The current API name is `UpdateDynamicTokenConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|oCWt_2">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project name, used to associate the current resource with the corresponding project.



**Action ** <span data-label="purple"> String  </span>`Optional` `Sample value: observe`

Specifies the action to take after dynamic token detection. Supported values are as follows:


* `observe`: Observe;

* `block`: Block;

* `js`: JS challenge;

* `captcha`: CAPTCHA.



**DetectionPath ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: -`

Specifies the list of paths for dynamic token detection. Wildcard \* is supported, and only one wildcard can be used in a single path.



**Enable ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Whether the dynamic token configuration is enabled. Supported values are as follows:


* `0`: Disable dynamic token configuration;

* `1`: Enable dynamic token configuration.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|LWj-Yt">必选</span> `Sample value: 1203.volcwaf001.com`

Specifies the target domain name for updating the dynamic token configuration.



**Region ** <span data-label="purple"> String  </span><span data-api-tag="require|45p-mX">必选</span> `Sample value: cn-beijing`

The region where the cloud WAF instance is located.


* Asia Pacific (Johor)：ap\-southeast\-1

* Asia Pacific (Jakarta)：ap\-southeast\-3

* China (Hong Kong)：cn\-hongkong

* Edge：byteplus\-global



**ValidityPeriod ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 30`

The validity period of the dynamic token. Valid range: 15–60 seconds.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
