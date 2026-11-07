---
title: "GetDynamicTokenConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/GetDynamicTokenConfig"
---

Retrieve the dynamic token configuration for the specified domain.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=GetDynamicTokenConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|oSpexL">必选</span> `Sample value: GetDynamicTokenConfig`

API name. The current API name is `GetDynamicTokenConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|LlWFkx">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the current resource with a project. Only projects that have permissions under the current identity can be associated.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|MbSGcK">必选</span> `Sample value: 1203.volcwaf001.com`

The target domain for which the dynamic token configuration needs to be retrieved.



**Region ** <span data-label="purple"> String  </span><span data-api-tag="require|UlT8ct">必选</span> `Sample value: cn-beijing`

The region where the cloud WAF instance is located.


* Asia Pacific (Johor)：ap\-southeast\-1

* Asia Pacific (Jakarta)：ap\-southeast\-3

* China (Hong Kong)：cn\-hongkong

* Edge：byteplus\-global



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Action ** <span data-label="purple"> String  </span>`Sample value: observe`

Action policy to apply after dynamic token detection. Supported values are as follows:


* `observe`: Observe;

* `block`: Block;

* `js`: JS challenge;

* `captcha`: CAPTCHA.



**DetectionPath ** <span data-label="purple"> String[]  </span>`Sample value: ["/test.html"]`

Detection path.



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The enabled status of the dynamic token configuration. Supported values are as follows:


* `1`: Enabled;

* `0`: Disabled.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: T000000055659`

Rule identifier.



**ValidityPeriod ** <span data-label="purple"> Integer  </span>`Sample value: 30`

Validity period of the dynamic token configuration.



**VerificationExemptionTime ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Exemption time after successful human\-machine verification, JS challenge, or proof\-of\-work verification.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
