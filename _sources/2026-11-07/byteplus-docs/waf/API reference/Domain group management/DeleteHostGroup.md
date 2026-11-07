---
title: "DeleteHostGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/DeleteHostGroup"
---

The DeleteHostGroup API is used to delete the host group corresponding to the specified ID, and supports deleting multiple host groups at the same time.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important notes


* It is recommended to confirm that the corresponding rules do not need to be associated with the host group before deleting. After a host group is deleted, its associated rules will simultaneously remove references to that host group.

* If a protection rule is only associated with the current host group, the corresponding rule will be deleted directly.


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=DeleteHostGroup&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|1P7fx1">必选</span> `Sample value: DeleteHostGroup`

API name. The name of the current API is `DeleteHostGroup`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|rtozr5">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**HostGroupIds ** <span data-label="purple"> Integer[]  </span><span data-api-tag="require|13S60G">必选</span> `Sample value: [7515,7516]`

List of host group IDs to be deleted. You can obtain the corresponding IDs through ListHostGroup.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The name of the project associated with the current resource. For how to obtain it, refer to ListProjectResources.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to get more information about error codes.
