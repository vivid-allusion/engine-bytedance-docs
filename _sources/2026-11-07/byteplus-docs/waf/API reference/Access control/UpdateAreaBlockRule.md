---
title: "UpdateAreaBlockRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateAreaBlockRule"
---

Modify the country or region information associated with the geographic access control policy.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* VolcanoEngine WAF service: Use `Country` to pass the country/region location code, and use `SubRegion` to pass the location code for subregions in China. The `Country` field is taken from the `AreaCode` in the `OverSeaAreaInfoList` returned by `GetAreaBlockInfo`, for example ["ES"]. The `SubRegion` sample is taken from the `AreaCode` in `CNAreaInfoList`, for example ["Beijing"].

* BytePlus WAF service: Use `Location` to pass the country/non\-Chinese mainland region location code. The `Location` field is taken from the `AreaCode` in the `OverSeaAreaInfoList` returned by `GetAreaBlockInfo`, for example ["ES"].


&nbsp;

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateAreaBlockRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|DMg7ZC">必选</span> `Sample value: UpdateAreaBlockRule`

API name. The current API name is `UpdateAreaBlockRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|FlApE_">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project name associated with the current resource. Only projects for which the current identity has permissions can be associated. The project name can be obtained by calling the `ListProjectResources` API, or you can create a new project by calling the `CreateProject` API. The default value is `default`.



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|XbAdpX">必选</span> `Sample value: observe`

Effective action. The supported values are as follows.


* `observe`: Observe.

* `block`: Block.



**Country ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["ES"]`

The list of country/region codes used in VolcanoEngine WAF service. You must first call the `GetAreaBlockInfo` API, then obtain the corresponding country's or region's `AreaCode` from the returned `OverSeaAreaInfoList` and pass it in.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|2SEBi_">必选</span> `Sample value: example.volcwaf001.com`

Specify the domain name to which the geographic access control rule will be applied.



**Location ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["ES"]`

The country/non\-Chinese mainland region location code used in BytePlus WAF service. You must first call the `GetAreaBlockInfo` API, then obtain the corresponding country/non\-Chinese mainland region `AreaCode` from the returned `OverSeaAreaInfoList` and pass it in.



**SubRegion ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["Beijing"]`

The list of country/region codes used in VolcanoEngine WAF service. You must first call the `GetAreaBlockInfo` API, then obtain the corresponding location code for the subregion in China from the `CNAreaInfoList` and pass in the `AreaCode`.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
