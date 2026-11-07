---
title: "Modify Virtual Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_Virtual_Properties"
---

<span id="5a54ede7"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/virtual_params

**Method**: PATCH

**Content\-type**: application/json

<span id="b184e4b6"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|name |str |Yes |$_vp_test_add_2 |name |
|show_name |str |No |null |display name |
|description |str |No |null |Description information |
|event_relation_strategy |str |No |any |event association type<br><br><br>* All are related<br><br>* Any association is association |
|value_type |str |Yes |int |attribute type |
|sql_rule |str |Yes |concat(user_profiles.device_model, ' ', user_profiles.os_version) |SQL expression |


```json
{
    "property_type": 1,
    "value_type": "int",
    "event_relation_strategy": "any",
    "sql_rule": "concat(user_profiles.device_model, ' ', user_profiles.os_version)",
    "name": "$_vp_test_add_2"
}
```


<span id="a8c8992b"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
