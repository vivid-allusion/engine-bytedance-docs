---
title: "Modify User Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_User_Properties"
---

<span id="94b86932"></span>
## Request description

**Path**:openapi/v1/metadata/<app_id: int\>/profile:batchOperate

**Method**: POST

**Content\-type**: application/json

<span id="e9ac50fa"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|profiles |list |Yes |See examples of requests below |user attributes |
|operation_type |int |Yes |6 |operation type<br><br><br>* 5 new additions<br><br>* 6 modifications |
|profiles[0].name |str |Yes |os_name |attribute name |
|profiles[0].status |int |No |1 |status information<br><br><br>* 0 disabled<br><br>* 1 enable<br><br>* 2 hide |
|profiles[0].description |str |No |os_name desc |Description information |
|profiles[0].show_name |str |No |os_name show_name |display information |
|profiles[0].value_type |str |No |int |Attribute types, currently supported<br><br><br>* int integer<br><br>* Floating point type<br><br>* String string type<br><br>* dateTime date type<br><br>* List List type<br><br>* Version Version number type |


```json
{
    "profiles": [
        {
            "name": "os_name",
            "show_name": "os_name show_name",
            "description": "os_name desc"
        }
    ],
    "operation_type": 6
}
```


<span id="5cd2b381"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": true
}
```
