---
title: "Get Event Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_Event_Properties"
---

<span id="b525d659"></span>
# Request description

**Path**:openapi/v1/metadata/<app_id: int\>/list/params

**Method**: POST

**Content\-type**: application/json

<span id="bf048b8e"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|filter |object |No |{<br><br>"name": "need_refresh"<br><br>} |Filter according to certain fields, and optional values are usually available:<br><br><br>* Name property name<br><br>* Status property status |
|with |list |No |events |When fetching an event, carry the metadata information associated with the fetch. The optional value is:<br><br><br>* Events associated with the events property<br><br>* values Event property value<br><br>* The front\-end display value corresponding to the alias attribute value<br><br>* property_dict Dimension Dictionary<br><br>* event_params the relationship between events and properties<br><br><br>Note: Connecting with more information will affect interface performance. |


```json
{
    "filter": {
        "name": "need_refresh"
    },
    "with": ["events", "event_params"]
}
```


<span id="5d9daa05"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "id": 6718923,
            "app_id": 2174,
            "name": "need_refresh",
            "value_type": "string",
            "show_name": "",
            "backing_show_name": "need_refresh",
            "show_name_en": null,
            "i18n_show_names": {},
            "preset": 0,
            "type": 1,
            "store_location": "string_params",
            "store_value_type": "string",
            "description": "",
            "status": 1,
            "used_users": 0,
            "used_times": 0,
            "used_times_updated_ts": 1649239508,
            "has_property_dict": false,
            "property_dict_version": null,
            "property_dict_updated_ts": 1638835525,
            "property_dict": {},
            "data_reported": 1,
            "platform": [
                "others"
            ],
            "verifier": "",
            "verify_time_ts": null,
            "status_disable_ts": null,
            "origin": 1,
            "creator_id": "",
            "updator_id": "",
            "created_at": 1638835525,
            "updated_at": 1638835525,
            "events": [
                {
                    "id": 3163686,
                    "app_id": 2174,
                    "name": "a",
                    "show_name": "",
                    "backing_show_name": "a",
                    "show_name_en": null,
                    "i18n_show_names": {},
                    "description": "",
                    "preset": 0,
                    "use_slot": 1,
                    "status": 1,
                    "used_users": 0,
                    "used_times": 0,
                    "used_times_updated_ts": 1649239495,
                    "created_at": 1638835525,
                    "updated_at": 1676995246,
                    "verifier": "",
                    "verify_time_ts": null,
                    "status_disable_ts": null,
                    "data_reported": 1,
                    "last_day_amounts": 10979,
                    "platform": [
                        "others"
                    ],
                    "origin": 1,
                    "creator_id": "runninginfo",
                    "updator_id": "runninginfo",
                    "principal": "",
                    "data_date": null,
                    "data_source_name": null,
                    "data_source": null,
                    "priority": null,
                    "event_category": null,
                    "owners": null,
                    "jump_url": null,
                    "param_status": 1,
                    "params": null,
                    "virtual_params": null,
                    "items": null,
                    "source_platform": null,
                    "event_groups": null
                }
            ],
            "event_params": [
                {
                    "id": 30535275,
                    "app_id": 2174,
                    "event_name": "a",
                    "param_name": "need_refresh",
                    "value_type": "string",
                    "slot_name": "_slot_param_2",
                    "slot_index": 2,
                    "store_value_type": "string",
                    "store_location": "string_params",
                    "cardinality": 0,
                    "value": null,
                    "status": 1,
                    "data_reported": 1,
                    "created_at": 1638835525,
                    "updated_at": 1672124621,
                    "show_name": "need_refresh",
                    "platform": "[\"others\"]"
                }
            ],
            "owners": null,
            "attr_classify": null
        }
    ]
}
```
