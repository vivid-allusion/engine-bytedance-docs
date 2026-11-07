---
title: "DeleteCCRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteCCRule"
---

Delete the corresponding CC rule by specifying its domain name and ID.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteCCRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|2hO31o">必选</span> `Sample value: DeleteCCRule`

API name. The current API name is `DeleteCCRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|aRSy2k">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|XkCTar">必选</span> `Sample value: 116869`

Rule ID. To obtain the Rule ID, refer to [ListCCRule](https://docs.byteplus.com/en/docs/waf/ListCCRule).



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|AIRXfI">必选</span> `Sample value: example.volcwaf001.com`

Domain name of the protected website.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project name associated with the current resource.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
