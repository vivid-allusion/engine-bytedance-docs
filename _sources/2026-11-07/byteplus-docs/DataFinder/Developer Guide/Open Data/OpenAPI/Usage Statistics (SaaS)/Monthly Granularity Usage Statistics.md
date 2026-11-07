---
title: "Monthly Granularity Usage Statistics"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Monthly_Granularity_Usage_Statistics"
---

<span id="4a4a99b0"></span>
## Request description

**Path**:/openapi/v1/usage_amount

**Method**: POST

**Content\-type**: application/json

<span id="1350d343"></span>
## Request parameters

**Body** : Refer to public parameter description

<span id="32428aa9"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "usage_amount": {
            "${app_id}": {
                "month_usage_amount": {
                    "{month}": {
                        "days": xx,
                        "mau": xx,
                        "dau": xxx,
                        "events_num": xxx
                    }
                },
                "app_info": {
                    "app_name": xx,
                    "app_en_name": xx
                }
            }
        }
    }
}
```


Field meaning description

The data format is `data. usage_amount. ${app_id}. month_usage_amount. ${month}: {concrete content}`.

The format of mount is `yyyyMM`.


|**Field** |**Type** |**Description** |
|---|---|---|
|days |int |days |
|mau |int |Value of MAU |
|dau |int |Value of DAU |
|events_num |int |event count |


<span id="cbcd0e71"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
body={
    "org_id": null,
    "app_ids": [164314],
    "start_time": 1643644800, #February 1, 2022
    "end_time": 1645977600 #February 28, 2022
}
res = bc.data_finder('/openapi/v1/usage_amount', body={body})
print(res.content)
```


<span id="b74d4e8d"></span>
## Back to example

Return result:

```python
{
    "code": 200,
    "message": "success",
    "data": {
        "usage_amount": {
            "164314": {
                "month_usage_amount": {
                    "202202": {
                        "days": 28,
                        "mau": 100000,
                        "dau": 100,
                        "events_num": 100000000
                    }
                },
                 "app_info": {
                    "app_name": "rangers_164314_ceshi",
                    "app_en_name": "rangers_164314_ceshi"
                }
            }
        }
    }
}
```
