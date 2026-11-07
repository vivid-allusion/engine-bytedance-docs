---
title: "Create a Cohort"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Create_a_Cohort"
---

<span id="88acbf37"></span>
## Interface description

This interface is used to create clusters, which can be created based on rules or uploaded files.


* When creating a cluster based on rules, you can directly call this interface.

* If you need to create clusters based on uploaded files, you need to upload the files first to get file file_key, see [Upload the file used to create the cluster](https://docs.byteplus.com/docs/DataFinder/Upload_the_File_which_is_Used_to_Create_the_Cohorts).


<span id="a99d7272"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts

**Method**: POST

**Content\-type**: application/json

<span id="8ef89a2c"></span>
## Request parameters

**Path\-parameters** : Reference[API Description and Public Parameters](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters__)

**Body**:

```json
{
    "cohort_name": "cohort name",
    "cohort_type": 4,
    "description": "cohort description",
    "dsl_content": {},
    "refresh_rule": 1
}
```


Field meaning description


|**Field** |**Type** |**Description** |
|---|---|---|
|cohort_name |int |group name |
|cohort_type |int |Cluster type:<br><br><br>* A value of 4 indicates that the cluster was created by the rule<br><br>* A value of 2 indicates that the cluster was created by uploading the file |
|description |string |grouping description information |
|dsl_content |object |Cluster rule or file information created:<br><br><br>* When creating based on rules, you can copy the clustering rules to the request parameters after configuring the front\-end UI for modification. See[Get the clustering DSL from the front end (recommended)](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters__#06f26e76)<br><br>* When creating based on an uploaded file, you need to configure the file to be uploaded file_key information, see[Upload the file used to create the cluster](https://docs.byteplus.com/docs/DataFinder/Upload_the_File_which_is_Used_to_Create_the_Cohorts) |
|refresh_rule |int |* 1: Manual refresh<br><br>* 2: Daily routine refresh<br><br>* 0: Refresh is not supported. When creating a cluster based on uploaded files, it needs to be configured as "0", and refresh is not supported. |


<span id="9f60ce35"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "cohort_id": 6
    }
}
```


Field meaning description


|**Field** |**Type** |**Description** |
|---|---|---|
|cohort_id |int |Create a successful cluster ID |


<span id="bf087b05"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
#For example, app_id = 164314

dsl = {
    "cohort_name": "openapi-creation",
    "cohort_type": 4, #4 Represents rule creation
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
    "refresh_rule": 1 #1 means manual refresh, 2 means daily refresh
}
resp = bc.data_finder("/openapi/v1/164314/cohorts"， body=dsl)
cohort_id = resp.json()["data"]["cohort_id"]
```


<span id="652fe85b"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "cohort_id": 6
    }
}
```
