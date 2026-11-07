---
title: "Add Events (General Operations)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Add_Events_General_Operations"
---

<span id="9c4227c3"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/events:batchOperate

**Method**: POST

**Content\-type**: application/json

<span id="2e4a32d4"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**sample value** |**Describe** |
|---|---|---|---|---|
|events |list |Yes |See examples of requests below |event list |
|operation_type |int |Yes |5 |Operation ID, currently only supported<br><br><br>* 5 Creation<br><br>* 6 modifications |


```json
{
    "events": [
        {
            "name": "aaaa",
            "show_name": "aaa",
            "event_group_ids": [
                11130
            ],
            "desc": "aaa"
        }
    ],
    "operation_type": 5
}
```


<span id="5b2cda73"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
