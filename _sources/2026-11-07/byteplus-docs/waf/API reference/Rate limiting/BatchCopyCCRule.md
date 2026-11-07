---
title: "BatchCopyCCRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/BatchCopyCCRule"
---

Batch copy rate limiting rules to target domains or domain groups based on the rule ID.

<span id="QFv00Xo7"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=BatchCopyCCRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|ECuq0-">必选</span> `Sample value: BatchCopyCCRule`

API name. The name of the current API is `BatchCopyCCRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|30gC76">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the current resource with the corresponding project. Only projects for which the current identity has permissions can be associated. To obtain the project name, refer to the `ListProjectResources` API (to get the project resource list), or call the `CreateProject` API to create a new project. The default value is `default`.



**DstHostGroupIDs ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [7061]`

List of target domain group IDs to which rate limiting rules are copied. Each array element is a domain group ID. Either this parameter or the `DstHosts` parameter can be used to specify the target object for rule copying.



**DstHosts ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: -`

List of target domains to which rate limiting rules are copied. Each array element is a domain string. Either this parameter or the `DstHostGroupIDs` parameter can be used to specify the target object for rule copying.



**DstRulePriorityAdjustType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|6-2myr">必选</span> `Sample value: 1`

Insertion method for the rule after copying. Supported values are as follows.


* `1`: Insert with the lowest priority;

* `2`: Insert with the highest priority.



**OverwriteSameName ** <span data-label="purple"> Boolean  </span>`Optional` `Sample value: true`

Whether to overwrite rate limiting rules with the same name under the target domain. The default value is `false`.


* If set to `true`, rules with the same name will be overwritten.

* If set to `false`, rules with the same name will be skipped.



**SrcRuleID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|uGuVcp">必选</span> `Sample value: 54253`

Specify the unique ID of the rate limiting rule to be copied. The API will locate the corresponding rule based on this ID and perform the batch copy operation.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**FailedHosts ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of domains for which copying rate limiting rules failed. Each element contains the domain and the reason for failure.


**Host ** <span data-label="purple"> String  </span>`Sample value: example.volcwaf.com`

Domain for which copying rate limiting rules failed.



**Reason ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Reason code for failure to copy rate limiting rules to the target domain, including:


* `0`: Unknown error;

* `1`: Internal error;

* `2`: Domain name does not exist;

* `3`: The number of CC rules has reached the limit;

* `4`: CC rule priority conflict;

* `5`: CC rule conflict;

* `6`: The number of advanced condition groups under the path has reached the limit.




**SkippedHosts ** <span data-label="purple"> String[]  </span>`Sample value: ["example.volc001.com"]`

List of domains skipped during batch copying of rate limiting rules. Each array element is a domain string.



**SuccessHosts ** <span data-label="purple"> String[]  </span>`Sample value: ["example.volc002.com"]`

When batch copying CCv3 rules, the list of target domains where rules were successfully copied. Each array element is a domain string.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
