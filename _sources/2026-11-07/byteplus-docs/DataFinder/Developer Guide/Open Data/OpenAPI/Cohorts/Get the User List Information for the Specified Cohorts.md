---
title: "Get the User List Information for the Specified Cohorts"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_the_User_List_Information_for_the_Specified_Cohorts"
---

<span id="015bbed9"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts/{cohort_id}/sample

**Method**: GET

**Content\-type**: application/json

<span id="e4e74fc9"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|cohort_id |int |Yes |1001076 |cluster ID |


**Query\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|count |int |Yes |30 |The limited number of clustered users to return |


<span id="5895ad39"></span>
## Return parameters

**Response**:

```json
{
    "code":200,
    "data":{
        "sampleUsers":[
            {
                "uid":"xxx",
                "user_unique_id":"xxx",
                "ssid":"xxx"
            }
        ]
    },
    "message":"success"
}
```


Field meaning description


|**Field** |**Type** |**Description** |
|---|---|---|
|uid |string |user ID |
|user_unqiue_id |string |user ID |
|ssid |string |Datafinder statistics |


<span id="d94be058"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
# for example, app_id= 164314 cohort id= 1001076
res = bc.data_finder('/openapi/v1/164314/cohorts/1001076/sample', method='get',params={"count":"30"})
print(res.content)
j=json.loads(res.content)
print(len(j["data"]["sampleUsers"]))
print(res.content)
```


<span id="605f47d5"></span>
## Back to example

Return result:

```json
{
    "code":200,
    "data":{
        "sampleUsers":[
            {
                "uid":"431108702006175",
                "user_unique_id":"431108702006175",
                "ssid":"2c46868d-c301-47d8-97fa-301f431d20af"
            }
        ]
    },
    "message":"success"
}
```
