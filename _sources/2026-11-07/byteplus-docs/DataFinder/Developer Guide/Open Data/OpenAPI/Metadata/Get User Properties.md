---
title: "Get User Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_User_Properties"
---

<span id="1789a41a"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/list/user_profiles

**Method**: POST

**Content\-type**: application/json

<span id="f1b2e7f1"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|filter |object |No |See examples of requests below |Filter according to certain fields, and optional values are usually available:<br><br><br>* Name property name<br><br>* Status property status |
|with |list |No ||When fetching an event, carry the metadata information associated with the fetch. The optional value is:<br><br><br>* Event attribute associated event<br><br>* Value Event property value<br><br>* The front\-end display value corresponding to the alias attribute value<br><br>* property_dict Dimension Dictionary<br><br><br>Note: Connecting with more information will affect interface performance. |


```json
{
    "filter": {
        "name": ["os_name"]
    }
}
```


<span id="7cd83544"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "id": 77584,
            "app_id": 2174,
            "name": "os_name",
            "show_name": "Operation system",
            "backing_show_name": "Operation system",
            "i18n_show_names": {
                "zh_CN": "操作系统",
                "en_US": "OS",
                "ja_JP": "オペレーティングシステム"
            },
            "description": "198273",
            "store_location": "os_name",
            "store_value_type": "string",
            "value_type": "string",
            "values": null,
            "aliases": {},
            "i18n_aliases": null,
            "has_property_dict": false,
            "property_dict_version": null,
            "property_dict_updated_ts": 1670838554,
            "property_dict": null,
            "used_users": 41,
            "used_times": 8268,
            "used_times_updated_ts": 1672650040,
            "cardinality": null,
            "slot_index": null,
            "slot_name": null,
            "source_type": 0,
            "status": 1,
            "operation_type": "all_value",
            "feature_code": "",
            "is_support_realtime": true,
            "creator_id": "preset",
            "updator_id": "Liuzhiqiang(10000450)",
            "verifier": null,
            "created_at": 1616472404,
            "updated_at": 1674962391,
            "verify_time_ts": null,
            "status_disable_ts": null,
            "origin": 0,
            "data_source_name": null,
            "data_source_field": null,
            "data_source": null,
            "principal": "",
            "data_reported": 1,
            "attr_classify": null
        }
    ]
}
```
