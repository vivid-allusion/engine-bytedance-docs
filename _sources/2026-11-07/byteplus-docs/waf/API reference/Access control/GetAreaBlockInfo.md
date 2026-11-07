---
title: "GetAreaBlockInfo"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/GetAreaBlockInfo"
---

Call this interface to query the available geographic location codes, which are used when updating geographic access control rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service interface call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=GetAreaBlockInfo&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|gmEvEz">必选</span> `Sample value: GetAreaBlockInfo`

Interface name. The current API name is `GetAreaBlockInfo`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|9kMTDJ">必选</span> `Sample value: 2023-12-25`

Interface version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: geo_management_project`

Specify the project name associated with the current resource. Only projects with permissions under the current identity can be associated. The project name can be obtained by calling the `ListProjectResources` interface.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**CNAreaInfoList ** <span data-label="purple"> Object[]  </span>`Sample value: -`

Applicable only to the Volcano Engine WAF service, displays the list of configurable geographic location information for subregions within China. Under the BytePlus WAF service, this list is empty.


**AlphabeticName ** <span data-label="purple"> String  </span>`Sample value: yidali`

The pinyin of the available geographic location name.



**AreaCode ** <span data-label="purple"> String  </span>`Sample value: IT`

The code corresponding to the available geographic location.



**AreaName ** <span data-label="purple"> String  </span>`Sample value: Italy`

The name corresponding to the available geographic location.



**Location ** <span data-label="purple"> String  </span>`Sample value: Europe`

The continent to which the available geographic location belongs.




**OverSeaAreaInfoList ** <span data-label="purple"> Object[]  </span>`Sample value: -`


* Under the Volcano Engine WAF service, displays the list of configurable country/region location information.

* Under the BytePlus WAF service, displays the list of location information of configurable country/region outside the Chinese mainland.



**AlphabeticName ** <span data-label="purple"> String  </span>`Sample value: yidali`

The pinyin of the available geographic location name.



**AreaCode ** <span data-label="purple"> String  </span>`Sample value: IT`

The code corresponding to the available geographic location.



**AreaName ** <span data-label="purple"> String  </span>`Sample value: Italy`

The name corresponding to the available geographic location.



**Location ** <span data-label="purple"> String  </span>`Sample value: Europe`

The continent to which the available geographic location belongs.




<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
