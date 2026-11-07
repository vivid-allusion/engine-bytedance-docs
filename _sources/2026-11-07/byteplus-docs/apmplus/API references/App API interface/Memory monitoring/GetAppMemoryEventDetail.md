---
title: "GetAppMemoryEventDetail"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppMemoryEventDetail"
---

Get details of a single memory event.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppMemoryEventDetail&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppMemoryEventDetail |The API name. The current API name is `GetAppMemoryEventDetail`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|raw_log_key |String |No |tos_key_example |The storage Key of the raw log. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppMemoryEventDetail&Version=2022-10-12
{
    "raw_log_key": "tos_key_example"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |JSON Map |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |event_id |The raw data value in the reported data. |
|value |String |2591\*\*\*\*0837 |The raw data value in the reported data. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_msg": "",
    "error_no": 0,
    "data": {
        "event_id": "2591****0837",
        "is_main_process": true,
        "issue_type": 32,
        "log_type": "battery_trace",
        "network_type": 4,
        "process_name": "com.ss.android.article.news",
        "scene": "com.ss.android.detail.feature.detail2.view.NewVideoDetailActivity",
        "sid": 1713867984852,
        "single_hold_time": 4532,
        "timestamp": 1713873673056
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
