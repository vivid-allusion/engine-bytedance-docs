---
title: "DeleteBotAnalyseProtectRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteBotAnalyseProtectRule"
---

Delete the specified bot statistics protection rule.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteBotAnalyseProtectRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|gN5OtY">必选</span> `Sample value: DeleteBotAnalyseProtectRule`

API name. The name of the current API is `DeleteBotAnalyseProtectRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|roLhGt">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



**Id ** <span data-label="purple"> Integer  </span><span data-api-tag="require|EJIa2d">必选</span> `Sample value: 18673`

Rule ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.
