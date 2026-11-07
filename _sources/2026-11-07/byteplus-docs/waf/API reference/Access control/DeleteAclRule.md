---
title: "DeleteAclRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteAclRule"
---

You can call the DeleteAclRule API to delete the corresponding access control rule based on the rule ID and access control type.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteAclRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|O9ukj4">必选</span> `Sample value: DeleteAclRule`

API name. The name of the current API is `DeleteAclRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Lr9Nne">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**AclType ** <span data-label="purple"> String  </span><span data-api-tag="require|obuAoh">必选</span> `Sample value: Block`

Access control rule type.


* Allow: Allowlist

* Block: Blocklist



**ID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|msQ1dT">必选</span> `Sample value: 126217`

The rule ID to be deleted. For how to obtain it, refer to [Query access control rules](https://docs.byteplus.com/en/docs/waf/ListAclRule).



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the project resource.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.
