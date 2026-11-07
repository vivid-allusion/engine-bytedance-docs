---
title: "ListAreaBlockRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListAreaBlockRule"
---

Query the configuration details of the current geographic location access control policy, that is, which countries or regions are restricted from access.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListAreaBlockRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|6lbG1a">必选</span> `Sample value: ListAreaBlockRule`

API name. The current API name is `ListAreaBlockRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|TmisAI">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**Host ** <span data-label="purple"> String  </span>`Optional` `Sample value: example.volcwaf001.com`

Specify the domain name to query.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project name associated with the current resource. Only projects with permissions under the current identity can be associated. The project name can be obtained by calling the `ListProjectResources` (get project resource list) API.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Action ** <span data-label="purple"> String  </span>`Sample value: observe`

Rule action. The supported values are as follows.


* `observe`: Observe;

* `block`: Block.



**SubRegion ** <span data-label="purple"> String[]  </span>`Sample value: ["Beijing"]`

List of codes for Chinese subregions that are restricted from access. Effective only under the Volcano Engine WAF service.



**Country ** <span data-label="purple"> String[]  </span>`Sample value: ["ES"]`

List of codes for countries or regions that are restricted from access. Effective only under the Volcano Engine WAF service.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: C000000000001`

Rule display ID.



**Host ** <span data-label="purple"> String  </span>`Sample value: example.volcwaf001.com`

Domain name where the rule takes effect.



**Location ** <span data-label="purple"> String[]  </span>`Sample value: ["CN"]`

List of codes for countries or regions outside the Chinese mainland that are restricted from access. Effective only under the BytePlus WAF service.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.
