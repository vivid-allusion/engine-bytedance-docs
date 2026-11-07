---
title: "Modify Event"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_Event"
---

<span id="de6b7b2c"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/events

**Method**: PATCH

**Content\-type**: application/json

<span id="1ac68682"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|id |int |Yes |3228105 |event id |
|status |int |No |1 |status information<br><br><br>* 0 disabled<br><br>* 1 enable<br><br>* 2 hide |
|description |str |No |null |Description information |
|show_name |str |No |null |display information |


```json
{
    "status": 1,
    "id": 3228105
}
```


<span id="87aa9410"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
