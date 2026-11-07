---
title: "Query Virtual Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Virtual_Properties"
---

<span id="d9145b70"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/list/virtual_params

**Method**: POST

**Content\-type**: application/json

<span id="1bdc3162"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|filter |object |No |See examples of requests below |Filter according to certain fields, and optional values are usually available:<br><br><br>* Name property name<br><br>* property_type 1 is the virtual event property, 2 is the virtual user property<br><br>* Status |
|with |list |No |events |When obtaining a virtual property, carry the metadata information associated with the acquisition. The optional value is:<br><br><br>* events<br><br><br>Note: Connecting with more information will affect interface performance. |


```json
{
    "filter": {
        "name": "$_vp_af32erfds",
        "property_type": 1
    },
    "with": ["events"]
}
```


<span id="33d8dc34"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "id": 3402868,
            "app_id": 2174,
            "name": "$_vp_af32erfds",
            "show_name": "",
            "description": "",
            "property_type": 1,
            "param_type": 2,
            "value_type": "string",
            "sql_rule": "concat(user_profiles.loc_province_id,'123')",
            "relation_event_param_properties": null,
            "relation_user_profile_properties": [
                "loc_province_id"
            ],
            "property_dict_version": null,
            "property_dict_updated_ts": 1669014312,
            "has_property_dict": false,
            "property_dict": null,
            "event_relation_strategy": "any",
            "status": 1,
            "used_times": 0,
            "used_times_updated_ts": 1669014312,
            "preset": 0,
            "creator_id": "10000088",
            "created_at": 1669014312,
            "updated_at": 1669014312,
            "events": [
                {
                    "id": 235692,
                    "app_id": 2174,
                    "name": "any_event",
                    "show_name": "any event",
                    "backing_show_name": null,
                    "show_name_en": "",
                    "i18n_show_names": null,
                    "description": "{             \"event\": \"test_event\",             \"params\": \"{\\\"int_1\\\":1}\",             \"local_time_ms\": 1666161845237         }",
                    "preset": 1,
                    "use_slot": 0,
                    "status": 1,
                    "used_users": 117,
                    "used_times": 66211,
                    "used_times_updated_ts": null,
                    "created_at": 1621755535000,
                    "updated_at": 1676995246000,
                    "verifier": "",
                    "verify_time_ts": null,
                    "status_disable_ts": null,
                    "data_reported": 1,
                    "last_day_amounts": 37425234,
                    "platform": null,
                    "origin": 0,
                    "creator_id": "preset",
                    "updator_id": "Zhangwei(10000150)",
                    "principal": "",
                    "data_date": null,
                    "data_source_name": null,
                    "data_source": null,
                    "priority": null,
                    "event_category": "normal",
                    "owners": null,
                    "jump_url": null,
                    "param_status": 1,
                    "params": null,
                    "virtual_params": null,
                    "items": null,
                    "source_platform": null,
                    "event_groups": null
                }
            ]
        }
    ]
}
```
