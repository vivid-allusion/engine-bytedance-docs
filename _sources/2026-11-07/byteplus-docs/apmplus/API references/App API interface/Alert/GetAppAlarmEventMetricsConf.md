---
title: "GetAppAlarmEventMetricsConf"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppAlarmEventMetricsConf"
---

Get alert configurations for app custom events.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: GET

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppAlarmEventMetricsConf&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppAlarmEventMetricsConf |The API name. The current API name is `GetAppAlarmEventMetricsConf`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Integer |Yes |123456 |Application ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppAlarmEventMetricsConf&Version=2022-10-12&aid=123456
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |JSON Map |\- |Alert metadata. |
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Long |0 |Error code. If the request was successful, its value is 0. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |\- |The exception type. |
|value |Object of [Config](https://docs.byteplus.com/en/docs/299/67877#config) |\- |Related data for this exception type. |


<span id="config"></span>
### Config


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|groups |Array of [Group](https://docs.byteplus.com/en/docs/299/67877#group) |\- |Grouping dimensions supported by this alert category. |
|filters |Array of [Filter](https://docs.byteplus.com/en/docs/299/67877#filter) |\- |Filter criteria supported by this category. |
|metrics |Array of [Meta](https://docs.byteplus.com/en/docs/299/67877#meta) |\- |Metrics supported by this alert category. |


<span id="group"></span>
### Group


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |normal |Grouping dimension type. |
|field |String |os |Grouping dimension key. |
|label |String |Operating system name |Grouping dimension name. |


<span id="filter"></span>
### Filter


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|op |Array of [KeyLabel](https://docs.byteplus.com/en/docs/299/67877#keylabel) |in |Condition symbols supported by this filter dimension. |
|type |String |normal |Filter dimension type. |
|filed |String |os |Filter dimension key. |
|label |String |Operating system name |Filter condition name. |
|values |Array of [FilterValue](https://docs.byteplus.com/en/docs/299/67877#filtervalue) |[] |Filter dimension value |
|sub_filter |Array of [Filter](https://docs.byteplus.com/en/docs/299/67877#filter) |\- |The sub\-condition. |


<span id="meta"></span>
### Meta


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|type |String |simple |Metric type. It can be a simple metric or a composite metric. |
|label |String |Ajax error count |The metric name. |
|metric |String |ajax_error_count |Metric key. |
|sub_meta |Array of [Meta](https://docs.byteplus.com/en/docs/299/67877#meta) |\- |Sub\-metric. |


<span id="keylabel"></span>
### KeyLabel


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |in |Condition symbol key. |
|label |String |= |Frontend display of condition symbol. |


<span id="filtervalue"></span>
### FilterValue


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |model |Label. |
|value |String |vivo X100T |Tag value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {},
    "error_no": 0,
    "error_msg": ""
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
