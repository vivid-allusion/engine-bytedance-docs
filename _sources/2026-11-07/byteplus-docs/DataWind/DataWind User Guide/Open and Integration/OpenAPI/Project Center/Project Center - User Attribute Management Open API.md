---
title: "Project Center - User Attribute Management Open API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Project_Center_-_User_Attribute_Management_Open_API"
---

<span id="b47aeb4b"></span>
# 1. Overview

The product provides OpenAPI interfaces for external users to trigger and manage user attributes.

Caution: Before using the interfaces described in this document, please first understand the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="539b90c0"></span>
# 2. Operation steps

<span id="更新属性"></span>
## 2.1 Update attributes


* **Request description**


Request URL: `PUT /aeolus/api/v3/open/userManagement/subjectAttributeList`

Authorization: Bearer jwt_token


* **Request parameters**



|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID |
|attributeList |array |Yes |["\*\*\* ** *.* ** "] |For existing attributes, the field attribute ID must be added. New attributes do not include the ID field. |


```JSON
{
    # 项目id
    "appId":{appId},
    # 已有属性，需添加字段属性id，新增属性不含id字段
    "attributeList":[
        {"id":63,"name":"属性1","isPublic":1,"adminList":["********.*****"]},
        {"name":"属性2","isPublic":1,"adminList":["********.*****"]}
    ]
}
```



* **Response parameters**


```JSON
     {
  "code": "aeolus/ok", 
  "data": {
    "fails": []
  }, 
  "msg": "成功"
}              
```


<span id="更新属性值"></span>
## 2.2 Update attribute values


* **Request description**


Request URL: `PUT /aeolus/api/v3/open/userManagement/subjectAttributeValue`

Authorization: Bearer jwt_token


* **Request parameters**



|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID |
|originId |string |Yes |2 |User name or group ID |
|type |int |Yes |0 |0 indicates a user, 1 indicates a group |
|attributeId |int |Yes |2 |Attribute ID |
|valueList |array |Yes |["1","1"] |When assigning multiple values, use the ["", ""] format. |



* **Response parameters**


```JSON
{
  "code": "aeolus/ok", 
  "data": , 
  "msg": "成功"
}
```


<span id="删除属性"></span>
## 2.3 Delete attributes


* **Request description**


Request URL: `DELETE /aeolus/api/v3/open/userManagement/subjectAttribute`

Authorization: Bearer jwt_token


* **Request parameters**



|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID |
|attributeId |int |Yes |65 |Attribute ID |



* **Response parameters**


```JSON
{
  "code": "aeolus/ok", 
  "data": 65, 
  "msg": "成功"
}
```
