---
title: "Add Virtual Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Add_Virtual_Properties"
---

<span id="e67cc93b"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/virtual_params

**Method**: POST

**Content\-type**: application/json

<span id="7b4d8e3a"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|name |str |Yes |$_vp_test_add |attribute name |
|show_name |str |No |null |display name |
|description |str |No |null |Description information |
|property_type |int |No |1 |Virtual Attribute Type<br><br><br>* 1 Event properties<br><br>* 2 User Attributes |
|event_relation_strategy |str |Yes |any |event association type<br><br><br>* All are related<br><br>* Any association is association |
|value_type |str |Yes |string |attribute type |
|sql_rule |str |Yes |concat(user_profiles.device_model, ' ', user_profiles.os_version) |SQL expression |


```json
{ 
    "property_type": 1,
    "value_type": "string",
    "event_relation_strategy": "any",
    "sql_rule": "concat(user_profiles.device_model, ' ', user_profiles.os_version)",
    "name": "$_vp_test_add"
}
```


<span id="6ad5388a"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": 1
}
```
