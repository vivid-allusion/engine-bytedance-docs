---
title: "Get Application and Configuration Information"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_Application_and_Configuration_Information"
---

<span id="f6985fe6"></span>
## Request description

**Path**:openapi/v1/metadata/apps

**Method**: POST

**Content\-type**: application/json

<span id="d6f80424"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|app_ids |list |Yes |[<br><br>1,<br><br>2<br><br>] |app id list |
|with_config |bool |No |null |Whether to return configuration information |
|accessed |bool |No |null |Is the connection successful? |


```json
{
    "app_ids": [
        1,
        2
    ]
}
```


<span id="933e2773"></span>
## Return parameters

**Response**:


* SaaS\-cloud native

   ```json
   {
           "code": 200,
           "message": "success",
           "data": {
                   "app_infos": [{
                           "app_id": 666***,
                           "tea_app_id": 666***,
                           "app_name": "\系\统\使\用\监\控", //system use monitor
                           "app_en_name": "system_usage_monitor",
                           "app_type": "web",
                           "data_center": 1,
                           "scale": 1,
                           "entrance_type": 4,
                           "products": 1,
                           "app_key": "6a74bf2bcdbf767e4b310abd2c***d89c5a",
                           "status": 1,
                           "description": null,
                           "project_id": 666***,
                           "subject_id": 1,
                           "creator_id": "admin",
                           "updator_id": "admin",
                           "created_at": 1754283944,
                           "updated_at": 1754283944,
                           "configs": null
                   }, {
                           "app_id": 666667,
                           "tea_app_id": 666667,
                           "app_name": "Tester\使\用\监\控", //Tester use monitor
                           "app_en_name": "tester_usage_monitor",
                           ……
                   }],
                   "total": null
           }
   }
   ```
   

* SaaS \- non\-cloud native

   ```json
   {
       "code": 200,
       "message": "success",
       "data": {
           "app_infos": [
               {
                   "app_id": 1,
                   "tea_app_id": 1,
                   "app_name": "test1",
                   "app_en_name": "test1",
                   "app_type": "web",
                   "data_center": 1,
                   "scale": 1,
                   "entrance_type": 4,
                   "app_key": "05d9577e67cfd***a",
                   "status": 1,
                   "description": null,
                   "configs": null,
                   "creator_id": "demo",
                   "updator_id": "demo",
                   "created_at": 1606985484,
                   "updated_at": 1624342801
               },
               {
                   "app_id": 2,
                   "tea_app_id": 2,
                    ...
               }
           ],
           "total": null
       }
   }
   ```
