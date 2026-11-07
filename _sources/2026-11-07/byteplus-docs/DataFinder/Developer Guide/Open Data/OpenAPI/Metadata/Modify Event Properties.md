---
title: "Modify Event Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_Event_Properties"
---

<span id="ca62b23a"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/params

**Method**: PATCH

**Content\-type**: application/json

<span id="c62fabae"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|name |str |Yes |need_refresh |property name |
|status |int |No |1 |status information<br><br><br>* 0 disabled<br><br>* 1 enable<br><br>* 2 hide |
|description |str |No |null |Description information |
|show_name |str |No |null |display information |
|value_type |str |No |string |property types, currently supported<br><br><br>* int integer<br><br>* Floating point type<br><br>* String string type<br><br>* dateTime date type<br><br>* List List type<br><br>* Version Version number type |


```json
{
    "name": "need_refresh",
    "value_type": "string",
    "show_name": "need_refresh show_name",
    "description": "need_refresh desc"
}
```


<span id="4d53298e"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
