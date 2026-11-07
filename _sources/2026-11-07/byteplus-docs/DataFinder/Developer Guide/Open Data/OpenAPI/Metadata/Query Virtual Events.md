---
title: "Query Virtual Events"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Virtual_Events"
---

<span id="51fee752"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/list/virtual_events

**Method**: POST

**Content\-type**: application/json

<span id="29e58f57"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|filter |object |No |name |Filter according to certain fields, and optional values are usually available:<br><br><br>* Name Event name<br><br>* Status Event status<br><br>* id event id<br><br>* creator_id event creator id |
|with |list |No |virtual_params |When fetching an event, carry the metadata information associated with the fetch. The optional value is:<br><br><br>* virtual_params virtual properties<br><br>* property_dict Data Dictionary<br><br>* values Event property value<br><br>* The front\-end display value corresponding to the Alias event property value<br><br>* event_groups event classification<br><br><br>Note: Connecting with more information will affect interface performance. |


```json
{
    "filter": {
        "name": ["aaaaaa"]
    },
    "with": ["virtual_params"]
}
```


<span id="3a191036"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "id": 22839602,
            "app_id": 2174,
            "name": "aaaaaa",
            "show_name": "aa",
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
            "updated_at": 1664196294000,
            "owners": [
                ""
            ],
            "event_groups": null,
            "params": null,
            "virtual_params": [{
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
                }],
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
    ]
}
```
