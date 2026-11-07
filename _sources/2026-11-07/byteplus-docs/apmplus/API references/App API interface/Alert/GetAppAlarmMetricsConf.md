---
title: "GetAppAlarmMetricsConf"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmMetricsConf"
---

Get app alert\-related metadata.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: GET

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppAlarmMetricsConf&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppAlarmMetricsConf |The API name. The current API name is `GetAppAlarmMetricsConf`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|Aid |Long |Yes |123456 |Application ID |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppAlarmMetricsConf&Version=2025-12-01&Aid=123456
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |Exception type. |
|value |Object of [Config](https://docs.byteplus.com/en/docs/299/67881#config) |\- |Data associated with this exception type.  |


<span id="config"></span>
### Config


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Groups |Array of [Group](https://docs.byteplus.com/en/docs/299/67881#group) |\- |Grouping dimensions supported by this alert category |
|Filters |Array of [Filter](https://docs.byteplus.com/en/docs/299/67881#filter) |\- |Filter criteria supported by this category |
|Metrics |Array of [Meta](https://docs.byteplus.com/en/docs/299/67881#meta) |\- |Metrics supported by this alert category |


<span id="group"></span>
### Group


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |normal |Grouping dimension type |
|Field |String |os |Grouping dimension key |
|Label |String |Operating system name |Grouping dimension name |


<span id="filter"></span>
### Filter


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Op |Array of [KeyLabel](https://docs.byteplus.com/en/docs/299/67881#keylabel) |\- |Condition symbols supported by this filter dimension |
|Type |String |normal |Filter dimension type |
|Filed |String |os |Filter dimension key |
|Label |String |Operating system name |Filter criterion name |
|Values |Array of [FilterValue](https://docs.byteplus.com/en/docs/299/67881#filtervalue) |\- |Filter dimension value |
|SubFilter |Array of [Filter](https://docs.byteplus.com/en/docs/299/67881#filter) |\- |Sub\-condition |


<span id="meta"></span>
### Meta


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Type |String |\- |Metric type. It can be a simple metric or a composite metric. |
|Label |String |Ajax error count |Metric Name |
|Metric |String |ajax_error_count |Metric key |
|SubMeta |Array of [Meta](https://docs.byteplus.com/en/docs/299/67881#meta) |\- |Sub\-metric |


<span id="keylabel"></span>
### KeyLabel


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Key |String |in |Condition symbol key |
|Label |String |= |Frontend display of condition symbol |


<span id="filtervalue"></span>
### FilterValue


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Label |String |Operating system |Display name of filter value |
|Value |String |iOS |Filter value |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

&nbsp;

```JSON
{
    "data": {},
    "error_no": 0,
    "error_msg": ""
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
