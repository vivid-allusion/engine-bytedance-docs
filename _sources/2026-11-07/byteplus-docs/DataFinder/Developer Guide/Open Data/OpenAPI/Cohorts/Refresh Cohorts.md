---
title: "Refresh Cohorts"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Refresh_Cohorts"
---

<span id="4e934afb"></span>
## Instructions for use

Note: Refresh grouping is resource intensive, and frequent calls to this interface may result in slower queries.

<span id="b52e051e"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts/{cohort_id}/refresh

**Method**: GET

**Content\-type**: application/json

<span id="d95fb099"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|cohort_id |int |Yes |6 |grouping id |


<span id="27723155"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "count": 9289,
        "refresh_time": "2022-07-11",
        "refresh_timestamp": 1657534754,
        "status": 1
    }
}
```


Field meaning description


|**Field** |**Type** |**Description** |
|---|---|---|
|count |int |Number of people in the cluster after refresh |
|refresh_time |string |Refresh completion date |
|refresh_timestamp |int |10\-Digit timestamp of the time the refresh completed |
|status |int |refresh status<br><br>0: Refreshing<br><br>1: Success<br><br>2: Error<br><br>4: Timeout<br><br>5: Clustering to be calculated |


<span id="8f03db26"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
# for example, app_id= 164314 cohort_id = 6

resp = bc.data_finder("/openapi/v1/164314/cohorts/6/refresh")
print(resp.json()["data"])
```


<span id="2a435070"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "count": 9289,
        "refresh_time": "2022-07-11",
        "refresh_timestamp": 1657534754,
        "status": 1
    }
}
```
