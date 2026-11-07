---
title: "UpdateHostGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateHostGroup"
---

The UpdateHostGroup API supports updating the specified domain group information by domain group ID, including the domain group name, domain group list, and more.

<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateHostGroup&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|4GP035">必选</span> `Sample value: UpdateHostGroup`

API name. The current API name is `UpdateHostGroup`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Ct-jwQ">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**Action ** <span data-label="purple"> String  </span>`Optional` `Sample value: Add`

Action for modifying the domain list


* Add: Add domain

* Delete: Delete domain

* ALL: Overwrite all domains

* Leave blank: Do not modify domain information



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: Project1`

Project name.



**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: Used for batch association with blocklist.`

Domain group description.



**HostGroupID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|_181da">必选</span> `Sample value: 1234`

The domain group ID to be updated, which can be obtained through the ListHostGroup.



**HostList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["volcwaf.com","www.testwaf.com"]`

Domain list information.



**Name ** <span data-label="purple"> String  </span>`Optional` `Sample value: Key protected domain name`

Domain group name.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to get more error code information.
