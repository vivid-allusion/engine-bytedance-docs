---
title: "Modify Created Cohorts"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Modify_Created_Cohorts"
---

<span id="6994ce72"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts/{cohort_id}

**Method**: PATCH

**Content\-type**: application/json

<span id="fc5bbb80"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|cohort_id |int |Yes |1001076 |cluster ID |


**Body**:

Modify to create clusters by uploading files:

```json
{
    "cohort_name": "cohort name",
    "cohort_type": 2, //2 means cohorts of file upload type
    "description": "cohort description",
    "dsl_content": {
        "uuid_file_key": "upload_uuid/164314/20220819/1eb8f3c6-4447-4e9c-a538-c1b33a1cd0e4.csv", 
        // uuid_file_key can be acquired after upload files through 9.1 interface
        "file_list": [
            {
                "name": "user_unique_id_template (3).csv" //upload file name
            }
        ],
        "dsl_type": "user_unique_id" // support user_unique_id、ssid、device_id、web_id
    },
    "refresh_rule": 1
}
```


Modify the rule to create a cluster:

```json
{
    "cohort_name": "cohort name",
    "cohort_type": 4 //4 means cohorts of rule upload type
    "description": "cohort description",
    "dsl_content": {},
    "refresh_rule": 1
}
```


<span id="07405c5e"></span>
## return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": null
}
```


<span id="1293dcfe"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
# for example, app_id= 164314 cohort id= 1001076
body = {
    "cohort_name": "openapi-modify",
    "cohort_type": 4, //4 means rule creation
    "description": "",
    "dsl_content": {
        "periods": [],
        "app_ids": [
            164314
        ],
        "content": {
            "profile_filters": [],
            "profile_groups": [],
            "queries": [
                [
                    {
                        "show_label": "event--A--A",
                        "event_name": "any_event",
                        "event_type": "origin",
                        "next_query_label": null,
                        "sequence_first": true,
                        "logic": true,
                        "condition": {
                            "property_operation": ">",
                            "property_values": [
                                0
                            ],
                            "period": {
                                "granularity": "day",
                                "last": {
                                    "amount": 7,
                                    "unit": "day"
                                },
                                "type": "last",
                                "timezone": "Asia/Shanghai"
                            }
                        },
                        "filters": [
                            {
                                "expression": {
                                    "logic": "and",
                                    "conditions": []
                                }
                            }
                        ],
                        "event_indicator": "events"
                    }
                ]
            ],
            "query_type": "$cohort"
        },
        "version": 3
    },
    "refresh_rule": 2 # modify from 1 to 2
}
resp = bc.data_finder("/openapi/v1/164314/cohorts/1001076"， body=dsl)
cohort_id = resp.json()["data"]["cohort_id"]
```


<span id="6faff376"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "cohort_id": 1001076
    }
}
```
