---
title: "Get Cohorts List"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_Cohorts_List"
---

<span id="da25f5de"></span>
## Request description

**Path**：/openapi/v1/{app_id}/cohorts

**Method**: GET

**Content\-type**: application/json

<span id="54fb78f0"></span>
## Request parameters

**Path\-parameters** : Reference [API Description and Public Parameters](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters__).

<span id="ea243cef"></span>
## Return parameters

**Response**:

```json
{
    "code":200,
    "message":"success",
    "data":[
        {
            "app_id":123,
            "cohort_id":1054321,
            "cohort_name":"分群展示名称", // Cohorts display name
            "cohort_status":1,
            "cohort_type":4,
            "count":3950,
            "creator":"00000",
            "creator_time":1648446690,
            "description":"",
            "dsl_content": Object{...},
            "modify_time":1648538157,
            "modify_user":"00000",
            "part_date":"",
            "refresh_rule":1,
            "status":1,
            "user_info":{},
            "version":1
        }
    ]
}
```



* Get the cohort_status meaning returned by the clustered list interface:

* 0: Indicates that the calculation is in progress

* 1: Indicates that the calculation is successful

* 2: Indicates that the calculation failed

* 3: Indicates that the query was terminated

* 4: Indicates that the query timed out

* 5: Indicates that the query is queuing up.

* TATUS has the same meaning as cohort_status, in order to be compatible with the old structure, refer to the cohort_status field.


Field meaning description:

Data is an array of JSON objects, where the JSON keyfields specify


|**Field** |**Type** |**Description** |
|---|---|---|
|cohort_id |int |cluster ID |
|cohort_name |string |subgroup name |
|refresh_rule |int |group refresh rule<br><br>0: unsupported refresh<br><br>1: manual support manual refresh<br><br>2: daily refresh |
|count |int |Number of users in the cluster |


<span id="3b283967"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
# for example, app_id= 164314
res = bc.data_finder('/openapi/v1/164314/cohorts', method='get')
print(res.content)
```


<span id="cf27164c"></span>
## Back to example

Return result:

```json
{
    "code":200,
    "data":[
        {
            "app_id":164314,
            "cohort_id":1591,
            "cohort_name":"一线活跃用户", // Active users in first tier cities
            "cohort_status":1,
            "cohort_type":4,
            "count":34259,
            "creator":"00000",
            "creator_time":1568202530,
            "description":"北上广深，30天内活跃过", // Users in Beijing, Shanghai, Guangzhou, and Shenzhen, that have been active in last 30 days
            "dsl_content":Object{...},
            "modify_time":1655270356,
            "modify_user":"00000",
            "part_date":"2022-06-15",
            "refresh_rule":2,
            "status":1,
            "user_info":Object{...},
            "version":10132
        },
        Object{...},
        Object{...}
    ],
    "message":"success"
}
```
