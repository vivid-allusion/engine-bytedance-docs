---
title: "DeleteCustomBotConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteCustomBotConfig"
---

Call the DeleteCustomBotConfig API to delete a custom bot rule by ID.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteCustomBotConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|UkDAgd">必选</span> `Sample value: DeleteCustomBotConfig`

API name. The name of the current API is `DeleteCustomBotConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|1qEoLZ">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**BotID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|WmjsPk">必选</span> `Sample value: 3624`

ID of the bot rule to be deleted. This is the actual numeric part of the rule's unique identifier (corresponding to `RuleTag`). For example, if `RuleTag = K000000003624`, then `BotID = 3624`. For how to obtain it, see [ListCustomBotConfig](https://docs.byteplus.com/en/docs/waf/ListCustomBotConfig).



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|CGxfoX">必选</span> `Sample value: example.volcwaf001.com`

Associated domain information.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
