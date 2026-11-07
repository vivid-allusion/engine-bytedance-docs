---
title: "Query Analysis - Get result Query Results (Privatization)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Analysis-Get_result_Query_Results_Privatization"
---

<span id="7d566811"></span>
## Request description


* **Context\-Path**: /datafinder

* **Path**：/openapi/v1/analysis/{result_id}/result

* **Method**: GET

* **Content\-type**: application/json


<span id="4762bc5a"></span>
## Request parameters


* **Path\-parameters**:

   
   |Parameter |Type |Is it required? |Sample value |Describe |
   |---|---|---|---|---|
   |result_id |int |Yes |resp.json()["data"]["result_id"] |query result ID |
   


<span id="b4a679cf"></span>
## Return parameters


* **Response**:

   Return structure Same as SaaS query return structure


<span id="b7fed823"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
dsl = {
    "version": 3,
    "app_ids": [164***],
    "use_app_cloud_id": True,
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 5,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "content": {
            "query_type": "event",
            "profile_groups_v2": [],
            "profile_filters": [],
            "queries": [
                [
                    {
                        "event_type": "origin",
                        "show_name": "active user amount",
                        "event_name": "app_launch",
                        "groups_v2": [],
                        "filters": [],
                        "show_label": "active_user",
                        "event_indicator": "event_users"
                    }
                ]
            ],
            "option": {
                "skip_cache": False
            }
        }
}

# Privatization logic
resp = bc.data_finder("/openapi/v1/analysis", body=dsl)
result_id = resp.json()["data"]["result_id"]
resp2 = bc.data_finder(f"/openapi/v1/analysis/{result_id}/result")
print(resp2.content)
```
