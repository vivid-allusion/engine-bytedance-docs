---
title: "Query Event"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Event"
---

<span id="688b3e08"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/list/events

**Method**: POST

**Content\-type**: application/json

<span id="fe50399b"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|filter |object |No |name |Filter according to certain fields, and optional values are usually available:<br><br><br>* Name Event name<br><br>* Status Event status<br><br>* id event id<br><br>* creator_id event creator id |
|with |list |No |virtual_params |When fetching an event, carry the metadata information associated with the fetch. The optional value is:<br><br><br>* virtual_params virtual properties<br><br>* property_dict Data Dictionary<br><br>* values Event property value<br><br>* The front\-end display value corresponding to the Alias event property value<br><br>* event_groups event classification<br><br>* Properties associated with the params event<br><br>* app_ids event\-related applications<br><br>* Dimension information associated with items events<br><br><br>Note: Connecting with more information will affect interface performance. |


```json
{
    "filter": {
        "name": ["app_launch", "predefine_pageview"],
        "status": [0, 1, 3, 4]
    },
    "with": ["params", "event_groups"]
}
```


<span id="919f7ef4"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "id": 390022,
            "app_id": 1234,
            "name": "app_launch",
            "show_name": "App launch",
            "backing_show_name": "App launch",
            "show_name_en": null,
            "i18n_show_names": {
                "en_US": "App launch",
                "zh_CN": "App launch",
                "ja_JP": "App launch"
            },
            "description": null,
            "preset": 1,
            "use_slot": 0,
            "status": 1,
            "used_users": 0,
            "used_times": 0,
            "used_times_updated_ts": 1672650039,
            "created_at": 1621755535,
            "updated_at": 1675332462,
            "verifier": "",
            "verify_time_ts": null,
            "status_disable_ts": 1673512602,
            "data_reported": 1,
            "last_day_amounts": 0,
            "platform": [
                "others",
                "mp"
            ],
            "origin": 0,
            "creator_id": "meta",
            "updator_id": "ranger-admin(852809798129652)",
            "principal": "",
            "data_date": null,
            "data_source_name": null,
            "data_source": null,
            "priority": null,
            "event_category": null,
            "owners": null,
            "jump_url": null,
            "param_status": null,
            "params": [
                {
                    "app_id": 1234,
                    "event_name": "app_launch",
                    "param_id": 369279,
                    "name": "extra",
                    "value_type": "string",
                    "show_name": "",
                    "backing_show_name": "extra",
                    "preset": 0,
                    "description": "",
                    "store_location": "string_params",
                    "store_value_type": "string",
                    "type": 1,
                    "status": 1,
                    "used_times": 0,
                    "used_times_updated_ts": 1649239503,
                    "cardinality": 0,
                    "value": null,
                    "aliases": null,
                    "i18n_aliases": null,
                    "has_property_dict": false,
                    "property_dict_version": null,
                    "property_dict_updated_ts": 1623318181,
                    "property_dict": null,
                    "slot_name": "extra",
                    "slot_index": null,
                    "created_at": 1621755549,
                    "updated_at": 1622960698,
                    "owners": null
                }
            ],
            "virtual_params": null,
            "items": null,
            "source_platform": null,
            "event_groups": [
                {
                    "id": 10373,
                    "group_type": 2,
                    "name": "121",
                    "pos": 1,
                    "creator_id": 204449,
                    "created_at": 1658371763,
                    "updated_at": 1658383757,
                    "events": null,
                    "public": false
                }
            ]
        }
    ]
}
```
