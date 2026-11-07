---
title: "Delete Created Cohorts"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Delete_Created_Cohorts"
---

<span id="8056fbb3"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts/{cohort_id}

**Method**: DELETE

**Content\-type**: application/json

<span id="9ef231e9"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|cohort_id |int |Yes |1001076 |cluster ID |


<span id="b90789cf"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": null
}
```


<span id="f198a7bc"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
# for example, app_id= 164314 cohort id= 1001076
res = bc.data_finder('/openapi/v1/164314/cohorts/1001076', method='delete')
print(res.content)
```


<span id="65461d7f"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": null
}
```
