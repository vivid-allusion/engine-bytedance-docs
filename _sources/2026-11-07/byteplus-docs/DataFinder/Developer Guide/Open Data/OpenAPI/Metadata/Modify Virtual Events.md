---
title: "Modify Virtual Events"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_Virtual_Events"
---

<span id="30922d67"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/virtual_events/<event_id: int\>

**Method**: PATCH

**Content\-type**: application/json

<span id="6bb31168"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|id |int |Yes |11 |event id |
|status |int |No |1 |status information<br><br><br>* 0 disabled<br><br>* 1 enable<br><br>* 2 hide |
|description |str |No |null |Description information |
|show_name |str |No |new_show_name |display information |
|dsl_content |object |No |null |Create rules for virtual events |


```json
{
    "description": "a",
    "status": 1,
    "show_name": "new_show_name"
}
```


<span id="db0fc7a5"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "id": 22839602,
        "app_id": 2174,
        "name": "aaaaaa",
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
        "used_times_updated_ts": 1660707999000,
        "creator_id": "213697",
        "updator_id": "245171",
        "created_at": 1660707999000,
        "updated_at": 1677063765000,
        "owners": [
            ""
        ],
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
