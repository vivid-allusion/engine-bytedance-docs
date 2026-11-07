---
title: "Add Virtual Events"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Add_Virtual_Events"
---

<span id="244cb930"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/virtual_events

**Method**: POST

**Content\-type**: application/json

<span id="c82b863d"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|name |str |Yes |aaaaaa\-3 |event name |
|status |int |Yes |1 |status information<br><br><br>* 0 disabled<br><br>* 1 enable<br><br>* 2 hide |
|description |str |No |null |Description information |
|show_name |str |No |null |display information |
|dsl_content |object |Yes |See examples of requests below |Create rules for virtual events |


```json
{
        "name": "aaaaaa-3",
        "show_name": "new_show_name",
        "status": 1,
        "dsl_content": {
            "logic": "or",
            "queries": [
                {
                    "event_id": 234913,
                    "event_name": "predefine_pageview",
                    "event_type": "origin",
                    "filters": [],
                    "show_label": "A",
                    "event_indicator": "",
                    "measure_info": {},
                    "indicator_show_name": ""
                }
            ]
        }
}
```


<span id="ff741ebc"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "id": 55345535,
        "app_id": 2174,
        "name": "aaaaaa-3",
        "show_name": "new_show_name",
        "status": 1,
        "dsl_content": {
            "logic": "or",
            "queries": [
                {
                    "event_id": 234913,
                    "event_name": "predefine_pageview",
                    "event_type": "origin",
                    "filters": [],
                    "show_label": "A",
                    "event_indicator": "",
                    "measure_info": {},
                    "indicator_show_name": ""
                }
            ]
        },
        "used_times": 0,
        "used_times_updated_ts": null,
        "creator_id": "213697",
        "updator_id": "213697",
        "created_at": null,
        "updated_at": null,
        "owners": null,
        "event_groups": null,
        "params": null,
        "virtual_params": null,
        "relation_events": null,
        "dsl": {
            "logic": "or",
            "queries": [
                {
                    "event_id": 234913,
                    "event_name": "predefine_pageview",
                    "event_type": "origin",
                    "filters": [],
                    "show_label": "A",
                    "event_indicator": "",
                    "measure_info": {},
                    "indicator_show_name": ""
                }
            ]
        }
    }
}
```
