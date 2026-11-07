---
title: "Query Dashboard Information"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Dashboard_Information"
---

<span id="60ef2eaa"></span>
## Request description

**Path**: The request path is set differently in different environments:


|Environment type |Path |
|---|---|
|SaaS\-cloud native |* Use project ID as path parameter (recommended):/openapi/v1/projects/{project_id}/dashboards/<br><br>* Use app ID as path parameter:/openapi/v1/{app_id}/dashboards/ |
|SaaS\-cloud native |* /openapi/v1/{app_id}/dashboards/ |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are not sure which environment you are currently using, please refer to the documentation to confirm the type of environment you are currently using: <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


**Method**: GET

**Content\-type**: application/json

<span id="9d18697c"></span>
## request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|dashboard_id |string |Yes |6737549040994484743 |Dashboard ID |


<span id="8b5f148c"></span>
## Return parameters

**Response**:

```json
{
    "code":200,
    "data":{
        "6737549040994484743":{
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{},
            "created_at":1568707880,
            "filters":[],
            "is_default":false,
            "partners":[],
            "extra":{},
            "name":"Core data overview",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6737549040994484743",
            "status":1
        }
    },
    "message":"success"
}
```


Field meaning description:

Data returns a JSON object in the format: `"{dashboard_id}": {dashboard_info}`, which describes the key fields of the Dashboard information


|**Parameter** |**Type** |Sample value |**Describe** |
|---|---|---|---|
|name |string |core data overview |Dashboard name |


<span id="8eeb5d16"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
# for example, app_id= 164314 dashboard= 6737549040994484743
bc.data_finder('/openapi/v1/164314/dashboards/6737549040994484743', method='get')
print(res.content)
```


<span id="e207be2c"></span>
## Back to example

Return result:

```json
{
    "code":200,
    "data":{
        "6737549040994484743":{
            "is_core":false,
            "creator":"Data Ranger",
            "partner_info":{

            },
            "created_at":1568707880,
            "filters":[

            ],
            "is_default":false,
            "partners":[
                "Data Ranger1",
                "Data Ranger2"
            ],
            "extra":{

            },
            "name":"Core data overview",
            "is_public":true,
            "is_subscribed":false,
            "app_id":164314,
            "dashboard_id":"6737549040994484743",
            "status":1
        }
    },
    "message":"success"
}
```
