---
title: "Daily Granularity Usage Statistics"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Daily_Granularity_Usage_Statistics"
---

<span id="cc8a5b8e"></span>
## Request description

**Path**:/openapi/v1/usage_amount/daily

**Method**: POST

**Content\-type**: application/json

<span id="f011af3d"></span>
## Request parameters

**Body**: Refer to public parameter description

<span id="987ec83a"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "${app_id}": {
            "day_usage_amount": {
                "{day}": {
                    "dau": 1,
                    "events_num": 1
                },
            "app_info": {
                    "app_name": xx,
                    "app_en_name": xx
                }
        }
    }
}
```


The data format is `data. ${app_id}. day_usage_amount. ${day}: {concrete content}`.

The format of mont is `yyyyMMdd`.


|**Field** |**Type** |**Description** |
|---|---|---|
|dau |int |Value of DAU |
|events_num |int |event count |


<span id="27a4115d"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
body={
    "org_id": null,
    "app_ids": [164314],
    "start_time": 1643644800, # 2022.February.1st
    "end_time": 1645977600 # 2022.February.28th
}
res = bc.data_finder('/openapi/v1/usage_amount/daily', body={body})
print(res.content)
```


<span id="60273a69"></span>
## Back to example

Return result:

```python
{
    "code": 200,
    "message": "success",
    "data": {
        "164314": {
            "day_usage_amount": {
                "20220201": {
                    "dau": 1,
                    "events_num": 1
                },
                "20220202": {
                    "dau": 1,
                    "events_num": 1
                },
                "20220203": {
                    "dau": 1,
                    "events_num": 1
                },
                ...
                ...
                ...
                "20220228": {
                    "dau": 1,
                    "events_num": 1
                }
            },
            "app_info": {
                    "app_name": "rangers_164314_ceshi",
                    "app_en_name": "rangers_164314_ceshi"
                }
        }
    }
}
```
