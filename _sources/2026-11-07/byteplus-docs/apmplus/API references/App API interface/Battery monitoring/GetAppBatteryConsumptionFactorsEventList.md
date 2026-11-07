---
title: "GetAppBatteryConsumptionFactorsEventList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppBatteryConsumptionFactorsEventList"
---

Get the app power consumption event list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppBatteryConsumptionFactorsEventList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppBatteryConsumptionFactorsEventList |The API name. The current API name is `GetAppBatteryConsumptionFactorsEventList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|start_time |Integer |No |1619827200 |Query start time (Unix timestamp). |
|end_time |Integer |No |1619913600 |Query end time (Unix timestamp). |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67909#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |
|bddid |String |No |bdd123456789 |device ID。 |
|calculation_method |String |No |all |Calculation method.<br><br><br>* all: Full lifecycle<br><br>* per_min: Average per minute |
|only_back |Integer |No |1 |Whether the app is running in the background.<br><br><br>* 1: Background<br><br>* 0: Foreground |
|order_by |String |No |traffic_p_capacity_ascend |Sorting basis.<br><br><br>* traffic_p_capacity_ascend: Sort by traffic in ascending order<br><br>* traffic_p_capacity_descend: Sort by traffic in descending order<br><br>* loc_p_time_ascend: Sort by location latency in ascending order<br><br>* loc_p_time_descend: Sort by location latency in descending order<br><br>* alarm_ascend: Sort by AlarmManager configuration times in ascending order<br><br>* alarm_descend: Sort by AlarmManager configuration times in descending order<br><br>* power_p_time_ascend: Sort by WakeLock latency in ascending order<br><br>* power_p_time_descend: Sort by WakeLock latency in descending order<br><br>* p_time_ascend: Sort by process lifetime in ascending order<br><br>* p_time_descend: Sort by process lifetime in descending order<br><br>* api_time_ascend: Sort by report time in ascending order<br><br>* api_time_descend: Sort by report time in descending order<br><br>* event_time_ascend: Sort by occurrence time in ascending order<br><br>* event_time_descend: Sort by occurrence time in descending order |
|page_no |Integer |No |1 |Page number to query. |
|page_size |Integer |No |20 |Number of items displayed per page. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67909#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppBatteryConsumptionFactorsEventList&Version=2022-10-12
{
    "start_time": 25,
    "end_time": 421,
    "filters": {
        "type": "and",
        "sub_conditions": [
            {
                "dimension": "apm_version",
                "type": "expression",
                "op": "in",
                "values": [
                    "1.4.5"
                ]
            },
            {
                "dimension": "device_model",
                "type": "expression",
                "op": "in",
                "values": [
                    "MI 5X"
                ]
            }
        ]
    },
    "bddid": "American",
    "calculation_method": "all",
    "only_back": 1,
    "order_by": "traffic_p_capacity_ascend",
    "page_no": 1,
    "page_size": 20
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ListBatterySummaryEventData](https://docs.byteplus.com/en/docs/299/67909#listbatterysummaryeventdata) |\- |Response data. |
|error_msg |String |\- |Error message. |
|error_no |Integer |0 |Error code. |


<span id="listbatterysummaryeventdata"></span>
### ListBatterySummaryEventData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of items in the list. |
|result |Array of [ListBatterySummaryEvent](https://docs.byteplus.com/en/docs/299/67909#listbatterysummaryevent) |\- |List details. |


<span id="listbatterysummaryevent"></span>
### ListBatterySummaryEvent


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|alarm |Double |0.1 |AlarmManager configuration times. |
|bddid |String |bdd123456789 |Device ID. |
|p_time |Double |0.4 |Process lifetime. |
|is_back |Integer |1 |Whether it is a background event.<br><br><br>* 1: Background<br><br>* 0: Foreground |
|api_time |Long |1619827200 |The report time. |
|event_id |String |event_12345 |Event ID. |
|event_time |Long |1619827230 |The time when the event occurs. |
|loc_p_time |Double |0.3 |Get location latency. |
|power_p_time |Double |0.2 |WakeLock latency. |
|process_name |String |com.example.app |Process name. |
|traffic_p_capacity |Double |0.5 |Traffic\-related power consumption. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": {
        "total": 2,
        "result": [
            {
                "alarm": 376,
                "bddid": "arm",
                "p_time": 565,
                "is_back": 181,
                "api_time": 214,
                "event_id": "Public",
                "event_time": 528,
                "loc_p_time": 739,
                "power_p_time": -92,
                "process_name": "hands",
                "traffic_p_capacity": 388
            }
        ]
    },
    "error_msg": "",
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
