---
title: "Add Event Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Add_Event_Properties"
---

<span id="377e51e7"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/params:batchOperate

**Method**: POST

**Content\-type**: application/json

<span id="5c17f1da"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|params |list |Yes |See examples of requests below |event property list |
|operation_type |int |Yes |5 |Operation ID, currently only supported<br><br><br>* 5 Creation<br><br>* 6 modifications |
|params.[0].type |int |Yes |1 |event property type<br><br><br>* 1 General event properties, requiring associated events<br><br>* 2 Event public properties, correlate all events |
|params.[0].name |str |Yes |add_1 |attribute name |
|params.[0].value_type |value_type |Yes |int |attribute type |
|params.[0].type |show_name |No |show_name_1 |display name |
|params.[0].type |desc |No |desc_1 |Description information |


```json
{
    "params": [
        {
            "name": "add_1",
            "value_type": "int",
            "type": 2,
            "show_name": "show_name_1",
            "desc": "desc_1"
        },
        {
            "name": "add_2",
            "value_type": "string",
            "desc": "desc_2",
            "show_name": "desc_2",
            "events": [
                {
                    "name": "app_launch"
                }
            ],
            "type": 1
        }
    ],
    "operation_type": 5
}
```


<span id="ec859243"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
