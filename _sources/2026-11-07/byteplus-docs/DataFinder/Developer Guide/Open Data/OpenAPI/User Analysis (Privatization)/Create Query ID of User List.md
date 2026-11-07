---
title: "Create Query ID of User List"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Create_Query_ID_of_User_List"
---

<span id="f35c1118"></span>
## Request description

**Path**:/openapi/v1/{app_id}/user_analysis/queries

**Method**: POST

**Content\-type**: application/json

<span id="f93b8167"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|profile_names |list |No |null |List of user property names to query<br><br><br>* When passing null, 20 user attributes are automatically queried<br><br>* When passing [], no user properties are queried<br><br>* If you only care about user IDs, it is strongly recommended to pass [] to speed up queries |
|id_types |list |No | |The id type to be queried, separated by commas (,) |
|query_type |str |Yes | |Query types for user lists, including:<br><br><br>* Analysis, microscope functions<br><br>* Cohort, grouping function |
|analysis |object |query_type for analysis | |When query_type analysis, this field needs to be passed to DSL. |
|cohort |object |query_type a cohort | |When query_type is cohort, this field needs to pass the group id. |
|limit |int |No | |The number of queries is temporarily forced to 1000 and cannot be modified. |


<span id="fb3c84ed"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "query_id": "za9fa417b308a1c8e01"
    }
}
```



|**Field** |**Type** |**Description** |
|---|---|---|
|query_id |str |Query ID of user list |


<span id="a40888ae"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
body={
    "analysis": {
        "dsl": {omit}
    },
    "limit": 1000,
    "profile_names": [],
    "query_type": "analysis"
}
res = bc.data_finder('/openapi/v1/12345/user_analysis/queries', body=body)
print(res.content)
```


<span id="00d96d46"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "query_id": "za9fa417b308a1c8e01"
    }
}
```


<span id="ba6e3d14"></span>
## 5.3 Creating a user list query id of type analysis

Create user lists from various advanced analysis microscopes to query ID for analysis type. The DSL in analysis can be obtained from the front end, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b40437a51834046a45ec4ca6faa8b43~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c5984612f0db7f785dd99237228e2f9.png) </span>

<span id="0fe2d447"></span>
## 5.4 Creating a user list query id of type cohort

The user list ID created from the cluster is of type cohort. When cohort type, the body parameter can be filled in as follows:

```json
{
    "cohort": {
        "cohort_id": <cohort_id: int>
    },
    "query_type": "cohort"
}
```


&nbsp;
